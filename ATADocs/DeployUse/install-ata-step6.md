---
# required metadata

title: Installare ATA | Microsoft Advanced Threat Analytics
description: Il passaggio finale dell'installazione di ATA consente di configurare le subnet di lease a breve termine e l'utente di tipo honeytoken.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installare ATA - Passaggio 6

>[!div class="step-by-step"]
[« Passaggio 5](install-ata-step5.md)

## Passaggio 6. Configurare le subnet di lease a breve termine e l'utente di tipo honeytoken
Le subnet di lease a breve termine sono subnet in cui l'assegnazione degli indirizzi IP cambia molto rapidamente, entro pochi secondi o minuti, ad esempio per quanto riguarda gli indirizzi IP usati per le VPN e gli indirizzi IP Wi-Fi. Per immettere l'elenco di subnet di lease a breve termine usate nell'organizzazione, seguire questa procedura:

1.  Nella Console ATA sul computer gateway ATA fare clic sull'icona delle impostazioni e selezionare **Configurazione**.

    ![Impostazioni di configurazione di ATA](media/ATA-config-icon.JPG)

2.  In **Detection** immettere quanto segue per le subnet di lease a breve termine. Immettere le subnet di lease a breve termine usando il formato di notazione con barra, ad esempio `192.168.0.0/24`, e fare clic sul segno di addizione.

3.  Per i SID degli account honeytoken, immettere il SID per l'account utente che non presenterà attività di rete e fare clic sul segno di addizione. Ad esempio: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > Per trovare il SID di un utente, cercare l'utente nella Console ATA e quindi fare clic sulla scheda **Account Info** (Info account). 

4.  Configurare le esclusioni: è possibile configurare gli indirizzi IP da escludere da attività sospette specifiche. Per altre informazioni, vedere [Uso delle impostazioni di rilevamento di ATA](working-with-detection-settings.md).

5.  Fare clic su **Salva**..

![Salva modifiche](media/ATA-VPN-Subnets.JPG)

La distribuzione di Microsoft Advanced Threat Analytics è stata completata.

Controllare la sequenza temporale di attacco per visualizzare le attività sospette rilevate e per cercare utenti o computer e visualizzare i relativi profili.

ATA inizierà immediatamente la ricerca di attività sospette. Determinate attività, ad esempio alcune legate a comportamenti sospetti, non saranno disponibili fino a quando ATA non avrà creato profili comportamentali (minimo tre settimane).


>[!div class="step-by-step"]
[« Passaggio 5](install-ata-step5.md)


## Vedere anche

- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurare la raccolta degli eventi](configure-event-collection.md)
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


