---
# required metadata

title: Modificare la configurazione di ATA - Indirizzo IP di ATA Center | Microsoft Advanced Threat Analytics
description: Viene descritto come modificare l'indirizzo IP, la porta o il certificato di ATA Center.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Modificare la configurazione di ATA - Indirizzo IP di ATA Center

>[!div class="step-by-step"]
[Certificato di ATA Center »](modifying-ata-config-centercert.md)

Dopo la distribuzione iniziale, le modifiche ad ATA Center devono essere apportate con attenzione. Usare le procedure seguenti quando si aggiornano l'indirizzo IP e la porta o il certificato.

## Modificare l'indirizzo IP usato dal server ATA Center
Se è necessario modificare l'indirizzo IP e la porta o il certificato di ATA Center, considerare gli aspetti seguenti.

I gateway ATA archiviano in locale l'indirizzo IP di ATA Center a cui devono connettersi. I gateway si connettono periodicamente ad ATA Center e acquisiscono le modifiche di configurazione. La modifica del modo in cui i gateway ATA si connettono ad ATA Center avviene in due fasi.

-   Prima fase: aggiornare l'indirizzo IP e la porta che dovranno essere usati dal servizio ATA Center. A questo punto, ATA Center è ancora in attesa sull'indirizzo IP originale e alla successiva sincronizzazione del gateway ATA la configurazione avrà due indirizzi IP per ATA Center. Purché il gateway ATA possa connettersi usando l'indirizzo IP originale (il primo), non tenterà di usare il nuovo indirizzo IP e la nuova porta.

-   Seconda fase: al termine della sincronizzazione di tutti i gateway con la configurazione aggiornata, attivare il nuovo indirizzo IP e la nuova porta su cui è in attesa ATA Center. Quando si attiva il nuovo indirizzo IP, il servizio ATA Center esegue l'associazione a questo indirizzo. I gateway ATA non riusciranno a connettersi all'indirizzo originale e proveranno ora a connettersi con il secondo (nuovo) indirizzo IP ottenuto per ATA Center. Una volta connesso ad ATA Center con il nuovo indirizzo IP, il gateway ATA acquisisce la configurazione più recente e ha quindi un singolo indirizzo IP per ATA Center, a meno che il processo non sia stato avviato di nuovo.

> [!NOTE]
> -   Se un gateway ATA era offline durante la prima fase e non ha ottenuto la configurazione aggiornata, è necessario aggiornare manualmente il file JSON di configurazione nel gateway ATA.
> -   Se il nuovo indirizzo IP è installato nel server ATA Center, è possibile selezionarlo nell'elenco degli indirizzi IP quando si apporta la modifica. Tuttavia, se per qualsiasi motivo non è possibile installare l'indirizzo IP nel server ATA Center, è possibile selezionarne uno personalizzato e aggiungerlo manualmente. Il nuovo indirizzo IP non potrà essere attivato finché non è installato nel server.
> -   Se è necessario distribuire un nuovo gateway ATA dopo aver attivato il nuovo indirizzo IP, è necessario scaricare di nuovo il pacchetto di installazione dei gateway ATA.

1.  Aprire la console ATA.

2.  Selezionare l'opzione delle impostazioni sulla barra degli strumenti e quindi **Configurazione**..

    ![Icona delle impostazioni di configurazione di ATA](media/ATA-config-icon.JPG)

3.  Selezionare **General** (Generale).

4.  In **ATA Center Service IP address: port** selezionare uno degli indirizzi IP esistenti oppure fare clic su **Add custom IP address** e immettere un indirizzo IP.

5.  Fare clic su **Salva**..

6.  Verrà visualizzata una notifica del numero di gateway ATA sincronizzati con la configurazione più recente.

    ![Immagine dei gateway sincronizzati con ATA Center](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >Prima di attivare la nuova configurazione, verificare che tutti i gateway ATA siano sincronizzati con la configurazione più recente. L'attivazione della nuova configurazione prima di tale sincronizzazione può causare un'interruzione del funzionamento previsto del gateway ATA. Se uno dei gateway ATA non viene sincronizzato, si verificherà questo errore quando si fa clic su Attiva:
    >
    >    ![Errore di sincronizzazione dei gateway ATA](media/ataGW-not-synced.png)


7.  Al termine della sincronizzazione di tutti i gateway ATA, fare clic su **Activate** per attivare il nuovo indirizzo IP.

    > [!NOTE]
    > Se è stato immesso un indirizzo IP personalizzato, non sarà possibile fare clic su **Activate** fino a quando l'indirizzo IP non viene installato in ATA Center.

8.  Assicurarsi che tutti i gateway ATA riescano a sincronizzare le proprie configurazioni dopo l'attivazione della modifica. La barra di notifica indicherà il numero di gateway ATA che hanno sincronizzato correttamente la propria configurazione.

>[!div class="step-by-step"]
[Modificare il certificato di ATA Center »](modifying-ata-config-centercert.md)


## Vedere anche
- [Uso della console ATA](working-with-ata-console.md)
- [Installare ATA](install-ata.md)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


