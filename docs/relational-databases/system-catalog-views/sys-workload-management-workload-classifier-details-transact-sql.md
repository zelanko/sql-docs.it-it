---
title: Sys.workload_management_workload_classifier_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 0e693c97ad2702eefb0e02084b6c49d138ef934a
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089527"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql"></a>Sys.workload_management_workload_classifier_details (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Restituisce i dettagli per ogni funzione di classificazione.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|ID del classificatore. Sottoponibile a join a [sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md). Non ammette i valori Null.|
|classifier_type|**sysname**|L'entità su cui viene eseguita la classificazione. Non ammette i valori Null.|MEMBERNAME|
|classifier_value|**sysname**|Il valore del classificatore. Non ammette i valori Null.||

## <a name="permissions"></a>Permissions

È richiesta l'autorizzazione VIEW SERVER STATE.

## <a name="next-steps"></a>Passaggi successivi
  
 Per un elenco di tutte le viste del catalogo per SQL Data Warehouse e Parallel Data Warehouse, vedere [viste del catalogo di Parallel Data Warehouse e SQL Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Per creare un classificatore di carico di lavoro, vedere [CLASSIFICATORE del carico di lavoro creare](../../t-sql/statements/create-workload-classifier-transact-sql.md). Per altre informazioni sulla classificazione del carico di lavoro, vedere SQL Data Warehouse [carico di lavoro di classificazione](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) e [importanza del carico di lavoro](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
