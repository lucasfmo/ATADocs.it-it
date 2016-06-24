---
# required metadata

title: ATA Health Center | Microsoft Advanced Threat Analytics
description: Usare ATA Health Center per controllare il funzionamento del servizio ATA e ricevere avvisi sui potenziali problemi.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA Health Center
ATA Health Center permette di determinare le prestazioni del servizio ATA e di ricevere avvisi sui problemi.

## Uso di ATA Health Center
ATA Health Center permette di identificare un problema attraverso la visualizzazione di un avviso (un punto rosso) sopra l'icona di Health Center sulla barra dei menu.

![Barra degli strumenti contrassegnata da un punto rosso del Centro di integrità ATA](media/ATA-Health-Center-Alert-red-dot.png)

### Gestione dell'integrità di ATA
Per controllare l'integrità complessiva del sistema, fare clic sull'icona di Health Center sulla barra dei menu ![Icona di ATA Health Center](media/ATA-red-dot.png)

-   È possibile gestire tutti gli avvisi aperti impostandoli su **Resolved** o **Dismissed**. In Alert fare clic su **Open** e scorrere verso il basso fino a **Resolved** o **Dismissed**.

-   Se si risolve un problema, ma ATA rileva che il problema persiste, il problema viene automaticamente riportato nell'elenco dei problemi **Open**. Se ATA rileva che un problema aperto è stato risolto, il problema viene automaticamente spostato nell'elenco dei problemi **Resolved**.

-   I problemi **Dismissed** sono problemi che ATA non deve continuare a controllare. Se, ad esempio, si riceve un avviso su un problema la cui esistenza è nota e che non si intende risolvere, ma per cui non si vuole continuare a ricevere notifiche né si vuole visualizzarlo nell'elenco dei problemi **Open**, è possibile impostarlo su **Dismissed**.

![Immagine dei problemi in ATA Health Center](media/ATA-Health-Issue.JPG)

## Vedere anche
- [Uso delle impostazioni di rilevamento di ATA](working-with-detection-settings.md)
- [Gestione di attività sospette](working-with-suspicious-activities.md)
- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


