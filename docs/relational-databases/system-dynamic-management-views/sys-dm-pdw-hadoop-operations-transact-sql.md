---
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 11c8cc0797bafff6cc8c38bffb55023be00003a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690428"
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene una riga per ogni processo MapReduce è propagato ad Hadoop come parte dell'esecuzione un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] query su una tabella esterna Hadoop. Ogni processo MapReduce rappresenta uno dei predicati della query. Viene utilizzato solo quando la distribuzione del predicato è abilitata per le query su tabelle esterne di Hadoop.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|ID per questa operazione esterna Hadoop.|Stesso ID in [DM pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Indice del passaggio della query che fa riferimento a questa operazione di Hadoop.|Uguale a step_index nel [DM pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|Descrive il tipo di operazione esterna.|'Operation Hadoop esterno'|  
|operation_name|**nvarchar(4000)**|L'ID di processo per un processo MapReduce. Questo valore viene restituito da Hadoop dopo [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] invia il processo.||  
|map_progress|**float**|La percentuale di dati di input che sono stati utilizzati finora dal processo di mapping.|Numero tra e includerlo, 0 e 100 in virgola mobile.|  
|reduce_progress|**int**|La percentuale del processo di riduzione che è stata completata...|Numero tra e includerlo, 0 e 100 in virgola mobile.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
