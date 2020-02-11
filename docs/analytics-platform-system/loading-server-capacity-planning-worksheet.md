---
title: Caricamento della pianificazione della capacità del server
description: Questo foglio di progettazione per la pianificazione della capacità consente di determinare i requisiti per un server di caricamento per il caricamento dei dati nella piattaforma di analisi parallela del sistema data warehouse ".
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 7dded8c79495d0bdc684927f4875a93c3160c1bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401037"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>Caricamento del foglio di progettazione per la pianificazione della capacità del server per la piattaforma Analytics
Questo foglio di progettazione per la pianificazione della capacità consente di determinare i requisiti per un server di caricamento per il caricamento dei dati in SQL Server PDW. Usare questo per creare il piano per l'acquisto o il provisioning di server di caricamento esistenti.  
  
## <a name="worksheet-notes"></a>Note sul foglio di foglio
  
1.  Questo foglio di controllo si applica ai server in cui verranno caricati i dati con lo strumento di caricamento da riga di comando **dwloader** .  
  
2.  Per il caricamento di dati con Integration Services o uno strumento di caricamento di terze parti, i requisiti possono variare a seconda delle differenze nel processo di caricamento.  
  
3.  La maggior parte dei requisiti si applica al caricamento di file di dati compressi o non compressi; le differenze nei requisiti sono indicate in grassetto.  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![Appunti](media/clipboard-icon.png "Appunti") Foglio di progettazione della pianificazione della capacità  
  
Stampare questo foglio di lavoro e compilarlo con i propri requisiti.  
  
|Componente|Requisito|Compilare questo articolo con i propri requisiti|Consigli|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Archiviazione|Numero massimo di byte che si prevede di archiviare nel server di caricamento in un determinato periodo di tempo.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|Per determinare i requisiti di archiviazione, determinare la quantità di dati che si prevede di archiviare nel server di caricamento in un determinato periodo di tempo.  I requisiti di capacità sono solo per i file di caricamento. il sistema operativo e i file di caricamento devono trovarsi su matrici di dischi diversi.<br /><br />Ad esempio: se si prevede di caricare 100 GB di dati dal disco 3 volte al giorno, ma non di eliminare i file di dati fino alla fine della settimana, è necessario un minimo di 2,1 TB per archiviare i file di dati. Si consiglia di essere prudenti e ottenere circa il 30% di spazio di archiviazione per tenere conto delle variazioni e della crescita.  Per questo esempio, è preferibile 2,73 TB di spazio di archiviazione.|  
|Velocità di caricamento|Numero massimo di byte per ora di dati da caricare in PDW.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|Si tratta di una stima. Quando si calcola questo requisito, si supponga che i file si trovino già nel server di caricamento e che le altre condizioni di caricamento siano le più valide possibile.<br /><br />Ad esempio: non è necessario fattorizzare la compressibilità dei dati perché dwloader Invia sempre dati non compressi al PDW. Non è necessario fattorizzare le conversioni dei tipi di dati e le dimensioni della tabella di destinazione.|  
|Rete|Tipo di connessione di rete.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|Determinare il tipo di connessione di rete migliore per i requisiti della velocità di caricamento.<br /><br />Ad esempio, InfiniBand o 10 Gbit Ethernet forniranno le tariffe di caricamento ottimali. 1 Ethernet Gbit limiterà le tariffe di carico a 360 GB all'ora o meno.|  
|I/O|Byte all'ora per letture e scritture.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|Per caricare i dati, dwloader deve leggere tutti i dati dal disco prima di inviarli a PDW.<br /><br />Ogni server di caricamento non è in grado di caricare i dati più velocemente che l'appliance possa ricevere dati da tutte le origini di caricamento. Per risparmiare denaro, pianificare la capacità di lettura I/O per il caricamento in modo che non superi la capacità di carico dell'appliance.<br /><br />Ad esempio:<br />PDW riceve e carica i dati in un'appliance da 1 rack a una velocità massima di 1,8 TB all'ora. Per un appliance con 2 o più rack, la velocità massima di caricamento è 3,6 TB all'ora.<br /><br />Se si prevede di caricare contemporaneamente da più server di caricamento, i requisiti di I/O per ogni server di caricamento saranno minori rispetto al momento in cui un server esegue tutto il caricamento.<br /><br />Ad esempio: un server di caricamento può caricare un massimo di 1,8 TB all'ora per un dispositivo a 1 rack. Due server di caricamento possono caricare simultaneamente 900 GB all'ora in un'appliance a 1 rack. Livelli più elevati di concorrenza possono ridurre l'efficienza e la velocità effettiva massima.<br /><br />Per la capacità di I/O, prendere in considerazione tutte le operazioni di I/O eseguite sul server di caricamento. Se il server di caricamento dispone di altro traffico di I/O oltre ai caricamenti dei dati, ad esempio la ricezione di file di dati da un server ETL, i requisiti di I/O aumenteranno.<br /><br />Per i dati compressi, i requisiti di I/O dipendono dal tasso di compressione dei dati. dwloader legge i dati compressi e quindi li decomprime prima di inviarli a PDW. Maggiore è il rapporto di compressione, minore sarà il numero di dati che il server di caricamento deve leggere dal disco.<br /><br />Ad esempio, se la frequenza di caricamento richiesta è 1,8 TB all'ora e i dati vengono archiviati nel server di caricamento con compressione 2:1, il server di caricamento deve leggere solo 900 GB all'ora dal disco anziché 1,8 TB. Un rapporto di compressione 3:1 indica che il server di caricamento deve leggere 600 GB all'ora dal disco.|  
|CPU|Numero di socket.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|Per il caricamento di dati non compressi, dwloader non è un'applicazione con utilizzo intensivo della CPU.  Come requisito minimo, si consiglia di usare un server a 2 socket prodotto di recente.<br /><br />Per caricare i dati compressi, è necessaria una quantità di memoria sufficiente per decomprimere i dati prima di inviarli a PDW. dwloader può eseguire 10 thread attivi contemporaneamente. Se si prevede di caricare 10 file compressi simultaneamente, è consigliabile che il server disponga di almeno una CPU a 10 core o di due CPU a 6 core.|  
|RAM|GB di memoria che consente a Windows di memorizzare nella cache i file durante i caricamenti.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|dwloader usa molto poca RAM nel server di caricamento. Per le prestazioni, Windows utilizza memoria per memorizzare nella cache i file di caricamento dopo la lettura dal disco.<br /><br />Per determinare i requisiti di RAM, vedere l'installazione di Windows Server e i requisiti dell'applicazione di terze parti. Se non si hanno requisiti da altre origini, è consigliabile un minimo di 32 GB.<br /><br />Per i dati compressi, la RAM più veloce è utile perché accelera la decompressione.|  
  
## <a name="see-also"></a>Vedere anche  
[Acquisire e configurare un server di caricamento](acquire-and-configure-loading-server.md)  
[Caricatore da riga di comando dwloader](dwloader.md)  
  
