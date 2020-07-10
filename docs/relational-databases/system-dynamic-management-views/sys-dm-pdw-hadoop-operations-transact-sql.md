---
title: sys. dm_pdw_hadoop_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6378ddd4b0604fabe81d669d272b59207781fdf8
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197076"
---
# <a name="sysdm_pdw_hadoop_operations-transact-sql"></a>sys. dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contiene una riga per ogni processo di riduzione della mappa che viene inserito in Hadoop come parte dell'esecuzione di una [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] query in una tabella Hadoop esterna. Ogni processo di riduzione della mappa rappresenta uno dei predicati nella query. Viene usato solo quando il predicato distribuzione è abilitato per le query su tabelle esterne Hadoop.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|ID per questa operazione Hadoop esterna.|Uguale all'ID in [sys. dm_pdw_exec_requests &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Indice del passaggio della query che fa riferimento a questa operazione Hadoop.|Uguale a step_index in [sys. dm_pdw_request_steps &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|Descrive il tipo di operazione esterna.|' Operazione Hadoop esterna '|  
|operation_name|**nvarchar(4000)**|ID processo per un processo di riduzione della mappa. Questa operazione viene restituita da Hadoop dopo [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] l'invio del processo.||  
|map_progress|**float**|Percentuale di dati di input che sono stati usati finora dal processo di mapping.|Numero a virgola mobile compreso tra e, tra cui 0 e 100.|  
|reduce_progress|**int**|Percentuale del processo di riduzione completato.|Numero a virgola mobile compreso tra e, tra cui 0 e 100.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
