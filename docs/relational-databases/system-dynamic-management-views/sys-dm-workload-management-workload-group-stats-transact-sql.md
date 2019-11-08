---
title: sys. dm_workload_management_workload_groups_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/02/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 6e77239d019cb51e66a34a3a5b909e01c28a7faa
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73633435"
---
# <a name="sysdm_workload_management_workload_groups_stats-transact-sql"></a>sys. dm_workload_management_workload_groups_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Restituisce le statistiche del gruppo di carico di lavoro e i valori effettivi del gruppo di carico di lavoro in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Nome colonna|tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|ID univoco del gruppo del carico di lavoro.||
|name|**sysname**|Nome del gruppo del carico di lavoro.||
|statistics_start_time|**datetime**|Ora di inizio della raccolta delle statistiche per il gruppo del carico di lavoro.  Il valore è quando è stato creato il gruppo del carico di lavoro o quando l'istanza viene sospesa o ridimensionata.||
|total_request_count|**bigint**|Conteggio cumulativo delle richieste completate nel gruppo del carico di lavoro.||
|total_shared_resource_reqeusts|**bigint**|Conteggio cumulativo delle richieste completate nel gruppo del carico di lavoro che ha utilizzato risorse dal pool condiviso.||
|total_queued_request_count|**bigint**|Conteggio cumulativo delle richieste accodate dopo il raggiungimento del limite max_concurrency.||
|total_request_execution_timeouts|**bigint**|Conteggio cumulativo delle richieste nel gruppo del carico di lavoro che si è verificato il timeout prima del completamento in base all'impostazione query_execution_timeout_sec.||
|effective_min_percentage_resource|**tinyint**|L'impostazione min_percentage_resource efficace consentita in considerazione del livello di servizio e delle impostazioni del gruppo di carico di lavoro. Il min_percentage_resource effettivo può essere modificato in un livello superiore rispetto ai livelli di servizio più bassi.  In DW100c, ad esempio, il min_percentage_resource più basso consentito è pari al 25%.  Il min_percentage_resource viene modificato in 0% se il valore non può essere concesso a livello di servizio.  Ad esempio, min_percentage_resource impostato sul 10% in DW6000c, avrà un effective_min_percentage_resource pari allo 0% quando viene ridotto a DW100c.||
|effective_cap_percentage_resource|**tinyint**|Cap_percentage_resource efficace per il gruppo del carico di lavoro.  Se sono presenti altri gruppi di carico di lavoro con min_percentage_resource > 0, il effective_cap_percentage_resource viene ridotto proporzionalmente.||
|effective_request_min_resource_grant_percent|**Decimal (5, 2)**|Valore di runtime effettivo per request_min_resource_grant_percent del gruppo di carico di lavoro. Valore effettivo che prende in considerazione il livello di servizio e la modalità di configurazione del gruppo di carico di lavoro.  Se min_percentage_resource viene regolato a causa del livello di servizio, effective_request_min_resource_grant_percent verrà regolato di conseguenza.||
|effective_request_max_resource_grant_percent|**Decimal (5, 2)**|Valore di runtime effettivo per request_max_resource_grant_percent del gruppo di carico di lavoro considerando la configurazione di tutti i gruppi del carico di lavoro.||
|||||

## <a name="see-also"></a>Vedere anche

 [Transact-SQL SQL Data Warehouse e Parallel data warehouse &#40;viste a gestione dinamica&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
