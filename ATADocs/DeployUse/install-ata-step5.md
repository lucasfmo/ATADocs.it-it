---
# required metadata

title: Installare ATA - Passaggio 5 | Microsoft Advanced Threat Analytics
description: Il quinto passaggio dell'installazione di ATA consente di configurare le impostazioni per il gateway ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installare ATA - Passaggio 5

>[!div class="step-by-step"] [« Passaggio 4](install-ata-step4.md)
[Passaggio 6 »](install-ata-step6.md)


## Passaggio 5. Configurare le impostazioni del gateway ATA
Dopo l'installazione del gateway ATA, seguire questa procedura per configurare le relative impostazioni.

1.  Nella Console ATA fare clic su **Configurazione** e selezionare la pagina **ATA Gateways** (Gateway ATA).

2.  Immettere le informazioni seguenti.

  - **Description**: <br>Immettere una descrizione del gateway ATA (facoltativo).
  - **Controller di dominio con mirroring delle porte (FQDN)** (informazione richiesta per il gateway ATA, impostazione non prevista per il gateway ATA Lightweight): <br>Immettere il nome di dominio completo (FQDN) del controller di dominio e fare clic sul segno di addizione per aggiungerlo all'elenco. Ad esempio, **dc01.contoso.com**<br /><br />![Immagine del nome FDQN di esempio](media/ATAGWDomainController.png)

Le informazioni seguenti si applicano ai server immessi nell'elenco **Controller di dominio**: -   All domain controllers whose traffic is being monitored via port mirroring by the ATA Gateway must be listed in the **Domain Controllers** list. (Tutti i controller di dominio il cui traffico viene monitorato tramite il mirroring delle porte dal gateway ATA devono essere inclusi nell'elenco Controller di dominio). Se un controller di dominio non è presente nell'elenco **Domain Controllers**, il rilevamento di attività sospette potrebbe non funzionare come previsto.
-   At least one domain controller in the list be a global catalog server. (Almeno un controller di dominio nell'elenco deve essere un server di catalogo globale). In questo modo, ATA potrà risolvere gli oggetti computer e utente negli altri domini nella foresta.

 - **Capture Network adapters** (obbligatorio):<br>
     - Per un gateway ATA in un server dedicato, selezionare le schede di rete configurate come porta mirror di destinazione. Queste riceveranno il traffico di controller di dominio con mirroring.
     - Per un gateway Lightweight ATA, selezionare tutte le schede di rete usate per la comunicazione con altri computer nell'organizzazione.

![Immagine della configurazione delle impostazioni del gateway](media/ATA-Config-GW-Settings.jpg)

 - **Candidato alla sincronizzazione del dominio**<br>
Ogni gateway ATA impostato per essere un candidato alla sincronizzazione del dominio può essere responsabile della sincronizzazione tra ATA e il dominio di Active Directory. A seconda delle dimensioni del dominio, la sincronizzazione iniziale può richiedere molto tempo e un notevole uso di risorse. Per impostazione predefinita, solo i gateway ATA vengono impostati come candidati alla sincronizzazione del dominio. <br>È consigliabile disabilitare questa impostazione predefinita per gateway ATA di un sito remoto.<br>Se il controller di dominio è di sola lettura, non impostarlo come candidato alla sincronizzazione del dominio. Per altre informazioni, vedere [ATA architecture](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features) (Architettura di ATA)

> [!NOTE] Il primo avvio del servizio gateway ATA richiederà alcuni minuti per la creazione della cache dei parser di acquisizione di rete.<br>
Le modifiche alla configurazione verranno applicate al gateway ATA alla successiva sincronizzazione pianificata tra il gateway ATA e ATA Center.



    

3. Facoltativamente, è possibile impostare il [listener di Syslog e la Raccolta di inoltro eventi di Windows](configure-event-collection.md). 
4. Abilitare **Update ATA Gateway automatically** (Aggiorna automaticamente il gateway ATA) in modo che, quando si aggiorna ATA Center nelle versioni future, tutti i gateway ATA verranno aggiornati in automatico.
3.  Fare clic su **Save**.


## Convalidare le installazioni
Per verificare che il gateway ATA sia stato distribuito correttamente, controllare gli aspetti seguenti:

1.  Controllare che il servizio denominato **Microsoft Advanced Threat Analytics Gateway** (Gateway Microsoft Advanced Threat Analytics) sia in esecuzione. Dopo aver salvato le impostazioni del gateway ATA, potrebbero essere necessari alcuni minuti per l'avvio del servizio.

2.  Se il servizio non viene avviato, esaminare il file "Microsoft.Tri.Gateway-Errors.log" nella cartella predefinita seguente, "%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs".

3.  Per assistenza, consultare l'articolo [ATA Troubleshooting](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors) (Risoluzione dei problemi di ATA).

4.  Se si tratta del primo gateway ATA installato, dopo alcuni minuti accedere alla console ATA e aprire il riquadro delle notifiche scorrendo rapidamente verso il lato destro dello schermo. Sulla barra di notifica a destra della console dovrebbe venire visualizzato l'elenco **Entities Recently Learned**.

5.  Sul desktop fare clic sul collegamento **Microsoft Advanced Threat Analytics** per connettersi alla Console ATA. Eseguire l'accesso con le stesse credenziali utente che sono state usate per installare il centro ATA.
6.  Nella console cercare un elemento nella barra di ricerca, ad esempio un utente o un gruppo nel dominio.
7.  Aprire Performance Monitor. Nell'albero delle prestazioni fare clic su **Performance Monitor** e quindi fare clic sull'icona a forma di segno di addizione per** **aggiungere un contatore. Espandere **Microsoft ATA Gateway** (Gateway Microsoft ATA), scorrere verso il basso fino a **Network Listener PEF Captured Messages/Sec** (Messaggi del parser PEF di NetworkListener/sec) e aggiungere questo contatore. Assicurarsi quindi che sul grafico venga visualizzata l'attività.

    ![Immagine dell'aggiunta di contatori delle prestazioni](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"] [« Passaggio 4](install-ata-step4.md)
[Passaggio 6 »](install-ata-step6.md)

## Vedere anche

- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurare la raccolta degli eventi](configure-event-collection.md)
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO3-->


