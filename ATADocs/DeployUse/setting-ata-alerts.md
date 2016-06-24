---
# required metadata

title: Impostazione di notifiche di ATA | Microsoft Advanced Threat Analytics
description: Viene descritto come impostare gli avvisi ATA per essere informati quando vengono rilevate attività sospette.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurazione delle notifiche di ATA
ATA può inviare una notifica quando rileva un'attività sospetta, tramite posta elettronica o usando l'inoltro di eventi ATA e inoltrando l'evento al server SIEM/Syslog. Prima di selezionare le notifiche che si desidera ricevere, è necessario [configurare il server di posta elettronica e il server Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Le notifiche tramite posta elettronica includono un collegamento che indirizza l'utente direttamente all'attività sospetta rilevata. La parte relativa al nome host del collegamento viene ricavata dall'impostazione dell'URL della console ATA nella pagina ATA Center. Per impostazione predefinita, l'URL della console ATA è l'indirizzo IP selezionato durante l'installazione di ATA Center.  Se si prevede di configurare le notifiche di posta elettronica, è consigliabile usare un nome di dominio completo (FQDN) come URL della Console ATA.
> -   Le notifiche vengono inviate da ATA Center al server SMTP e al server Syslog.

Per ricevere notifiche tramite posta elettronica, impostare le seguenti opzioni:


1. Nella Console ATA selezionare l'opzione delle impostazioni sulla barra degli strumenti e quindi **Configurazione**.
![Icona delle impostazioni di configurazione di ATA](media/ATA-config-icon.JPG)

2. Selezionare **Notifiche**.
3. In **Email notifications**(Notifiche posta elettronica) usare i comandi per selezionare le notifiche da inviare:


    - New suspicious activity is detected (Rilevata nuova attività sospetta)
    - New health issue is detected (Rilevato nuovo problema di integrità)
    - New software update is available (Nuovo aggiornamento software disponibile)

4. Specificare i destinatari che riceveranno le notifiche tramite posta elettronica.

    [Nota:] gli avvisi di posta elettronica per le attività sospette vengono inviati solo quando viene creata l'attività sospetta.


5. Fare clic su **Save**.

Per ricevere notifiche Syslog, impostare le seguenti opzioni:


1. Nella Console ATA selezionare l'opzione delle impostazioni sulla barra degli strumenti e quindi **Configurazione**.
![Icona delle impostazioni di configurazione di ATA](media/ATA-config-icon.JPG)

2. Selezionare **Notifiche**.
3. In **Syslog notifications** (Notifiche Syslog) usare i comandi per selezionare le notifiche da inviare:


    - New suspicious activity is detected (Rilevata nuova attività sospetta)
    - Existing suspicious activity is updated (Aggiornamento attività sospetta esistente)
    - New health issue is detected (Rilevato nuovo problema di integrità)
5. Fare clic su **Save**.
![Immagine delle impostazioni delle notifiche di ATA](media/ATA-notification-settings.png)




## Vedere anche
[Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->


