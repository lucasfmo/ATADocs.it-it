---
# required metadata

title: Installare ATA in modalità invisibile all'utente | Microsoft Advanced Threat Analytics
description: Questo articolo descrive come eseguire un'installazione di ATA invisibile all'utente.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installazione di ATA invisibile all'utente
Questo articolo fornisce istruzioni dettagliate per l'installazione di ATA invisibile all'utente.
## Prerequisiti

Microsoft ATA 1.6 richiede l'installazione completa di Microsoft .NET Framework 4.6.1. 

Quando si installa o aggiorna ATA, .Net Framework 4.6.1 verrà automaticamente installato come parte della distribuzione di Microsoft ATA.

> [!Note] Per l'installazione di .Net Framework 4.6.1 può essere necessario riavviare il server. Quando si installa il gateway ATA nei controller di dominio, si consiglia di pianificare una finestra di manutenzione per i controller di dominio.
Quando si usa il metodo di installazione invisibile all'utente di ATA, il programma di installazione viene configurato per riavviare automaticamente il server al termine dell'installazione (se necessario). Per evitare il riavvio del server come parte dell'installazione, usare il flag `-NoRestart`. Quando si usa il flag `-NoRestart` e il riavvio viene richiesto come parte dell'installazione, il programma di installazione viene sospeso fino al riavvio del server. Per tenere traccia dell'avanzamento della distribuzione, controllare i log del programma di installazione di ATA in **%AppData%\Local\Temp**..


## Installare il Centro ATA

Per installare il Centro ATA, usare il comando seguente:

**Sintassi**:

    “Microsoft ATA Center Setup.exe” [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments=”/q”] [InstallationPath=“<InstallPath>”] [DatabaseDataPath= “<DBPath>”] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint=“<CertThumbprint>”] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint=”<CertThumbprint >”]
    
**Opzioni di installazione**:

|Nome|Sintassi|Obbligatoria per l'installazione invisibile all'utente?|Descrizione|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sì|Esegue il programma di installazione senza visualizzare richieste e interfaccia utente.|
|NoRestart|/norestart|No|Elimina tutti i tentativi di riavvio. Per impostazione predefinita, prima del riavvio viene visualizzata la richiesta dell'interfaccia utente.|
|Help|/help|No|Fornisce la guida e riferimenti rapidi. Visualizza l'uso corretto del comando di installazione incluso un elenco di tutte le opzioni e i comportamenti.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sì|Specifica i parametri per l'installazione di .Net Framework. È necessario impostare questa opzione per attivare l'installazione invisibile all'utente di .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Sì|Indica che la licenza è stata letta e approvata. È necessario impostare questa opzione sull'installazione invisibile all'utente.|

**Parametri di installazione**:

|Nome|Sintassi|Obbligatorio per l'installazione invisibile all'utente?|Descrizione|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath="<InstallPath>"|No|Imposta il percorso di installazione dei file binari ATA. Il percorso predefinito è: C:\Programmi\Microsoft Advanced Threat Analytics\Center.|
|DatabaseDataPath|DatabaseDataPath="<DBPath>"|No|Imposta il percorso della cartella dati del database ATA. Il percorso predefinito è: C:\Programmi\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|Sì|Imposta l'indirizzo IP del servizio del Centro ATA.|
|CenterPort|CenterPort=<CenterPort>|Sì|Imposta la porta di rete del servizio del Centro ATA.|
|CenterCertificateThumbprint|CenterCertificateThumbprint="<CertThumbprint>"|No|Imposta l'identificazione personale del certificato per il servizio del Centro ATA. Tale certificato viene usato per garantire la comunicazione tra il Centro ATA e il gateway ATA. Se non viene impostato, l'installazione genererà un certificato autofirmato.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|Sì|Imposta l'indirizzo IP della Console ATA.|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint="<CertThumbprint >"|No|Specifica l'identificazione personale del certificato per la Console ATA. Tale certificato viene usato per convalidare l'identità del sito Web della Console ATA. Se non viene specificato, l'installazione genererà un certificato autofirmato|

