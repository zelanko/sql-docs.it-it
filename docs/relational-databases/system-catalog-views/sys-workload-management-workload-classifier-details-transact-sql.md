---
title: sys. workload_management_workload_classifier_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 58b3f3315309a734a22e2732af5207b64e2f0a9d
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632920"
---
# <a name="sysworkload_management_workload_classifier_details-transact-sql"></a>sys. workload_management_workload_classifier_details (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Restituisce i dettagli per ogni classificatore.  
  
|Nome colonna|tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|ID del classificatore.  Non ammette i valori Null.|
|classifier_type|**sysname**|Joinable a [sys. workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md).|`membername`</br>`wlm_label`</br>`wlm_context`</br>`start_time`</br>`end_time`|
|classifier_value|**sysname**|Valore del classificatore. Non ammette i valori Null.||

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione VIEW SERVER STATE.

## <a name="next-steps"></a>Passaggi successivi
  
Per un elenco di tutte le viste del catalogo per SQL Data Warehouse e data warehouse parallele, vedere [SQL data warehouse e le viste del catalogo data warehouse parallele](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Per creare un classificatore del carico di lavoro, vedere [creare un classificatore del carico di lavoro](../../t-sql/statements/create-workload-classifier-transact-sql.md). Per ulteriori informazioni sulla classificazione del carico di lavoro, vedere SQL Data Warehouse [classificazione del carico](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) di lavoro e [importanza del carico](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
