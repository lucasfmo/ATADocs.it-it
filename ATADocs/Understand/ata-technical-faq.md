---
# required metadata

title: Domande frequenti su ATA | Microsoft Advanced Threat Analytics
description: Fornisce un elenco di domande frequenti su ATA e le relative risposte
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Domande frequenti su ATA
Questo articolo fornisce un elenco di domande frequenti su ATA con informazioni dettagliate e risposte.


## In che modo sono concesse le licenze per ATA?
Per informazioni sulla licenza, vedere [Come acquistare Advanced Threat Analytics](https://www.microsoft.com/en-us/server-cloud/products/advanced-threat-analytics/Purchasing.aspx)


## Il gateway ATA non si avvia. Come procedere?
Esaminare l'errore più recente nel registro errori corrente (la posizione in cui è installato ATA, nella cartella "Logs").
## Come è possibile testare ATA?
È possibile simulare attività sospette, ovvero eseguire un test end-to-end tramite una delle operazioni seguenti:

1.  Esplorazione del DNS tramite Nslookup.exe
2.  Esecuzione remota tramite psexec.exe


Questa operazione deve essere eseguita in remoto nel controller di dominio monitorato e non dal gateway ATA.

## Come è possibile verificare l'inoltro degli eventi di Windows?
È possibile eseguire il comando riportato di seguito dal prompt dei comandi della directory: **\Programmi\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**:

        mongo ATA --eval "printjson(db.getCollectionNames())" | find /C "NtlmEvents"`
## ATA funziona con il traffico crittografato?
Il traffico crittografato non sarà analizzato (ad esempio: LDAPS, IPSEC ESP).
## ATA funziona con la blindatura Kerberos?
La blindatura Kerberos, conosciuta anche come FAST (Flexible Authentication Secure Tunneling), è supportata da ATA, ad eccezione del superamento del rilevamento dell'hash, che non funziona.
## Quanti gateway ATA sono necessari?

Innanzitutto, è consigliabile usare i gateway ATA Lightweight su controller di dominio idonei. Per informazioni, vedere [Dimensionamento del gateway ATA Lightweight](/advanced-threat-analytics/plan-design/ata-capacity-planning#ATA-Lightweight-Gateway-Sizing). 

Se tutti i controller di dominio possono essere gestiti mediante gateway ATA Lightweight, non sono necessari gateway ATA.

Riguardo ai controller di dominio che non possono essere gestiti mediante il gateway ATA Lightweight, per decidere il numero di gateway ATA necessari tenere presente quanto segue:

 - La quantità totale di traffico prodotta dai controller di dominio e l'architettura di rete (per configurare il mirroring delle porte). Per altre informazioni su come stabilire la quantità di traffico prodotta dai controller di dominio, vedere [Stima del traffico dei controller di dominio](/advanced-threat-analytics/plan-design/ata-capacity-planning#Domain-controller-traffic-estimation).
 - Anche i limiti operativi del mirroring delle porte determinano quanti gateway ATA sono necessari per supportare i controller di dominio, ad esempio per opzione, per data center o per area. Ogni ambiente necessita di considerazioni specifiche. 

## Quanto spazio di archiviazione è necessario per ATA?
Per ogni giorno completo con una media di 1000 pacchetti/sec sono necessari 0,3 GB di spazio di archiviazione.<br /><br />Per altre informazioni sul dimensionamento del Centro ATA, vedere [Pianificazione della capacità di ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).


## Perché alcuni account sono considerati sensibili?
Ciò si verifica quando un account è membro di alcuni gruppi considerati sensibili (ad esempio: "Domain Admins").

Per comprendere il motivo per cui un account sia considerato sensibile, è possibile esaminarne l'appartenenza ai gruppi al fine di conoscere a quale gruppo sensibile esso appartenga (il gruppo a cui appartiene può essere sensibile anche a causa di un altro gruppo, quindi è necessario eseguire lo stesso processo fino a individuare il gruppo sensibile di livello più alto).

## Come monitorare un controller di dominio virtuale mediante ATA?
La maggior parte dei controller di dominio virtuali può essere gestita mediante il gateway ATA Lightweight. Per determinare se il gateway ATA Lightweight è appropriato per l'ambiente in uso, vedere [Pianificazione della capacità di ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).

Se un controller di dominio virtuale non può essere gestito mediante il gateway ATA Lightweight, è possibile usare un gateway ATA fisico o virtuale, come descritto in [Configurare il mirroring delle porte](/advanced-threat-analytics/deploy-use/configure-port-mirroring).  <br />Il modo più semplice è dotare ogni host in cui è presente un controller di dominio virtuale di un gateway ATA virtuale.<br />Se i controller di dominio virtuali si spostano tra gli host, è necessario eseguire una delle operazioni seguenti:

-   Quando il controller di dominio virtuale si sposta su un altro host, preconfigurare il gateway ATA su tale host per ricevere il traffico dal controller di dominio virtuale spostato di recente.
-   Accertarsi di associare il gateway ATA virtuale con il controller di dominio virtuale in modo che, in caso di spostamento, venga spostato anche il gateway ATA.
-   Esistono alcuni commutatori virtuali in grado di inviare il traffico da un host all'altro.

## Come è possibile eseguire il backup di ATA?
Gli elementi su cui eseguire il backup sono 2:

-   Il traffico e gli eventi archiviati da ATA, di cui è possibile eseguire il backup usando qualsiasi procedura di backup di database supportata. Per altre informazioni, vedere [ATA database management (Gestione del database ATA)](/advanced-threat-analytics/deploy-use/ata-database-management) 
-   La configurazione di ATA, che viene archiviata nel database e di cui viene eseguito il backup automatico ogni ora. 

## Cosa è possibile rilevare con ATA?
ATA rileva tecniche e attacchi dannosi noti, problemi di sicurezza e rischi.
Per l'elenco completo dei rilevamenti di ATA, vedere [What is Microsoft Advanced Threat Analytics? (Che cos'è Microsoft Advanced Threat Analytics?)](what-is-ata.md).

## Quale tipo di archiviazione è necessario per ATA?
È consigliabile usare l'archiviazione veloce (i dischi 7200 RPM non sono consigliati) con accesso al disco a bassa latenza (meno di 10 ms). La configurazione RAID dovrebbe supportare carichi di scrittura pesanti (RAID-5/6 e derivati non sono consigliati).

## Quante NIC (scheda di interfaccia di rete) sono necessarie per il gateway ATA?
Il gateway ATA richiede almeno due schede di rete:<br>1. Una NIC per la connessione alla rete interna e al Centro ATA.<br>2. Una NIC che verrà usata per acquisire e analizzare il traffico di rete dei controller di dominio tramite il mirroring delle porte.<br>* Non si applica al gateway ATA Lightweight, che usa in modo nativo tutte le schede di rete usate dal controller di dominio.

## Quale tipo di integrazione esiste tra ATA e i sistemi SIEM?
ATA offre un'integrazione bidirezionale con i sistemi SIEM, come indicato di seguito:

1. ATA può essere configurato per inviare un avviso Syslog a tutti i server SIEM che usano il formato CEF in caso di rilevamento di un'attività sospetta.
2. ATA può essere configurato per ricevere messaggi Syslog per ogni evento di Windows con ID 4776 da [questi SIEM](/advanced-threat-analytics/deploy-use/configure-event-collection#SIEM-support).

## ATA è in grado di monitorare i controller di dominio visualizzati nella soluzione IaaS in uso?

Sì, è possibile usare il gateway ATA Lightweight per monitorare i controller di dominio presenti in qualsiasi soluzione IaaS.

## Si tratta di un'offerta locale o nel cloud?
Microsoft Advanced Threat Analytics è un prodotto locale.

## Questo prodotto diventerà parte di Azure Active Directory o Active Directory locale?
Questa soluzione è attualmente un'offerta autonoma, ovvero non fa parte di Azure Active Directory o Active Directory locale.

## È necessario scrivere regole personalizzate e creare una soglia/linee di base?
Con Microsoft Advanced Threat Analytics non è necessario creare regole, soglie o linee di base e regolarle. ATA analizza i comportamenti di utenti, dispositivi e risorse, nonché la relazione tra di essi ed è in grado di rilevare velocemente attività sospette e attacchi noti. Tre settimane dopo la distribuzione, ATA inizia a rilevare attività sospette sul comportamento. Tuttavia, ATA avvia il rilevamento di attacchi dannosi e problemi di sicurezza noti immediatamente dopo la distribuzione.

## Se si è già verificata una violazione, Microsoft Advanced Threat Analytics è in grado di rilevare i comportamenti anomali?
Sì, anche se installato dopo una violazione, ATA è in grado di rilevare le attività sospette degli hacker. ATA non monitora solo il comportamento dell'utente ma osserva anche agli altri utenti inclusi nella mappa di sicurezza dell'organizzazione. Durante la fase di analisi iniziale, se il comportamento dell'utente malintenzionato è anomalo, questo viene identificato come "outlier" e ATA continua a segnalarne il comportamento anomalo. In aggiunta, ATA può rilevare attività sospette se l'hacker tenta di rubare le credenziali di un altro utente, ad esempio nel caso degli attacchi Pass-the-Ticket, o se tenta di avviare un'esecuzione remota su uno dei controller di dominio.

## Il prodotto usa solo il traffico proveniente da Active Directory?
Oltre ad analizzare il traffico di Active Directory con la tecnologia di analisi approfondita dei pacchetti, ATA è anche in grado di raccogliere gli eventi rilevanti dal sistema SIEM e creare profili di entità in base alle informazioni provenienti dai Servizi di dominio Active Directory. Se l'organizzazione configura l'inoltro del registro eventi di Windows, ATA raccoglie anche gli eventi dai registri eventi.

## Che cos'è il mirroring delle porte?
Conosciuto anche come SPAN (Switched Port Analyzer), il mirroring delle porte è un metodo di monitoraggio del traffico della rete. Abilitando il mirroring delle porte, viene inviata una copia di tutti i pacchetti di rete visualizzati su una porta (o su un'intera VLAN) a un'altra porta, in cui il pacchetto può essere analizzato.

## ATA monitora solo i dispositivi appartenenti a un dominio?
No. ATA monitora tutti i dispositivi nella rete che eseguono richieste di autenticazione e autorizzazione in Active Directory, inclusi i dispositivi mobili non Windows.

## ATA monitora sia gli account computer che gli account utente?
Sì. Poiché gli account computer (così come qualsiasi altra entità) possono essere usati per eseguire attività dannose, ATA monitora il comportamento di tutti gli account computer e le altre entità presenti nell'ambiente.

## ATA è in grado di supportare più domini e foreste?
Con disponibilità a livello generale, Microsoft Advanced Threat Analytics supporta più domini all'interno della stessa foresta. La foresta rappresenta il "confine di protezione" effettivo. Supportando più domini, ATA consente ai clienti di beneficiare di copertura completa per i propri ambienti.

## È possibile verificare l'integrità complessiva della distribuzione?
Sì, è possibile visualizzare l'integrità complessiva della distribuzione, dei problemi specifici relativi alla configurazione, alla connettività e così via. Quando questi eventi si verificano, l'utente riceve un avviso.


## Vedere anche
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Pianificazione della capacità di ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurare la raccolta degli eventi](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurazione dell'inoltro degli eventi di Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO3-->


