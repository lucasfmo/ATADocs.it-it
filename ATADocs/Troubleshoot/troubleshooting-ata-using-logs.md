---
# required metadata

title: Risoluzione dei problemi tramite i registri ATA | Microsoft Advanced Threat Analytics
description: Descrive come usare i registri ATA per risolvere i problemi
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Risoluzione dei problemi tramite i registri ATA
I registri ATA forniscono informazioni dettagliate per comprendere le operazioni svolte da ogni componente di ATA in un determinato momento.

## Registri del gateway ATA
In questa sezione, ogni riferimento al gateway ATA riguarda anche il gateway ATA Lightweight. 

I registri del gateway ATA si trovano nella sottocartella **Logs**. Nel percorso di installazione predefinito, i registri possono essere trovati in: **C:\Programmi\Microsoft Advanced Threat Analytics\Gateway\Logs**.

Il gateway ATA include i seguenti registri:

-   **Microsoft.Tri.Gateway.log**: questo file di registro contiene tutti gli eventi che si verificano nel gateway ATA (inclusi risoluzione ed errori). L'uso principale fa riferimento allo stato complessivo di tutte le operazioni nell'ordine cronologico in cui si sono verificate.

-   **Microsoft.Tri.Gateway-Resolution.log**: questo file di registro contiene i dettagli per la risoluzione delle entità visualizzate nel traffico dal gateway ATA. L'uso principale fa riferimento all'analisi dei problemi di risoluzione delle entità.

-   **Microsoft.Tri.Gateway-Errors.log**: questo file di registro contiene solo gli errori rilevati dal gateway ATA. L'uso principale fa riferimento all'esecuzione di controlli di integrità e analisi dei problemi che devono essere correlati a orari specifici.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log**: questo file di registro raggruppa tutti gli errori e le eccezioni simili e ne calcola la somma.
    Questo file è vuoto a ogni nuovo avvio del servizio gateway ATA e viene aggiornato ogni minuto. L'uso principale fa riferimento alla scoperta di eventuali nuovi errori o problemi nel gateway ATA. Grazie al raggruppamento degli errori, è facile leggere e verificare se sono presenti nuovi tipi di errori o problemi.

> [!NOTE]
> I primi tre file di registro hanno una dimensione massima di 50 MB. Quando viene raggiunta la dimensione massima, viene aperto un nuovo file di registro e quello precedente viene rinominato come "&lt;nome file originale&gt;-Archived-00000", in cui il numero aumenta a ogni nuova assegnazione del nome.

### Registri del Centro ATA
I registri del centro ATA si trovano nella sottocartella **Logs**. Nel percorso di installazione predefinito, i registri possono essere trovati in: **C:\Programmi\Microsoft Advanced Threat Analytics\Center\Logs**.

Il Centro ATA include i seguenti registri:

-   **Microsoft.Tri.Center.log**: questo file di registro contiene tutti gli eventi che si verificano nel Centro ATA, inclusi rilevamenti ed errori. L'uso principale fa riferimento allo stato complessivo di tutte le operazioni nell'ordine cronologico in cui si sono verificate.

-   **Microsoft.Tri.Center-Detection.log**: questo file di registro contiene solo i dettagli del rilevamento del Centro ATA. L'uso principale fa riferimento all'analisi dei problemi di rilevamento.

-   **Microsoft.Tri.Center-Errors.log**: questo file di registro contiene solo gli errori rilevati dal Centro ATA. L'uso principale fa riferimento all'esecuzione di controlli di integrità e analisi dei problemi che devono essere correlati a orari specifici.

-   **Microsoft.Tri.Center-ExceptionStatistics.log**: questo file di registro raggruppa tutti gli errori e le eccezioni simili e ne calcola la somma.
    Questo file è vuoto a ogni nuovo avvio del servizio Centro ATA e viene aggiornato ogni minuto. L'uso principale fa riferimento alla scoperta di eventuali nuovi errori o problemi nel centro ATA. Grazie al raggruppamento degli errori, è facile leggere e verificare se sono presenti nuovi tipi di errori o problemi.

> [!NOTE]
> I primi tre file di registro hanno una dimensione massima di 50 MB. Quando viene raggiunta la dimensione massima, viene aperto un nuovo file di registro e quello precedente viene rinominato come "&lt;nome file originale&gt;-Archived-00000", in cui il numero aumenta a ogni nuova assegnazione del nome.

### Registri della Console ATA
I registri della Console ATA (registri dell'API di gestione) si trovano in una sottocartella denominata **Logs**. Nel percorso di installazione predefinito, i registri possono essere trovati in: **C:\Programmi\Microsoft Advanced Threat Analytics\Center\Management\Logs**.

La Console ATA include i seguenti registri:

-   **w3wp.log**: questo file di registro contiene tutti gli eventi che si verificano durante il processo di gestione (IIS).


-   **w3wp-Errors.log**: questo file di registro contiene solo gli errori rilevati dal processo di gestione (IIS).


-   **8e75f9f1-ExceptionStatistics.log**: questo file di registro raggruppa tutti gli errori e le eccezioni simili e ne calcola la somma.
    Questo file è vuoto a ogni nuovo avvio del servizio gateway e viene aggiornato ogni minuto. L'uso principale fa riferimento alla scoperta di eventuali nuovi errori o problemi nel centro ATA. Grazie al raggruppamento degli errori, è facile leggere e verificare se sono presenti nuovi tipi di errori o problemi.

> [!NOTE]
> I primi due file di registro hanno una dimensione massima di 50 MB. Quando viene raggiunta la dimensione massima, viene aperto un nuovo file di registro e quello precedente viene rinominato come "&lt;nome file originale&gt;-Archived-00000", in cui il numero aumenta a ogni nuova assegnazione del nome.

### Registri di distribuzione ATA
I registri di distribuzione ATA si trovano nella directory Temp dell'utente che ha installato il prodotto. Nel percorso di installazione predefinito, i registri possono essere trovati in: **C:\Utenti\Amministratore\AppData\Local\Temp** (o in una directory superiore a %temp%).

Registri di distribuzione del Centro ATA:

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log**: questo file di registro elenca i passaggi del processo di distribuzione del Centro ATA. L'uso principale fa riferimento al monitoraggio del processo di distribuzione del centro ATA.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log**: questo file di registro elenca i passaggi del processo di distribuzione di MongoDB nel Centro ATA. L'uso principale fa riferimento al monitoraggio del processo di distribuzione di MongoDB.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log**: questo file di registro elenca i passaggi del processo di distribuzione dei file binari del Centro ATA. L'uso principale fa riferimento al monitoraggio della distribuzione dei file binari del centro ATA.

Registri di distribuzione del gateway ATA Lightweight e del gateway ATA:

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log**: questo file di registro elenca i passaggi del processo di distribuzione del gateway ATA. L'uso principale fa riferimento al monitoraggio del processo di distribuzione del gateway ATA.

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log**: questo file di registro elenca i passaggi del processo di distribuzione dei file binari del gateway ATA. L'uso principale fa riferimento al monitoraggio della distribuzione dei file binari del gateway ATA.

## Vedere anche
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Pianificazione della capacità di ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurare la raccolta degli eventi](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurazione dell'inoltro degli eventi di Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


