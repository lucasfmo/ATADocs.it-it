---
# required metadata

title: Gestione del database ATA | Microsoft Advanced Threat Analytics
description: Procedure per lo spostamento, il backup e il ripristino del database ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Gestione del database ATA
Se è necessario spostare il database ATA o eseguirne il backup o il ripristino, usare queste procedure per l'uso di MongoDB.

## Backup del database ATA
Fare riferimento alla [documentazione di MongoDB pertinente](http://docs.mongodb.org/manual/administration/backup/)..

## Ripristino del database ATA
Fare riferimento alla [documentazione di MongoDB pertinente](http://docs.mongodb.org/manual/administration/backup/)..

## Spostare il database ATA in un'altra unità

1.  Arrestare il servizio **Microsoft Advanced Threat Analytics Center**.

2.  Arrestare il servizio **MongoDB**.

3.  Aprire il file di configurazione di Mongo, che per impostazione predefinita si trova in: C:\Programmi\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Trovare il parametro `storage: dbPath`

4.  Spostare la cartella specificata nel parametro `dbPath` nel nuovo percorso.

5.  Modificare il parametro `dbPath` all'interno del file di configurazione di Mongo nel nuovo percorso della cartella e quindi salvare e chiudere il file.

    ![Immagine della modifica della configurazione di MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Avviare il servizio **MongoDB**.

7.  Aprire un prompt dei comandi ed eseguire la shell di Mongo tramite `mongo.exe ATA` .

    Per impostazione predefinita, mongo.exe si trova in: C:\Programmi\Microsoft Advanced Threat Analytics\Center\MongoDB\bin

8.  Eseguire questo comando: `db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}}) Instead of <New DB Location>`, dove &lt;New DB Location&gt; è il nuovo percorso della cartella.

9.  Aggiornare HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath al nuovo percorso della cartella.

9. Avviare il servizio **Microsoft Advanced Threat Analytics Center**.

## Vedere anche
- [Architettura di ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO1-->


