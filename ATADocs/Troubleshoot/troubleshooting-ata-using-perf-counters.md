---
# required metadata

title: Risoluzione dei problemi di ATA mediante i contatori delle prestazioni | Microsoft Advanced Threat Analytics
description: Descrive come usare i contatori delle prestazioni per la risoluzione dei problemi con ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Risoluzione dei problemi di ATA mediante i contatori delle prestazioni
I contatori delle prestazioni di ATA consentono di acquisire informazioni dettagliate sulle prestazioni di ogni componente ATA. I componenti di ATA elaborano i dati in modo sequenziale, in modo che quando si verifica un problema, viene generata una reazione a catena che causa l'interruzione del traffico. Per risolvere il problema, è necessario capire quale componente ne è all'origine e risolverlo all'inizio della catena.
Per informazioni sul flusso dei componenti ATA interni, vedere [Architettura ATA](/advanced-threat-analytics/plan-design/ata-architecture).

**Processo del componente ATA**:

1.  Quando un componente raggiunge la sua massima dimensione, blocca il componente precedente impedendo a questo di inviargli ulteriori entità.

2.  Alla fine, perciò, il componente precedente inizierà ad aumentare la **propria** dimensione fino a bloccare il componente che lo precede impedendogli di inviare ulteriori entità.

3.  Questo si verifica a catena fino al componente NetworkListener iniziale che eliminerà il traffico quando non potrà più inoltrare ulteriori elementi.

4. Usare i dati nei contatori delle prestazioni per comprendere il funzionamento di ogni componente.

## Contatori delle prestazioni del gateway ATA

In questa sezione, ogni riferimento al gateway ATA fa riferimento anche al gateway ATA Lightweight.

È possibile osservare lo stato delle prestazioni in tempo reale del gateway ATA aggiungendo i contatori delle prestazioni del gateway ATA.
Questa operazione viene eseguita aprendo "Performance Monitor" e aggiungendo tutti i contatori per il gateway ATA. Il nome dell'oggetto contatore delle prestazioni è: "Microsoft ATA Gateway".

