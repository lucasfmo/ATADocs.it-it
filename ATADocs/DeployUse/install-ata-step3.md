---
# required metadata

title: Installare ATA - Passaggio 3 | Microsoft Advanced Threat Analytics
description: Il terzo passaggio dell'installazione di ATA consente di scaricare il pacchetto di installazione dei gateway ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installare ATA - Passaggio 3

>[!div class="step-by-step"]
[« Passaggio 2](install-ata-step2.md)
[Passaggio 4 »](install-ata-step4.md)

## Passaggio 3. Scaricare il pacchetto di installazione dei gateway ATA
Dopo aver configurato le impostazioni di connettività del dominio, è possibile scaricare il pacchetto di installazione dei gateway ATA. Il gateway ATA può essere installato su un server dedicato o in un controller di dominio. Se si installa il gateway in un controller di dominio, verrà installato come gateway ATA Lightweight. Per altre informazioni sul gateway ATA Lightweight, vedere [ATA architecture](/advanced-threat-analytics/plan-design/ata-architecture) (Architettura di ATA).. 

Per scaricare il pacchetto dei gateway ATA:

1.  Dalla Console ATA, fare clic sull'icona delle impostazioni e selezionare **Configurazione**..

    ![Impostazioni di configurazione dei gateway ATA](media/ATA-config-icon.JPG)

2.  Nella scheda **ATA Gateways** (Gateway ATA) fare clic su **Download ATA Gateway Setup** (Scarica l'installazione del gateway ATA)..

3.  Salvare il pacchetto in locale.
4.  Copiare il pacchetto sul server dedicato o nel controller di dominio in cui si sta installando il gateway ATA. In alternativa, è possibile aprire la Console ATA dal controller di dominio o dal server dedicato e ignorare questo passaggio.

Il file ZIP include quanto segue:

-   Programma di installazione del gateway ATA

-   File delle impostazioni di configurazione con le informazioni necessarie per connettersi ad ATA Center


>[!div class="step-by-step"]
[« Passaggio 2](install-ata-step2.md)
[Passaggio 4 »](install-ata-step4.md)

## Vedere anche

- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurare la raccolta degli eventi](configure-event-collection.md)
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=May16_HO1-->


