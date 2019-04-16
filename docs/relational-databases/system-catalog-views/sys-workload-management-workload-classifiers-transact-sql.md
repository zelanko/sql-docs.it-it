---
title: Sys.workload_management_workload_classifiers (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 3b023654728375aee76bfb0c4434a8413dc81e7d
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582564"
---
# <a name="sysworkloadmanagementworkloadclassifiers-transact-sql-preview"></a>Sys.workload_management_workload_classifiers (Transact-SQL) (anteprima)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

> [!Note]
> La classificazione del carico di lavoro è disponibile in anteprima in SQL Data Warehouse Gen2. Anteprima carico di lavoro gestione classificazione e priorità è per le compilazioni con una data di rilascio di 9 aprile 2019 o versione successiva.  Gli utenti consigliabile evitare di usare le compilazioni precedenti a tale data per il test di carico di lavoro gestione.  Per determinare se la compilazione è in grado di gestione del carico di lavoro, eseguire select @@version quando si è connessi all'istanza di SQL Data Warehouse.

 Restituisce i dettagli per classificatori di carico di lavoro.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|ID univoco del classificatore. Non ammette i valori Null||
group_name|**sysname**|Nome del gruppo di carico di lavoro, la funzione di classificazione viene assegnato a. Non ammette i valori Null. |Classi di risorse statiche</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80 </br> </br>Classi di risorse dinamiche</br>smallrc</br>mediumrc</br>largerc</br>xlargerc|
NAME|**sysname**|Nome del classificatore. Deve essere univoco per l'istanza. Non ammette i valori Null.||
|importance|**sysname**|È l'importanza relativa di una richiesta in questo gruppo di carico di lavoro e nei gruppi del carico di lavoro per le risorse condivise.  Importanza specificata nella funzione di classificazione sostituisce l'impostazione di priorità di gruppo del carico di lavoro.|bassa, below_normal, normale, above_normal, elevato |
|create_time|**datetime**|Ora che è stato creato il classificatore. Non ammette i valori Null.||
modify_time|**datetime**|Ora del che ultima modifica la funzione di classificazione. Non ammette i valori Null.||
is_enabled|**bit**|Indica se la funzione di classificazione è abilitato o meno. È abilitato per impostazione predefinita. Non ammette i valori Null.|0 = la funzione di classificazione non è abilitato </br> 1 = la funzione di classificazione è abilitata|
|&nbsp;||||
  
## <a name="permissions"></a>Permissions

È richiesta l'autorizzazione VIEW SERVER STATE.

## <a name="next-steps"></a>Passaggi successivi

 Per un elenco di tutte le viste del catalogo per SQL Data Warehouse e Parallel Data Warehouse, vedere [viste del catalogo di Parallel Data Warehouse e SQL Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Per creare un classificatore di carico di lavoro, vedere [CLASSIFICATORE del carico di lavoro creare](../../t-sql/statements/create-workload-classifier-transact-sql.md). Per altre informazioni sulla classificazione del carico di lavoro, vedere [classificazione del carico di lavoro di SQL DATA Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
