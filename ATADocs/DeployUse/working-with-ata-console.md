---
# required metadata

title: Uso della Console ATA | Microsoft Advanced Threat Analytics
description: Viene descritto come accedere alla Console ATA e ai relativi componenti
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Uso della console ATA

Usare la Console ATA per monitorare e rispondere a eventuali attività sospette rilevate da ATA.

## Abilitazione dell'accesso alla Console ATA
Tutti gli utenti membri del gruppo Administrators locale sul server del Centro ATA dispongono dell'autorizzazione per accedere alla Console ATA e gestire le impostazioni di ATA.
Per consentire all'utente di accedere alla Console ATA senza diritti di amministratore locale, aggiungerlo al gruppo locale **Microsoft Advanced Threat Analytics Administrators**.

## Accesso alla Console ATA

1. Nel server ATA Center fare clic sull'icona **Microsoft ATA Console** (Console Microsoft ATA) sul desktop oppure aprire un browser e passare alla Console ATA.

    ![Icona server ATA](media/ata-server-icon.png)

    > [!NOTE]È anche possibile aprire un browser da ATA Center o dal gateway ATA e passare all'indirizzo IP configurato nell'installazione di ATA Center per la Console ATA.    

2.  Immettere nome utente e password, quindi fare clic su **Accedi**.

![Immagine della schermata di accesso ATA](media/ATA-log-in-screen.jpg)

    > [!NOTE]
    > You have to log in with a user who is a member of the local administrator group OR of the Microsoft Advanced Threat Analytics Administrators group.

## Console ATA

La Console ATA fornisce una rapida panoramica di tutte le attività sospette in ordine cronologico. Consente di esaminare i dettagli di qualsiasi attività ed eseguire azioni basate su tali attività. Nella Console vengono visualizzati anche avvisi e notifiche per evidenziare problemi della rete ATA o nuove attività sospette.

Questi sono gli elementi principali della Console ATA.


### Sequenza temporale degli attacchi

Questa è la pagina di destinazione predefinita che viene visualizzata quando si accede alla Console ATA. Per impostazione predefinita, tutte le attività sospette aperte vengono visualizzate sulla sequenza temporale. È possibile filtrare la sequenza temporale degli attacchi per visualizzare le attività sospette in base ai filtri Tutte, Aperte, Ignorate o Risolte. È anche possibile visualizzare il livello di gravità assegnato a ogni attività.

![Immagine della sequenza temporale degli attacchi ATA](media/attack-timeline.png)

Per altre informazioni, vedere [Working with suspicious activities](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities) (Gestione di attività sospette).

### Barra di notifica

Quando viene rilevata una nuova attività sospetta, la barra di notifica si apre automaticamente sul lato destro. Se sono presenti nuove attività sospette dall'ultima connessione, la barra di notifica si aprirà dopo il corretto accesso dell'utente. Per accedervi, è possibile fare clic sulla freccia a destra nella barra di notifica in qualsiasi momento.

![Immagine della barra di notifica ATA](media/notification-bar.png)

### Pannello di filtraggio

È possibile filtrare le attività sospette visualizzate nella sequenza temporale degli attacchi o nella scheda delle attività sospette del profilo di entità in base a Stato e Gravità.

### Barra di ricerca

Nel menu in alto è disponibile una barra di ricerca, che consente di cercare un utente, un computer o gruppi specifici in ATA. Per fare una prova, iniziare a digitare.

![Immagine ricerca Console ATA](media/ATA-console-search.png)

### Centro di integrità

Il Centro di integrità fornisce avvisi in presenza di un'anomalia di funzionamento nella distribuzione ATA.

![Immagine del Centro di integrità ATA](media/health-center.png)

Ogni volta che il sistema rileva un problema, ad esempio un errore di connettività o un gateway ATA disconnesso, l'icona del Centro di integrità notifica questo evento visualizzando un punto rosso. ![Immagine del punto rosso del Centro di integrità ATA](media/ATA-Health-Center-Alert-red-dot.png)

Gli avvisi del Centro di integrità possono essere ignorati o risolti e prevedono tre livelli di gravità: Alta, Media, Bassa. Se si risolve un avviso che il servizio ATA rileva ancora come attivo, questo verrà spostato automaticamente nell'elenco degli avvisi aperti. Se il sistema rileva che la causa di un avviso non sussiste più, ad esempio se la situazione è stata corretta, l'avviso verrà spostato automaticamente nell'elenco degli avvisi risolti.

### Profili utente e computer

ATA crea un profilo per ogni utente e computer nella rete. Nel profilo utente sono visualizzate le informazioni generali, ad esempio l'appartenenza al gruppo, gli ultimi accessi e le risorse usate di recente.

![Profilo utente](media/user-profile.png)

Nel profilo computer sono visualizzate le informazioni generali, ad esempio gli ultimi accessi e le risorse usate di recente.

![Profilo computer](media/computer-profile.png)

ATA fornisce informazioni aggiuntive sulle entità, ad esempio computer, dispositivi, utenti, nelle pagine seguenti: Riepilogo, Attività e Attività sospette.

I profili non completamente risolti da ATA sono identificati da un'icona a semicerchio accanto ad essi.


![Immagine di un profilo non risolto da ATA](media/ATA-Unresolved-Profile.jpg)

### Profilo breve

Se si posiziona il puntatore del mouse in qualsiasi parte della console in cui è presente una singola entità, ad esempio un utente o un computer, verrà automaticamente aperto un profilo breve contenente le informazioni seguenti, se disponibili:

![Immagine del profilo breve ATA](media/ATA-mini-profile.jpg)

-   Nome

-   Immagine

-   Posta elettronica

-   Telefono

-   Numero di attività sospette in base alla gravità



## Vedere anche
[Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


