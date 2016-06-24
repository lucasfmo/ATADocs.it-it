---
# required metadata

title: Installare ATA - Passaggio 1 | Microsoft Advanced Threat Analytics
description: Il primo passaggio per installare ATA richiede di scaricare e installare il centro ATA sul server selezionato.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installare ATA - Passaggio 1

>[!div class="step-by-step"]

[Passaggio 2 »](install-ata-step2.md)

Questa procedura di installazione contiene le istruzioni necessarie per una nuova installazione di ATA 1.6. Per informazioni sull'aggiornamento di una distribuzione ATA esistente da una versione precedente, vedere la [guida per la migrazione di ATA alla versione 1.6](/advanced-threat-analytics/understand-explore/ata-update-1.6-migration-guide).

> [!IMPORTANT] Installare KB2934520 nel server ATA Center e nei server gateway ATA prima di iniziare l'installazione, altrimenti durante l'installazione di ATA verrà installato questo aggiornamento e sarà richiesto un riavvio nel corso della procedura di installazione di ATA.

## Passaggio 1. Scaricare e installare il centro ATA
Dopo aver verificato che il server soddisfi i requisiti, è possibile procedere con l'installazione del centro ATA.

Eseguire i passaggi seguenti sul server del centro ATA.

1.  Scaricare ATA dal [Centro servizi per contratti multilicenza](https://www.microsoft.com/Licensing/servicecenter/default.aspx), dal [TechNet Evaluation Center](http://www.microsoft.com/en-us/evalcenter/) o da [MSDN](https://msdn.microsoft.com/en-us/subscriptions/downloads).

2.  Accedere al computer in cui si sta installando ATA Center come utente membro del gruppo Administrators locale.

3.  Eseguire **Microsoft ATA Center Setup.EXE** e seguire l'installazione guidata.

4.  Se Microsoft .Net Framework non è installato, verrà richiesto di farlo all'avvio dell'installazione. Dopo l'installazione di .NET Framework, potrebbe essere necessario riavviare il computer.
5.  Nella pagina di **benvenuto** selezionare la lingua per le schermate di installazione di ATA e fare clic su **Next** (Avanti).

6.  Leggere le Condizioni di licenza software Microsoft, selezionare la casella di controllo per accettarle e quindi fare clic su **Next** (Avanti).

7.  È consigliabile impostare gli aggiornamenti automatici di ATA. In caso contrario, verrà visualizzata la schermata **Use Microsoft Update to help keep your computer secure and up to date** (Usare Microsoft Update per mantenere il computer protetto e aggiornato). 
    ![Immagine dell'aggiornamento di ATA](media/ata_ms_update.png)

8. Selezionare **Use Microsoft Update when I check for updates (recommended)** (Usa Microsoft Update per verificare la disponibilità di aggiornamenti (scelta consigliata)). In questo modo, le impostazioni di Windows vengono modificate per abilitare gli aggiornamenti per altri prodotti Microsoft, incluso ATA, come illustrato di seguito. 
    ![Immagine dell'aggiornamento automatico di Windows](media/ata_installupdatesautomatically.png)

8.  Nella pagina **ATA Center Configuration** (Configurazione ATA Center) immettere le seguenti informazioni in base all'ambiente:

    |Campo|Descrizione|Commenti|
    |---------|---------------|------------|
    |Percorso di installazione|Questa è la posizione in cui il centro ATA sarà installato. Per impostazione predefinita si tratta di %programfiles%\Microsoft Advanced Threat Analytics\Center|Mantenere il valore predefinito|
    |Percorso dati del database|Questo è il percorso in cui i file di database di MongoDB saranno posizionati. Per impostazione predefinita si tratta di %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Modificare il percorso in una posizione in cui si dispone dello spazio necessario per consentire l'aumento determinato dal ridimensionamento. **Nota:** <ul><li>negli ambienti di produzione si deve usare un'unità che abbia spazio sufficiente in base alla pianificazione della capacità.</li><li>Per le distribuzioni grandi il database deve trovarsi su un disco fisico separato.</li></ul>Vedere l'argomento [ATA capacity planning](/advanced-threat-analytics/plan-design/ata-capacity-planning) (Pianificazione della capacità di ATA) per informazioni sulle dimensioni.|
    |Indirizzo IP del servizio centro ATA: porta|Questo è l'indirizzo IP su cui il servizio centro ATA attenderà le comunicazioni dai gateway ATA.<br /><br />**Porta predefinita:** 443|Fare clic sulla freccia rivolta in basso per selezionare l'indirizzo IP che deve essere usato dal servizio centro ATA.<br /><br />L'indirizzo IP e la porta del servizio centro ATA non possono essere gli stessi della console ATA. Assicurarsi di modificare la porta della console ATA.|
    |Certificato SSL del servizio centro ATA|Questo è il certificato che sarà usato dal servizio centro ATA.|Fare clic sull'icona della chiave per selezionare un certificato installato o un certificato autofirmato per la distribuzione in un ambiente di testing.|
    |Indirizzo IP della console ATA|Questo è l'indirizzo IP che sarà usato da IIS per la console ATA.|Fare clic sulla freccia rivolta in basso per selezionare l'indirizzo IP utilizzato dalla console ATA. **Nota:** prendere nota di questo indirizzo IP per facilitare l'accesso alla console ATA dal gateway ATA.|
    |Certificato SSL della console ATA|Questo è il certificato che deve essere usato da IIS.|Fare clic sull'icona della chiave per selezionare un certificato installato o un certificato autofirmato per la distribuzione in un ambiente di testing.|

    ![Immagine della configurazione del centro ATA](media/ATA-Center-Configuration.JPG)

10.  Fare clic su **Installa** per installare ATA Center e i relativi componenti.
    Durante l'installazione del centro ATA vengono installati e configurati i seguenti componenti:

    -   Internet Information Services (IIS)

    -   Servizio centro ATA e sito IIS della console ATA

    -   MongoDB

    -   Set di raccolta dati di monitoraggio delle prestazioni personalizzato

    -   Certificati autofirmati (se si seleziona l'opzione durante l'installazione)

11.  Al termine dell'installazione fare clic su **Avvia** per connettersi alla console ATA.
A questo punto, si passa automaticamente alla pagina delle impostazioni **General** (Generale) per continuare la configurazione e la distribuzione dei gateway ATA.
Dal momento che si esegue l'accesso al sito usando un indirizzo IP, sarà visualizzato un avviso relativo al certificato. Si tratta di un messaggio standard. Fare clic su **Continue to this website** (Continuare con il sito Web).

### Convalidare l'installazione

1.  Verificare che il servizio **Microsoft Advanced Threat Analytics Center** sia in esecuzione.
2.  Sul desktop fare clic sul collegamento **Microsoft Advanced Threat Analytics** per connettersi alla Console ATA. Eseguire l'accesso con le stesse credenziali utente che sono state usate per installare il centro ATA.



>[!div class="step-by-step"] [« Pre-installazione](preinstall-ata.md)
[Passaggio 2 »](install-ata-step2.md)

## Vedere anche

- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurare la raccolta degli eventi](configure-event-collection.md)
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO4-->


