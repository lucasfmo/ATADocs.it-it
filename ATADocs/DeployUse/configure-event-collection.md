---
# required metadata

title: Configurare la raccolta degli eventi | Microsoft Advanced Threat Analytics
description: Descrive le opzioni per configurare la raccolta degli eventi con ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurare la raccolta degli eventi
Per migliorare le funzionalità di rilevamento, ATA necessita dell'ID 4776 del registro eventi di Windows. Questo può essere inoltrato al gateway ATA in due modi: configurando il gateway ATA per l'attesa degli eventi SIEM oppure [configurando l'inoltro degli eventi di Windows](#configuring-windows-event-forwarding)..

## Raccolta eventi
Oltre a raccogliere e ad analizzare il traffico di rete da e verso i controller di dominio, ATA può usare l'evento 4776 di Windows per migliorare ulteriormente il rilevamento dei Pass-the-Hash ATA. È possibile riceverlo dal SIEM o impostando l'inoltro degli eventi di Windows dal controller di dominio. Gli eventi raccolti forniscono ad ATA informazioni aggiuntive che non sono disponibili mediante il traffico di rete del controller di dominio.

### SIEM/Syslog
Perché ATA possa consumare dati da un server Syslog, è necessario eseguire le operazioni seguenti:

-   Configurare uno dei server del gateway ATA in modo che attenda e accetti gli eventi inoltrati dal server SIEM/Sylog.

-   Configurare il server SIEM/Syslog in modo che inoltri eventi specifici al gateway ATA.

> [!IMPORTANT]
> -   Non inoltrare tutti i dati del Syslog al gateway ATA.
> -   ATA supporta il traffico UDP dal server SIEM/Syslog.

Vedere la documentazione del server SIEM/Syslog per informazioni su come configurare l'inoltro di eventi specifici a un altro server. 

### Inoltro degli eventi di Windows
Se non si usa un server SIEM/Syslog, è possibile configurare i controller di dominio di Windows in modo da inoltrare l'ID evento di Windows 4776 affinché sia raccolto e analizzato da ATA. L'ID evento di Windows 4776 fornisce dati sulle autenticazioni NTLM.

## Configurazione del gateway ATA per l'ascolto degli eventi SIEM

1.  Nella configurazione del gateway ATA attivare l'opzione **Syslog Listener UDP** (UDP del listener Syslog)..

    Impostare l'indirizzo IP di attesa come indicato nell'immagine sotto. La porta predefinita è la 514.

    ![Attivare l'immagine dell'UDP del listener Syslog](media/ATA-enable-siem-forward-events.png)

2.  Configurare il server SIEM o Syslog per l'inoltro dell'ID evento di Windows 4776 all'indirizzo IP selezionato sopra. Per altre informazioni sulla configurazione del SIEM, vedere le informazioni di guida online o rivolgersi all'assistenza tecnica di SIEM per i requisiti di formattazione specifici per ciascun server SIEM.

### Supporto di SIEM
ATA supporta gli eventi SIEM nei formati seguenti:

#### Analisi di sicurezza RSA
&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   L'intestazione Syslog è facoltativa.

-   Il separatore di caratteri "\n" è obbligatorio fra i singoli campi.

-   I campi, in ordine, sono:

    1.  Costante RsaSA (deve apparire).

    2.  Il timestamp dell'evento effettivo (assicurarsi che non sia il timestamp dell'arrivo al SIEM o dell'invio ad ATA). Preferibilmente con la precisione ai millisecondi, questo è molto importante.

    3.  L'ID evento di Windows

    4.  Il nome del provider di eventi di Windows

    5.  Il nome del registro eventi di Windows

    6.  Il nome del computer che riceve l'evento (il DC in questo caso)

    7.  Il nome dell'utente che si autentica

    8.  Il nome dell'host di origine

    9. Il codice del risultato di NTLM

-   L'ordine è importante e nel messaggio non deve essere incluso nient'altro.

#### HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Il controller di dominio ha tentato di convalidare le credenziali per un account.|Basso| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Ragione o codice di errore

-   Deve essere conforme con la definizione del protocollo.

-   Nessuna intestazione Syslog.

-   La parte dell'intestazione (la parte che è separata da un pipe) deve esistere (come stabilito nel protocollo).

-   Le chiavi seguenti della parte dell'_estensione_ devono essere presenti nell'evento:

    -   externalId = l'ID evento di Windows

    -   rt = il timestamp dell'evento effettivo (assicurarsi che non sia il timestamp dell'arrivo al SIEM o dell'invio ricevuto). Preferibilmente con la precisione ai millisecondi, questo è molto importante.

    -   cat = il nome del registro eventi di Windows

    -   shost = il nome dell'host di origine

    -   dhost = il computer che riceve l'evento (il DC in questo caso)

    -   duser = il nome dell'utente che si autentica

-   L'ordine non è importante per la parte dell'_estensione_

-   Deve essere presente una chiave personalizzata e una keyLable per questi due campi:

    -   “EventSource”

    -   “Ragione o codice di errore” = Il codice risultato di NTLM

#### Splunk
&lt;Syslog Header&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

Il computer ha tentato di convalidare le credenziali per un account.

Pacchetto di autenticazione:              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Account di accesso: amministratore

Workstation di origine:       SIEM

Codice di errore:         0x0

-   L'intestazione Syslog è facoltativa.

-   C'è un separatore di caratteri "\r\n" fra i singoli campi richiesti.

-   I campi sono nel formato chiave=valore.

-   Le seguenti chiavi devono esistere e avere un valore:

    -   EventCode = l'ID evento di Windows

    -   Logfile = il nome del registro eventi di Windows

    -   SourceName = il nome del provider di eventi di Windows

    -   TimeGenerated = Il timestamp dell'evento effettivo (assicurarsi che non sia il timestamp dell'arrivo al SIEM o dell'invio ad ATA). Il formato deve corrispondere ad aaaaMMggHHmmss.FFFFFF, preferibilmente con la precisione ai millisecondi, questo è molto importante.

    -   ComputerName = il nome dell'host di origine

    -   Message = il testo dell'evento originale dall'evento di Windows

-   La chiave e il valore del messaggio DEVONO essere ultimi.

-   L'ordine non è importante per le coppie chiave=valore.

#### QRadar
QRadar consente la raccolta di eventi tramite un agente. Se i dati vengono raccolti tramite un agente, il formato ora viene raccolto senza dati in millisecondi. Dal momento che ATA richiede dati in millisecondi, è necessario impostare QRadar per usare la raccolta di eventi di Windows senza agente. Per altre informazioni, vedere [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol")..

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

I campi necessari sono:

- Il tipo di agente per la raccolta
- Il nome del provider del registro eventi di Windows
- La fonte del registro eventi di Windows
- Il nome dominio completo del controller di dominio
- L'ID evento di Windows

TimeGenerated = Il timestamp dell'evento effettivo (assicurarsi che non sia il timestamp dell'arrivo al SIEM o dell'invio ad ATA). Il formato deve corrispondere ad aaaaMMggHHmmss.FFFFFF, preferibilmente con la precisione ai millisecondi, questo è molto importante.

Message = il testo dell'evento originale dell'evento di Windows

Assicurarsi che \t sia presente tra le coppie chiave=valore.

>[!NOTE] L'uso della raccolta eventi WinCollect per Windows non è supportato.

## Configurazione dell'inoltro degli eventi di Windows
Se non si ha un server SIEM è possibile configurare i controller di dominio in modo da inoltrare l'ID evento di Windows 4776 direttamente a uno dei gateway ATA.

1.  Accedere a tutti i controller di dominio e ai computer gateway ATA usando un account di dominio con i privilegi di amministratore.
2. Assicurarsi che tutti i controller di dominio e i gateway ATA a cui ci si connette siano uniti allo stesso dominio.
3.  Su ciascun controller di dominio digitare quanto segue a un prompt dei comandi con privilegi elevati:
```
winrm quickconfig
```
4.  Sul gateway ATA digitare quanto segue al prompt dei comandi con privilegi elevati:
```
wecutil qc
```
5.  Su ciascun controller di dominio, in **Utenti e computer di Active Directory**, passare alla cartella **Builtin** e fare doppio clic sul gruppo **Lettori registri eventi**.<br>
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)<br>
Fare clic con il pulsante destro del mouse e selezionare **Proprietà**. Sulla scheda **Membri** aggiungere l'account computer di ciascun gateway ATA.
![popup dell'agente di lettura del registro eventi wef_ad](media/wef_ad-event-log-reader-popup.png)
6.  Nel gateway ATA aprire il Visualizzatore eventi e fare clic con il pulsante destro del mouse su **Sottoscrizioni**, quindi selezionare **Create Subscription** (Crea sottoscrizione)..  

    a. Sotto **Tipo sottoscrizione e computer di origine** fare clic su **Seleziona computer**, aggiungere i controller di dominio e verificare la connettività.
    ![proprietà wef_subscription](media/wef_subscription-prop.png)

    b. Sotto **Eventi da raccogliere** fare clic su **Seleziona eventi**. Selezionare **Per registro** e scorrere verso il basso per selezionare **Sicurezza**. Nel campo **Includes/Excludes Event IDs** (Includi/Escludi ID evento) digitare **4776**..<br>
    ![wef_4776](media/wef_4776.png)

    c. In **Change user account or configure advanced settings** (Modificare l'account utente o configurare le impostazioni avanzate) fare clic su **Avanzate**..
Impostare l'opzione **Protocollo** su **HTTP** e **Porta** su **5985**..<br>
    ![wef_http](media/wef_http.png)

7.  [Facoltativo] Se si desidera un intervallo di polling più breve, nel gateway ATA impostare l'heartbeat sottoscrizione su 5 secondi per una velocità di polling maggiore.
    wecutil ss <CollectionName>/cm:custom
    wecutil ss <CollectionName> /hi:5000

8. Nella pagina di configurazione del gateway ATA attivare **Windows Event Forwarding Collections** (Raccolta di inoltro eventi di Windows)..

> [!NOTE]
Quando si attiva questa impostazione, il gateway ATA cercherà nel registro degli eventi inoltrati gli eventi di Windows che gli sono stati inoltrati dai controller di dominio.

Per altre informazioni vedere: [Configurare i computer per l'inoltro e la raccolta degli eventi](https://technet.microsoft.com/en-us/library/cc748890)

## Vedere anche
- [Installare ATA](install-ata.md)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


