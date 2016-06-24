---
# required metadata

title: Risoluzione dei problemi del registro errori ATA | Microsoft Advanced Threat Analytics
description: Descrive come risolvere gli errori comuni in ATA 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Risoluzione dei problemi del registro errori ATA
Questa sezione descrive errori che possono verificarsi nelle distribuzioni di ATA e i passaggi necessari per risolverli.
## Errori del gateway ATA
|Errore|Descrizione|Soluzione|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: Errore locale|Non è stato possibile eseguire l'autenticazione del gateway ATA per il controller di dominio.|1. Verificare che il record DNS del controller di dominio sia configurato correttamente nel server DNS. <br>2. Verificare che l'ora del gateway ATA sia sincronizzata con l'ora del controller di dominio.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: Failed to validate certificate chain (Convalida catena di certificati non riuscita)|Il gateway ATA non ha potuto convalidare il certificato del centro ATA.|1. Verificare che il certificato CA radice sia installato nell'archivio certificati dell'autorità di certificazione attendibile nel gateway ATA. <br>2. Verificare che l'elenco di revoche di certificati (CRL) sia disponibile e che sia possibile eseguire la convalida della revoca del certificato.|
|Microsoft.Common.ExtendedException: Failed to parse time generated (Analisi ora generata non riuscita)|Il gateway ATA non ha potuto analizzare i messaggi syslog inoltrati dal SIEM.|Verificare che il SIEM sia configurato per inoltrare i messaggi in uno dei formati supportati da ATA.|
|System.ServiceModel.FaultException: Errore durante la verifica della sicurezza del messaggio.|Il gateway ATA non ha potuto eseguire l'autenticazione del centro ATA.|Verificare che l'ora del gateway ATA sia sincronizzata con l'ora del centro ATA.|
|System.ServiceModel.EndpointNotFoundException: Impossibile connettersi a net.tcp://center.ip.addr:443/IEntityReceiver|Il gateway ATA non ha potuto stabilire la connessione al centro ATA.|Assicurarsi che le impostazioni di rete siano corrette e che la connessione di rete tra il gateway ATA e il centro ATA sia attiva.|
|System.DirectoryServices.Protocols.LdapException: Server LDAP non disponibile.|Il gateway ATA non ha potuto eseguire una query sul controller di dominio tramite il protocollo LDAP.|1. Verificare che l'account utente usato da ATA per connettersi al dominio di Active Directory disponga dell'accesso in lettura a tutti gli oggetti nella struttura di Active Directory. <br>2. Assicurarsi che il controller di dominio non sia stato finalizzato per evitare che LDAP esegua query dall'account utente usato da ATA.|
|Microsoft.Tri.Infrastructure.ContractException: Contract exception (Eccezione contratto)|Il gateway ATA non ha potuto sincronizzare la configurazione dal centro ATA.|Completare la configurazione del gateway ATA nella Console ATA.|
|System.Reflection.ReflectionTypeLoadException: Impossibile caricare uno o più tipi richiesti. Recuperare la proprietà LoaderExceptions per ulteriori informazioni.|Message Analyzer è installato sul gateway ATA.| Disinstallare Message Analyzer.|
|Error [Layout] System.OutOfMemoryException: È stata generata un'eccezione di tipo 'System.OutOfMemoryException'.|La memoria del gateway ATA non è sufficiente.|Aumentare la quantità di memoria nel controller di dominio.|
|Fail to start live consumer  ---> (Non è possibile avviare il consumer) Microsoft.Opn.Runtime.Monitoring.MessageSessionException: The PEFNDIS event provider is not ready (Il provider di eventi PEFNDIS non è pronto)|PEF (Message Analyzer) non è stato installato correttamente.|Contattare il supporto per una soluzione alternativa.|
|Installazione non riuscita. Errore: 0x80070652|Esistono altre installazioni in sospeso nel computer.|Attendere che le altre installazioni siano completate e, se necessario, riavviare il computer.|

## Errori della Console ATA
|Errore|Descrizione|Risoluzione|
|-------------|----------|---------|
|Errore HTTP 500.19 - Errore interno del server|Non è stato possibile installare correttamente il modulo IIS di riscrittura dell'URL.|Disinstallare e reinstallare il modulo IIS di riscrittura dell'URL.<br>[Scaricare il modulo IIS di riscrittura dell'URL](http://go.microsoft.com/fwlink/?LinkID=615137)|

## Errori di distribuzione
|Errore|Descrizione|Risoluzione|
|-------------|----------|---------|
|L'installazione di .Net Framework 4.6.1 ha dato esito negativo con errore 0x800713ec|I prerequisiti di .Net Framework 4.6.1 non sono installati nel server. |Prima di installare ATA, verificare che gli aggiornamenti di Windows [KB2919442](https://www.microsoft.com/en-us/download/details.aspx?id=42135) e [KB2919355](https://support.microsoft.com/en-us/kb/2919355) vengano installati nel server.|

![Immagine di errore dell'installazione .NET ATA](media/netinstallerror.png)


## Vedere anche
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Pianificazione della capacità di ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurare la raccolta degli eventi](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurazione dell'inoltro degli eventi di Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#ATA_event_WEF)
- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


