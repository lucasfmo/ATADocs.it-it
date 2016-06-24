---
# required metadata

title: Convalidare il mirroring delle porte| Microsoft Advanced Threat Analytics
description: Viene descritto come verificare che il mirroring delle porte sia configurato correttamente
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Convalidare il mirroring delle porte
> [!NOTE] Questo articolo si riferisce solo alla distribuzione di gateway ATA al posto di gateway ATA Lightweight. Per stabilire se è necessario usare i gateway ATA, vedere [Choosing the right gateways for your deployment](/advanced-threat-analytics/plan-design/ata-capacity-planning#Choosing-the-right-gateway-type-for-your-deployment) (Scelta dei gateway corretti per la distribuzione)
 
I passaggi seguenti consentono di eseguire il processo di convalida della corretta configurazione del mirroring delle porte. Per il corretto funzionamento di ATA, il gateway ATA deve poter vedere il traffico da e verso il controller di dominio. L'origine dati principale usata da ATA è un'analisi approfondita dei pacchetti del traffico di rete da e verso i controller di dominio. Per consentire ad ATA di vedere il traffico di rete, è necessario configurare il mirroring delle porte. Il mirroring delle porte copia il traffico da una porta (la porta di origine) a un'altra porta (la porta di destinazione).

## Convalidare il mirroring delle porte tramite uno script Windows PowerShell

1. Salvare il testo dello script in un file denominato ATAdiag.ps1.
2. Eseguire lo script dal gateway ATA.
Lo script genera traffico ICMP dal gateway ATA al controller di dominio e cerca il traffico nella scheda di interfaccia di rete per l'acquisizione nel controller di dominio.
Se il gateway ATA vede il traffico ICMP con un indirizzo IP di destinazione uguale all'indirizzo IP di controller di dominio immesso nella Console ATA, considera configurato il mirroring delle porte. 

Esempio di esecuzione dello script:

    # ATAdiag.ps1 -CaptureIP n.n.n.n -DCIP n.n.n.n -TestCount n
    
    param([parameter(Mandatory=$true)][string]$CaptureIP, [parameter(Mandatory=$true)][string]$DCIP, [int]$PingCount = 10)

    # Set variables
    
        $ErrorActionPreference = "stop"
    $starttime = get-date
    $byteIn = new-object byte[] 4
    $byteOut = new-object byte[] 4
    $byteData = new-object byte[] 4096  # size of data
    
    $byteIn[0] = 1  # for promiscuous mode
    $byteIn[1-3] = 0
    $byteOut[0-3] = 0



    # Convert network data to host format
        function NetworkToHostUInt16 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt16($value,0)
        }
    
    function NetworkToHostUInt32 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt32($value,0)
        }
    
    function ByteToString ($value)
        {
        $AsciiEncoding = new-object system.text.asciiencoding
        $AsciiEncoding.GetString($value)
            }
    
    Write-Host "Testing Port Mirroring..." -ForegroundColor Yellow
    Write-Host ""
    Write-Host "Here is a summary of the connection we will test." -ForegroundColor Yellow

    # Initialize a first ping connection
    Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue
    Write-Host ""
    
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    Write-Host ""
    Write-Host "Sending ICMP and Capturing data..." -ForegroundColor Yellow
    
    # Open a socket
    
    $socket = new-object system.net.sockets.socket([Net.Sockets.AddressFamily]::InterNetwork,[Net.Sockets.SocketType]::Raw,[Net.Sockets.ProtocolType]::IP)
    
    # Include the IP header
    $socket.setsocketoption("IP","HeaderIncluded",$true)
    
    $socket.ReceiveBufferSize = 10000
    
    $ipendpoint = new-object system.net.ipendpoint([net.ipaddress]"$CaptureIP",0)
    $socket.bind($ipendpoint)
    
    # Enable promiscuous mode
    [void]$socket.iocontrol([net.sockets.iocontrolcode]::ReceiveAll,$byteIn,$byteOut)
    
    # Initialize test variables
    $tests = 0
    $TestResult = "Noise"
    $OneSuccess = 0
    
    while ($tests -le $PingCount)
        {
        if (!$socket.Available)  # see if any packets are in the queue
            {
            start-sleep -milliseconds 500
            continue
            }
    
    # Capture traffic
        $rcv = $socket.receive($byteData,0,$byteData.length,[net.sockets.socketflags]::None)
    
    # Decode the header so we can read ICMP
    
        $MemoryStream = new-object System.IO.MemoryStream($byteData,0,$rcv)
        $BinaryReader = new-object System.IO.BinaryReader($MemoryStream)
    
    # Set IP version & header length
        $VersionAndHeaderLength = $BinaryReader.ReadByte()
    
        # TOS
        $TypeOfService= $BinaryReader.ReadByte()
    
        # More values, and the Protocol Number for ICMP traffic
        # Convert network format of big-endian to host format of little-endian 
        $TotalLength = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    
        $Identification = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $FlagsAndOffset = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $TTL = $BinaryReader.ReadByte()
        $ProtocolNumber = $BinaryReader.ReadByte()
        $Checksum = [Net.IPAddress]::NetworkToHostOrder($BinaryReader.ReadInt16())
    
        # The source and destination IP addresses
        $SourceIPAddress = $BinaryReader.ReadUInt32()
        $DestinationIPAddress = $BinaryReader.ReadUInt32()
    
        # The source and destimation ports
        $sourcePort = [uint16]0
        $destPort = [uint16]0
            
        # Close the stream reader
        $BinaryReader.Close()
        $memorystream.Close()
    
        # Cast DCIP into an IPaddress type
        $DCIPP = [ipaddress] $DCIP
        $DestinationIPAddressP = [ipaddress] $DestinationIPAddress
    
        #Ping the DC at the end after starting the capture
        Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue | Out-Null
            
        # This is the match logic - check to see if Destination IP from the Ping sent matches the DCIP entered by in the ATA Console  
        # The only way the ATA Gateway should see a destination of the DC is if Port Spanning is configured
        
            if ($DestinationIPAddressP -eq $DCIPP)  # is the destination IP eq to the DC IP? 
            {
            $TestResult = "Port Spanning success!"
            $OneSuccess = 1
            } else {
                $TestResult = "Noise"
            }
        
        # Put source, destination, test result in Powershell object
        
        new-object psobject | add-member -pass noteproperty CaptureSource $([system.net.ipaddress]$SourceIPAddress) | add-member -pass noteproperty CaptureDestination $([system.net.ipaddress]$DestinationIPAddress) | Add-Member -pass NoteProperty Result $TestResult | Format-List | Out-Host
        #Count tests
        $tests ++
        }
    
        If ($OneSuccess -eq 1){
            Write-Host "Port Spanning Success!" -ForegroundColor Green
            Write-Host ""
            Write-Host "At least one packet which was addressed to the DC, was picked up by the Gateway." -ForegroundColor Yellow
            Write-Host "A little noise is OK, but if you don't see a majority of successes, you might want to re-run." -ForegroundColor Yellow
        } Else {
            Write-Host "No joy, all noise.  You may want to re-run, increase the number of Ping Counts, or check your config." -ForegroundColor Red
        }
    
    Write-Host ""
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    
    
