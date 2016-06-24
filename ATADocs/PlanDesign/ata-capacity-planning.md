---
# required metadata

title: Pianificazione della distribuzione ATA | Microsoft Advanced Threat Analytics
description: Consente di pianificare la distribuzione e decidere il numero di server ATA necessari per supportare la rete
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Pianificazione della capacità di ATA
Questo argomento consente di determinare il numero di server ATA necessari per supportare la rete. Sono incluse informazioni relative al numero di gateway ATA e ATA Lightweight necessari e alla capacità del server per il Centro ATA e i gateway ATA.

## Dimensionamento del Centro ATA
Il Centro ATA richiede un minimo consigliato di 30 giorni di dati per l'analisi del comportamento dell'utente. Lo spazio su disco richiesto per il database ATA su ogni controller di dominio viene definito di seguito. Se si dispone di più controller di dominio, sommare lo spazio su disco richiesto per ogni controller di dominio per calcolare la quantità totale di spazio necessaria per il database ATA.

|Pacchetti al secondo&#42;|CPU (Core&#42;&#42;)|Memoria (GB)|Archiviazione giornaliera del database (GB)|Archiviazione mensile del database (GB)|IOPS&#42;&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1,000|2|32|0,3|9|30 (100)
|10,000|4|48|3|90|200 (300)
|40,000|8|64|12|360|500 (1,000)
|100,000|12|96|30|900|1,000 (1,500)
|400.000|40|128|120|1,800|2,000 (2,500)
& #42; Numero medio giornaliero totale di pacchetti al secondo da tutti i controller di dominio monitorati da tutti i gateway ATA.

& #42; & #42; Include core fisici e core senza hyperthreading.

& #42; & #42; & #42; Numeri medi (numeri massimi)
> [!NOTE]
> -   Il Centro ATA può gestire un massimo aggregato di 400.000 fotogrammi al secondo (FPS) da tutti i controller di dominio monitorati.
> -   Le quantità di spazio di archiviazione qui indicate sono valori netti. È sempre necessario considerare la crescita futura e verificare che il disco su cui si trova il database disponga almeno del 20% di spazio libero.
> -   Se lo spazio libero raggiunge almeno il 20% o 100 GB, la raccolta di dati meno recente verrà eliminata. Questa operazione continuerà a verificarsi finché rimarranno solo due giorni di dati, il 5% o 50 GB di spazio libero. A quel punto, la raccolta dei dati terminerà.
> -  La latenza di archiviazione per le attività di lettura e scrittura deve essere inferiore a 10 ms.
> -  Il rapporto tra le attività di lettura e scrittura è di circa 1:3 per un numero di pacchetti al secondo inferiore a 100.000 e di 1:6 per un numero di pacchetti al secondo superiore a 100.000.

## Scelta del tipo di gateway corretto per la distribuzione
È consigliabile usare, quando possibile, un gateway ATA Lightweight anziché un gateway ATA, a condizione che i controller di dominio siano conformi alla tabella di dimensionamento seguente.
La maggior parte dei controller di dominio può e dovrebbe essere gestita mediante i gateway ATA Lightweight. L'unica eccezione è rappresentata dalla mancata conformità dei controller ai requisiti della [tabella di dimensionamento dei gateway ATA Lightweight](#ata-lightweight-gateway-sizing).
Di seguito sono riportati esempi di scenari in cui tutti i controller di domino dovrebbero essere gestiti mediante gateway ATA Lightweight:

-   Siti di succursale
-   Controller di dominio virtuali di qualsiasi fornitore IaaS


## Dimensionamento dei gateway ATA Lightweight
È consigliabile usare, quando possibile, un gateway ATA Lightweight anziché un gateway ATA, a condizione che i controller di dominio siano conformi alla tabella di dimensionamento riportata di seguito.

Un gateway ATA Lightweight può supportare il monitoraggio di un controller di dominio in base alla quantità di traffico di rete generata dal controller di dominio stesso. 

|Pacchetti al secondo&#42;|CPU (Core&#42;&#42;)|Memoria (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1,000|2|6|
|5000|6|16|
    |10,000|10|24|

&#42;Numero totale di pacchetti al secondo sul controller di dominio monitorato dallo specifico gateway ATA Lightweight.

&#42;&#42;Quantità totale di core senza tecnologia hyperthreading installati dal controller di dominio.<br>Anche se la tecnologia hyperthreading è accettabile per il gateway ATA Lightweight, quando si pianifica la capacità è necessario contare i core effettivi e non quelli con tale tecnologia.

&#42;&#42;&#42;Quantità totale di memoria installata dal controller di dominio.
> [!NOTE]   Se il controller di dominio non dispone della quantità di risorse richiesta dal gateway ATA Lightweigh, le sue prestazioni non verranno compromesse ma è possibile che il gateway ATA Lightweight non funzioni nel modo previsto.


## Dimensionamento del gateway ATA

