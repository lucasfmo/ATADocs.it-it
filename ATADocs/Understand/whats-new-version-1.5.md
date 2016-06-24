---
# required metadata

title: Novità in ATA versione 1.5 | Microsoft Advanced Threat Analytics
description: Vengono elencate le novità in ATA versione 1.5 e i problemi noti
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Novità in ATA versione 1.5
Queste note sulla versione offrono informazioni sui problemi noti relativi a questa versione di Advanced Threat Analytics.

## Novità nell'aggiornamento ad ATA 1.5
L'aggiornamento ad ATA 1.5 offre miglioramenti nelle aree seguenti:

-   Tempi di rilevamento più rapidi

-   Algoritmo di rilevamento automatico migliorato per i dispositivi NAT (Network Address Translation)

-   Processo di risoluzione dei nomi migliorato per i dispositivi non appartenenti a un dominio

-   Supporto per la migrazione dei dati durante gli aggiornamenti del prodotto

-   Maggiore velocità di risposta dell'interfaccia utente per le attività sospette con migliaia di entità coinvolte

-   Risoluzione automatica degli avvisi di monitoraggio migliorata

-   Contatori delle prestazioni aggiuntivi per la risoluzione dei problemi e il monitoraggio avanzati

## Problemi noti
Questa versione presenta i problemi noti descritti di seguito.

### L'installazione di un nuovo gateway ATA non riesce
Dopo aver aggiornato la distribuzione di ATA ad ATA versione 1.5, viene visualizzato l'errore seguente quando si installa un nuovo gateway ATA: Microsoft Advanced Threat Analytics Gateway is not installed (Il gateway Microsoft Advanced Threat Analytics non è installato)

![Errore del gateway ATA](media/ata-install-error.png)

<b>Soluzione:</b> inviare un'email a <ataeval@microsoft.com> per richiedere i passaggi per la risoluzione del problema.
### Distribuzione
La cartella specificata per il percorso dei dati del database e per il percorso del journal del database deve essere vuota, ovvero non deve contenere file o sottocartelle.
In caso contrario, la distribuzione non proseguirà.

### Installazione da file ZIP
Quando si installa il gateway ATA, assicurarsi di estrarre i file dal file ZIP in una directory locale e di installarlo da questa directory. Non installare il gateway ATA direttamente dal file ZIP, altrimenti l'installazione non riuscirà.

### Configurazione
Quando dopo aver impostato la configurazione per un gateway ATA questo viene avviato per la prima volta, viene visualizzata l'etichetta "Not Synced" fino a quando il servizio non è completamente avviato, operazione che può richiedere fino a 10 minuti per il primo avvio del servizio.

### Software di acquisizione di rete
Nel gateway ATA l'unico software di acquisizione di rete supportato che è possibile installare è [Microsoft Network Monitor 3.4](http://www.microsoft.com/en-us/download/details.aspx?id=4865). Non installare Microsoft Message Analyzer o altro software di acquisizione di rete. L'installazione di un software diverso impedisce immediatamente il funzionamento corretto del gateway ATA.

### Hotfix della Knowledge Base nell'host di virtualizzazione
Non installare l'hotfix disponibile nell'articolo KB 3047154 in un host di virtualizzazione. Questa operazione potrebbe impedire il corretto funzionamento del mirroring delle porte.

## Vedere anche

[Update ATA to version 1.5 - migration guide (Aggiornare ATA alla versione 1.5 - Guida alla migrazione)](ata-update-1.5-migration-guide.md)

[Update ATA to version 1.6 - migration guide (Aggiornare ATA alla versione 1.6 - Guida alla migrazione)](ata-update-1.6-migration-guide.md)

[Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


