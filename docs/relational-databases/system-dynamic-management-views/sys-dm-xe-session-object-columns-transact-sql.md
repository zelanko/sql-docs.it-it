---
title: sys.dm_xe_session_object_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_session_object_columns_TSQL
- sys.dm_xe_session_object_columns_TSQL
- dm_xe_session_object_columns
- sys.dm_xe_session_object_columns
dev_langs:
- TSQL
helpviewer_keywords:
- xe
- sys.dm_xe_session_object_columns dynamic management view
ms.assetid: e97f3307-2da6-4c54-b818-a474faec752e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 039c3b0be4feab53215bae22836b7fd5be4ecfb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090228"
---
# <a name="sysdmxesessionobjectcolumns-transact-sql"></a>sys.dm_xe_session_object_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mostra i valori di configurazione per gli oggetti associati a una sessione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|Indirizzo di memoria della sessione dell'evento. Ha una relazione molti-a-uno con sys.dm_xe_sessions.address. Non ammette i valori Null.|  
|column_name|**nvarchar(256)**|Nome del valore di configurazione. Non ammette i valori Null.|  
|column_id|**int**|ID della colonna. Valore univoco all'interno dell'oggetto. Non ammette i valori Null.|  
|column_value|**nvarchar(3072)**|Valore configurato della colonna. Ammette i valori Null.|  
|object_type|**nvarchar(60)**|Tipo dell'oggetto. Non ammette i valori Null. object_type è uno di:<br /><br /> event<br /><br /> target|  
|object_name|**nvarchar(256)**|Nome dell'oggetto a cui appartiene la colonna. Non ammette i valori Null.|  
|object_package_guid|**uniqueidentifier**|GUID del pacchetto che contiene l'oggetto. Non ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
### <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|Per|Relazione|  
|----------|--------|------------------|  
|dm_xe_session_object_columns.object_name,<br /><br /> dm_xe_session_object_columns.object_package_guid|Sys.dm_xe_objects.package_guid,<br /><br /> sys.dm_xe_objects.name|Molti-a-uno|  
|dm_xe_session_object_columns.column_name,<br /><br /> dm_xe_session_object_columns.column_id|Sys.dm_xe_object_columns.Name,<br /><br /> sys.dm_xe_object_columns.column_id|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

