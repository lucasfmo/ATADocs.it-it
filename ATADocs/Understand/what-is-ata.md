---
# required metadata

title: Informazioni su Microsoft Advanced Threat Analytics (ATA) | Microsoft Advanced Threat Analytics
description: Viene spiegato che cos'è Microsoft Advanced Threat Analytics (ATA) e quali tipi di attività sospette è in grado di rilevare.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


## Informazioni su ATA
Microsoft Advanced Threat Analytics (ATA) è una soluzione leader sul mercato delle analisi comportamentali di utenti ed entità che aiuta i professionisti che si occupano di sicurezza IT a proteggere l'organizzazione da attacchi mirati avanzati (APT) e minacce interne. Analizzando, apprendendo e identificando automaticamente comportamenti normali e anomali delle entità (utente, dispositivi e risorse) tramite tecnologie avanzate di Machine Learning, ATA consente di identificare tecniche e attacchi dannosi noti oltre a problemi e rischi della sicurezza. Grazie all'ingegno e all'intuizione di ricercatori esperti di sicurezza di fama mondiale, questa tecnologia innovativa è progettata per aiutare le aziende a concentrarsi sull'individuazione di violazioni alla sicurezza prima che possano provocare danni.

## Funzioni svolte da ATA
ATA rileva:

  - Minacce persistenti avanzate (APT) in una fase precoce della catena della criminalità informatica, prima che possano provocare danni.

  - Minacce interne

ATA consente di separare le attività sospette reali dal rumore per concentrarsi sugli aspetti importanti.

Il motore di rilevamento di ATA si avvale di Machine Learning, dell'analisi approfondita dei pacchetti contestuale all'entità, dell'analisi dei log e delle informazioni di Active Directory (AD) per analizzare il comportamento dell'utente e dell'entità.

ATA esegue analisi approfondite del traffico dell'organizzazione e sfrutta tecnologie di Machine Learning per generare una mappa che rappresenta lo scenario normale di attività, traffico e uso nell'organizzazione. Controlla e invia una notifica quando si verificano eventi anomali. Questa operazione viene eseguita tramite la tecnologia di analisi approfondita dei pacchetti (DPI) di Microsoft, che consente l'ispezione dei pacchetti contestuale all'entità in modo che ATA possa analizzare in modo più approfondito tutti i livelli del traffico di rete.

ATA raccoglie anche eventi rilevanti da sistemi SIEM e controller di dominio. Dopo l'analisi, ATA genera una visualizzazione dinamica e continuamente aggiornata di tutti gli utenti, i dispositivi e le risorse all'interno di un'organizzazione. Grazie a questa visualizzazione completa, ATA è in grado di rilevare attacchi dannosi noti, ad esempio Pass-the-Hash, Pass-the-Ticket, attacchi di esplorazione e altri, cercando anche eventuali anomalie nel comportamento delle entità nella rete.

Dopo aver rilevato un'attività sospetta, genera un avviso, riducendo al minimo il numero di falsi positivi grazie all'impiego di algoritmi avanzati per l'aggregazione e la verifica del contesto.



## Minacce ricercate da ATA

ATA assicura il rilevamento nelle seguenti fasi di un attacco avanzato: esplorazione, violazione delle credenziali, movimento laterale, escalation dei privilegi, dominanza del dominio e altre. I rilevamenti hanno lo scopo di individuare attacchi avanzati e minacce interne prima che possano causare danni all'organizzazione.

Il rilevamento di ogni fase produce diverse attività sospette attinenti alla fase in questione, in cui ogni attività sospetta è correlata a diverse varianti di possibili attacchi.

### Esplorazione
ATA assicura più rilevamenti di esplorazione. I rilevamenti includono:

-   **Esplorazione tramite enumerazione account**<br>Rileva i tentativi da parte di utenti malintenzionati che usano il protocollo Kerberos di scoprire se un utente esiste, anche se l'attività non è stata registrata come un evento nel controller di dominio.
-   **Enumerazione Net Session**<br>
Nell'ambito della fase di esplorazione, gli utenti malintenzionati potrebbero eseguire query sul controller di dominio per tutte le sessioni SMB attive sul server, consentendo l'accesso a tutti gli utenti e agli indirizzi IP associati alle sessioni SMB. L'enumerazione delle sessioni SMB può essere usata dagli utenti malintenzionati per prendere di mira account sensibili e spostarsi lateralmente sulla rete.
-   **Esplorazione tramite DNS**<br>
Le informazioni DNS nella rete di destinazione costituiscono spesso informazioni di esplorazione molto utili. Le informazioni DNS contengono un elenco di tutti i server e spesso di tutti i client, nonché il mapping degli indirizzi IP. La visualizzazione delle informazioni DNS può fornire una visione dettagliata delle entità presenti nell'ambiente, consentendo agli utenti malintenzionati di concentrarsi sulle entità rilevanti per la campagna.

