---
# required metadata

title: Gestire le impostazioni di telemetria | Microsoft Advanced Threat Analytics
description: Vengono descritti i dati raccolti da ATA e sono inclusi i passaggi per disattivare la raccolta dati.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Gestire le impostazioni di telemetria
Advanced Threat Analytics (ATA) raccoglie dati di telemetria anonimi su ATA e li trasmette tramite una connessione HTTPS ai server Microsoft.  Questi dati vengono usati da Microsoft per migliorare le future versioni di ATA.

## Dati raccolti
I dati anonimi raccolti includono i seguenti:

-   Contatori delle prestazioni sia di ATA Center sia del gateway ATA

-   ID prodotto dalle copie con licenza di ATA

-   Data di distribuzione di ATA Center

-   Numero di gateway ATA distribuiti

-   Le seguenti informazioni di Active Directory anonime:

    -   ID dominio per il dominio il cui nome è il primo in ordine alfabetico

    -   Numero di controller di dominio

    -   Numero di controller di dominio monitorati da ATA tramite il mirroring delle porte

    -   Numero di siti

    -   Numero di computer

    -   Numero di gruppi

    -   Numero di utenti

-   Attività sospette: per ogni attività sospetta vengono raccolti i dati anonimi indicati di seguito:

    I nomi dei computer, i nomi degli utenti e gli indirizzi IP **non** vengono raccolti.

    -   Tipo di attività sospetta

    -   ID attività sospetta

    -   Stato

    -   Ora di inizio e fine

    -   Input fornito

### Disabilitare la raccolta dati
Per arrestare la raccolta e l'invio di dati di telemetria a Microsoft, seguire i passaggi seguenti:

1.  Accedere alla Console ATA. Fare clic sui tre puntini di sospensione sulla barra degli strumenti e selezionare **About** (Informazioni).

2.  Deselezionare la casella **Invia informazioni sull’utilizzo per aiutarci a migliorare l’analisi utilizzo software in futuro**.

## Vedere anche
- [Novità nella versione 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


