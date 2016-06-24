---
# required metadata

title: Modificare la configurazione di ATA - Certificato IIS | Microsoft Advanced Threat Analytics
description: Viene descritto come modificare il certificato usato da IIS per ATA Center.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Modificare la configurazione di ATA - Certificato IIS

>[!div class="step-by-step"]
[« Indirizzo IP della console ATA](modifying-ata-config-consoleip.md)
[Password di connettività del dominio »](modifying-ata-config-dcpassword.md)

## Modificare il certificato IIS
Nella console è possibile selezionare e modificare il certificato per il servizio ATA Center, ma non è possibile modificare il certificato usato da IIS.

Se si vuole modificare questo certificato, usare la procedura seguente:

> [!NOTE]
> Dopo aver modificato il certificato IIS, è necessario scaricare il pacchetto di installazione dei gateway ATA prima di installare nuovi gateway ATA.

Se è necessario modificare il certificato usato da IIS per ATA Center, eseguire questi passaggi nel server ATA Center.

1.  Installare il nuovo certificato nel server ATA Center.

2.  Aprire Gestione Internet Information Services (IIS).

3.  Espandere il nome del server e quindi espandere **Siti**.

4.  Selezionare il sito della Console Microsoft ATA e nel riquadro **Azioni** fare clic su **Bindings** (Associazioni).

    ![Azioni delle associazioni della console ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Selezionare **HTTPS** e fare clic su **Modifica**.

6.  In **Certificato SSL** selezionare il nuovo certificato.

7.  Scaricare il pacchetto di installazione dei gateway ATA prima di installare un nuovo gateway ATA.

>[!div class="step-by-step"]
[« Indirizzo IP della console ATA](modifying-ata-config-consoleip.md)
[Password di connettività del dominio »](modifying-ata-config-dcpassword.md)

## Vedere anche
- [Uso della console ATA](working-with-ata-console.md)
- [Installare ATA](install-ata.md)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