### Violazione delle credenziali

Per rilevare la violazione delle credenziali, ATA sfrutta sia l'analisi comportamentale basata su Machine Learning sia il rilevamento di tecniche e attacchi dannosi noti.

Grazie all'analisi comportamentale e al Machine Learning, ATA è in grado di rilevare attività sospette, come accessi anomali, accesso anomalo alle risorse e orari di lavoro insoliti, potenziali indici di una violazione delle credenziali.
Al fine di proteggerle, ATA rileva le tecniche e gli attacchi dannosi noti seguenti:
:

 - **Forza bruta** <br>Negli attacchi di forza bruta, gli utenti malintenzionati tentano di indovinare le credenziali provando più utenti e password. Gli utenti malintenzionati spesso usano algoritmi complessi o dizionari per provare tutti i valori consentiti da un sistema.

- **Account sensibile esposto nell'autenticazione in testo normale**<br>
In caso di invio di credenziali di account con privilegi elevati in testo normale, ATA avvisa l'utente in modo da aggiornare la configurazione del computer.

- **Servizio che espone gli account nell'autenticazione in testo normale** <br>
Se un servizio in un computer invia più credenziali di account in testo normale, ATA avvisa l'utente in modo da aggiornare la configurazione del servizio.

- **Attività sospette di account di tipo honeytoken**<br>
Gli account di tipo honeytoken sono account fittizi creati per intercettare, identificare e rilevare attività dannose che tentano di usare questi account. ATA segnala tutte le attività che si verificano sugli account di tipo honeytoken.
-   **Implementazione dei protocolli insolita**<br>
Le richieste di autenticazione, sia Kerberos sia NTLM, vengono in genere eseguite tramite un set normale di metodi e protocolli. Tuttavia, per eseguire l'autenticazione la richiesta deve soddisfare solo un set di requisiti specifici. Gli utenti malintenzionati possono implementare questi protocolli con deviazioni minori rispetto all'implementazione normale dell'ambiente. Queste deviazioni potrebbero indicare la presenza di un utente malintenzionato che tenta di usare o sfruttare le credenziali compromesse.
-   **Richiesta di informazioni private per la protezione contro dati dannosi**<br>
Data Protection API (DPAPI) è un servizio di protezione dei dati basato su password. Questo servizio è usato da varie applicazioni che archiviano i dati segreti degli utenti, come ad esempio le password dei siti Web e le credenziali per la condivisione di file. Per supportare gli scenari di perdita delle password, gli utenti possono decrittografare i dati protetti tramite una chiave di ripristino che non comporta la necessità di password. In un ambiente di dominio, gli utenti malintenzionati potrebbero intercettare in modalità remota la chiave di ripristino e usarla per decrittografare i dati protetti su tutti i computer aggiunti al dominio.
-   **Comportamento anomalo**<br>
Spesso, in caso di minacce interne o attacchi avanzati, le credenziali dell'account possono essere compromesse tramite metodi di ingegneria sociale o metodi e tecniche nuovi e non ancora conosciuti. ATA è in grado di rilevare questi tipi di violazione analizzando il comportamento delle entità, rilevando e segnalando le anomalie delle operazioni eseguite dalle entità.

### Movimento laterale
Per fornire il rilevamento del movimento laterale, quando gli utenti usufruiscono di credenziali che consentono l'accesso ad alcune risorse per accedere ad altre risorse senza autorizzazione, ATA sfrutta sia l'analisi comportamentale basata su Machine Learning sia il rilevamento di tecniche e attacchi dannosi noti.

Grazie all'analisi comportamentale e al Machine Learning, ATA rileva l'accesso anormale alle risorse, l'uso anomalo di dispositivi e altri indicatori di movimento laterale.

Inoltre, è in grado di rilevare le tecniche usate da utenti malintenzionati per eseguire il movimento laterale, ad esempio:

