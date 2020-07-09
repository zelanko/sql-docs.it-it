---
title: Oggetto Cursor Manager by Type di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 68a5d93f420ba40e71ee43cfbcd088bb97c839b6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773165"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>Oggetto Gestione cursori per tipo di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  L'oggetto **SQLServer:Gestione cursori per tipo** include contatori per il monitoraggio dei cursori, raggruppati per tipo.  
  
 Nella tabella seguente vengono descritti i contatori dell'oggetto **Gestione cursori per tipo** di SQL Server.  
  
|Contatori di Gestione cursori per tipo|Descrizione|  
|-------------------------------------|-----------------|  
|**Cursori attivi**|Numero di cursori attivi.|  
|**Percentuale riscontri cache**|Rapporto tra riscontri e ricerche nella cache.|  
|**Base percentuale riscontri cache**|Solo per uso interno.| 
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
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