![Immagine dell'aggiunta di contatori delle prestazioni](media/ATA-performance-counters.png)

Ecco l'elenco dei principali contatori del gateway ATA a cui prestare attenzione:

|Contatore|Descrizione|Threshold|Risoluzione dei problemi|
|-----------|---------------|-------------|-------------------|
|Messaggi del parser PEF di NetworkListener/sec|La quantità di traffico elaborata dal gateway ATA ogni secondo.|Nessuna soglia|Consente di conoscere la quantità di traffico che viene analizzata dal gateway ATA.|
|Eventi eliminati PEF di NetworkListener/Sec|La quantità di traffico che viene eliminata dal gateway ATA ogni secondo.|Questo numero deve essere sempre zero (rari e brevi burst di eliminazioni sono accettabili).|Controllare se è presente qualche componente che ha raggiunto la dimensione massima e blocca i componenti precedenti fino al NetworkListener. Vedere **Processo del componente ATA** sopra.<br /><br />Verificare che non ci siano problemi con la CPU o la memoria.|
|Eventi eliminati ETW di NetworkListener/Sec|La quantità di traffico che viene eliminata dal gateway ATA ogni secondo.|Questo numero deve essere sempre zero (rari e brevi burst di eliminazioni sono accettabili).|Controllare se è presente qualche componente che ha raggiunto la dimensione massima e blocca componenti precedenti fino al NetworkListener. Vedere **Processo del componente ATA** sopra.<br /><br />Verificare che non ci siano problemi con la CPU o la memoria.|
|Dimensione del blocco # di dati del messaggio di NetworkActivityTranslator|La quantità di traffico messa in coda per la conversione in attività di rete (NA).|Deve essere minore del numero massimo-1 (numero massimo predefinito: 100.000)|Controllare se è presente qualche componente che ha raggiunto la dimensione massima e blocca componenti precedenti fino al NetworkListener. Vedere **Processo del componente ATA** sopra.<br /><br />Verificare che non ci siano problemi con la CPU o la memoria.|
|Dimensione del blocco attività di EntityResolver|La quantità di attività di rete (NA) in coda per la risoluzione.|Deve essere minore del numero massimo-1 (numero massimo predefinito: 10.000)|Controllare se è presente qualche componente che ha raggiunto la dimensione massima e blocca componenti precedenti fino al NetworkListener. Vedere **Processo del componente ATA** sopra.<br /><br />Verificare che non ci siano problemi con la CPU o la memoria.|
|Dimensione del blocco di batch dell'entità EntitySender|La quantità di attività di rete (NA) in coda per l'invio al centro ATA.|Deve essere minore del numero massimo-1 (numero massimo predefinito: 1.000.000)|Controllare se è presente qualche componente che ha raggiunto la dimensione massima e blocca componenti precedenti fino al NetworkListener. Vedere **Processo del componente ATA** sopra.<br /><br />Verificare che non ci siano problemi con la CPU o la memoria.|
|Ora di invio del batch EntitySender|La quantità di tempo impiegato per l'invio dell'ultimo batch.|Deve essere minore di 1000 millisecondi per la maggior parte del tempo|Controllare se ci sono problemi di rete fra il gateway ATA e il centro ATA.|

> [!NOTE]
> -   I contatori con valori di tempo sono espressi in millisecondi.
> -   A volte è più conveniente monitorare l'elenco completo dei contatori usando il tipo di grafico "Report" (esempio: monitoraggio in tempo reale di tutti i contatori)

## Contatori delle prestazioni del centro ATA
È possibile osservare lo stato delle prestazioni in tempo reale del centro ATA aggiungendo i contatori delle prestazioni del centro ATA.

Questa operazione viene eseguita aprendo "Performance Monitor" e aggiungendo tutti i contatori per il centro ATA. Il nome dell'oggetto contatore delle prestazioni è: "Microsoft ATA Center".

![Il centro ATA e i contatori delle prestazioni](media/ATA-Gateway-perf-counters.png)

Ecco l'elenco dei principali contatori del centro ATA a cui prestare attenzione:

|Contatore|Descrizione|Threshold|Risoluzione dei problemi|
|-----------|---------------|-------------|-------------------|
|Dimensione del blocco di batch dell'entità EntityReceiver|Il numero di batch di entità messi in coda dal centro ATA.|Deve essere minore del numero massimo-1 (numero massimo predefinito: 10.000)|Controllare se è presente qualche componente che ha raggiunto la dimensione massima e blocca componenti precedenti fino al NetworkListener.  Vedere **Processo del componente ATA** sopra.<br /><br />Verificare che non ci siano problemi con la CPU o la memoria.|
|Dimensione del blocco di attività di rete del NetworkActivityProcessor|Il numero di attività di rete (NA) in coda per l'elaborazione.|Deve essere minore del numero massimo-1 (numero massimo predefinito: 50.000)|Controllare se è presente qualche componente che ha raggiunto la dimensione massima e blocca componenti precedenti fino al NetworkListener. Vedere **Processo del componente ATA** sopra.<br /><br />Verificare che non ci siano problemi con la CPU o la memoria.|
|Dimensione del blocco di attività di rete di EntityProfiler|Il numero di attività di rete (NA) messe in coda per il profiling.|Deve essere minore del numero massimo-1 (numero massimo predefinito: 10.000)|Controllare se è presente qualche componente che ha raggiunto la dimensione massima e blocca componenti precedenti fino al NetworkListener. Vedere **Processo del componente ATA** sopra.<br /><br />Verificare che non ci siano problemi con la CPU o la memoria.|
|CenterDatabase &#42; Dimensione blocco|Il numero di attività di rete, di un tipo specifico, in coda per essere scritte nel database.|Deve essere minore del numero massimo-1 (numero massimo predefinito: 50.000)|Controllare se è presente qualche componente che ha raggiunto la dimensione massima e blocca componenti precedenti fino al NetworkListener. Vedere **Processo del componente ATA** sopra.<br /><br />Verificare che non ci siano problemi con la CPU o la memoria.|


> [!NOTE]
> -   I contatori con valori di tempo sono espressi in millisecondi
> -   A volte è più conveniente monitorare l'elenco completo dei contatori usando il tipo di grafico per i report (esempio: monitoraggio in tempo reale di tutti i contatori)

## Contatori del sistema operativo
Di seguito è riportato l'elenco dei principali contatori del sistema operativo a cui prestare attenzione:

|Contatore|Descrizione|Threshold|Risoluzione dei problemi|
|-----------|---------------|-------------|-------------------|
|Processore(_Totale)\% di tempo del processore|La percentuale del tempo che il processore impiega per eseguire un thread attivo.|Minore dell'80% in media|Controllare se è presente un processo specifico che impiega molto più tempo del processore rispetto a quanto previsto.<br /><br />Aggiungere altri processori.<br /><br />Ridurre la quantità di traffico per server.<br /><br />Il contatore "Processore(_Totale)\% di tempo del processore" può essere meno preciso sui server virtuali, nel qual caso il modo più preciso per misurare la mancanza di potenza del processore è mediante il contatore "Sistema\Lunghezza della coda del processore".|
|Sistema\Scambi contesto/sec|La frequenza combinata a cui tutti i processori vengono passati da un thread all'altro.|Meno di 5000&#42;core (core fisici)|Controllare se è presente un processo specifico che impiega molto più tempo del processore rispetto a quanto previsto.<br /><br />Aggiungere altri processori.<br /><br />Ridurre la quantità di traffico per server.<br /><br />Il contatore "Processore(_Totale)\% di tempo del processore" può essere meno preciso sui server virtuali, nel qual caso il modo più preciso per misurare la mancanza di potenza del processore è mediante il contatore "Sistema\Lunghezza della coda del processore".|
|Sistema\Lunghezza coda processore|Il numero di thread pronti per essere eseguiti e in attesa di essere pianificati.|Meno di 5&#42;core (core fisici)|Controllare se è presente un processo specifico che impiega molto più tempo del processore rispetto a quanto previsto.<br /><br />Aggiungere altri processori.<br /><br />Ridurre la quantità di traffico per server.<br /><br />Il contatore "Processore(_Totale)\% di tempo del processore" può essere meno preciso sui server virtuali, nel qual caso il modo più preciso per misurare la mancanza di potenza del processore è mediante il contatore "Sistema\Lunghezza della coda del processore".|
|Memoria\Megabyte disponibili|La quantità di memoria fisica (RAM) disponibile per l'allocazione.|Deve essere maggiore di 512|Controllare se è presente un processo specifico che impiega molta più memoria fisica rispetto a quanto previsto.<br /><br />Aumentare la quantità di memoria fisica.<br /><br />Ridurre la quantità di traffico per server.|
|LogicalDisk(&#42;)\Media Disk sec/Read|La latenza media per la lettura dei dati dal disco (è necessario scegliere l'unità del database come istanza).|Deve essere minore di 10 millisecondi|Controllare se c'è un processo specifico che utilizza l'unità del database più del previsto.<br /><br />Consultare il team/fornitore dell'archiviazione se questa unità può fornire il carico di lavoro attuale avendo una latenza minore di 10 ms. Il carico di lavoro attuale può essere determinato usando i contatori di uso del disco.|
|LogicalDisk(&#42;)\Media Disk sec/Write|La latenza media per la scrittura dei dati sul disco (è necessario scegliere l'unità del database come istanza).|Deve essere minore di 10 millisecondi|Controllare se c'è un processo specifico che utilizza l'unità del database più del previsto.<br /><br />Consultare il team/fornitore dell'archiviazione se questa unità può fornire il carico di lavoro attuale avendo una latenza minore di 10 ms. Il carico di lavoro attuale può essere determinato usando i contatori di uso del disco.|
|\LogicalDisk(&#42;)\Letture sul disco/sec|La frequenza di esecuzione delle operazioni di lettura sul disco.|Nessuna soglia|I contatori di uso del disco possono aggiungere informazioni utili durante la risoluzione dei problemi relativi alla latenza dell'archiviazione.|
|\LogicalDisk(&#42;)\Byte di lettura sul disco/sec|Il numero di byte al secondo che vengono letti dal disco.|Nessuna soglia|I contatori di uso del disco possono aggiungere informazioni utili durante la risoluzione dei problemi relativi alla latenza dell'archiviazione.|
|\LogicalDisk(&#42;)\Scritture sul disco/sec|La frequenza di esecuzione delle operazioni di scrittura sul disco.|Nessuna soglia|Contatori di uso del disco (possono aggiungere informazioni durante la risoluzione dei problemi relativi alla latenza dell'archiviazione)|
|\LogicalDisk(&#42;)\Byte di scrittura sul disco/sec|Il numero di byte al secondo che vengono scritti sul disco.|Nessuna soglia|I contatori di uso del disco possono aggiungere informazioni utili durante la risoluzione dei problemi relativi alla latenza dell'archiviazione.|

## Vedere anche
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Pianificazione della capacità di ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurare la raccolta degli eventi](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurazione dell'inoltro degli eventi di Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


