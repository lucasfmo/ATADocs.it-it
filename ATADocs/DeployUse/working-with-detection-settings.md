---
# required metadata

title: Uso delle impostazioni di rilevamento di ATA | Microsoft Advanced Threat Analytics
description: Viene descritto come configurare un elenco di subnet e indirizzi IP che presentano circostanze non comuni e che devono essere gestiti in modo diverso rispetto alle altre entità nella rete
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Uso delle impostazioni di rilevamento di ATA
La pagina di configurazione **Detection** consente di impostare un elenco di subnet e indirizzi IP che presentano circostanze non comuni e che devono essere gestiti in modo leggermente diverso rispetto alle altre entità nella rete.

## Configurazione del rilevamento
Nella pagina **Detection** è possibile definire le opzioni seguenti:

-   **Short-term lease subnets**: se l'organizzazione usa subnet in cui gli indirizzi IP sono molto a breve termine, ad esempio subnet di indirizzi IP VPN o subnet Wi-Fi, è importante immettere questi indirizzi IP e subnet in ATA, in modo che ATA sia in grado di archiviare l'associazione tra un computer e un indirizzo IP in questi intervalli per un periodo di tempo più breve rispetto a quello necessario per gli altri indirizzi IP.

-   **Honeytoken account SIDs**: si tratta di un account utente che non dovrebbe avere attività di rete. Questo account verrà configurato come utente ATA di tipo honeytoken. Se un utente prova a usare questo account, ATA creerà un'attività sospetta e considererà questo tentativo come indicazione di attività dannosa. Per configurare l'utente di tipo honeytoken è necessario il SID dell'account utente, non il nome utente.

È possibile escludere gli indirizzi IP dai rilevamenti seguenti. Se si immette un indirizzo IP in uno di questi elenchi, ATA escluderà l'indirizzo IP da questo tipo specifico di attività rilevata.

-   Esclusioni di indirizzi IP di esplorazione DNS

-   Esclusioni di indirizzi IP di tipo pass-the-ticket

## Vedere anche
- [Gestione di attività sospette](working-with-suspicious-activities.md)
- [Modifica della configurazione di ATA](modifying-ata-configuration.md)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


