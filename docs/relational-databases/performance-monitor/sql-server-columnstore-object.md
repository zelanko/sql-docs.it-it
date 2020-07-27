---
title: Oggetto Columnstore di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto SQLServer:Columnstore, che fornisce i contatori per monitorare l'esecuzione dell'indice columnstore in SQL Server.
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
ms.openlocfilehash: f00f4405144cec17b0b0266308ebc6df39336a70
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458416"
---
# <a name="sql-server-columnstore-object"></a>SQL Server, oggetto Columnstore
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  L'oggetto **SQLServer:Columnstore** fornisce i contatori per monitorare l'esecuzione dell'indice columnstore in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Nella tabella seguente vengono descritti i contatori dell'oggetto **Columnstore** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
  
  
