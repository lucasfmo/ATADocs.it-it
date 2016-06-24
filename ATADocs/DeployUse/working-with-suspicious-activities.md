---
# required metadata

title: Gestione di attività sospette | Microsoft Advanced Threat Analytics
description: Viene descritto come esaminare le attività sospette identificate da ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Gestione di attività sospette
Questo argomento illustra le nozioni di base per lavorare con Advanced Threat Analytics.

## Esaminare le attività sospette nella sequenza temporale di attacco
Dopo l'accesso alla console ATA, viene automaticamente visualizzata la **sequenza temporale delle attività sospette**. Le attività sospette sono elencate in ordine cronologico con quelle più recenti nella parte superiore della sequenza temporale.
Ogni attività sospetta include informazioni relative agli aspetti seguenti:

-   Entità coinvolte, inclusi utenti, computer, server, controller di dominio e risorse.

-   Orari e intervallo di tempo delle attività sospette.

-   Gravità dell'attività sospetta, che può essere alta, media o bassa.

-   Stato aperto, risolto o ignorato.

-   Possibilità di

    -   Condividere l'attività sospetta con altre persone dell'organizzazione tramite posta elettronica.

    -   Esportare l'attività sospetta in Excel.

    -   Aggiungere una nota all'attività sospetta.

    -   Fornire input sull'attività sospetta.

-   Consigli su come rispondere all'attività sospetta.

> [!NOTE]
> -   Quando si passa il puntatore del mouse su un utente o un computer, viene visualizzato un breve profilo di entità che fornisce informazioni aggiuntive sull'entità e include il numero di attività sospette a cui l'entità è collegata.
> -   Se si fa clic su un'entità, viene visualizzato il profilo di entità dell'utente o del computer.

![Immagine della sequenza temporale delle attività sospette di ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## Filtrare l'elenco di attività sospette
Per filtrare l'elenco di attività sospette:

1.  Nel riquadro **Filtra per** a sinistra dello schermo selezionare una delle opzioni seguenti: **All** (Tutte), **Open** (Aperte), **Resolved**(Risolte) o **Dismissed** (Ignorate).

2.  Per filtrare ulteriormente l'elenco, selezionare **High** (Elevata), **Medium** (Media) o **Low** (Bassa).

**Gravità delle attività sospette**

-   **Low**

    Indica attività sospette che possono portare ad attacchi progettati per consentire a utenti malintenzionati o software dannoso di ottenere l'accesso ai dati aziendali.

-   **Medium**

    Indica attività sospette che possono mettere identità specifiche a rischio di attacchi più gravi che potrebbero comportare il furto di identità o l'escalation dei privilegi.

-   **High**

    Indica attività sospette che possono comportare il furto di identità, l'escalation dei privilegi o altri attacchi a impatto elevato.

**Stato delle attività sospette**

-   **Open**

    In questo elenco sono visualizzate tutte le nuove attività sospette.

-   **Resolved**

    Questo stato viene usato per tenere traccia delle attività sospette identificate, analizzate e corrette per attenuare i rischi.

    > [!NOTE]
    > ATA può riaprire un'attività risolta se la stessa attività viene rilevata di nuovo entro un breve periodo di tempo.

-   **Dismissed**

    Attività ignorate manualmente. Se ATA rileva un'attività sospetta simile, verrà creato un nuovo rilevamento.

## Fornire input su un'attività sospetta
Per consentire ad ATA di apprendere informazioni sulla rete, alcune attività sospette (esplorazione DNS, attacchi di tipo pass-the-ticket, enumerazione delle sessioni SMB, comportamento anomalo ed esecuzione remota) richiedono l'input dell'utente per migliorare il rilevamento di attività sospette in futuro.

1.  Per le attività sospette che consentono di fornire input, la domanda di input viene visualizzata automaticamente. Verrà chiesto di rispondere a domande sulle attività nella rete e di indicare se devono o meno essere considerate sospette. Nell'esempio seguente viene chiesto se è consentita l'esecuzione di strumenti di scansione in un computer specifico.

    ![Immagine della richiesta di input per le attività sospette in ATA](media/ATA-Input.JPG)

2.  Se si risponde di no, questa attività viene considerata sospetta e ogni volta che ATA la rileva nel computer si riceverà un avviso.

3.  Se tuttavia si risponde di sì, l'attività sospetta può venire ignorata e le attività future di questo tipo in questo computer potrebbero non generare un'attività sospetta oppure generare un'attività che viene ignorata automaticamente.

4.  Se non si è certi di come rispondere, è possibile fare clic su **Annulla**.

## Modificare lo stato di un'attività sospetta
È possibile modificare lo stato di un'attività sospetta facendo clic sullo stato corrente della stessa e selezionando una delle opzioni seguenti: **Open** (Aperta), **Resolved** (Risolta) o **Dismissed**(Ignorata).

## Vedere anche
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Uso delle impostazioni di rilevamento di ATA](working-with-detection-settings.md)
- [Modifica della configurazione di ATA](modifying-ata-configuration.md)


<!--HONumber=May16_HO1-->


