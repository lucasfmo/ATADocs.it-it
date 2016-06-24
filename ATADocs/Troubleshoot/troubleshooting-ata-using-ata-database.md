---
# required metadata

title: Risoluzione dei problemi relativi ad ATA tramite il database ATA | Microsoft Advanced Threat Analytics
description: Viene descritto come usare il database ATA per risolvere i problemi 
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

# Risoluzione dei problemi relativi ad ATA tramite il database ATA
ATA usa MongoDB come database.
È possibile interagire con il database usando la riga di comando predefinita o tramite uno strumento di interfaccia utente per eseguire attività e operazioni di risoluzione dei problemi avanzate.

## Interazione con il database
Il metodo predefinito e più elementare di eseguire query sul database consiste nell'usare la shell di Mongo:

1.  Aprire una finestra della riga di comando e modificare il percorso della cartella bin di MongoDB. Il percorso predefinito è: **C:\Programmi\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Eseguire `mongo.exe ATA`. Assicurarsi di digitare ATA tutto in maiuscolo.

|Procedure|Sintassi|Note|
|-------------|----------|---------|
|Controllare le raccolte nel database.|`show collections`|Utile come test end-to-end per verificare che il traffico venga scritto nel database e che l'evento 4776 venga ricevuto da ATA.|
|Ottenere i dettagli di un utente/computer/gruppo (UniqueEntity), ad esempio un ID utente.|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|Trovare il traffico di autenticazione Kerberos proveniente da un computer specifico in un determinato giorno.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Per ottenere l'&lt;ID del computer di origine&gt;, è possibile eseguire una query sulle raccolte UniqueEntity, come mostrato nell'esempio.<br /><br />Ogni tipo di attività di rete, ad esempio le autenticazioni Kerberos, ha la propria raccolta per data UTC.|
|Trovare il traffico NTLM proveniente da un computer specifico in relazione a un certo account in un determinato giorno.|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Per ottenere l'&lt;ID del computer di origine&gt; e l'&lt;ID dell'account&gt;, è possibile eseguire una query sulle raccolte UniqueEntity, come mostrato nell'esempio.<br /><br />Ogni tipo di attività di rete, ad esempio le autenticazioni NTLM, ha la propria raccolta per data UTC.|
|Cercare proprietà avanzate, ad esempio le date di attivazione di un account. |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|Per ottenere l'&lt;ID dell'account&gt;, è possibile eseguire una query sulle raccolte UniqueEntity, come mostrato nell'esempio.<br>Il nome della proprietà che indica le date in cui l'account è stato attivo è "ActiveDates". <br>
Ad esempio, si potrebbe voler determinare se un account è attivo almeno da 21 giorni perché sia possibile eseguirvi l'algoritmo di Machine Learning per i comportamenti anomali.|
|Apportare modifiche di configurazione avanzate. In questo esempio vengono modificate le dimensioni della coda di invio per tutti i gateway ATA specificando 10.000.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

Nell'esempio seguente viene fornito un codice di esempio usando la sintassi riportata sopra. Se si esamina un'attività sospetta che si è verificata il 20/10/2015 e si vuole saperne di più sulle attività NTLM eseguite da "John Doe" in tale giorno:<br /><br />Prima di tutto, trovare l'ID di "John Doe"

`db.UniqueEntity.find({Name: "John Doe"})`<br>Annotare l'ID, indicato dal valore di "`_id`". Per questo esempio, si supponga che l'ID sia "`123bdd24-b269-h6e1-9c72-7737as875351`"<br>Cercare quindi la raccolta con la data più vicina precedente alla data cercata, ovvero 20/10/2015 nell'esempio.<br>Cercare quindi le attività NTLM dell'account di John Doe: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`
## File di configurazione di ATA
La configurazione di ATA viene archiviata nella raccolta "SystemProfile" nel database.
Ogni ora il servizio ATA Center esegue il backup di questa raccolta in un file chiamato "SystemProfile.json". Questo file si trova in una sottocartella chiamata "Backup". Nel percorso di installazione predefinito di ATA questa cartella si trova qui: **C:\Programmi\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile.json**. 

**Nota**: è consigliabile eseguire il backup di questo file in un altro percorso quando si apportano modifiche importanti ad ATA.

È possibile ripristinare tutte le impostazioni eseguendo il comando seguente:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Vedere anche
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Pianificazione della capacità di ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurare la raccolta degli eventi](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurazione dell'inoltro degli eventi di Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


