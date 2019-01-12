---
title: Sys.dm_xe_database_sessions (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 33ea5179-16bb-4abd-96cc-9bc696e80987
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 7602e03864a736c6011142fd56c3e6129efcb718
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143271"
---
# <a name="sysdmxedatabasesessions-azure-sql-database"></a>sys.dm_xe_database_sessions (database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni sugli eventi di sessione. Gli eventi sono punti di esecuzione discreti. I predicati possono essere applicati agli eventi per arrestarne la generazione se l'evento non contiene le informazioni necessarie.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Versione 12 e tutte le versioni successive.|  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|Indirizzo di memoria della sessione dell'evento. Non ammette i valori Null.|  
|event_name|**nvarchar(60)**|Nome dell'evento associato all'azione. Non ammette i valori Null.|  
|event_package_guid|**uniqueidentifier**|GUID per il pacchetto che contiene l'evento. Non ammette i valori Null.|  
|event_predicate|**nvarchar(2048)**|Rappresentazione XML dell'albero predicativo applicato all'evento. Ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
A partire da 2015-07-13, '. dm xe_objects' è una di queste DMV XEvent che non contengono database' nel nome. Non è un errore di digitazione o un errore nella colonna a destra della tabella seguente. Il nome è lo stesso in Microsoft SQL Server e Database SQL di Azure.  
  
|From|Per|Relazione|  
|--------|------|----------------|  
|sys.dm_xe_database_session_events.event_session_address|sys.dm_xe_database_sessions.address|Molti-a-uno|  
|Sys.dm_xe_database_session_events.event_package_guid, sys.dm_xe_database_session_events.event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
[Eventi estesi nel Database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
[Eventi estesi](../../relational-databases/extended-events/extended-events.md)  
  
 
