---
title: Contatori delle prestazioni XTP di SQL Server (OLTP in memoria) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 62f5c67db29c95b9d3e5ff15739b4c7a5286023e
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53379342"
---
# <a name="sql-server-xtp-in-memory-oltp-performance-counters"></a>Contatori delle prestazioni XTP di SQL Server (OLTP in memoria)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce oggetti e contatori utilizzabili da Performance Monitor per il monitoraggio dell'attività OLTP in memoria. Gli oggetti e i contatori sono condivisi tra tutte le istanze di una determinata versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del computer, a partire da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 In passato i nomi degli oggetti e dei contatori iniziavano con *XTP*, come in **XTP Cursors**. Ora, a partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], i nomi adottano il modello seguente:  
  
-   **SQL Server** *\<versione>* **XTP Cursors**  
  
 Il valore per *\<versione>* è qualcosa come 2016.  
  
##  <a name="SQLServerPOs"></a> Oggetti prestazione XTP di SQL Server  
 Nella tabella seguente sono descritti gli oggetti prestazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Oggetto prestazione|Descrizione|  
|------------------------|-----------------|  
|[XTP Cursors di SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-cursors.md)|L'oggetto prestazione SQL Server XTP Cursors contiene contatori correlati ai cursori interni del motore OLTP in memoria. I cursori sono i blocchi predefiniti di basso livello usati dal motore OLTP in memoria per elaborare query [!INCLUDE[tsql](../../includes/tsql-md.md)] . Di conseguenza, in genere non si ha controllo diretto su di essi.|  
|[SQL Server XTP Databases](../../relational-databases/performance-monitor/sql-server-xtp-databases.md)|L'oggetto prestazione SQL Server XTP Databases fornisce contatori specifici del database OLTP in memoria.|  
|[XTP Garbage Collection di SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-garbage-collection.md)|L'oggetto prestazione SQL Server XTP Garbage Collection contiene contatori correlati al Garbage Collector del motore OLTP in memoria.|  
|[XTP IO Governor di SQL Server 2016](../../relational-databases/performance-monitor/sql-server-xtp-io-governor.md)|L'oggetto prestazione XTP IO Governor di SQL Server include i contatori correlati a IO Rate Governor di OLTP in memoria.|
|[XTP Phantom Processor di SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-phantom-processor.md)|L'oggetto prestazione SQL Server XTP Phantom Processor contiene contatori correlati al sottosistema di elaborazione fantasma del motore OLTP in memoria. Con questo componente è possibile rilevare le righe fantasma nelle transazioni in esecuzione a livello di isolamento SERIALIZABLE.|  
|[Archiviazione XTP di SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-storage.md)|L'oggetto prestazione SQL Server XTP Storage include i contatori correlati all'archiviazione OLTP in memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Log transazioni XTP di SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transaction-log.md)|L'oggetto prestazione SQL Server XTP Transaction Log include i contatori correlati alla registrazione delle transazioni OLTP in memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Transazioni XTP di SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transactions.md)|L'oggetto prestazione SQL Server XTP Transactions contiene i contatori correlati alle transazioni del motore OLTP in memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  
