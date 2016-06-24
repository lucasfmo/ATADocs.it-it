---
# required metadata

title: Impostazione di notifiche di ATA | Microsoft Advanced Threat Analytics
description: Viene descritto come impostare ATA in modo da inviare una notifica (tramite posta elettronica o inoltro di eventi ATA) quando rileva attività sospette 
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

## Fornire ad ATA le impostazioni del server di posta elettronica
ATA può inviare una notifica quando rileva un'attività sospetta. Perché ATA possa inviare notifiche tramite posta elettronica, è prima di tutto necessario configurare le **Email server settings** (Impostazioni del server di posta elettronica).

1.  Nel server ATA Center fare clic sull'icona per la** **gestione di Microsoft Advanced Threat Analytics sul desktop.

2.  Immettere nome utente e password e quindi fare clic su **Log in** (Accedi)..

3.  Selezionare l'opzione delle impostazioni sulla barra degli strumenti e quindi **Configurazione**..

    ![Icona delle impostazioni di configurazione di ATA](media/ATA-config-icon.JPG)

4.  Nella scheda **General** (Generale), in **Email server** (Server di posta elettronica), immettere le informazioni seguenti:

    |Campo|Descrizione|Valore|
    |---------|---------------|---------|
    |SMTP server endpoint (obbligatorio)|Immettere il nome di dominio completo (FQDN) del server SMTP.|Ad esempio:<br />smtp.contoso.com|
    |SSL|Attivare o disattivare SSL in base a quanto richiesto da SMTP. **Nota:** se si abilita SSL, sarà necessario anche modificare il numero di porta.|L'opzione è disabilitata per impostazione predefinita|
    |Authentication|Abilitare l'opzione se il server SMTP richiede l'autenticazione. **Nota:** se si abilita l'autenticazione, è necessario fornire nome utente e password di un account di posta elettronica con l'autorizzazione per la connessione al server SMTP.|L'opzione è disabilitata per impostazione predefinita|
    |Send from (obbligatorio)|Immettere un indirizzo di posta elettronica da cui verrà inviato il messaggio di posta elettronica.|Ad esempio:<br />ATA@contoso.com|
    ![Immagine delle impostazioni del server di posta elettronica ATA](media/ATA-email-server.png)

## Fornire ad ATA le impostazioni del server Syslog
Quando rileva un'attività sospetta, ATA può inviare una notifica al server Syslog. Se si abilitano le notifiche per Syslog, è possibile impostare le opzioni descritte di seguito.

1.  Prima di configurare le notifiche per Syslog, rivolgersi all'amministratore SIEM per ottenere le informazioni seguenti:

    -   FQDN o indirizzo IP del server SIEM

    -   Porta su cui è in ascolto il server SIEM

    -   Trasporto da usare: UDP, TCP o TLS (Syslog sicuro)

    -   Formato in cui inviare i dati, RFC 3164 o 5424

2.  Nel server ATA Center fare clic sull'icona per la** **gestione di Microsoft Advanced Threat Analytics sul desktop.

3.  Immettere nome utente e password e quindi fare clic su **Log in** (Accedi)..

4.  Selezionare l'opzione delle impostazioni sulla barra degli strumenti e quindi **Configurazione**..

    ![Icona delle impostazioni di configurazione di ATA](media/ATA-config-icon.JPG)

5.  Selezionare **Syslog server** (Server Syslog) e immettere le informazioni seguenti:

    |Campo|Descrizione|
    |---------|---------------|
    |Syslog server endpoint|FQDN del server Syslog|
    |Trasporto|Può essere UDC, TCP o TLS (Syslog sicuro)|
    |Format|Formato usato da ATA per inviare gli eventi al server SIEM, RFC 5424 o RFC 3164.|





## Vedere anche
[Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


