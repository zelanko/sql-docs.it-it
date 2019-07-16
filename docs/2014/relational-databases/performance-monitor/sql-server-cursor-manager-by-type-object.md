---
title: Oggetto Cursor Manager by Type di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35fa15dc6651d8bfd9b6d32cafd00cd47698560b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206975"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>Oggetto Gestione cursori per tipo di SQL Server
  L'oggetto **SQLServer:Gestione cursori per tipo** include contatori per il monitoraggio dei cursori, raggruppati per tipo.  
  
 Nella tabella seguente vengono descritti i contatori dell'oggetto **Gestione cursori per tipo** di SQL Server.  
  
|Contatori di Gestione cursori per tipo|Descrizione|  
|-------------------------------------|-----------------|  
|**Cursori attivi**|Numero di cursori attivi.|  
|**Percentuale riscontri cache**|Rapporto tra riscontri e ricerche nella cache.|  
|**Conteggio cursori nella cache**|Numero di cursori di un determinato tipo disponibili nella cache.|  
|**Conteggio utilizzi cache cursori/sec**|Numero di utilizzi di ogni tipo di cursore nella cache.|  
|**Utilizzo memoria cursori**|Quantità di memoria utilizzata dai cursori in KB.|  
|**Richieste cursori/sec**|Numero di richieste di cursori SQL ricevute dal server.|  
|**Utilizzo tabelle di lavoro cursori**|Numero di tabelle di lavoro utilizzate dai cursori.|  
|**Numero piani cursore attivi**|Numero di piani di cursore.|  
  
 Per ogni contatore nell'oggetto sono disponibili le istanze seguenti:  
  
|Istanza di Gestione cursori|Descrizione|  
|-----------------------------|-----------------|  
|**_Total**|Informazioni relative a tutti i cursori.|  
|**API Cursor**|Solo informazioni relative al cursore API.|  
|**TSQL Global Cursor**|Solo informazioni relative al cursore [!INCLUDE[tsql](../../includes/tsql-md.md)] globale.|  
|**TSQL Local Cursor**|Solo informazioni relative al cursore [!INCLUDE[tsql](../../includes/tsql-md.md)] locale.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
