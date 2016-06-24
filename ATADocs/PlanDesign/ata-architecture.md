---
# required metadata

title: Architettura di ATA | Microsoft Advanced Threat Analytics
description: Descrive l'architettura di Microsoft Advanced Threat Analytics (ATA)
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Architettura di ATA
Questo diagramma descrive in dettaglio l'architettura di Advanced Threat Analytics:

![Diagramma della topologia dell'architettura di ATA](media/ATA-architecture-topology.jpg)

ATA esegue il monitoraggio del traffico di rete dei controller di dominio usando il mirroring delle porte verso un gateway ATA tramite commutatori fisici o virtuali oppure distribuendo il gateway ATA Lightweight direttamente ai controller di dominio, senza ricorrere al mirroring delle porte. Inoltre, ATA può sfruttare gli eventi di Windows (inoltrati direttamente dai controller di dominio o da un server SIEM) e analizzare i dati per rilevare eventuali attacchi e minacce.
Questa sezione illustra il flusso del traffico di rete e dell'acquisizione di eventi e descrive in dettaglio le funzionalità dei componenti principali dell'architettura di ATA: il gateway ATA, il gateway ATA Lightweight (che ha le stesse funzionalità di base del gateway ATA) e il Centro ATA.


![Diagramma di flusso del traffico di ATA](media/ATA-traffic-flow.jpg)

## Componenti di ATA
ATA include gli elementi seguenti:

-   **Centro ATA** <br>
Il Centro ATA riceve dati da qualsiasi gateway ATA e/o gateway ATA Lightweight distribuito.
-   **Gateway ATA**<br>
Il gateway ATA viene installato in un server dedicato che esegue il monitoraggio del traffico dai controller di dominio tramite il mirroring delle porte o un dispositivo TAP di rete.
-   **Gateway ATA Lightweight**<br>
Il gateway ATA Lightweight viene installato nei controller di dominio ed esegue direttamente il monitoraggio del traffico, senza bisogno di un server dedicato o di una configurazione di mirroring delle porte. Rappresenta un'alternativa al gateway ATA.

Una distribuzione ATA può essere costituita da un unico Centro ATA connesso a tutti i gateway ATA, a tutti i gateway ATA Lightweight o a una combinazione dei due tipi di gateway.


## Opzioni di distribuzione
Per la distribuzione di ATA è possibile usare le combinazioni seguenti di gateway:

-   **Solo gateway ATA** <br>
Se la distribuzione di ATA include solo gateway ATA, senza alcun gateway ATA Lightweight, tutti i controller di dominio devono essere configurati in modo da abilitare il mirroring delle porte verso un gateway ATA oppure devono essere presenti dispositivi TAP di rete.
-   **Solo gateway ATA Lightweight**<br>
Se la distribuzione di ATA include solo gateway ATA Lightweight, questi vengono distribuiti in ogni controller di dominio e non sono necessari né server aggiuntivi né una configurazione di mirroring delle porte.
-   **Entrambi i tipi di gateway**<br>
Se la distribuzione di ATA include sia gateway ATA sia gateway ATA Lightweight, i secondi sono installati in alcuni controller di dominio (ad esempio, tutti i controller di dominio dei siti di filiali), mentre i primi eseguono il monitoraggio di altri controller di dominio (ad esempio, i controller di dominio più grandi dei data center principali).

Nei tre scenari, tutti i gateway inviano i dati al Centro ATA.




## Centro ATA
Il **Centro ATA** esegue le funzioni seguenti:

-   Gestisce le impostazioni di configurazione del gateway ATA e del gateway ATA Lightweight.

-   Riceve dati da gateway ATA e gateway ATA Lightweight. 

-   Rileva attività sospette.

-   Esegue algoritmi ATA comportamentali di Machine Learning per rilevare eventuali comportamenti anomali.

-   Esegue vari algoritmi deterministici per rilevare attacchi avanzati in base alla relativa kill chain.

-   Esegue la Console ATA.

-   Facoltativo: il Centro ATA è configurabile per l'invio di messaggi di posta elettronica ed eventi quando viene rilevata un'attività sospetta.

Il Centro ATA riceve traffico analizzato dal gateway ATA e dal gateway ATA Lightweight, esegue la profilatura, il rilevamento deterministico e gli algoritmi di Machine Learning e comportamentali in modo da ottenere informazioni sulla rete per abilitare il rilevamento di anomalie e avvisare l'utente riguardo ad attività sospette.

|||
|-|-|
|Destinatario entità|Riceve batch di entità da tutti i gateway ATA e ATA Lightweight.|
|Processore delle attività di rete|Elabora tutte le attività della rete all'interno di ogni batch ricevuto. Ad esempio, esegue l'associazione tra i diversi passaggi di Kerberos eseguiti su computer potenzialmente diversi|
|Profiler di entità|Esegue la profilatura di tutte le entità univoche in base al traffico e agli eventi. Ad esempio, quando ATA aggiorna l'elenco dei computer connessi per ogni profilo utente.|
|Database del Centro|Gestisce il processo di scrittura delle attività di rete e degli eventi nel database. |
|Database|ATA usa MongoDB per archiviare tutti i dati del sistema:<br /><br />-   Attività della rete<br />-   Attività degli eventi<br />-   Entità univoche<br />-   Attività sospette<br />-   Configurazione di ATA|
|Rilevatori|I rilevatori usano algoritmi di Machine Learning e regole deterministiche per individuare attività sospette e comportamenti anomali da parte dell'utente sulla rete.|
|Console ATA|La Console ATA viene usata per la configurazione di ATA e il monitoraggio delle attività sospette rilevate da ATA sulla rete. La Console ATA non dipende dal servizio Centro ATA e viene eseguita anche quando il servizio è disattivo, purché sia abilitata la comunicazione con il database.|
Prima di decidere quanti Centri ATA distribuire sulla rete, considerare gli elementi seguenti:

-   Un Centro ATA è in grado di monitorare una singola foresta Active Directory. Se si dispone di più di una foresta Active Directory, è necessario almeno un Centro ATA per ogni foresta Active Directory.

-    Nelle distribuzioni molto grandi di Active Directory un singolo Centro ATA potrebbe non essere in grado di gestire tutto il traffico proveniente da tutti i controller di dominio. In questo caso, sono necessari più Centri ATA. Il numero di Centri ATA dipende dalla [pianificazione della capacità ATA](ata-capacity-planning.md)..

## Gateway ATA e gateway ATA Lightweight

### Funzionalità principali dei gateway
Il **gateway ATA** e il **gateway ATA Lightweight** presentano le stesse funzionalità di base:

-   Acquisiscono e ispezionano il traffico di rete dei controller di dominio (traffico con mirroring delle porte nel caso di un gateway ATA e traffico locale del controller di dominio nel caso di un gateway ATA Lightweight). 

-   Ricevono gli eventi di Windows dai server SIEM o Syslog o dai controller di dominio tramite l'inoltro degli eventi di Windows.

-   Recuperano i dati su utenti e computer dal dominio di Active Directory.

-   Eseguono la risoluzione di entità di rete (utenti, gruppi e computer).

-   Trasferiscono i dati pertinenti al Centro ATA.

-   Eseguono il monitoraggio dei controller di dominio (più controller da un singolo gateway ATA o un unico controller per un gateway ATA Lightweight).

Il gateway ATA riceve il traffico di rete e gli eventi di Windows dalla rete e li elabora nei componenti principali seguenti:

|||
|-|-|
|Listener di rete|Il Listener di rete è responsabile dell'acquisizione e dell'analisi del traffico di rete. Si tratta di un'attività che richiede un utilizzo elevato della CPU ed è quindi particolarmente importante verificare i [prerequisiti di ATA](ata-prerequisites.md) quando si pianifica il gateway ATA o il gateway ATA Lightweight.|
|Listener di eventi|Il Listener di eventi è responsabile dell'acquisizione e dell'analisi degli eventi di Windows inoltrati da un server SIEM sulla rete.|
|Lettore registro eventi di Windows|Il lettore registro eventi di Windows è responsabile della lettura e dell'analisi degli eventi di Windows inoltrati al registro eventi di Windows del gateway ATA dai controller di dominio.|
|Convertitore delle attività di rete | Converte il traffico analizzato in una rappresentazione logica del traffico usato da ATA (NetworkActivity).
|Strumento di risoluzione entità|Lo strumento di risoluzione entità acquisisce i dati analizzati (traffico di rete ed eventi) e risolve i dati con Active Directory per cercare informazioni su identità e account. Le informazioni rilevate vengono quindi confrontate con gli indirizzi IP trovati nei dati analizzati. Lo strumento di risoluzione entità esamina le intestazioni dei pacchetti in modo efficiente, al fine di abilitare l'analisi dei pacchetti di autenticazione per nomi, proprietà e identità dei computer. Lo strumento combina quindi i pacchetti di autenticazione analizzati con i dati presenti nel pacchetto effettivo.|
|Mittente entità|Il mittente entità è responsabile dell'invio dei dati analizzati e associati al Centro ATA.|

## Funzionalità del gateway ATA Lightweight

Le funzionalità seguenti presentano differenze a seconda che sia in esecuzione un gateway ATA o un gateway ATA Lightweight.

-   **Candidato alla sincronizzazione del dominio**<br>
Il gateway di sincronizzazione del dominio è responsabile della sincronizzazione proattiva di tutte le entità da un dominio specifico di Active Directory, in modo analogo al meccanismo adottato dagli stessi controller di dominio per la replica. Un gateway viene scelto in modo casuale, dall'elenco dei candidati, per svolgere la funzione di sincronizzazione del dominio. <br><br>
Se il gateway di sincronizzazione rimane offline per più di 30 minuti, viene scelto un altro candidato. Se è non disponibile alcun gateway di sincronizzazione per un dominio specifico, ATA non sarà in grado di sincronizzare in modo proattivo le entità e le relative modifiche, ma riuscirà a recuperare le nuove entità rilevate nel traffico monitorato. 
<br>Se non è disponibile alcun gateway di sincronizzazione del dominio e si vuole cercare un'entità a cui non sono correlati dati sul traffico, non verrà visualizzato alcun risultato.<br><br>
Per impostazione predefinita, tutti i gateway ATA sono candidati alla sincronizzazione.<br><br>
Al contrario, tutti i gateway ATA Lightweight hanno maggiori probabilità di essere distribuiti nei siti di filiali e nei controller di dominio di piccole dimensioni e non sono quindi candidati alla sincronizzazione per impostazione predefinita.


-   **Limitazioni delle risorse**<br>
Il gateway ATA Lightweight include un componente di monitoraggio che valuta la capacità di calcolo e di memoria disponibile nel controller di dominio su cui è in esecuzione. Il processo di monitoraggio viene eseguito ogni 10 secondi e aggiorna dinamicamente la quota di utilizzo di CPU e memoria per il processo del gateway ATA Lightweight per assicurarsi che, in qualsiasi momento, il controller di dominio disponga di almeno il 15% di risorse di calcolo e memoria libere.<br><br>
Indipendentemente da quanto accade sul controller di dominio, questo processo libera sempre le risorse in modo da non influire sulla funzionalità di base del controller di dominio.<br><br>
Se in questo modo il gateway ATA Lightweight esaurisce le risorse, il traffico viene monitorato solo parzialmente e nella pagina relativa allo stato viene visualizzato un avviso per segnalare che il traffico di rete con mirroring delle porte verrà ignorato.

La tabella seguente illustra un esempio di un controller di dominio con risorse di calcolo sufficienti per garantire la disponibilità di una quota maggiore di quella attualmente necessaria, in modo da consentire il monitoraggio di tutto il traffico:

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Gateway ATA Lightweight (Microsoft.Tri.Gateway.exe)|Varie (altri processi) |Quota del gateway ATA Lightweight|Traffico ignorato dal gateway|
|30%|20%|10%|45%|No|

Se Active Directory richiede maggiore capacità di calcolo, la quota necessaria per il gateway ATA Lightweight viene ridotta. Nell'esempio seguente il gateway ATA Lightweight richiede una quota maggiore rispetto a quella allocata e ignora parte del traffico, eseguendo un monitoraggio del traffico parziale:

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Gateway ATA Lightweight (Microsoft.Tri.Gateway.exe)|Varie (altri processi) |Quota del gateway ATA Lightweight|Traffico ignorato dal gateway|
|60%|15%|10%|15%|sì|



## Componenti della rete
Per eseguire il monitoraggio con ATA, verificare quanto segue:

### Mirroring delle porte
Se si usano gateway ATA, è necessario configurare il mirroring delle porte per i controller di dominio che verranno monitorati e impostare il gateway ATA come destinazione tramite commutatori fisici o virtuali. Un'altra soluzione consiste nell'uso di dispositivi TAP di rete. ATA continuerà a funzionare anche se non tutti i controller di dominio vengono monitorati, ma le attività di rilevamento saranno meno efficaci.

Durante il mirroring di tutto il traffico di rete dei controller di dominio verso il gateway ATA, solo una percentuale molto piccola del traffico viene inviata, in forma compressa, al Centro ATA per l'analisi.

I controller di dominio e i gateway ATA possono essere fisici o virtuali. Per altre informazioni, vedere [Configure Port Mirroring (Configurare il mirroring delle porte)](/advanced-threat-analytics/deploy-use/configure-port-mirroring).


### Eventi
Per migliorare il rilevamento ATA di attacchi di forza bruta, Pass-the-Hash e Honey Token, ATA richiede l'ID 4776 del registro eventi di Windows. Questo può essere inoltrato al gateway ATA in due modi, configurando il gateway ATA per l'ascolto degli eventi SIEM o usando l'inoltro degli eventi di Windows.

-   Configurazione del gateway ATA per l'ascolto degli eventi SIEM <br>Configurare il SIEM per inoltrare eventi specifici di Windows ad ATA. ATA supporta numerosi fornitori di SIEM. Per altre informazioni, vedere [Configure Event Collection (Configurare la raccolta degli eventi)](/advanced-threat-analytics/deploy-use/configure-event-collection)..

-   Configurazione dell'inoltro degli eventi di Windows<br>Un altro modo perché ATA possa ottenere gli eventi è tramite la configurazione di controller di dominio per l'inoltro dell'evento 4776 di Windows al gateway ATA. Questo metodo risulta particolarmente utile se non si dispone di un SIEM o se il SIEM non è attualmente supportato da ATA. Per altre informazioni sull'inoltro di eventi di Windows in ATA, vedere [Configuring Windows event forwarding (Configurazione dell'inoltro degli eventi di Windows)](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)..

## Vedere anche
- [Prerequisiti di ATA](ata-prerequisites.md)
- [Pianificazione della capacità di ATA](ata-capacity-planning.md)
- [Configurare la raccolta degli eventi](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurazione dell'inoltro degli eventi di Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO2-->


