---
title: sys.dm_xe_database_session_targets
titleSuffix: Azure SQL Database
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: ac4b9b01b85b6c8b4832a591ba18654ac58e9125
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826693"
---
# <a name="sysdm_xe_database_session_targets-azure-sql-database"></a>sys.dm_xe_database_session_targets (database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni sulle destinazioni della sessione.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a qualsiasi versione futura.|  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|Indirizzo di memoria della sessione dell'evento. Ha una relazione molti-a-uno con sys. dm_xe_database_sessions. Address. Non ammette i valori Null.|  
|target_name|**nvarchar(60)**|Nome della destinazione in una sessione. Non ammette i valori Null.|  
|target_package_guid|**uniqueidentifier**|GUID del pacchetto che contiene la destinazione. Non ammette i valori Null.|  
|execution_count|**bigint**|Numero di volte in cui la destinazione è stata eseguita per la sessione. Non ammette i valori Null.|  
|execution_duration_ms|**bigint**|Tempo totale di esecuzione della destinazione, espresso in millisecondi. Non ammette i valori Null.|  
|target_data|**nvarchar(max)**|Dati che la destinazione gestisce, ad esempio informazioni di aggregazione di evento. Ammette i valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|A|Relazione|  
|----------|--------|------------------|  
|sys. dm_xe_database_session_targets. event_session_address|sys. dm_xe_database_sessions. Address|Molti-a-uno|  
  
  
