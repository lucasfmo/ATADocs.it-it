---
# required metadata

title: Configurare il mirroring delle porte| Microsoft Advanced Threat Analytics
description: Descrive le opzioni di mirroring delle porte e in che modo configurarle per ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurare il mirroring delle porte
> [!NOTE] Questo articolo si riferisce solo alla distribuzione di gateway ATA al posto di gateway ATA Lightweight. Per stabilire se è necessario usare i gateway ATA, vedere [Choosing the right gateways for your deployment](/advanced-threat-analytics/plan-design/ata-capacity-planning#Choosing-the-right-gateway-type-for-your-deployment) (Scelta dei gateway corretti per la distribuzione)
 
L'origine dati principale usata da ATA è un'analisi approfondita dei pacchetti del traffico di rete da e verso i controller di dominio. Perché ATA possa vedere il traffico di rete, è necessario configurare il mirroring delle porte o usare un TAP di rete.

Se si sceglie di configurare il **mirroring delle porte** è necessario farlo per ciascun controller di dominio da monitorare, come **origine** del traffico di rete. Per la configurazione del mirroring delle porte generalmente è necessario collaborare con il team della rete o della virtualizzazione.
Per altre informazioni vedere la documentazione del fornitore.

I controller di dominio e i gateway ATA possono essere fisici o virtuali. Seguono alcuni metodi comuni per il mirroring e alcune considerazioni. Per altre informazioni, vedere la documentazione dei commutatori o dei server di virtualizzazione. Il produttore del commutatore potrebbe usare una terminologia diversa.

**Switched Port Analyzer (SPAN)** – Copia il traffico di rete da uno o più porte del commutatore a un'altra porta dello stesso commutatore. Sia i gateway ATA sia i controlleri di dominio devono essere collegati allo stesso commutatore fisico.

**Remote Switch Port Analyzer (RSPAN)** – Consente di monitorare il traffico di rete dalle porte di origine distribuite su più commutatori fisici. RSPAN copia il traffico di origine in una speciale VLAN configurata con RSPAN. Questa VLAN deve avere un collegamento trunk agli altri commutatori coinvolti. RSPAN funziona al Livello 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** – È una tecnologia proprietaria Cisco che funziona al Livello 3. ERSPAN consente di monitorare il traffico sui commutatori senza il bisogno di trunk VLAN. ERSPAN usa Generic Routing Encapsulation (GRE) per copiare il traffico di rete monitorato. ATA al momento non può ricevere direttamente il traffico ERSPAN. Perché ATA funzioni con il traffico ERSPAN, è necessario configurare un commutatore o un router che possa disincapsulare il traffico come destinazione di ERSPAN dove il traffico sarà disincapsulato. Il commutatore o il router dovrà quindi essere configurato per inoltrarlo al gateway ATA usando SPAN o RSPAN.

> [!NOTE]
> Se il controller di dominio con mirroring delle porte è connesso mediante un collegamento WAN, assicurarsi che il collegamento WAN possa gestire il carico aggiuntivo del traffico ERSPAN.

## Opzioni di mirroring delle porte supportate

|Gateway ATA|Controller di dominio|Considerazioni|
|---------------|---------------------|------------------|
|Le macchine|Virtuale sullo stesso host|Il commutatore virtuale deve supportare il mirroring delle porte.<br /><br />Lo spostamento di una sola delle macchine virtuali a un altro host potrebbe interrompere il mirroring delle porte.|
|Le macchine|Virtuale su host diversi|Assicurarsi che il commutatore virtuale supporti questo scenario.|
|Le macchine|Fisico|Richiede un adattatore di rete dedicato altrimenti ATA vedrà tutto il traffico in ingresso e in uscita dall'host, compreso il traffico che invia al centro ATA.|
|Fisico|Le macchine|Assicurarsi che il commutatore virtuale supporti questo scenario e la configurazione del mirroring delle porte sui commutatori fisici in base allo scenario:<br /><br />Se l'host virtuale si trova sullo stesso commutatore fisico, sarà necessario configurare SPAN a livello di commutatore.<br /><br />Se l'host virtuale è su un commutatore diverso, sarà necessario configurare RSPAN o ERSPAN&#42;.|
|Fisico|Fisico sullo stesso commutatore|Il commutatore fisico deve supportare SPAN/mirroring delle porte.|
|Fisico|Fisico su un altro commutatore|Richiede che i commutatori fisici supportino RSPAN o ERSPAN&#42;.|
&#42; ERSPAN è supportato solo quando viene effettuato il decapsulamento prima che il traffico sia analizzato da ATA.

> [!NOTE]
> Assicurarsi che i controller di dominio e i gateway ATA siano sincronizzati con meno di 5 minuti l'uno dall'altro.

**Se si lavora con i cluster di virtualizzazione:**

-   Per ogni controller di dominio in esecuzione nel cluster di virtualizzazione in una macchina virtuale con il gateway ATA, configurare l'affinità tra il controller di dominio e il gateway ATA. In questo modo, quando il controller di dominio si sposterà su un altro host nel cluster, il gateway ATA lo seguirà. Questo funziona bene quando sono presenti pochi controller di dominio.
> [!NOTE]
> Se l'ambiente supporta il processo da macchina virtuale a macchina virtuale su host diversi (RSPAN), non è necessario preoccuparsi dell'affinità.
> 
-   Per assicurarsi che i gateway ATA siano correttamente dimensionati per gestire il monitoraggio di tutti i DC da soli, provare questa opzione: installare una macchina virtuale su ciascun host di virtualizzazione e installare un gateway ATA su ciascun host. Configurare ogni gateway ATA in modo che monitori tutti i controller di dominio eseguiti sul cluster. In questo modo saranno monitorati tutti gli host su cui i controller di dominio sono eseguiti.

Dopo aver configurato il mirroring delle porte, convalidare il suo funzionamento prima di installare il gateway ATA.

## Vedere anche
- [Convalidare il mirroring delle porte](validate-port-mirroring.md)
- [Installare ATA](install-ata.md)
- [Consulta il forum di ATA.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


