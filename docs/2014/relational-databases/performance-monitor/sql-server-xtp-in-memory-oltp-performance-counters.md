---
title: Contatori delle prestazioni XTP (OLTP in memoria) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4363a526ada3694e92d18cac0d7abe8a26f6a92f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016937"
---
# <a name="xtp-in-memory-oltp-performance-counters"></a>Contatori delle prestazioni XTP (OLTP in memoria)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce oggetti e contatori utilizzabili da Performance Monitor per il monitoraggio dell'attività OLTP in memoria.  
  
##  <a name="xtp-in-memory-oltp-performance-objects"></a><a name="SQLServerPOs"></a>Oggetti prestazioni XTP (OLTP in memoria)  
 Nella seguente tabella vengono descritti gli oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Oggetto prestazione|Descrizione|  
|------------------------|-----------------|  
|[XTP Cursors](../cursors.md)|L'oggetto prestazione XTP Cursors contiene contatori correlati ai cursori interni del motore XTP. I cursori sono i blocchi predefiniti di basso livello utilizzati dal motore XTP per elaborare query [!INCLUDE[tsql](../../includes/tsql-md.md)]. Di conseguenza, in genere non si ha controllo diretto su di essi.|  
|[XTP Garbage Collection](sql-server-xtp-garbage-collection.md)|L'oggetto prestazione XTP Garbage Collection contiene contatori correlati al Garbage Collector del motore XTP.|  
|[XTP Phantom Processor](sql-server-xtp-phantom-processor.md)|L'oggetto prestazione XTP Phantom Processor contiene contatori correlati al sottosistema di elaborazione fantasma del motore XTP. Con questo componente è possibile rilevare le righe fantasma nelle transazioni in esecuzione a livello di isolamento SERIALIZABLE.|  
|[Archiviazione XTP](sql-server-xtp-storage.md)|Nell'oggetto prestazione dell'archiviazione XTP sono inclusi i contatori correlati all'archiviazione XTP di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[XTP Transaction Log](sql-server-xtp-transaction-log.md)|L'oggetto prestazione XTP Transaction Log contiene contatori correlati alla registrazione delle transazioni XTP in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[XTP Transactions](sql-server-xtp-transactions.md)|L'oggetto prestazione XTP Transactions contiene contatori correlati alle transazioni del motore XTP in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  
