---
# required metadata

title: "Guida alla migrazione: aggiornamento di ATA alla versione 1.6 | Microsoft Advanced Threat Analytics"
description: "Procedure per aggiornare ATA alla versione 1.6"
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guida alla migrazione: aggiornamento di ATA alla versione 1.6
L'aggiornamento ad ATA 1.6 offre miglioramenti nelle aree seguenti:

-   Nuovi rilevamenti

-   Miglioramenti dei rilevamenti esistenti

-   Gateway ATA Lightweight

-   Aggiornamenti automatici

-   Miglioramento delle prestazioni di ATA Center

-   Minori requisiti di archiviazione

-   Supporto per IBM QRadar

## Aggiornamento di ATA alla versione 1.6
> [!NOTE] Se ATA non è installato nell'ambiente in uso, scaricare la versione completa di ATA che include la versione 1.6 e seguire la procedura di installazione standard descritta in [Install ATA](/advanced-threat-analytics/deploy-use/install-ata) (Installare ATA).

Se è già distribuita la versione 1.5 di ATA, questa procedura descrive il processo di aggiornamento della distribuzione.

> [!NOTE] Non è possibile installare la versione 1.6 di ATA sulla versione 1.4. Installare prima la versione 1.5 di ATA. Se per errore si è tentato di installare la versione 1.6 di ATA senza aver prima installato la versione 1.5, verrà visualizzato un errore a indicare che **nel computer è già installata una versione più recente**. Prima di installare la versione 1.5 di ATA, è quindi necessario disinstallare le parti rimanenti della versione 1.6 di ATA, che resteranno tuttavia nel computer anche se l'installazione non è riuscita.

Seguire questa procedura per l'aggiornamento ad ATA versione 1.6:

1. Prima di iniziare il processo di aggiornamento, è necessario seguire la procedura per gestire [l'errore di migrazione durante l'aggiornamento alla versione 1.6 di ATA](whats-new-version-1.6#Migration-failure-when-updating-from-ATA-1.5)
2. Assicurarsi che lo spazio disponibile sia sufficiente a completare l'aggiornamento. Eseguire l'installazione fino al punto di controllo della preparazione per ottenere una stima dello spazio disponibile necessario e quindi riavviare l'aggiornamento dopo aver allocato lo spazio su disco necessario. L'aggiornamento occuperà almeno il 2% della dimensione del database. Per altre informazioni, vedere [ATA Capacity Planning](/advanced-threat-analytics/plan-design/ata-capacity-planning) (Pianificazione della capacità ATA).
1.  [Scaricare l'aggiornamento 1.6](http://www.microsoft.com/en-us/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
In questa versione, viene usato lo stesso file di installazione (Microsoft ATA Center Setup.exe) per l'installazione di una nuova distribuzione di ATA e per l'aggiornamento delle distribuzioni esistenti.

2.  Aggiornare il Centro ATA

3.  Scaricare il pacchetto del gateway ATA aggiornato

4.  Aggiornare i gateway ATA

    > [!IMPORTANT] Aggiornare tutti i gateway ATA affinché ATA funzioni correttamente.

### Passaggio 1: Aggiornare il Centro ATA

1.  Eseguire il backup del database: facoltativo

    -   Se il Centro ATA è in esecuzione come macchina virtuale e si desidera applicare un punto di arresto, arrestare innanzitutto la macchina virtuale.

    -   Se il Centro ATA è in esecuzione su un server fisico, seguire la procedura consigliata per [eseguire il backup di MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Eseguire il file di installazione, Microsoft ATA Center Setup.exe, e seguire le istruzioni visualizzate per installare l'aggiornamento.

    1.  ATA 1.6 richiede che sia installato .Net Framework 4.6.1. Se non è già installato, la procedura di installazione di ATA installerà .Net Framework 4.6.1 come parte dell'installazione.<br>
    > [!NOTE]In alcuni casi per l'installazione di .Net Framework 4.6.1 può essere necessario riavviare il server. L'installazione di ATA continuerà solo dopo il riavvio del server.
5.  Nella pagina **Welcome** selezionare la lingua e fare clic su **Next**.

    6.  Leggere il contratto di licenza con l'utente finale e, se si accettano i termini, fare clic su **Avanti**.

    7.  Per ricevere gli aggiornamenti, è ora possibile usare Microsoft Update per ATA.  Nella pagina Microsoft Update scegliere **Usa Microsoft Update per verificare la disponibilità di aggiornamenti (scelta consigliata)**.
    ![Immagine aggiornamento ATA](media/ata_ms_update.png) In questo modo le impostazioni di Windows vengono modificate per abilitare gli aggiornamenti per altri prodotti Microsoft, incluso ATA, come illustrato di seguito. 
     ![Immagine dell'aggiornamento automatico di Windows](media/ata_installupdatesautomatically.png)

    8.  Prima di avviare l'installazione, ATA eseguirà un controllo di conformità. Esaminare i risultati della verifica per assicurarsi che i prerequisiti siano configurati correttamente e che si disponga almeno della quantità minima di spazio su disco. 
    ![Immagine - Controllo di conformità di ATA](media/ata_install_readinesschecks.png)

    3.  Fare clic su **Aggiorna**. Dopo aver selezionato l'opzione, ATA rimane offline fino al completamento della procedura di aggiornamento.

4.  Dopo aver aggiornato il Centro ATA, i gateway ATA segnaleranno di non essere aggiornati.

    ![Immagine dei gateway non aggiornati](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Aggiornare tutti i gateway ATA per verificare che ATA funzioni correttamente.

### Passaggio 2: Scaricare il pacchetto di installazione dei gateway ATA
Dopo aver configurato le impostazioni di connettività del dominio, è possibile scaricare il pacchetto di installazione dei gateway ATA.

Per scaricare il pacchetto dei gateway ATA:

1.  Eliminare tutte le versioni del pacchetto del gateway ATA scaricate in precedenza.

2.  Sul computer del gateway ATA aprire un browser e immettere l'indirizzo IP configurato nel Centro ATA per la Console ATA. Quando la Console ATA si apre, fare clic sull'icona delle impostazioni e selezionare **Configurazione**.

    ![Icona delle impostazioni di configurazione](media/ATA-config-icon.JPG)

3.  Nella scheda **ATA Gateways (Gateway ATA)** scheda, fare clic su **Download ATA Gateway Setup (Scarica l'installazione del gateway ATA)**.

4.  Salvare il pacchetto in locale.

Il file ZIP include quanto segue:

-   Programma di installazione del gateway ATA

-   File delle impostazioni di configurazione contenente le informazioni necessarie per connettersi al Centro ATA

### Passaggio 3: Aggiornare i gateway ATA

1.  Su ogni gateway ATA estrarre i file dal pacchetto di gateway ATA ed eseguire il file **Microsoft ATA Gateway Setup.exe**.

    > [!NOTE] È anche possibile usare questo pacchetto per installare nuovi gateway ATA.

2.  Le impostazioni precedenti verranno mantenute. Il riavvio del servizio potrebbe però richiedere alcuni minuti.

3.  Ripetere questo passaggio per tutti gli altri gateway ATA distribuiti.

> [!NOTE] Dopo aver aggiornato un gateway ATA, la notifica non aggiornata relativa al gateway ATA specifico non verrà più visualizzata.

Sarà possibile sapere che tutti i gateway ATA sono stati aggiornati quando tutti i gateway segnalano l'avvenuta sincronizzazione e non viene più visualizzato il messaggio che informa della disponibilità di un pacchetto ATA Gateway aggiornato.

![Immagine dei gateway aggiornati](media/ATA-gw-updated.png)


## Vedere anche

- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


