---
# required metadata

title: Installare ATA - Passaggio 2 | Microsoft Advanced Threat Analytics
description: Il secondo passaggio dell'installazione di ATA consente di configurare le impostazioni di connettività del dominio nel server ATA Center
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installare ATA - Passaggio 2

>[!div class="step-by-step"] [« Passaggio 1](install-ata-step1.md)
[Passaggio 3 »](install-ata-step3.md)

## Passaggio 2: Configurare le impostazioni generali del gateway ATA
Le impostazioni nella scheda delle impostazioni **General** (Generale) si applicano a tutti i gateway ATA gestiti da ATA Center.

Per configurare le impostazioni generali del gateway ATA seguire questa procedura:

1.  Aprire la console ATA e accedere. Per istruzioni, vedere [Working with the ATA Console](working-with-ata-console.md) (Uso della console ATA).

2.  Fare clic sull'icona Impostazioni e selezionare **Configurazione**.

    ![Impostazioni di configurazione dei gateway ATA](media/ATA-config-icon.JPG)

3.  Nella scheda **General** (Generale), in **ATA Gateways** (Gateway ATA), immettere le informazioni seguenti e fare clic su **Salva**.

    |Campo|Commenti|
    |---------|------------|
    |**Username** (obbligatorio)|Immettere il nome utente di sola lettura, ad esempio: **utente1**.|
    |**Password** (obbligatorio)|Immettere la password per l'utente di sola lettura, ad esempio: **Matita1**. **Nota:** assicurarsi che la password sia corretta. Se si salva la password sbagliata, l'esecuzione del servizio ATA nei server gateway ATA verrà interrotta.|
    |**Domain** (obbligatorio)|Immettere il dominio per l'utente di sola lettura, ad esempio: **contoso.com**. **Nota:** è importante immettere il nome di dominio completo (FQDN) per il dominio in cui si trova l'utente. Ad esempio, se l'account dell'utente è nel dominio corp.contoso.com, è necessario immettere `corp.contoso.com` e non contoso.com|
    |Aggiornare tutti i gateway ATA automaticamente |Se si abilita questa impostazione, quando si aggiorna ATA Center nelle versioni future, tutti i gateway ATA verranno aggiornati in automatico.|

    ![Immagine delle impostazioni di connettività del dominio ATA](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"] [« Passaggio 1](install-ata-step1.md)
[Passaggio 3 »](install-ata-step3.md)


## Vedere anche

- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurare la raccolta degli eventi](configure-event-collection.md)
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=May16_HO3-->


