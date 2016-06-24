---
# required metadata

title: Novità in ATA versione 1.4 | Microsoft Advanced Threat Analytics
description: Vengono elencate le novità in ATA versione 1.4 e i problemi noti
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Novità in ATA versione 1.4
Queste note sulla versione offrono informazioni sui problemi noti relativi alla versione 1.4 di Advanced Threat Analytics.

## Novità in questa versione

-   Supporto per Windows Event Forwarding (WEF) per l'invio di eventi direttamente dai controller di dominio al gateway ATA.

-   Miglioramenti relativi al rilevamento di attacchi pass-the-hash in risorse aziendali tramite la combinazione di DPI (Deep Packet Inspection) e registri eventi di Windows.

-   Miglioramenti per il supporto di dispositivi non appartenenti a un dominio e dispositivi non Windows per il rilevamento e la visibilità.

-   Miglioramenti correlati alle prestazioni per supportare traffico maggiore per ogni gateway ATA.

-   Miglioramenti correlati alle prestazioni per supportare più gateway ATA per ogni ATA Center.

-   È stato aggiunto un nuovo processo di risoluzione dei nomi automatico che associa nomi di computer e indirizzi IP. Questa esclusiva funzionalità permette di risparmiare tempo prezioso nel processo di analisi e offre solide prove per gli analisti della sicurezza.

-   Capacità migliorata di raccogliere l'input degli utenti per ottimizzare automaticamente il processo di rilevamento.

-   Rilevamento automatico per i dispositivi NAT.

-   Failover automatico quando i controller di dominio non sono raggiungibili.

-   Il monitoraggio dell'integrità del sistema e le notifiche associate forniscono ora informazioni sullo stato di integrità complessivo della distribuzione, nonché su problemi specifici di configurazione e connettività.

-   Visibilità in siti e percorsi in cui operano le entità.

-   Supporto per più domini.

-   Supporto per domini con etichetta singola.

-   Supporto per la modifica dell'indirizzo IP e del certificato dei gateway ATA e di ATA Center.

-   Telemetria per migliorare l'esperienza dei clienti.

## Problemi noti
Questa versione presenta i problemi noti descritti di seguito.

### Software di acquisizione di rete
Nel gateway ATA l'unico software di acquisizione di rete supportato che è possibile installare è [Microsoft Network Monitor 3.4](http://www.microsoft.com/en-us/download/details.aspx?id=4865). Non installare Microsoft Message Analyzer o altro software di acquisizione di rete. L'installazione di un software diverso impedisce immediatamente il funzionamento corretto del gateway ATA.

### Installazione da file ZIP
Quando si installa il gateway ATA, assicurarsi di estrarre i file dal file ZIP in una directory locale e di installarlo da questa directory. Non installare il gateway ATA direttamente dal file ZIP, altrimenti l'installazione non riuscirà.

### Disinstallazione di versioni precedenti di ATA
Se è stata installata una versione precedente di ATA, di anteprima pubblica o anteprima privata, è necessario disinstallare ATA e i gateway ATA prima di installare questa versione.

È anche necessario eliminare i file di database e i file di log. I database delle versioni precedenti di ATA non sono compatibili con la versione disponibile a livello generale di ATA.

Se quando si prova a disinstallare ATA Center o il gateway ATA viene avviata l'installazione invece della disinstallazione, è necessario aggiungere la chiave del Registro di sistema seguente e quindi disinstallare di nuovo ATA.

**ATA Center**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

-   Aggiungere un nuovo valore stringa chiamato `InstallationPath` con il valore `C:\Program Files\Microsoft Advanced Threat Analytics\Center`. Questa è la cartella di installazione predefinita. Se la cartella di installazione è stata modificata, immettere il percorso in cui è stato installato ATA.

    ![Percorso di installazione di ATA Center nell'editor del Registro di sistema](media/ATA-uninstall-center-bug.jpg)

**Gateway ATA**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   Aggiungere un nuovo valore stringa chiamato `InstallationPath` con il valore `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway`. Questa è la cartella di installazione predefinita.  Se la cartella di installazione è stata modificata, immettere il percorso in cui è stato installato ATA.

    ![Percorso di installazione del gateway ATA nell'editor del Registro di sistema](media/ATA-GW-uninstall-bug.jpg)

Al termine della disinstallazione, eliminare la cartella di installazione sia in ATA Center sia nel gateway ATA.  Se il database è stato installato in una cartella separata, eliminare la cartella del database in ATA Center.

### Avviso di integrità - Gateway ATA disconnesso
Se sono presenti più gateway ATA e vengono visualizzati avvisi sulla disconnessione dei gateway ATA, la risoluzione automatica funziona per uno solo, lasciando gli altri con stato aperto. È necessario verificare manualmente che il gateway ATA sia attivo e che il servizio sia in esecuzione e quindi risolvere manualmente l'avviso.

### Hotfix della Knowledge Base nell'host di virtualizzazione
Non installare l'hotfix disponibile nell'articolo KB 3047154 in un host di virtualizzazione. Questa operazione potrebbe impedire il corretto funzionamento del mirroring delle porte.

## Vedere anche

[Update ATA to version 1.6 - migration guide (Guida alla migrazione: aggiornamento di ATA alla versione 1.6)](ata-update-1.6-migration-guide.md)

[Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

<!--HONumber=May16_HO3-->