- **Pass-the-Ticket** <br>
Negli attacchi Pass-the-Ticket gli utenti malintenzionati rubano un ticket Kerberos da un computer e lo usano per accedere a un altro computer assumendo l'identità di un'entità nella rete.
- **Pass-the-Hash** <br>
Negli attacchi Pass-the-Hash gli utenti malintenzionati rubano l'hash NTLM di un'entità e lo usano per autenticarsi con NTLM, assumere l'identità dell'entità e accedere alle risorse sulla rete.
- **Over-pass-the-Hash**<br>
Negli attacchi Over-pass-the-Hash i pirati informatici usano un hash NTLM sottratto in modo fraudolento per autenticarsi con Kerberos e ottenere un ticket TGT Kerberos valido che viene quindi usato per autenticarsi come un utente valido e accedere alle risorse di rete.
-   **Comportamento anomalo**<br>
Il movimento laterale è una tecnica spesso usata dagli utenti malintenzionati per spostarsi tra i dispositivi e le aree della rete della vittima al fine di accedere a credenziali privilegiate o informazioni riservate di interesse per l'utente malintenzionato. ATA è in grado di rilevare il movimento laterale analizzando il comportamento di utenti e dispositivi, nonché le relazioni all'interno della rete aziendale e rileva eventuali modelli di accesso anomali che potrebbero indicare uno spostamento laterale eseguito da un utente malintenzionato.

### Escalation dei privilegi
ATA è in grado di rilevare un attacco di escalation dei privilegi, che si verifica quando gli utenti malintenzionati tentano di aumentare i privilegi esistenti e usarli più volte per ottenere il completo controllo sull'ambiente della vittima. 

ATA consente il rilevamento di attacchi di escalation dei privilegi combinando analisi comportamentali finalizzate al rilevamento di comportamenti anomali degli account con privilegi, nonché attacchi e tecniche dannosi noti, spesso usati per l'escalation dei privilegi. Ad esempio:

- **Exploit MS14-068 (PAC contraffatte)**<br>
Le PAC contraffatte sono attacchi in cui l'utente malintenzionato infiltra dati di autorizzazione nel ticket TGT valido sotto forma di un'intestazione di autorizzazione contraffatta, ottenendo autorizzazioni aggiuntive che non gli erano state concesse dall'organizzazione. In questo scenario, l'utente malintenzionato usa le credenziali precedentemente violate o intercettate durante operazioni di movimento laterale.
- **Exploit MS11-013 (PAC silver)**<br>
Gli exploit MS11-013 rappresentano una vulnerabilità in Kerberos relativa all'elevazione dei privilegi che consente la contraffazione di alcuni aspetti di un ticket di servizio Kerberos. Un utente malintenzionato o l'autore di un attacco può sfruttare efficacemente questa vulnerabilità per ottenere un token con privilegi elevati sul controller di dominio. In questo scenario, l'utente malintenzionato usa le credenziali precedentemente violate o intercettate durante operazioni di movimento laterale.

### Dominanza del dominio
ATA rileva gli utenti malintenzionati che tentano o riescono ad acquisire controllo e dominanza completi sull'ambiente della vittima tramite il rilevamento di tecniche note usate dagli utenti malintenzionati, tra cui:

- **Malware Skeleton key**<br>
Negli attacchi Skeleton key sul controller di dominio dell'utente viene installato malware che consente agli utenti malintenzionati di autenticarsi come qualsiasi utente pur continuando a permettere l'accesso agli utenti legittimi.
- **Golden Ticket**<br>
Negli attacchi Golden Ticket un utente malintenzionato ruba le credenziali del KBTGT, Kerberos Golden Ticket. Tale ticket consente all'utente malintenzionato di creare un ticket TGT offline da usare per accedere alle risorse della rete.
- **Esecuzione remota**<br>
Gli utenti malintenzionati possono tentare di controllare la rete eseguendo il codice da remoto sul controller di dominio.
-   **Richieste di repliche dannose**
Gli ambienti Active Directory (AD) sono costantemente interessati da repliche tra i controller di dominio. Nel tentativo di recuperare i dati archiviati in AD, inclusi gli hash delle password, un utente malintenzionato può eseguire lo spoofing di una richiesta di replica AD, talvolta rappresentando un controller di dominio, senza usare tecniche più intrusive come ad esempio Copia Shadow del volume.

## Passaggi successivi

-   Per altre informazioni sulla modalità di integrazione ATA nella rete, vedere [ATA architecture](/advanced-threat-analytics/plan-design/ata-architecture) (Architettura ATA)

-   Per iniziare a distribuire ATA, vedere [Install ATA](/advanced-threat-analytics/deploy-use/install-ata) (Installare ATA)

## Vedere anche
[Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


