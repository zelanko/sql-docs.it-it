---
title: Oggetto Query Store di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store object
- SQL Server:Query Store
ms.assetid: b4a04acd-0b66-44a5-b72d-1a45b49e13e6
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 08cc5200801b99442c8973583f4ab7caa9ea9fb5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68140733"
---
# <a name="sql-server-query-store-object"></a>SQL Server, oggetto archivio query
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'oggetto archivio query fornisce contatori per monitorare l'utilizzo delle risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per archiviare i testi delle query, i piani di esecuzione e le statistiche di runtime per gli oggetti come stored procedure, istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc e preparate e trigger.  
  
 Questa tabella illustra i contatori **SQLServer:Query Store**.  
  
|Contatori di archivio query di SQL Server|Descrizione|  
|-------------------------------------|-----------------|  
|**Utilizzo della CPU dell'archivio query**|Indica l'utilizzo della CPU dell'archivio query.|  
|**Letture logiche dell'archivio query**|Indica il numero di letture logiche eseguite dall'archivio query.|  
|**Scritture logiche dell'archivio query**|Indica la quantità di dati accodata per essere scaricata dall'archivio query. La frequenza e il ritardo dell'aggiunta di elementi (che rappresentano le statistiche di runtime) alla coda sono controllati dall'impostazione Intervallo di scaricamento dati.|  
|**Letture fisiche dell'archivio query**|Indica il numero di letture fisiche eseguite dall'archivio query.|  
  
 Per ogni contatore nell'oggetto sono disponibili le istanze seguenti:  
  
|Istanza dell'archivio query|Descrizione|  
|--------------------------|-----------------|  
|**_Total**|Informazioni per l'archivio query per questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|\<nome database>|Informazioni dell'archivio query per questo database.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Stored procedure di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
