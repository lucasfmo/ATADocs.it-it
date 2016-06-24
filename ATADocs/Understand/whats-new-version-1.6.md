---
# required metadata

title: Novità in ATA versione 1.6 | Microsoft Advanced Threat Analytics
description: Vengono elencate le novità in ATA versione 1.6 e i problemi noti
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

# Novità in ATA versione 1.6
Queste note sulla versione offrono informazioni sui problemi noti relativi a questa versione di Advanced Threat Analytics.

## Novità nell'aggiornamento ad ATA 1.6
L'aggiornamento ad ATA 1.6 offre miglioramenti nelle aree seguenti:

-   Nuovi rilevamenti

-   Miglioramenti dei rilevamenti esistenti

-   Gateway ATA Lightweight

-   Aggiornamenti automatici

-   Miglioramento delle prestazioni di ATA Center

-   Minori requisiti di archiviazione

-   Supporto per IBM QRadar

### Nuovi rilevamenti


- **Richiesta di informazioni private, protezione da dati dannosi** Data Protection API (DPAPI) è un servizio di protezione dati basato su password. Questo servizio è usato da varie applicazioni che archiviano i dati segreti degli utenti, come ad esempio le password dei siti Web e le credenziali per la condivisione di file. Per supportare gli scenari di perdita delle password, gli utenti possono decrittografare i dati protetti tramite una chiave di ripristino che non comporta la necessità di password. In un ambiente di dominio gli utenti malintenzionati possono intercettare in modalità remota la chiave di ripristino e usarla per decrittografare i dati protetti su tutti i computer aggiunti al dominio.


- **Enumerazione della sessione di rete** La ricognizione è una fase fondamentale nella catena avanzata di eliminazione degli attacchi. I controller di dominio funzionano come file server per la distribuzione di oggetti Criteri di gruppo tramite il protocollo Server Message Block (SMB). Nell'ambito della fase di esplorazione, gli utenti malintenzionati possono eseguire query sul controller di dominio per tutte le sessioni SMB attive sul server, consentendo l'accesso a tutti gli utenti e agli indirizzi IP associati alle sessioni SMB. L'enumerazione delle sessioni SMB può essere usata dagli utenti malintenzionati per prendere di mira account sensibili e spostarsi lateralmente sulla rete.


- **Richieste di repliche da parte di malintenzionati** Gli ambienti Active Directory sono costantemente interessati da repliche tra controller di dominio. Mentre tenta di recuperare i dati archiviati in Active Directory, inclusi gli hash delle password, un utente malintenzionato può eseguire lo spoofing di una richiesta di replica Active Directory, talvolta rappresentando un controller di dominio, senza usare tecniche più intrusive come ad esempio Copia Shadow del volume.


- **Rilevamento della vulnerabilità MS11-013** In Kerberos esiste una vulnerabilità che riguarda l'elevazione dei privilegi che consente la contraffazione di alcuni aspetti di un ticket di servizio Kerberos. Un utente malintenzionato o l'autore di un attacco possono sfruttare efficacemente questa vulnerabilità per ottenere un token con privilegi elevati sul controller di dominio.


- **Implementazione anomala di protocolli** Le richieste di autenticazione Kerberos o NTLM vengono in genere eseguite tramite un set standard di metodi e protocolli. Tuttavia, per eseguire l'autenticazione la richiesta deve soddisfare solo un set di requisiti specifici. Gli utenti malintenzionati potrebbero implementare questi protocolli con deviazioni minori rispetto all'implementazione standard dell'ambiente. Queste deviazioni potrebbero indicare la presenza di un utente malintenzionato che tenti di eseguire attacchi di tipo Pass-the-Hash, forza bruta o altro.


### Miglioramenti dei rilevamenti esistenti
ATA 1.6 include il miglioramento di una logica di rilevamento che riduce gli scenari di falsi positivi e falsi negativi per i rilevamenti esistenti come Golden Ticket, Honey Token, forza bruta ed esecuzione remota.

