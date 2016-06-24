---
# required metadata

title: Prerequisiti di ATA | Microsoft Advanced Threat Analytics
description: Vengono descritti i requisiti per una corretta distribuzione di ATA nell'ambiente in uso
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Prerequisiti di ATA
Questo articolo descrive i requisiti per una corretta distribuzione di ATA nell'ambiente in uso.

>[!NOTE] Per altre informazioni sulla pianificazione delle risorse e della capacità, vedere [Pianificazione della capacità di ATA](ata-capacity-planning.md).


ATA include il Centro ATA, il gateway ATA e/o il gateway ATA Lightweight. Per altre informazioni sui componenti di ATA, vedere [Architettura di ATA](ata-architecture.md).


[Prima di iniziare](#before-you-start): questa sezione elenca le informazioni da raccogliere, nonché le entità di rete e gli account necessari prima di iniziare l'installazione di ATA.

[ATA Center](#ata-center-requirements): questa sezione elenca requisiti software, hardware e impostazioni per la configurazione del server ATA Center.

[Gateway ATA](#ata-gateway-requirements): questa sezione elenca requisiti software, hardware e impostazioni per la configurazione dei server gateway ATA.

[Gateway ATA Lightweight](#ata-lightweight-gateway-requirements): questa sezione elenca i requisiti hardware e software del gateway ATA Lightweight.

[Console ATA](#ata-console): questa sezione elenca i requisiti del browser per l'esecuzione della console ATA.

![Diagramma dell'architettura di ATA](media/ATA-architecture-topology.jpg)

## Prima di iniziare
Questa sezione elenca le informazioni da raccogliere, nonché le entità di rete e gli account necessari prima di iniziare l'installazione di ATA.


-   Account utente e password con accesso in lettura a tutti gli oggetti nei domini che verranno monitorati.

    > [!NOTE] Se sono stati impostati elenchi ACL personalizzati in diverse unità organizzative (OU, Organizational Unit) nel dominio, assicurarsi che l'utente selezionato disponga delle autorizzazioni di lettura per tali unità organizzative.

-   È consigliabile tenere un elenco di tutte le subnet usate nella rete per VPN e Wi-Fi, che prevedono la riassegnazione degli indirizzi IP tra dispositivi in un intervallo di tempo molto breve (secondi o minuti).  Identificando queste subnet di lease a breve termine, si consente ad ATA di ridurre la durata della cache in base alla riassegnazione rapida tra dispositivi. Per la configurazione di subnet di lease a breve termine, vedere [Installare ATA](/advanced-threat-analytics/deploy-use/install-ata).
-   Assicurarsi che Analizzatore messaggi e Wire Shark non siano installati sul gateway ATA o sul centro ATA.
-    Facoltativo: l'utente deve avere autorizzazioni di sola lettura per il contenitore degli oggetti eliminati. In questo modo, ATA può rilevare l'eliminazione in blocco di oggetti nel dominio. Per informazioni sulla configurazione delle autorizzazioni di sola lettura per il contenitore degli oggetti eliminati, vedere la sezione relativa alla **modifica delle autorizzazioni per un contenitore di oggetti eliminati** dell'argomento [Visualizzare o impostare autorizzazioni in un oggetto directory](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Facoltativo: un account di un utente senza attività di rete. Questo account verrà configurato come utente ATA di tipo honeytoken. Per configurare l'utente di tipo honeytoken è necessario il SID dell'account utente, non il nome utente.

-   Facoltativo: oltre a raccogliere e analizzare il traffico di rete da e verso i controller di dominio, ATA può usare l'evento 4776 di Windows per migliorare ulteriormente il rilevamento degli attacchi pass-the-hash in ATA. È possibile ricevere questo evento dal sistema di gestione delle informazioni e degli eventi di sicurezza (SIEM, Security Information and Event Management) oppure impostando l'inoltro di eventi Windows dal controller di dominio. Gli eventi raccolti forniscono ad ATA informazioni aggiuntive che non sono disponibili tramite il traffico di rete del controller di dominio.


## Requisiti di ATA Center
Questa sezione elenca i requisiti per ATA Center.
### Generale
ATA Center supporta l'installazione in un server che esegue Windows Server 2012 R2. È possibile installare ATA Center in un server membro di un dominio o di un gruppo di lavoro.

È supportata l'installazione di ATA Center come macchina virtuale. 

Se si esegue ATA Center come macchina virtuale, arrestare il server prima di creare un nuovo checkpoint per evitare potenziali danni al database.
### Specifiche del server
Il database ATA richiede la **disabilitazione** dell'accesso non uniforme alla memoria (NUMA, Non-Uniform Memory Access) nel BIOS. Il sistema può fare riferimento a NUMA come interfoliazione dei nodi e in questo caso sarà necessario **abilitare** l'interfoliazione dei nodi per disabilitare NUMA. Per altre informazioni, vedere la documentazione del BIOS.<br>
Per ottenere prestazioni ottimali, impostare **Power Option** (Opzioni potenza) nel Centro ATA su **High Performance** (Prestazioni elevate).<br>
Il numero di controller di dominio monitorati e il carico di ciascun controller di dominio determinano i requisiti hardware. Per informazioni dettagliate, vedere [Pianificazione della capacità di ATA](ata-capacity-planning.md).

### Sincronizzazione dell'ora
Il server del Centro ATA, i server del gateway ATA e i controller di dominio devono essere sincronizzati con meno di 5 minuti l'uno dall'altro.


### Schede di rete
È necessario disporre di quanto segue:
-   Almeno una scheda di rete.

-   Due indirizzi IP (consigliato ma non obbligatorio)

La comunicazione tra ATA Center e il gateway ATA viene crittografata usando SSL sulla porta 443. La console ATA, inoltre, viene eseguita in IIS e protetta usando SSL sulla porta 443. Sono consigliati **due indirizzi IP**. Il servizio ATA Center assocerà la porta 443 al primo indirizzo IP e IIS assocerà la porta 443 al secondo indirizzo IP.

> [!NOTE] È possibile usare un singolo indirizzo IP con due porte diverse, ma sono consigliati due indirizzi IP.

### Porte
La tabella seguente elenca le porte minime che devono essere aperte per il corretto funzionamento di ATA Center.

In questa tabella l'indirizzo IP 1 è associato al servizio Centro ATA e l'indirizzo IP 2 è associato al servizio IIS per la Console ATA:

|Protocollo|Trasporto|Porta|A/da|Direzione|Indirizzo IP|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (comunicazioni ATA)|TCP|443 o configurabile|Gateway ATA|In ingresso|Indirizzo IP 1|
|**HTTP**|TCP|80|Rete aziendale|In ingresso|Indirizzo IP 2|
|**HTTPS**|TCP|443|Rete aziendale e gateway ATA|In ingresso|Indirizzo IP 2|
|**SMTP** (facoltativo)|TCP|25|Server SMTP|In uscita|Indirizzo IP 2|
|**SMTPS** (facoltativo)|TCP|465|Server SMTP|In uscita|Indirizzo IP 2|
|**Syslog** (facoltativo)|TCP|514|Server Syslog|In uscita|Indirizzo IP 2|

### Certificati
Assicurarsi che il Centro ATA abbia accesso al punto di distribuzione CRL. Se i gateway ATA non hanno accesso a Internet, seguire la [procedura per importare manualmente un elenco CRL](https://technet.microsoft.com/en-us/library/aa996972%28v=exchg.65%29.aspx), assicurandosi di installare tutti i punti di distribuzione CRL per l'intera catena.

Per semplificare l'installazione di ATA Center, è possibile installare certificati autofirmati durante il processo di installazione. Dopo la distribuzione, è possibile sostituire il certificato autofirmato con un certificato di un'autorità di certificazione interna per l'uso da parte del gateway ATA.<br>
> [!NOTE] Il provider del certificato deve essere di tipo provider del servizio di crittografia (CSP).


ATA Center richiede i certificati per i servizi seguenti:

-   Internet Information Services (IIS) - Certificato server Web

-   Servizio ATA Center - Certificato di autenticazione server

> [!NOTE] Se si prevede di accedere alla Console ATA da altri computer, assicurarsi che tali computer considerino attendibile il certificato usato da IIS. In caso contrario, prima di passare alla pagina di accesso verrà visualizzata una pagina di avviso che indica un problema con il certificato di protezione del sito Web.

## Requisiti del gateway ATA
Questa sezione elenca i requisiti relativi al gateway ATA.
### Generale
Il gateway ATA supporta l'installazione in un server che esegue Windows Server 2012 R2.
È possibile installare il gateway ATA in un server membro di un dominio o di un gruppo di lavoro.

Prima di installare il gateway ATA, verificare che sia stato installato l'aggiornamento seguente: [KB2919355](https://support.microsoft.com/en-us/kb/2919355/).

È possibile controllare eseguendo il cmdlet di Windows PowerShell seguente: `[Get-HotFix -Id kb2919355]`.

Per informazioni sull'uso di macchine virtuali con il gateway ATA, vedere [Configurare il mirroring delle porte](/advanced-threat-analytics/deploy-use/configure-port-mirroring).

### Specifiche del server
Per ottenere prestazioni ottimali, impostare **Power Option** nel gateway ATA su **High Performance**.<br>
Un gateway ATA può supportare il monitoraggio di più controller di dominio, a seconda della quantità di traffico di rete da e verso i controller di dominio.


### Sincronizzazione dell'ora
Il server del Centro ATA, i server del gateway ATA e i controller di dominio devono essere sincronizzati con meno di 5 minuti l'uno dall'altro.

### Schede di rete
Il gateway ATA richiede almeno una scheda di gestione e almeno una scheda di acquisizione:

-   **Scheda di gestione**: verrà usata per le comunicazioni nella rete aziendale. Questa scheda deve essere configurata con gli elementi seguenti:

    -   Indirizzo IP statico con gateway predefinito

    -   Server DNS preferito e alternativo

    -   L'opzione **DNS suffix for this connection** deve corrispondere al nome DNS del dominio per ogni dominio monitorato.

        ![Configurare il suffisso DNS nelle impostazioni TCP/IP avanzate](media/ATA-DNS-Suffix.png)

        > [!NOTE] Se il gateway ATA è un membro del dominio, questa impostazione viene configurata automaticamente.

-   **Scheda di acquisizione**: verrà usata per acquisire il traffico da e verso i controller di dominio.

    > [!IMPORTANT]
    > -   Configurare il mirroring delle porte per la scheda di acquisizione come destinazione del traffico di rete dei controller di dominio. Per altre informazioni, vedere [Configurare il mirroring delle porte](/advanced-threat-analytics/deploy-use/configure-port-mirroring). Per la configurazione del mirroring delle porte è in genere necessario collaborare con il team che si occupa della rete o della virtualizzazione.
    > -   Configurare un indirizzo IP statico non indirizzabile per l'ambiente senza gateway predefinito e senza indirizzi server DNS. Ad esempio, 1.1.1.1/32. Ciò garantisce che la scheda di rete di acquisizione possa acquisire la quantità massima di traffico e la scheda di rete di gestione venga usata per inviare e ricevere il traffico di rete richiesto.

### Porte
La tabella seguente elenca le porte minime che il gateway ATA richiede che vengano configurate nella scheda di gestione:

|Protocollo|Trasporto|Porta|A/da|Direzione|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP e UDP|389|Controller di dominio|In uscita|
|LDAP sicuro (LDAPS, Secure LDAP)|TCP|636|Controller di dominio|In uscita|
|LDAP verso il catalogo globale|TCP|3268|Controller di dominio|In uscita|
|LDAPS verso il catalogo globale|TCP|3269|Controller di dominio|In uscita|
|Kerberos|TCP e UDP|88|Controller di dominio|In uscita|
|Netlogon|TCP e UDP|445|Controller di dominio|In uscita|
|Ora di Windows|UDP|123|Controller di dominio|In uscita|
|DNS|TCP e UDP|53|Server DNS|In uscita|
|NTLM su RPC|TCP|135|Tutti i dispositivi nella rete|In uscita|
|NetBIOS|UDP|137|Tutti i dispositivi nella rete|In uscita|
|SSL|TCP|443 o in base a quanto configurato per il servizio ATA Center|ATA Center:<br /><br />- Indirizzo IP del servizio ATA Center<br />- Indirizzo IP di IIS|In uscita|
|Syslog (facoltativo)|UDP|514|Server SIEM|In ingresso|

> [!NOTE] Per il processo di risoluzione eseguito dal gateway ATA, è necessario che le porte seguenti siano aperte nei dispositivi in rete per il traffico in ingresso proveniente dai gateway ATA.
>
> -   NTLM su RPC
> -   NetBIOS

### Certificati
Assicurarsi che il Centro ATA abbia accesso al punto di distribuzione CRL. Se i gateway ATA non hanno accesso a Internet, seguire la procedura per importare manualmente un elenco CRL, assicurandosi di installare tutti i punti di distribuzione CRL per l'intera catena.<br>
Per semplificare l'installazione di ATA Center, è possibile installare certificati autofirmati durante il processo di installazione. Dopo la distribuzione, è possibile sostituire il certificato autofirmato con un certificato di un'autorità di certificazione interna per l'uso da parte del gateway ATA.

> [!NOTE]
Il provider del certificato deve essere di tipo provider del servizio di crittografia (CSP).<br>

Nell'archivio del computer locale del gateway ATA deve essere installato un certificato che supporti l'**autenticazione server**. Tale certificato deve essere considerato attendibile da ATA Center.

## Requisiti del gateway ATA Lightweight
Questa sezione elenca i requisiti relativi al gateway ATA Lightweight.
### Generale
Il gateway ATA Lightweight supporta l'installazione in un controller di dominio che esegue Windows Server 2008 R2, Windows Server 2012 o Windows Server 2012 R2.

Il controller di dominio deve essere un controller di dominio di sola lettura (RODC).

Il controller di dominio non può essere Server Core.

### Specifiche del server

Il gateway ATA Lightweight richiede almeno 2 core e 6 GB di RAM installati nel controller di dominio.
Per ottenere prestazioni ottimali, impostare **Power Option** (Opzioni potenza) nel gateway ATA Lightweight su **High Performance** (Prestazioni elevate).
Il gateway ATA Lightweight può essere distribuito su controller di dominio di diversi carichi e dimensioni, a seconda della quantità di traffico di rete da e verso i controller di dominio e della quantità di risorse installate in tali controller di dominio.

### Sincronizzazione dell'ora
Il server del Centro ATA, i server del gateway ATA Lightweight e i controller di dominio devono essere sincronizzati con meno di 5 minuti l'uno dall'altro.
### Schede di rete
Il gateway ATA Lightweight esegue il monitoraggio del traffico locale su tutte le schede di rete dei controller di dominio. <br>
Dopo la distribuzione, è possibile usare la Console ATA per modificare l'elenco delle schede di rete da monitorare.

### Porte
La tabella seguente elenca le porte minime richieste dal gateway ATA Lightweight.

|Protocollo|Trasporto|Porta|A/da|Direzione|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP e UDP|53|Server DNS|In uscita|
|NTLM su RPC|TCP|135|Tutti i dispositivi nella rete|In uscita|
|NetBIOS|UDP|137|Tutti i dispositivi nella rete|In uscita|
|SSL|TCP|443 o in base a quanto configurato per il servizio ATA Center|ATA Center:<br /><br />- Indirizzo IP del servizio ATA Center<br />- Indirizzo IP di IIS|In uscita|
|Syslog (facoltativo)|UDP|514|Server SIEM|In ingresso|

> [!NOTE] Per il processo di risoluzione eseguito dal gateway ATA Lightweight, è necessario che le porte seguenti siano aperte nei dispositivi in rete per il traffico in ingresso proveniente dai gateway ATA Lightweight.
>
> -   NTLM su RPC
> -   NetBIOS

### Certificati
Assicurarsi che il Centro ATA abbia accesso al punto di distribuzione CRL. Se i gateway ATA Lightweight non hanno accesso a Internet, seguire la procedura per importare manualmente un elenco CRL, assicurandosi di installare tutti i punti di distribuzione CRL per l'intera catena.
Per semplificare l'installazione di ATA Center, è possibile installare certificati autofirmati durante il processo di installazione. Dopo la distribuzione, è possibile sostituire il certificato autofirmato con un certificato di un'autorità di certificazione interna per l'uso da parte del gateway ATA Lightweight.
> [!NOTE]
Il provider del certificato deve essere di tipo provider del servizio di crittografia (CSP).

Nell'archivio del computer locale del gateway ATA Lightweight deve essere installato un certificato che supporti l'autenticazione server. Tale certificato deve essere considerato attendibile da ATA Center.

## Console ATA
L'accesso alla console ATA avviene con un browser, che supporta quanto segue:

-   Internet Explorer 10 e versioni successive

-   Google Chrome 40 e versioni successive

-   Risoluzione minima dello schermo di 1700 pixel

## Vedere anche

- [Architettura di ATA](ata-architecture.md)
- [Installare ATA](/advanced-threat-analytics/deploy-use/install-ata)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO4-->


