---
# required metadata

title: Modificare la configurazione di ATA - Indirizzo IP della console ATA | Microsoft Advanced Threat Analytics
description: Viene descritto come modificare l'indirizzo IP della console ATA, usato per creare un collegamento alla console ATA nei gateway ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Modificare la configurazione di ATA - Indirizzo IP della console ATA

>[!div class="step-by-step"]
[« Certificato di ATA Center](modifying-ata-config-centercert.md)
[Certificato IIS »](modifying-ata-config-iiscert.md)

## Modificare l'indirizzo IP della console ATA
Per impostazione predefinita, l'URL della console ATA è l'indirizzo IP selezionato per la console ATA durante l'installazione di ATA Center.

L'URL viene usato negli scenari seguenti:

-   Installazione di gateway ATA: quando viene installato un gateway ATA, questo registra se stesso in ATA Center. Questo processo di registrazione viene eseguito tramite la connessione alla console ATA. Se si immette un FQDN per l'URL della Console ATA, è necessario assicurarsi che il gateway ATA sia in grado di risolvere l'FQDN all'indirizzo IP con cui la Console ATA è associata in IIS. L'URL viene inoltre usato per creare il collegamento alla console ATA nei gateway ATA.

-   Avvisi: quando ATA invia un avviso tramite SIEM o posta elettronica, include un collegamento all'attività sospetta. La parte del collegamento che definisce l'host è l'impostazione dell'URL della console ATA.

-   Se è stato installato un certificato dall'Autorità di certificazione (CA) interna, probabilmente è necessario che l'URL corrisponda al nome soggetto nel certificato, per evitare che gli utenti non ricevano un messaggio di avviso durante la connessione alla console ATA.

-   L'uso di un FQDN per l'URL della console ATA permette di modificare l'indirizzo IP usato da IIS per la console ATA senza eliminare gli avvisi inviati in passato o dover scaricare di nuovo il pacchetto dei gateway ATA. È sufficiente aggiornare il DNS con il nuovo indirizzo IP.

> [!NOTE]
> Dopo aver modificato l'URL della console ATA, è necessario scaricare il pacchetto di installazione dei gateway ATA prima di installare nuovi gateway ATA.

Se è necessario modificare l'indirizzo IP usato da IIS per la console ATA, seguire questi passaggi nel server ATA Center.

1.  Installare l'indirizzo IP nel server ATA Center.

2.  Aprire Gestione Internet Information Services (IIS).

3.  Espandere il nome del server e quindi espandere **Siti**.

4.  Selezionare il sito della Console Microsoft ATA e nel riquadro **Azioni** fare clic su **Bindings** (Associazioni).

    ![Immagine delle azioni delle associazioni della console ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Selezionare **HTTP** e quindi fare clic su **Modifica** per selezionare il nuovo indirizzo IP. Ripetere l'operazione per **HTTPS** selezionando lo stesso indirizzo IP.

    ![Immagine della modifica delle associazioni del sito](media/ATA-change-console-IP.jpg)

6.  Nel riquadro **Azioni** fare clic su **Riavvia** in **Manage Website** (Gestisci sito Web).

7.  Aprire un prompt dei comandi con privilegi di amministratore e digitare i comandi seguenti per aggiornare il driver HTTP.SYS:

    -   Per aggiungere il nuovo indirizzo IP: `netsh http add iplisten ipaddress=newipaddress`

    -   Per verificare che venga usato il nuovo indirizzo IP: `netsh http show iplisten`

    -   Per eliminare l'indirizzo IP precedente: `netsh http delete iplisten ipaddress=oldipaddress`

8.  Se l'URL della console ATA usa ancora un indirizzo IP, aggiornare l'URL in base al nuovo indirizzo IP e scaricare il pacchetto di installazione dei gateway ATA prima di distribuire nuovi gateway ATA.

9. Se l'URL della console ATA è un FQDN, aggiornare il DNS con il nuovo indirizzo IP per l'FQDN.

>[!div class="step-by-step"]
[« Certificato di ATA Center](modifying-ata-config-centercert.md)
[Certificato IIS »](modifying-ata-config-iiscert.md)


## Vedere anche
- [Uso della console ATA](working-with-ata-console.md)
- [Installare ATA](install-ata.md)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


