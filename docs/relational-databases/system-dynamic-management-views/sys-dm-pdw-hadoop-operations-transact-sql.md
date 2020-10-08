---
description: sys.dm_pdw_hadoop_operations (Transact-SQL)
title: sys.dm_pdw_hadoop_operations (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: d86092480b71c6971a72f70fe8b00b4fd10c497e
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834358"
---
# <a name="sysdm_pdw_hadoop_operations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contiene una riga per ogni processo di riduzione della mappa che viene inserito in Hadoop come parte dell'esecuzione di una [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] query in una tabella Hadoop esterna. Ogni processo di riduzione della mappa rappresenta uno dei predicati nella query. Viene usato solo quando il predicato distribuzione è abilitato per le query su tabelle esterne Hadoop.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|ID per questa operazione Hadoop esterna.|Uguale all'ID in [sys.dm_pdw_exec_requests &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Indice del passaggio della query che fa riferimento a questa operazione Hadoop.|Uguale a step_index in [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|Descrive il tipo di operazione esterna.|' Operazione Hadoop esterna '|  
|operation_name|**nvarchar(4000)**|ID processo per un processo di riduzione della mappa. Questa operazione viene restituita da Hadoop dopo [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] l'invio del processo.||  
|map_progress|**float**|Percentuale di dati di input che sono stati usati finora dal processo di mapping.|Numero a virgola mobile compreso tra e, tra cui 0 e 100.|  
|reduce_progress|**int**|Percentuale del processo di riduzione completato.|Numero a virgola mobile compreso tra e, tra cui 0 e 100.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;&#41;Transact-SQL ](../../t-sql/language-reference.md)  
  
