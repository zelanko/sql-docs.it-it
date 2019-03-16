---
title: Sys.workload_management_workload_classifier_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
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
ms.openlocfilehash: 421f47aee86c2e5bbdffe485ffea0cffef73bafd
ms.sourcegitcommit: 05bb10710489bef16bb2c53b3803e9b8eea1429a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2019
ms.locfileid: "57988777"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>Sys.workload_management_workload_classifier_details (Transact-SQL) (anteprima)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Restituisce i dettagli per ogni funzione di classificazione.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|ID del classificatore. Sottoponibile a join a [sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md). Non ammette i valori Null.|
|classifier_type|**sysname**|L'entità su cui viene eseguita la classificazione. Non ammette i valori Null.|[Classificazione del carico di lavoro SQL DATA Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)|
|classifier_value|**sysname**|Il valore del classificatore. Non ammette i valori Null.||

## <a name="permissions"></a>Permissions

È richiesta l'autorizzazione VIEW SERVER STATE.

## <a name="next-steps"></a>Passaggi successivi
  
 Per un elenco di tutte le viste del catalogo per SQL Data Warehouse e Parallel Data Warehouse, vedere [viste del catalogo di Parallel Data Warehouse e SQL Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Per creare un classificatore di carico di lavoro, vedere [CLASSIFICATORE del carico di lavoro creare](../../t-sql/statements/create-workload-classifier-transact-sql.md). Per altre informazioni sulla classificazione del carico di lavoro, vedere [classificazione del carico di lavoro di SQL DATA Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
