---
description: sys.dm_xe_database_session_object_columns (database SQL di Azure)
title: sys.dm_xe_database_session_object_columns
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 0e6adc54-4d97-4ef0-bf4f-b4538d69f136
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 9cc81fb4eb394bfa3876d0e25f42404e756c3ca3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88322857"
---
# <a name="sysdm_xe_database_session_object_columns-azure-sql-database"></a>sys.dm_xe_database_session_object_columns (database SQL di Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Mostra i valori di configurazione per gli oggetti associati a una sessione.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a tutte le versioni successive.|  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|Indirizzo di memoria della sessione dell'evento. Ha una relazione molti-a-uno con sys. dm_xe_database_sessions. Address. Non ammette i valori Null.|  
|column_name|**nvarchar(60)**|Nome del valore di configurazione. Non ammette i valori Null.|  
|column_id|**int**|ID della colonna. Valore univoco all'interno dell'oggetto. Non ammette i valori Null.|  
|column_value|**nvarchar(2048)**|Valore configurato della colonna. Ammette i valori Null.|  
|object_type|**nvarchar(60)**|Tipo dell'oggetto.  Non ammette valori null. object_type è uno dei seguenti:<br /><br /> event<br /><br /> target|  
|object_name|**nvarchar(60)**|Nome dell'oggetto a cui appartiene la colonna. Non ammette i valori Null.|  
|object_package_guid|**uniqueidentifier**|GUID del pacchetto che contiene l'oggetto. Non ammette i valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|A|Relazione|  
|----------|--------|------------------|  
|dm_xe_database_session_object_columns. object_name<br /><br /> dm_xe_database_session_object_columns. object_package_guid|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|Molti-a-uno|  
|dm_xe_database_session_object_columns. column_name<br /><br /> dm_xe_database_session_object_columns. column_id|sys.dm_xe_object_columns.name<br /><br /> sys.dm_xe_object_columns.column_id|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)  
  
  
