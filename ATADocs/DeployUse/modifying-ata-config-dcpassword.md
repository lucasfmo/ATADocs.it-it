---
# required metadata

title: Modificare la configurazione di ATA - Password di connettività del dominio | Microsoft Advanced Threat Analytics
description: Viene descritto come modificare la password di connettività del dominio nel gateway ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Modificare la configurazione di ATA - Password di connettività del dominio

>[!div class="step-by-step"]
[« Certificato IIS](modifying-ata-config-iiscert.md)


## Modificare la password di connettività del dominio
Se si modifica la password di connettività del dominio, assicurarsi che la password immessa sia corretta. In caso contrario, l'esecuzione del servizio ATA verrà arrestata nei gateway ATA.

Se si sospetta questo problema, nel gateway ATA esaminare il file Microsoft.Tri.Gateway-Errors.log per individuare questa voce:
`The supplied credential is invalid.`

Per correggere il problema, seguire questa procedura per aggiornare la password di connettività del dominio nel gateway ATA:

1.  Aprire la console ATA nel gateway ATA.

2.  Selezionare l'opzione delle impostazioni sulla barra degli strumenti e quindi **Configurazione**..

    ![Icona delle impostazioni di configurazione di ATA](media/ATA-config-icon.JPG)

3.  Selezionare **General** (Generale).

    ![Immagine della modifica della password del gateway ATA](media/ATA-GW-change-DC-password.JPG)

4.  In **General** (Generale), modificare la password.

5.  Fare clic su **Salva**..

6.  Dopo aver modificato la password, controllare manualmente che il servizio gateway ATA sia in esecuzione nei server gateway ATA.

>[!div class="step-by-step"]
[« Certificato IIS](modifying-ata-config-iiscert.md)

## Vedere anche
- [Uso della console ATA](working-with-ata-console.md)
- [Installare ATA](install-ata.md)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


