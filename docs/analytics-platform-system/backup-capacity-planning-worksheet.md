---
title: Pianificazione della capacità del server di backup
description: Questo foglio di elaborazione per la pianificazione della capacità consente di determinare i requisiti per un server di backup per l'esecuzione di operazioni parallele di backup e ripristino del database data warehouse. Questa operazione consente di creare un piano per l'acquisto di nuovi server di backup o di provisioning.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 46dbdded5adf41a847f017cf4ee203597df13962
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401339"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>Foglio di data warehouse della pianificazione della capacità del server di backup-parallelo
Questo foglio di elaborazione per la pianificazione della capacità consente di determinare i requisiti per un server di backup per l'esecuzione di SQL Server PDW operazioni di backup e ripristino del database. Questa operazione consente di creare un piano per l'acquisto di nuovi server di backup o di provisioning.  
  
Questo foglio di esecuzione è un supplemento alle istruzioni in [acquisire e configurare un server di backup](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Foglio di progettazione della pianificazione della capacità per i server di backup  

### <a name="notes"></a>Note  
  
1.  Questo foglio di lavori si applica ai server che eseguiranno operazioni di backup e ripristino per i database PDW.  
  
2.  L'unico modo per eseguire il backup e il ripristino dei database PDW consiste nell'usare i comandi BACKUP DATABASE e RESTOre DATABASE SQL. Tuttavia, una volta che i dati di backup si trovino nel server di backup, esiste come un set di file di Windows. È possibile archiviare i file di backup dal server in un altro percorso di archiviazione usando i tradizionali metodi di backup basati su file di Windows.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Icona degli Appunti](media/clipboard-icon.png "Icona degli Appunti") Foglio di progettazione della pianificazione della capacità 
  
Stampare questo foglio di lavoro e compilarlo con i propri requisiti.  
  
|Componente|Requisito|Compilare questo articolo con i propri requisiti|Raccomandazioni|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Archiviazione|Numero massimo di byte che si prevede di archiviare nel server di backup in un determinato periodo di tempo.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|Per determinare i requisiti di archiviazione, determinare la quantità di dati che si prevede di archiviare nel server di backup in un determinato periodo di tempo.<br /><br />I dati di backup vengono archiviati nel server di backup in formato compresso. I tassi di compressione dei dati dipendono dalle caratteristiche dei dati.<br /><br />Ad esempio, come stima approssimativa, è consigliabile stimare un rapporto di compressione 7:1 rispetto alla dimensione dei dati non compressi. Si presuppone che almeno il 80% dei dati sia archiviato negli indici columnstore cluster. Se, ad esempio, si dispone di 700 GB di dati non compressi in un database ed è archiviato in indici columnstore cluster, è possibile stimare che il backup del database necessiti di circa 100 GB.<br /><br />Se si prevede di avere più copie dei backup del database nel server di backup, è necessario tenerne conto.<br /><br />Ad esempio, se si prevede di eseguire il backup di 10 database contenenti ogni 5 TB di dati non compressi, i database avranno dimensioni combinate di 50 TB. Se si prevede di eseguire il backup di questi 10 database ogni giorno per 5 giorni in una riga, le dimensioni totali non compresse sono 250 TB. Factoring in un rapporto di compressione 7:1, sarà necessario 250/7 = 35,7 TB di spazio di archiviazione nel server di backup. È consigliabile essere prudenti e ottenere circa il 30% di capacità aggiuntiva per tenere conto delle variazioni e aumentare.  In questo esempio, 46,6 TB sarebbe migliore.|  
|Rete|Tipo di connessione di rete.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|Determinare il tipo di connessione di rete migliore che può soddisfare i requisiti della velocità di caricamento.<br /><br />Ad esempio, InfiniBand o 10 Gbit Ethernet fornirà le tariffe di caricamento ottimali. 1Gbit Ethernet limiterà le tariffe di carico a 360 GB all'ora o meno.|  
|I/O|Byte all'ora per le Scritture.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|Per la scrittura di backup su disco, le velocità di scrittura di 4 TB per ora sono ottimali.<br /><br />Ad esempio: per le unità che possono scrivere 50 MB/sec, è necessario disporre di almeno 24 unità, più altre per il mirroring o la parità.<br /><br />Per la capacità di I/O, prendere in considerazione tutte le operazioni di I/O eseguite sul server di caricamento. Se il server di caricamento dispone di altro traffico di I/O oltre ai caricamenti dei dati, ad esempio la ricezione di file di dati da un server ETL, i requisiti di I/O aumenteranno.|  
|CPU|Numero di socket.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|La ricezione e l'archiviazione dei file di backup non è un'applicazione con utilizzo intensivo della CPU.  Come requisito minimo, si consiglia di usare un server a 2 socket prodotto di recente.|  
|RAM|GB di memoria che consente a Windows di memorizzare nella cache i file durante i caricamenti.|![Icona a forma di matita](media/pencil-icon.png "Icona a forma di matita")|Per la ricezione e l'archiviazione dei file di backup è necessaria una quantità di RAM minima sul server di caricamento.<br /><br />Per determinare i requisiti di RAM, vedere l'installazione di Windows Server e i requisiti dell'applicazione di terze parti. Se non si hanno requisiti da altre origini, è consigliabile un minimo di 32 GB.|  
  
Al termine della determinazione dei requisiti di capacità, tornare all'argomento [acquisire e configurare un server di caricamento](acquire-and-configure-loading-server.md) per pianificare l'acquisto.  
  
## <a name="see-also"></a>Vedere anche  
[Backup e caricamento dell'hardware](backup-and-loading-hardware.md)  
  
