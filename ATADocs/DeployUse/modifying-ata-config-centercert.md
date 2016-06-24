---
# required metadata

title: Modificare la configurazione di ATA - Certificato di ATA Center | Microsoft Advanced Threat Analytics
description: Viene descritto il processo in due fasi per il rinnovo o la sostituzione del certificato nell'archivio del computer locale nel server ATA Center. 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Modificare la configurazione di ATA - Certificato di ATA Center

>[!div class="step-by-step"]
[« Indirizzo IP del server ATA Center](modifying-ata-config-centerip.md)
[Indirizzo IP della console ATA »](modifying-ata-config-consoleip.md)

## Modificare il certificato di ATA Center
Se i certificati scadono e devono essere rinnovati o sostituiti dopo l'installazione del nuovo certificato nell'archivio del computer locale nel server ATA Center, sostituire il certificato tramite il processo in due fasi seguente:

-   Prima fase: aggiornare il certificato che dovrà essere usato dal servizio ATA Center. A questo punto, il servizio ATA Center è ancora associato al certificato originale. Quando i gateway ATA sincronizzano la propria configurazione, avranno due possibili certificati validi per l'autenticazione reciproca. Purché il gateway ATA possa connettersi usando il certificato originale, non tenterà di usare quello nuovo.

-   Seconda fase: al termine della sincronizzazione di tutti i gateway con la configurazione aggiornata, è possibile attivare il nuovo certificato cui è associato il servizio ATA Center. Quando si attiva il nuovo certificato, il servizio ATA Center esegue l'associazione al certificato. I gateway ATA non riusciranno a eseguire correttamente l'autenticazione reciproca del servizio ATA Center e proveranno l'autenticazione tramite il secondo certificato. Una volta connesso al servizio ATA Center, il gateway ATA acquisisce la configurazione più recente e ha quindi un singolo certificato per ATA Center, a meno che il processo non sia stato avviato di nuovo.

> [!NOTE]
> -   Se un gateway ATA era offline durante la prima fase e non ha ottenuto la configurazione aggiornata, è necessario aggiornare manualmente il file JSON di configurazione nel gateway ATA.
> -   Il certificato usato deve essere ritenuto attendibile dai gateway ATA.
> -   Se è necessario distribuire un nuovo gateway ATA dopo aver attivato il nuovo certificato, è necessario scaricare di nuovo il pacchetto di installazione dei gateway ATA.

1.  Aprire la console ATA.

2.  Selezionare l'opzione delle impostazioni sulla barra degli strumenti e quindi **Configurazione**..

    ![Icona delle impostazioni di configurazione di ATA](media/ATA-config-icon.JPG)

3.  Selezionare **ATA Center**.

4.  In **Certificate** selezionare uno dei certificati nell'elenco.

5.  Fare clic su **Salva**..

6.  Verrà visualizzata una notifica del numero di gateway ATA sincronizzati con la configurazione più recente.

7.  Al termine della sincronizzazione di tutti i gateway ATA, fare clic su **Activate** per attivare il nuovo certificato.
    >[!IMPORTANT]
    >Prima di attivare la nuova configurazione, verificare che tutti i gateway ATA siano sincronizzati con la configurazione più recente. L'attivazione della nuova configurazione prima di tale sincronizzazione può causare un'interruzione del funzionamento previsto del gateway ATA. Se uno dei gateway ATA non viene sincronizzato, si verificherà questo errore quando si fa clic su Attiva:
    >
    >    ![Errore di sincronizzazione dei gateway ATA](media/ataGW-not-synced.png)

8.  Assicurarsi che tutti i gateway ATA riescano a sincronizzare le proprie configurazioni dopo l'attivazione della modifica.

>[!div class="step-by-step"]
[« Indirizzo IP del server ATA Center](modifying-ata-config-centerip.md)
[Indirizzo IP della console ATA »](modifying-ata-config-consoleip.md)

## Vedere anche
- [Uso della console ATA](working-with-ata-console.md)
- [Installare ATA](install-ata.md)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