**Esempi**:
Per installare il Centro ATA con percorsi di installazione predefiniti e un singolo indirizzo IP:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Per installare il Centro ATA con percorsi di installazione predefiniti, due indirizzi IP e le identificazioni personali del certificato definite dall'utente:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F”
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint=”G9530253C976BFA9342FD1A716C0EC94207BFD5A”

## Aggiornare il Centro ATA

Per aggiornare il Centro ATA, usare il comando seguente:

**Sintassi**:

    Microsoft ATA Center Setup.exe” [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments=”/q”]


**Opzioni di installazione**:

|Nome|Sintassi|Obbligatoria per l'installazione invisibile all'utente?|Descrizione|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sì|Esegue il programma di installazione senza visualizzare richieste e interfaccia utente.|
|NoRestart|/norestart|No|Elimina tutti i tentativi di riavvio. Per impostazione predefinita, prima del riavvio viene visualizzata la richiesta dell'interfaccia utente.|
|Help|/help|No|Fornisce la guida e riferimenti rapidi. Visualizza l'uso corretto del comando di installazione incluso un elenco di tutte le opzioni e i comportamenti.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sì|Specifica i parametri per l'installazione di .Net Framework. È necessario impostare questa opzione per attivare l'installazione invisibile all'utente di .Net Framework.|


Quando si aggiorna ATA, il programma di installazione rileva automaticamente che ATA è già installato nel server e non è necessaria alcuna opzione di installazione dell'aggiornamento.

**Esempi**:
Per aggiornare il Centro ATA in modalità invisibile all'utente. In ambienti di grandi dimensioni, l'aggiornamento del Centro ATA può richiedere alcuni minuti. Monitorare i log di ATA per tenere traccia dell'avanzamento dell'aggiornamento.

        “Microsoft ATA Center Setup.exe” /quiet NetFrameworkCommandLineArguments="/q"

## Disinstallare il Centro ATA in modalità invisibile all'utente

Per eseguire una disinstallazione del Centro ATA in modalità invisibile all'utente, usare il comando seguente:
**Sintassi**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**Opzioni di installazione**:

|Nome|Sintassi|Obbligatoria per la disinstallazione invisibile all'utente?|Descrizione|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sì|Esegue il programma di disinstallazione senza visualizzare richieste e interfaccia utente.|
|Uninstall|/uninstall|Sì|Esegue la disinstallazione invisibile all'utente del Centro ATA dal server.|
|NoRestart|/norestart|No|Elimina tutti i tentativi di riavvio. Per impostazione predefinita, prima del riavvio viene visualizzata la richiesta dell'interfaccia utente.|
|Help|/help|No|Fornisce la guida e riferimenti rapidi. Visualizza l'uso corretto del comando di installazione incluso un elenco di tutte le opzioni e i comportamenti.|

**Parametri di installazione**:

|Nome|Sintassi|Obbligatorio per la disinstallazione invisibile all'utente?|Descrizione|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|No|Elimina tutti i file del database esistente.|

**Esempi**:
Per disinstallare in modalità invisibile all'utente il Centro ATA dal server, rimuovere tutti i dati del database esistenti:


    “Microsoft ATA Center Setup.exe” /quiet /uninstall --DeleteExistingDatabaseData

## Installazione del gateway ATA invisibile all'utente
Per installare il gateway ATA in modalità invisibile all'utente, usare il comando seguente:

**Sintassi**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint=”<CertThumbprint >”] [ConsoleAccountName=”<AccountName>”] 
    [ConsoleAccountPassword=”<AccountPassword>”]

**Opzioni di installazione**:

