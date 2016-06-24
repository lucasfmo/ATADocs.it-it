---
# required metadata

title: "Guida alla migrazione: aggiornamento di ATA alla versione 1.5 | Microsoft Advanced Threat Analytics"
description: "Procedure per aggiornare ATA alla versione 1.5"
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

# Guida alla migrazione: aggiornamento di ATA alla versione 1.5
L'aggiornamento di ATA alla versione 1.5 offre miglioramenti nelle aree seguenti:

-   Tempi di rilevamento più rapidi

-   Algoritmo di rilevamento automatico migliorato per i dispositivi NAT (Network Address Translation)

-   Processo di risoluzione dei nomi migliorato per i dispositivi non appartenenti a un dominio

-   Supporto per la migrazione dei dati durante gli aggiornamenti del prodotto

-   Maggiore velocità di risposta dell'interfaccia utente per le attività sospette con migliaia di entità coinvolte

-   Risoluzione automatica degli avvisi di monitoraggio migliorata

-   Contatori delle prestazioni aggiuntivi per il monitoraggio e la risoluzione dei problemi avanzati

## Aggiornamento di ATA alla versione 1.5
> [!NOTE]
> Se ATA non è installato nell'ambiente in uso, scaricare la versione completa di ATA che include la versione 1.5 e seguire la procedura di installazione standard descritta in [Install ATA](/advanced-threat-analytics/deploy-use/install-ata) (Installare ATA)..

Se è già distribuita la versione 1.4 di ATA, questa procedura descrive il processo di aggiornamento dell'installazione.

Seguire questa procedura per l'aggiornamento ad ATA versione 1.5:

1.  [Scaricare l'aggiornamento 1.5](http://aka.ms/ata1_5update)
      > [!NOTE]
         È anche possibile usare la versione di ATA completa e aggiornata per eseguire l'aggiornamento alla versione 1.5.


2.  Aggiornare il Centro ATA

3.  Scaricare il pacchetto del gateway ATA aggiornato

4.  Aggiornare i gateway ATA

    > [!IMPORTANT]
    > Aggiornare tutti i gateway ATA per verificare che ATA funzioni correttamente.

### Passaggio 1: Aggiornare il Centro ATA

1.  Eseguire il backup del database: facoltativo

    -   Se il Centro ATA è in esecuzione come macchina virtuale e si desidera applicare un punto di arresto, arrestare innanzitutto la macchina virtuale.

    -   Se il Centro ATA è in esecuzione su un server fisico, seguire la procedura consigliata per [eseguire il backup di MongoDB](https://docs.mongodb.org/manual/core/backups/)..

2.  Eseguire il file di aggiornamento Microsoft ATA Center Update.exe e seguire le istruzioni visualizzate per installare l'aggiornamento.

    1.  Nella pagina **iniziale** selezionare la lingua e fare clic su **Next** (Avanti)..

    2.  Leggere il contratto di licenza con l'utente finale e, se si accettano i termini, fare clic sulla casella di controllo e quindi su **Next** (Avanti)..

    3.  Selezionare se si desidera eseguire la migrazione completa (impostazione predefinita) o parziale.

        ![Scegliere la migrazione completa o parziale](media/ATA-center-fullpartial.png)

        -   Se si seleziona **Parziale**, l'eventuale traffico di rete raccolto e gli eventi Windows inoltrati analizzati da ATA saranno eliminati, mentre i profili comportamentali dell'utente dovranno essere nuovamente acquisiti, operazione che richiede almeno tre settimane. Se lo spazio su disco insufficiente, è opportuno eseguire una migrazione **Parziale**.

        -   Se si esegue una migrazione **Completa**, è necessario spazio aggiuntivo su disco, calcolato automaticamente nella pagina dell'aggiornamento e la migrazione può richiedere più tempo, a seconda del traffico di rete. La migrazione completa consente di mantenere tutti i dati raccolti in precedenza e i profili comportamentali dell'utente: ATA non richiede tempo aggiuntivo per apprendere i profili comportamentali e i comportamenti anomali possono essere rilevati subito dopo l'aggiornamento.

3.  Fare clic su **Aggiorna**. Dopo aver selezionato l'opzione, ATA rimane offline fino al completamento della procedura di aggiornamento.

4.  Dopo aver aggiornato il Centro ATA, i gateway ATA segnaleranno di non essere aggiornati.

    ![Immagine dei gateway non aggiornati](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Aggiornare tutti i gateway ATA per verificare che ATA funzioni correttamente.

### Passaggio 2: Scaricare il pacchetto di installazione del gateway ATA
Dopo aver configurato le impostazioni di connettività del dominio, è possibile scaricare il pacchetto di installazione dei gateway ATA.

Per scaricare il pacchetto del gateway ATA:

1.  Eliminare tutte le versioni del pacchetto del gateway ATA scaricate in precedenza.

2.  Nel computer gateway ATA aprire un browser e immettere l'indirizzo IP configurato in ATA Center per la console ATA. Quando viene visualizzata la Console ATA fare clic sull'icona delle impostazioni e selezionare **Configuration** (Configurazione)..

    ![Icona delle impostazioni di configurazione](media/ATA-config-icon.JPG)

3.  Nella scheda **ATA Gateways** (Gateway ATA) fare clic su **Download ATA Gateway Setup** (Scarica l'installazione del gateway ATA)..

4.  Salvare il pacchetto in locale.

Il file ZIP include quanto segue:

-   Programma di installazione del gateway ATA

-   File delle impostazioni di configurazione contenente le informazioni necessarie per connettersi al Centro ATA

### Passaggio 3: Aggiornare i gateway ATA

1.  Su ogni gateway ATA, estrarre i file dal pacchetto del ATA Gateway ed eseguire il file Microsoft ATA Gateway Setup.

    > [!NOTE]
    > È anche possibile usare questo pacchetto ATA Gateway per installare nuovi gateway ATA.

2.  Le impostazioni precedenti verranno mantenute, ma potrebbero essere necessari alcuni minuti per il riavvio del servizio.

3.  Ripetere questo passaggio per tutti gli altri gateway ATA distribuiti.

> [!NOTE]
> Dopo aver aggiornato correttamente un gateway ATA, la notifica non aggiornata relativa al gateway ATA specifico non viene più visualizzata.

Sarà possibile sapere che tutti i gateway ATA sono stati aggiornati quando tutti i gateway segnalano l'avvenuta sincronizzazione e non viene più visualizzato il messaggio che informa della disponibilità di un pacchetto ATA Gateway aggiornato.

![Immagine dei gateway aggiornati](media/ATA-gw-updated.png)

## Vedere anche

- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


