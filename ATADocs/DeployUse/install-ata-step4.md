---
# required metadata

title: Installare ATA - Passaggio 4 | Microsoft Advanced Threat Analytics
description: Il quarto passaggio dell'installazione di ATA consente di installare il gateway ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installare ATA - Passaggio 4

>[!div class="step-by-step"]
[« Passaggio 3](install-ata-step3.md)
[Passaggio 5 »](install-ata-step5.md)

## Passaggio 4. Installare il gateway ATA

Prima di installare il gateway ATA su un server dedicato, verificare che il mirroring delle porte sia configurato correttamente e che il gateway ATA possa vedere il traffico da e verso i controller di dominio. Per altre informazioni, vedere[Validate port mirroring](validate-port-mirroring.md) (Convalidare il mirroring delle porte).


> [!IMPORTANT]
> Assicurarsi di avere installato [KB2919355](http://support.microsoft.com/kb/2919355/).  Eseguire il cmdlet di PowerShell seguente per verificare l'installazione dell'hotfix:
>
> `Get-HotFix -Id kb2919355`

Seguire questa procedura nel server gateway ATA.

1.  Estrarre i file dal file ZIP. 
> [!NOTE] Non è possibile eseguire l'installazione diretta dal file ZIP.

2.  Da un prompt dei comandi con privilegi elevati eseguire **Microsoft ATA Gateway Setup.exe** e seguire l'installazione guidata.

3.  Nella pagina di **benvenuto** selezionare la lingua e fare clic su **Avanti**..

4.  In **ATA Gateway Configuration** immettere le informazioni seguenti in base all'ambiente:

    ![Immagine della configurazione del gateway ATA](media/ATA-Gateway-Configuration.JPG)

    |Campo|Descrizione|Commenti|
    |---------|---------------|------------|
    |Installation Path|Posizione di installazione del gateway ATA. Per impostazione predefinita, l'installazione viene eseguita in %programfiles%\Microsoft Advanced Threat Analytics\Gateway.|Mantenere il valore predefinito.|
    |ATA Gateway Service SSL certificate|Certificato che verrà usato dal gateway ATA.|Usare un certificato autofirmato solo per ambienti lab.|
    |ATA Gateway Registration|Immettere nome utente e password dell'amministratore ATA.|Per la registrazione del gateway ATA in ATA Center, immettere nome utente e password dell'utente che ha installato ATA Center. L'utente deve essere membro di uno dei gruppi locali seguenti in ATA Center.<br /><br />-   Administrators<br />-   Microsoft Advanced Threat Analytics Administrators **Nota:** queste credenziali vengono usate solo per la registrazione e non sono archiviate in ATA.|
    Durante l'installazione del gateway ATA vengono installati e configurati i componenti seguenti:

    -   KB 3047154

        > [!IMPORTANT]
        > -   Non installare KB 3047154 in un host di virtualizzazione (l'host che sta eseguendo la virtualizzazione, è possibile eseguirla su una macchina virtuale). Questa operazione potrebbe impedire il corretto funzionamento del mirroring delle porte. 
        > -   Non installare Message Analyzer, Wireshark o altri software di acquisizione di rete nel gateway ATA. Se è necessario acquisire il traffico di rete, installare e usare Microsoft Network Monitor 3.4.

    -   Servizio gateway ATA

    -   Microsoft Visual C++ 2013 Redistributable

    -   Set di raccolta dati di monitoraggio delle prestazioni personalizzato

5.  Al termine dell'installazione, per il gateway ATA fare clic su **Avvia** per aprire il browser e accedere alla Console ATA, mentre per il gateway ATA Lightweight fare clic su **Fine**.


>[!div class="step-by-step"]
[« Passaggio 3](install-ata-step3.md)
[Passaggio 5 »](install-ata-step5.md)

## Vedere anche

- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurare la raccolta degli eventi](configure-event-collection.md)
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


