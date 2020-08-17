---
description: sys.dm_xe_database_session_events (database SQL di Azure)
title: sys.dm_xe_database_session_events
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 9e985a19-f93f-4c56-b644-12c529298011
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-lt-2019
ms.openlocfilehash: 06de1e7657008f924e80427b3e9bfa04eae225a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88323057"
---
# <a name="sysdm_xe_database_session_events-azure-sql-database"></a>sys.dm_xe_database_session_events (database SQL di Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Restituisce informazioni sugli eventi di sessione. Gli eventi sono punti di esecuzione discreti. I predicati possono essere applicati agli eventi per arrestarne la generazione se l'evento non contiene le informazioni necessarie.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a tutte le versioni successive.|  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|Indirizzo di memoria della sessione dell'evento. Non ammette i valori Null.|  
|event_name|**nvarchar(60)**|Nome dell'evento associato all'azione. Non ammette i valori Null.|  
|event_package_guid|**uniqueidentifier**|GUID per il pacchetto che contiene l'evento. Non ammette i valori Null.|  
|event_predicate|**nvarchar(2048)**|Rappresentazione XML dell'albero predicativo applicato all'evento. Ammette i valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|A|Relazione|  
|----------|--------|------------------|  
|sys. dm_xe_database_session_events. event_session_address|sys. dm_xe_database_sessions. Address|Molti-a-uno|  
|sys. dm_xe_database_session_events. event_package_guid, sys. dm_xe_database_session_events. event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|Molti-a-uno|  
  
  
