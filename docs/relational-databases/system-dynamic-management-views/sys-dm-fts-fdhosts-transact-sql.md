---
title: sys. dm_fts_fdhosts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_fdhosts
- dm_fts_fdhosts_TSQL
- sys.dm_fts_fdhosts
- sys.dm_fts_fdhosts_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_fdhosts dynamic management view
- troubleshooting [SQL Server], full-text search
ms.assetid: d42a6334-4362-4361-83da-f8324fe55ec7
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1b954e5d9c122f09d1ed16162f34ce94cdbc4100
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734566"
---
# <a name="sysdm_fts_fdhosts-transact-sql"></a>sys.dm_fts_fdhosts (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce informazioni sull'attività corrente dell'host o degli host del daemon di filtri nell'istanza del server.  
  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**fdhost_id**|**int**|ID dell'host del daemon di filtri.|  
|**fdhost_name**|**nvarchar(120)**|Nome dell'host del daemon di filtri.|  
|**fdhost_process_id**|**int**|ID del processo Windows dell'host del daemon di filtri.|  
|**fdhost_type**|**nvarchar(120)**|Tipo di documento elaborato dall'host del daemon di filtri, ad esempio:<br /><br /> A thread singolo<br /><br /> Multi-thread<br /><br /> Documento di grandi dimensioni|  
|**max_thread**|**int**|Numero massimo di thread nell'host del daemon di filtri.|  
|**batch_count**|**int**|Numero di batch in elaborazione nell'host del daemon di filtri.|  
  
## <a name="permissions"></a>Autorizzazioni  

In è [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] richiesta l' `VIEW SERVER STATE` autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, richiede l' `VIEW DATABASE STATE` autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli standard e Basic, richiede l' **amministratore del server** o un account **amministratore Azure Active Directory** .   

## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il nome dell'host del daemon di filtri e il numero massimo di thread relativi. Viene inoltre monitorato il numero di batch attualmente in esecuzione nel daemon di filtri. Queste informazioni possono essere utilizzate nella diagnosi delle prestazioni.  
  
```  
SELECT fdhost_name, batch_count, max_thread FROM sys.dm_fts_fdhosts;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica per la ricerca full-text e la ricerca semantica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Ricerca full-text](../../relational-databases/search/full-text-search.md)  
  
  
