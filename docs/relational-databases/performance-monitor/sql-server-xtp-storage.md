---
title: XTP Storage di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2b0f5e749190fbc144306053025beac6911d928b
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158570"
---
# <a name="sql-server-xtp-storage"></a>Archiviazione XTP di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'oggetto prestazione dell'archiviazione XTP di SQL Server include i contatori correlati all'archiviazione su disco per OLTP in memoria in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Nella tabella seguente sono descritti i contatori dell' **archiviazione XTP di SQL Server** .  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|**Checkpoint chiusi**|Conteggio di checkpoint chiusi eseguiti dall'agente online.|  
|**Checkpoint completati**|Conteggio di checkpoint elaborati dal thread offline dei checkpoint.|  
|**Operazioni di unioni principali completate**|Numero di operazioni di unioni principali completate dal thread di lavoro di tipo merge. Queste operazioni devono ancora essere installate.|  
|**Valutazioni dei criteri di unione**|Numero di valutazioni dei criteri di unione dall'avvio del server.|  
|**Richieste di tipo merge in sospeso**|Numero di richieste di tipo merge in sospeso dall'avvio del server.|  
|**Operazioni di unione abbandonate**|Numero di operazioni di unione abbandonate a causa di un errore.|  
|**Operazioni di unione installate**|Numero di operazioni di unione installate correttamente.|  
|**File totali uniti**|Numero totale di file di origine uniti. Questo numero può essere utilizzato per trovare il numero medio di file di origine nell'unione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Contatori delle prestazioni XTP &#40;OLTP in memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