|Nome|Sintassi|Obbligatoria per l'installazione invisibile all'utente?|Descrizione|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sì|Esegue il programma di installazione senza visualizzare richieste e interfaccia utente.|
|NoRestart|/norestart|No|Elimina tutti i tentativi di riavvio. Per impostazione predefinita, prima del riavvio viene visualizzata la richiesta dell'interfaccia utente.|
|Help|/help|No|Fornisce la guida e riferimenti rapidi. Visualizza l'uso corretto del comando di installazione incluso un elenco di tutte le opzioni e i comportamenti.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sì|Specifica i parametri per l'installazione di .Net Framework. È necessario impostare questa opzione per attivare l'installazione invisibile all'utente di .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Sì|Indica che la licenza è stata letta e approvata. È necessario impostare questa opzione sull'installazione invisibile all'utente.|

**Parametri di installazione**:

|Nome|Sintassi|Obbligatoria per l'installazione invisibile all'utente?|Descrizione|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint="<CertThumbprint >"|No|Imposta l'identificazione personale del certificato per il servizio del Centro ATA. Tale certificato viene usato per garantire la comunicazione tra il Centro ATA e il gateway ATA. Se non viene impostato, l'installazione genererà un certificato autofirmato.|
|ConsoleAccountName|ConsoleAccountName="<AccountName>"|Sì|Imposta il nome dell'account utente (utente@dominio.com) usato per registrare il gateway ATA con il Centro ATA.|
|ConsoleAccountPassword|ConsoleAccountPassword="<AccountPassword>"|Sì|Imposta la password dell'account utente (utente@dominio.com) usato per registrare il gateway ATA con il Centro ATA.|

**Esempi**:
Per installare il gateway ATA in modalità invisibile all'utente e registrarlo con il Centro ATA usando le credenziali specificate:

    “Microsoft ATA Gateway Setup.exe” /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName=”user@contoso.com” ConsoleAccountPassword=“userpwd”
    

## Aggiornare il gateway ATA

Per aggiornare il gateway ATA in modalità invisibile all'utente, usare il comando seguente:

**Sintassi**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**Opzioni di installazione**:

|Nome|Sintassi|Obbligatoria per l'installazione invisibile all'utente?|Descrizione|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sì|Esegue il programma di installazione senza visualizzare richieste e interfaccia utente.|
|NoRestart|/norestart|No|Elimina tutti i tentativi di riavvio. Per impostazione predefinita, prima del riavvio viene visualizzata la richiesta dell'interfaccia utente.|
|Help|/help|No|Fornisce la guida e riferimenti rapidi. Visualizza l'uso corretto del comando di installazione incluso un elenco di tutte le opzioni e i comportamenti.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sì|Specifica i parametri per l'installazione di .Net Framework. È necessario impostare questa opzione per attivare l'installazione invisibile all'utente di .Net Framework.|


**Esempi**:
Per aggiornare il gateway ATA in modalità invisibile all'utente:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## Disinstallare il gateway ATA in modalità invisibile all'utente

Per eseguire una disinstallazione del gateway ATA in modalità invisibile all'utente, usare il comando seguente:
**Sintassi**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**Opzioni di installazione**:

|Nome|Sintassi|Obbligatoria per la disinstallazione invisibile all'utente?|Descrizione|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sì|Esegue il programma di disinstallazione senza visualizzare richieste e interfaccia utente.|
|Uninstall|/uninstall|Sì|Esegue la disinstallazione invisibile all'utente del gateway ATA dal server.|
|NoRestart|/norestart|No|Elimina tutti i tentativi di riavvio. Per impostazione predefinita, prima del riavvio viene visualizzata la richiesta dell'interfaccia utente.|
|Help|/help|No|Fornisce la guida e riferimenti rapidi. Visualizza l'uso corretto del comando di installazione incluso un elenco di tutte le opzioni e i comportamenti.|

**Esempi**:
Per disinstallare in modalità invisibile all'utente il gateway ATA dal server:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## Vedere anche

- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurare la raccolta degli eventi](configure-event-collection.md)
- [Prerequisiti di ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)

<!--HONumber=May16_HO1-->