Prima di decidere quanti gateway ATA distribuire, considerare gli elementi seguenti.

La maggior parte dei domini può essere gestita da un gateway ATA Lightweight, che dovrebbe essere pianificato in base alla tabella di dimensionamento dei gateway ATA Lightweight sopra riportata.

Se sono ancora necessari gateway ATA, di seguito sono riportate informazioni sul numero di gateway ATA da distribuire:<br>

-   **Foreste e domini Active Directory**<br>
    ATA è in grado di monitorare il traffico proveniente da più domini e da una singola foresta Active Directory. Il monitoraggio di più foreste Active Directory richiede distribuzioni ATA separate. Evitare di configurare una singola distribuzione ATA per monitorare il traffico di rete dei controller di dominio da foreste diverse.

-   **Mirroring delle porte**<br>
Per quanto riguarda il mirroring delle porte, può essere necessario distribuire più gateway ATA per data center o sito di succursale.

-   **Capacità**<br>
    Un gateway ATA può supportare il monitoraggio di più controller di dominio, a seconda della quantità di traffico di rete dei controller di dominio monitorati. 
<br>

|Pacchetti al secondo&#42;|CPU (Core&#42;&#42;)|Memoria (GB)|
|---------------------------|-------------------------|---------------|
|1,000|1|6|
|5000|2|10|
|10,000|3|12|
|20,000|6|24|
|50.000|16|48|
& #42; Numero totale medio di pacchetti al secondo da tutti i controller di dominio monitorati dal gateway ATA specifico durante le ore del giorno con i massimi livelli di attività.

& #42; La quantità totale di traffico con mirroring delle porte dei controller di dominio non può superare la capacità di acquisizione NIC del gateway ATA.

& #42; & #42; L'hyperthreading deve essere disabilitato.



## Stima del traffico dei controller di dominio
Sono disponibili vari strumenti per individuare la media dei pacchetti al secondo dei controller di dominio. Se non si dispone di tutti gli strumenti per monitorare questo contatore, è possibile usare Performance Monitor per raccogliere le informazioni necessarie.

Per determinare il numero di pacchetti al secondo, eseguire questa procedura su ogni controller di dominio:

1.  Aprire Performance Monitor.

    ![Immagine di Performance Monitor](media/ATA-traffic-estimation-1.png)

2.  Espandere **Insiemi agenti di raccolta dati**.

    ![Immagine di Insiemi agenti di raccolta dati](media/ATA-traffic-estimation-2.png)

3.  Fare clic con il pulsante destro del mouse su **Definito dall'utente** e selezionare **Nuovo** &gt; **Insieme agenti di raccolta dati**.

    ![Immagine di Nuovo insieme agenti di raccolta dati](media/ATA-traffic-estimation-3.png)

4.  Immettere un nome per l'insieme agenti di raccolta e selezionare **Crea manualmente (per utenti esperti)**.

5.  In **Tipi di dati** selezionare **Crea registri dati e Contatore delle prestazioni**.

    ![Immagine di Tipi di dati del nuovo insieme agenti di raccolta dati](media/ATA-traffic-estimation-5.png)

6.  In **Registrazione contatori delle prestazioni** fare clic su **Aggiungi**.

7.  Espandere **Scheda di rete**, selezionare **Pacchetti/sec** e scegliere l'istanza appropriata. Se non si è certi, è possibile selezionare **&lt;Tutte le istanze&gt;** e quindi fare clic su **Aggiungi** e **OK**.

    > [!NOTE] A tale scopo, in una riga di comando eseguire `ipconfig /all` per visualizzare il nome della scheda e della configurazione.

    ![Immagine dell'aggiunta di contatori delle prestazioni](media/ATA-traffic-estimation-7.png)

8.  Impostare **Intervallo di campionamento** su **1 secondo**.

9. Impostare il percorso in cui si desidera salvare i dati.

10. In **Creazione insieme agenti di raccolta dati** selezionare **Avvia l'insieme agenti di raccolta dati** e fare clic su **Fine**.

    A questo punto sull'insieme agenti di raccolta dati appena creato si noterà un triangolo verde che indica che è in funzione.

11. Dopo 24 ore, arrestare l'insieme agenti di raccolta dati facendo clic con il pulsante destro del mouse su quest'ultimo e selezionando **Arresta**.

    ![Immagine dell'arresto dell'insieme agenti di raccolta dati](media/ATA-traffic-estimation-12.png)

12. In Esplora File, cercare la cartella in cui è stato salvato il file con estensione blg e fare doppio clic su esso per aprirlo in Performance Monitor.

13. Selezionare il contatore Pacchetti/sec e registrare i valori medi e massimi.

    ![Immagine del contatore di pacchetti al secondo](media/ATA-traffic-estimation-14.png)

## Vedere anche
- [Prerequisiti di ATA](ata-prerequisites.md)
- [Architettura di ATA](ata-architecture.md)
- [Consultare il forum di ATA](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