### Gateway ATA Lightweight
Questa versione di ATA introduce una nuova opzione di distribuzione per il gateway ATA per la relativa installazione direttamente nel controller di dominio. Questa opzione di distribuzione rimuove le funzionalità non critiche del gateway ATA e introduce la gestione dinamica delle risorse in base alle risorse disponibili nel controller di dominio, in modo che le operazioni del controller di dominio esistenti rimangano invariate. Il gateway ATA Lightweight riduce i costi della distribuzione ATA semplificando nel contempo la distribuzione alle succursali, dove la capacità delle risorse hardware è limitata oppure non è possibile configurare un supporto di mirroring delle porte.
Per altre informazioni sul gateway ATA Lightweight, vedere [ATA architecture](/advanced-threat-analytics/plan-design/ata-architecture#ata-gateway-and-ata-lightweight-gateway) (Architettura di ATA).

Per altre informazioni sulle considerazioni relative alla distribuzione e sulla scelta del tipo corretto di gateway per l'utente, vedere [ATA capacity planning](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment) (Pianificazione della capacità di ATA).


### Aggiornamenti automatici
A partire dalla versione 1.6 è possibile aggiornare ATA Center tramite Microsoft Update. Inoltre, ora è possibile aggiornare automaticamente i gateway ATA tramite il canale di comunicazione standard di ATA Center.
### Miglioramento delle prestazioni di ATA Center
Questa versione consente il monitoraggio di un numero maggiore di controller di dominio in un unico ATA Center grazie al caricamento di un database più leggero oltre a una maggiore efficienza di esecuzione di tutti i rilevamenti.

### Minori requisiti di archiviazione
ATA 1.6 richiede molto meno spazio di archiviazione per l'esecuzione del database ATA, ora pari a solo il 20% dello spazio di archiviazione usato nelle versioni precedenti.

### Supporto per IBM QRadar
Ora ATA può ricevere eventi della soluzione QRadar SIEM di IBM, oltre alle soluzioni SIEM già supportate.

## Problemi noti
Questa versione presenta i problemi noti descritti di seguito.

### Errore di riconoscimento dei nuovi percorsi dei database spostati manualmente

Nelle distribuzioni in cui lo spostamento di un percorso viene eseguito manualmente, la distribuzione di ATA non usa il nuovo percorso del database per l'aggiornamento. Questo potrebbe causare gli inconvenienti seguenti:


- ATA potrebbe usare tutto lo spazio libero nell'unità di sistema di ATA Center senza eliminare in modo circolare le precedenti attività di rete.


- L'aggiornamento di ATA alla versione 1.6 potrebbe completare con esito negativo le verifiche di conformità dell'aggiornamento preliminare, come illustrato nell'immagine seguente.
    ![Errore nelle verifiche di conformità](media/ata_failed_readinesschecks.png)
    >[!Important]
Prima di aggiornare ATA alla versione 1.6, aggiornare la chiave di registro seguente con il percorso database corretto:  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`

### Errore durante la migrazione per l'aggiornamento di ATA 1.5
Durante l'aggiornamento di ATA alla versione 1.6, il processo di aggiornamento potrebbe avere esito negativo e restituire il codice errore seguente:

![Errore di aggiornamento di ATA alla versione 1.6](http://i.imgur.com/QrLSApr.png)Se viene visualizzato questo errore, esaminare il registro di distribuzione in: **C:\Utenti\<Utente>\AppData\Local\Temp** e cercare l'eccezione seguente:

    System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }

È possibile che venga visualizzato anche questo errore: System. ArgumentNullException. Il valore non può essere null.
    
Se viene visualizzato uno di questi errori, eseguire la soluzione alternativa seguente.

**Soluzione alternativa**: 

1.  Spostare la cartella "data_old" in una cartella temporanea, in genere ubicata in %ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin.
2.  Disinstallare ATA Center 1.5 ed eliminare tutti i dati dei database.
![Disinstallare ATA 1.5](http://i.imgur.com/x4nJycx.png)
3.  Installare nuovamente ATA Center 1.5. Assicurarsi di usare la stessa configurazione dell'installazione di ATA 1.5 precedente (certificati, indirizzi IP, percorso database, ecc.).
4.  Arrestare i servizi seguenti rispettando l'ordine indicato:
    1.  Microsoft Advanced Threat Analytics Center
    2.  MongoDB
5.  Sostituire i file del database MongoDB con i file nella cartella "data_old".
6.  Avviare i servizi seguenti rispettando l'ordine indicato:
    1.  MongoDB
    2.  Microsoft Advanced Threat Analytics Center
7.  Esaminare i registri per verificare che il prodotto venga eseguito senza errori.
8.  [Download](http://aka.ms/ataremoveduplicateprofiles "Scaricare") lo strumento "RemoveDuplicateProfiles.exe" e copiarlo nel percorso di installazione principale, ovvero %ProgramFiles%\Microsoft Advanced Threat Analytics\Center.
9.  In un prompt dei comandi con privilegi elevati eseguire "RemoveDuplicateProfiles.exe" e attendere finché non viene completato correttamente.
10. Da qui: …\Microsoft Advanced Threat Analytics\Center\MongoDB\directory bin: **Mongo ATA** e digitare il comando seguente:

    db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });

![Soluzione alternativa di aggiornamento](http://i.imgur.com/Nj99X2f.png)

Questo comando dovrebbe restituire WriteResult({ "nRemoved" : XX }) dove "XX" è il numero di attività sospette eliminate. Se il numero è maggiore di 0, uscire dal prompt dei comandi e continuare il processo di aggiornamento.


### Riavvio del server per NET Framework 4.6.1

In alcuni casi l'installazione di .Net Framework 4.6.1 potrebbe richiedere il riavvio del server. Si noti che facendo clic su OK nella finestra di dialogo **Microsoft Advanced Threat Analytics Center Setup** (Installazione di Microsoft Advanced Threat Analytics Center) il server verrà riavviato automaticamente. Questo è particolarmente importante durante l'installazione del gateway ATA Lightweight in un controller di dominio quando si considera di pianificare una finestra di manutenzione prima dell'installazione.
    ![Riavvio di .Net Framework](media/ata-net-framework-restart.png)

### Migrazione delle attività di rete non necessaria
La nuova versione di ATA offre il miglioramento del motore di rilevamento con funzionalità di rilevamento più accurate e riduzione di numerosi scenari di falsi positivi, in particolare per gli attacchi di tipo Pass-the-Hash.
Il nuovo e migliorato motore di rilevamento usa la tecnologia di rilevamento inline che consente l'attivazione del rilevamento senza necessità di accedere alle attività di rete cronologiche, al fine di migliorare notevolmente le prestazioni di ATA Center. Non è quindi necessario eseguire la migrazione delle attività di rete cronologiche durante la procedura di aggiornamento.
Per esigenze di analisi future, la procedura di aggiornamento di ATA esporta i dati in `<Center Installation Path>\Migration` come file con estensione JSON.

## Vedere anche
[Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

[Update ATA to version 1.6 - migration guide (Guida alla migrazione: aggiornamento di ATA alla versione 1.6)](ata-update-1.6-migration-guide.md)

<!--HONumber=May16_HO4-->