## Convalidare il mirroring delle porte tramite Net Mon
1.  Installare [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865).

    > [!IMPORTANT]
    > Non installare Microsoft Message Analyzer o altri software di acquisizione del traffico nel gateway ATA.

2.  Aprire Network Monitor e creare una nuova scheda di acquisizione.

    1.  Selezionare solo la scheda di rete di** **acquisizione o la scheda di rete connessa alla porta di commutazione configurata come destinazione del mirroring delle porte.

    2.  Assicurarsi che l'opzione P-Mode sia abilitata.

    3.  Fare clic su **New Capture** (Nuova acquisizione).

        ![Immagine delle creazione di una nuova scheda di acquisizione](media/ATA-Port-Mirroring-Capture.jpg)

3.  Nella finestra Display Filter (Visualizza filtro) immettere il filtro seguente: **KerberosV5 OR LDAP** e quindi fare clic su **Applica**.

    ![Immagine dell'applicazione del filtro Apply KerberosV5 or LDAP](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  Fare clic su **Start** per avviare la sessione di acquisizione. Se il traffico da e verso il controller di dominio non viene visualizzato, esaminare la configurazione del mirroring delle porte.

    ![Immagine dell'avvio della sessione di acquisizione](media/ATA-Port-Mirroring-Capture-traffic.jpg)

    > [!NOTE]
    > È importante assicurarsi che sia possibile visualizzare il traffico da e verso i controller di dominio.
    

5.  Se viene visualizzato solo il traffico in una direzione, collaborare con i team che si occupano della virtualizzazione o della rete per risolvere i problemi di configurazione del mirroring delle porte.

## Vedere anche

- [Configurare il mirroring delle porte](configure-port-mirroring.md)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


