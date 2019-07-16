---
title: Il caricamento delle capacità del server pianificazione - sistema di piattaforma Analitica | Microsoft Docs
description: Questo foglio di lavoro di pianificazione della capacità aiuta a determinare i requisiti per un server di caricamento per il caricamento dei dati di Analitica piattaforma Parallel Data Warehouse di System."
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0bb15fdd3b20c538237b3e012df4217ad5568bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960661"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>Durante il caricamento di foglio di lavoro di pianificazione della capacità server per il sistema di piattaforma Analitica
Questo foglio di lavoro di pianificazione della capacità aiuta a determinare i requisiti per un server di caricamento per il caricamento dei dati in SQL Server PDW. Usarlo per creare il piano di acquisto o il provisioning esistente caricamento server.  
  
## <a name="worksheet-notes"></a>Note di foglio di lavoro
  
1.  Questo foglio di lavoro si applica ai server che sarà possibile il caricamento dei dati con il **dwloader** dello strumento di caricamento della riga di comando.  
  
2.  Per il caricamento dei dati con Integration Services o un terzo strumento durante il caricamento di entità, i requisiti possono variare a seconda le differenze nel processo di caricamento.  
  
3.  La maggior parte dei requisiti si applicano al caricamento di entrambi i file di dati compresso o; eventuali differenze nei requisiti sono indicate in grassetto.  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![Negli Appunti](media/clipboard-icon.png "negli Appunti") foglio di lavoro di pianificazione della capacità  
  
Stampa questo foglio di lavoro e compilarlo con i propri requisiti.  
  
|Componente|Requisito|Compilare questa colonna con le proprie esigenze|Consigli|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Archiviazione|Numero massimo di byte che si prevede di archiviare nel server durante il caricamento in qualsiasi periodo di tempo specifico.|![Icona della matita](media/pencil-icon.png "sull'icona a forma di matita")|Per determinare i requisiti di archiviazione, individuare la quantità di dati si intende archiviare nel server durante il caricamento in qualsiasi periodo di tempo specifico.  I requisiti di capacità sono per caricare file di sola lettura. il sistema operativo e i file di carico devono essere in array di dischi diversi.<br /><br />Ad esempio:  Se si prevede di caricare 100 GB di dati dal disco 3 volte ogni giorno, ma non elimina i dati di file fino alla fine della settimana, sarà necessario un minimo TB 2.1 per archiviare i file di dati. È consigliabile essere prudenti e recupero sull'archiviazione superiori del 30% per tenere conto delle varianze e aumento delle dimensioni.  Per questo esempio, sarebbe meglio 2,73 TB di spazio di archiviazione.|  
|Frequenza di caricamento|Numero massimo di byte per ogni ora di dati da caricare in PDW.|![Icona della matita](media/pencil-icon.png "sull'icona a forma di matita")|Si tratta di una stima. Quando si calcola questo requisito, presuppongono che i file sono già nel server durante il caricamento, ma che altre condizioni di carico sono maniera migliore.<br /><br />Ad esempio:  Non è necessario tenere in considerazione la natura dei dati poiché dwloader invia sempre senza compressione dei dati per il PDW. Non è necessario tenere in considerazione le conversioni di tipo di dati e le dimensioni della tabella di destinazione.|  
|Rete|Tipo di connessione di rete.|![Icona della matita](media/pencil-icon.png "sull'icona a forma di matita")|Determinare il tipo di connessione di rete ottimo per le proprie esigenze di velocità di carico.<br /><br />Ad esempio: InfiniBand o 10 Gbit Ethernet fornirà le frequenze di caricamento ottimali. 1 Gbit Ethernet limiterà tassi di carico a 360 GB all'ora o meno.|  
|I/O|Byte per ogni ora per letture e scritture.|![Icona della matita](media/pencil-icon.png "sull'icona a forma di matita")|Per caricare i dati, dwloader devono leggere tutti i dati dal disco prima di inviarlo a PDW.<br /><br />Ogni server durante il caricamento non è possibile caricare i dati più velocemente di quanto il dispositivo può ricevere dati da tutte le origini di caricamento. Per risparmiare denaro, pianificare il / o leggere la capacità per il caricamento in modo che non superi la capacità di carico dell'appliance.<br /><br />Ad esempio:<br />PDW riceve e carica i dati in un'appliance 1 rack con una frequenza massima di 1,8 TB per ogni ora. Per un'appliance con 2 o più rack, la velocità di carico massimo è 3,6 TB per ogni ora.<br /><br />Se si prevede di caricare da più server di caricamento nello stesso momento, i requisiti dei / o per ogni server durante il caricamento sarà minore quando un server esegue tutti il caricamento.<br /><br />Ad esempio:  Un server di caricamento può caricare un massimo di 1,8 TB per ogni ora per un'appliance 1 rack. Due server il caricamento è stato possibile ognuno caricare simultaneamente 900 GB all'ora in un'appliance 1 rack. Livelli più elevati di concorrenza possono ridurre l'efficienza e la velocità effettiva massima.<br /><br />Per la capacità dei / o, tenere in considerazione tutti il / o nel server durante il caricamento in corso. Se il server durante il caricamento ha altro traffico dei / o oltre ai caricamenti di dati, ad esempio la ricezione di file di dati da un server ETL, si aumenterà i requisiti dei / o.<br /><br />Per i dati compressi, i requisiti dei / o dipendono dal tasso di compressione dati. dwloader legge i dati compressi e quindi lo decomprime prima di inviarlo a PDW. Maggiore il rapporto di compressione, i dati meno il server durante il caricamento sarà necessario leggere dal disco.<br /><br />Ad esempio: Se la velocità di carico appropriato è 1,8 TB per ogni ora e i dati vengono archiviati nel server durante il caricamento con la compressione di 2:1, quindi il server di caricamento deve solo leggere 900 GB all'ora dal disco anziché 1,8 TB. Un rapporto di compressione 3:1 significa che il server di caricamento deve leggere almeno 600 GB all'ora dal disco.|  
|CPU|Numero di socket.|![Icona della matita](media/pencil-icon.png "sull'icona a forma di matita")|Per il caricamento dei dati non compressi, dwloader non è un'applicazione a elevato utilizzo della CPU.  Come requisito minimo, è consigliabile usare un server a 2 socket recente fabbricazione.<br /><br />Per il caricamento dei dati compressi, è necessario sufficiente potenza della CPU per decomprimere i dati prima di inviarlo a PDW. dwloader eseguibili 10 thread attivi in una sola volta. Se si prevede di caricare simultaneamente i 10 file compressi, è consigliabile che il server disponga di almeno 10 core CPU o due 6 core CPU.|  
|RAM|GB di memoria che consente a Windows per i file nella cache durante il caricamento.|![Icona della matita](media/pencil-icon.png "sull'icona a forma di matita")|dwloader Usa minima di RAM nel server durante il caricamento. Per prestazioni ottimali, Windows Usa la memoria per memorizzare nella cache il caricamento dei file dopo la lettura dal disco.<br /><br />Per determinare i requisiti di RAM, fare riferimento per l'installazione di Windows Server e tutti i requisiti dell'applicazione di terze parti 3rd. Se non si dispone di requisiti da altre origini, si consiglia un minimo di 32 GB.<br /><br />Per i dati compressi, RAM più veloce è utile perché che consente di velocizzare la decompressione.|  
  
## <a name="see-also"></a>Vedere anche  
[Acquisire e configurare un server di caricamento](acquire-and-configure-loading-server.md)  
[Caricatore della riga di comando dwloader](dwloader.md)  
  
