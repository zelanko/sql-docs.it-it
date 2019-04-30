---
title: Pianificazione della capacità di server di backup - Parallel Data Warehouse | Microsoft Docs
description: Questo foglio di lavoro di pianificazione della capacità aiuta a determinare i requisiti per un server di backup per l'esecuzione di backup del database Parallel Data Warehouse e le operazioni di ripristino. Usarlo per creare il piano per i server di backup di acquisto nuove o provisioning esistenti.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 500bebab375a0d0b94032a1855af3844bc2e6fa7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63295057"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>Il server di backup capacità pianificazione foglio di lavoro - Parallel Data Warehouse
Questo foglio di lavoro di pianificazione della capacità aiuta a determinare i requisiti per un server di backup per l'esecuzione di backup del database di SQL Server PDW e operazioni di ripristino. Usarlo per creare il piano per i server di backup di acquisto nuove o provisioning esistenti.  
  
Questo foglio di lavoro costituisce un'integrazione per le istruzioni riportate in [acquisire e configurare un Server di Backup](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Foglio di lavoro di pianificazione della capacità per i server di Backup  

### <a name="notes"></a>Note  
  
1.  Questo foglio di lavoro si applica ai server che esegue operazioni di backup e ripristino per i database PDW.  
  
2.  L'unico modo per eseguire il backup e ripristino di database PDW è usare i comandi di DATABASE di BACKUP e ripristino di DATABASE SQL. Tuttavia, dopo aver aggiunto i dati di backup il server di backup, è presente come un set di file di Windows. È possibile archiviare i file di backup dal server in un'altra posizione di archiviazione utilizzando Windows basati su file backup ai metodi tradizionali.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Icona degli Appunti](media/clipboard-icon.png "icona degli Appunti") foglio di lavoro di pianificazione della capacità 
  
Stampa questo foglio di lavoro e compilarlo con i propri requisiti.  
  
|Componente|Requisito|Compilare questa colonna con le proprie esigenze|Indicazioni|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Archiviazione|Numero massimo di byte che si prevede di archiviare nel server di backup in qualsiasi periodo di tempo specifico.|![Pencil icon](media/pencil-icon.png "Pencil icon")|Per determinare i requisiti di archiviazione, individuare la quantità di dati si intende archiviare nel server di backup in qualsiasi periodo di tempo specifico.<br /><br />I dati di backup vengono archiviati nel server di backup in un formato compresso. Le frequenze di compressione dati dipendono dalle caratteristiche dei dati.<br /><br />Ad esempio:  Come una stima approssimativa, si consiglia la stima di un rapporto di compressione 7:1 relativo alle dimensioni dei dati non compressi. Ciò presuppone almeno l'80% dei dati vengono archiviati in indici columnstore cluster. Ad esempio, se si dispone di 700 GB di dati non compressi in un database e viene archiviato in indici columnstore cluster, quindi è possibile stimare che il backup del database sarà necessari circa 100 GB.<br /><br />Se si prevede di avere più copie di backup del database nel server di backup, è necessario tenere conto per loro.<br /><br />Ad esempio: Se si prevede di eseguire il backup di 10 database, ciascuno contenente 5 TB di dati non compressi, i database hanno una dimensione combinata di 50 TB. Se si prevede di eseguire il backup ogni giorno questi 10 database per 5 giorni in una riga, la dimensione non compressa totale è 250 TB. Considerando un rapporto di compressione 7:1, sarà necessario 250 / 7 = 35.7 TB di spazio di archiviazione sul server di backup. È consigliabile essere prudenti e recupero sul 30% di capacità aggiuntiva per consentire eventuali variazioni e aumento delle dimensioni.  In questo esempio, sarebbe meglio 46,6 TB.|  
|Rete|Tipo di connessione di rete.|![Pencil icon](media/pencil-icon.png "Pencil icon")|Determinare il tipo di connessione di rete migliori che possa soddisfare i requisiti di velocità di carico.<br /><br />Ad esempio:  InfiniBand o tariffe il caricamento di 10 Gbit Ethernet fornirà ottimale. Ethernet da 1 Gbit limiterà tassi di carico a 360 GB all'ora o meno.|  
|I/O|Byte per ogni ora per le scritture.|![Pencil icon](media/pencil-icon.png "Pencil icon")|Per la scrittura di backup su disco, da 4 TB per ogni ora le velocità di scrittura sono ottimale.<br /><br />Ad esempio:  Per le unità che possono essere scritte a 50 MB/sec, è consigliabile almeno 24 unità, oltre a informazioni per il mirroring o parità.<br /><br />Per la capacità dei / o, tenere in considerazione tutti il / o nel server durante il caricamento in corso. Se il server durante il caricamento ha altro traffico dei / o oltre ai caricamenti di dati, ad esempio la ricezione di file di dati da un server ETL, si aumenterà i requisiti dei / o.|  
|CPU|Numero di socket.|![Pencil icon](media/pencil-icon.png "Pencil icon")|Ricezione e l'archiviazione file di backup non è un'applicazione a elevato utilizzo della CPU.  Come requisito minimo, è consigliabile usare un server a 2 socket recente fabbricazione.|  
|RAM|GB di memoria che consente a Windows per i file nella cache durante il caricamento.|![Pencil icon](media/pencil-icon.png "Pencil icon")|Ricezione e l'archiviazione file di backup richiede la minima di RAM nel server durante il caricamento.<br /><br />Per determinare i requisiti di RAM, fare riferimento per l'installazione di Windows Server e tutti i requisiti dell'applicazione di terze parti 3rd. Se non si dispone di requisiti da altre origini, si consiglia un minimo di 32 GB.|  
  
Quando si è finito di determinare i requisiti di capacità, tornare alla [acquisire e configurare un Server di caricamento](acquire-and-configure-loading-server.md) argomento per pianificare l'acquisto.  
  
## <a name="see-also"></a>Vedere anche  
[Backup e il caricamento dell'hardware](backup-and-loading-hardware.md)  
  
