---
title: Oggetto Columnstore di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 334a8388b7abc217123071fdc37c9e1091f6a3fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987139"
---
# <a name="sql-server-columnstore-object"></a>SQL Server, oggetto Columnstore
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'oggetto **SQLServer:Columnstore** fornisce i contatori per monitorare l'esecuzione dell'indice columnstore in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Nella tabella seguente sono descritti i contatori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Columnstore** counters.  
  
|Contatori Columnstore|Descrizione|  
|--------------------------|-----------------|  
|**Rowgroup differenziali chiusi**|Numero di rowgroup differenziali chiusi.|  
|**Rowgroup differenziali compressi**|Numero di rowgroup differenziali compressi.|  
|**Rowgroup differenziali creati**|Numero di rowgroup differenziali creati.|  
|**Percentuale riscontri nella cache di segmenti**|Percentuale di segmenti di colonna trovati nel pool columnstore senza dover eseguire una lettura dal disco.|  
|**Base riscontri nella cache di segmenti**|Solo per uso interno.|
|**Letture segmenti/sec**|Numero di letture fisiche di segmenti eseguite.|  
|**Totale buffer di eliminazione migrati**|Numero di operazioni di pulizia del buffer di eliminazione eseguite dal motore di tuple.|  
|**Totale valutazioni dei criteri di unione**|Numero di valutazioni eseguite per i criteri di unione per columnstore.|  
|**Totale rowgroup compressi**|Numero totale di rowgroup compressi.|  
|**Rowgroup totali adatti per l'operazione di unione**|Numero di rowgroup di origine adatti per l'operazione MERGE dall'avvio di SQL Server.|  
|**Totale rowgroup compressi tramite l'operazione MERGE**|Numero di rowgroup di destinazione compressi creati con l'operazione MERGE dall'avvio di SQL Server.|  
|**Totale rowgroup di origine uniti**|Numero di rowgroup di origine uniti dall'avvio di SQL Server.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
