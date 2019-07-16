---
title: sys.pdw_distributions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7deddb57cdc02410fe161728f45190492ac18a16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127548"
---
# <a name="syspdwdistributions-transact-sql"></a>sys.pdw_distributions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene informazioni sulle distribuzioni nell'appliance. Elenca una riga per ogni distribuzione di appliance.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|Id numerico univoco associata alla distribuzione.<br /><br /> Chiave per questa visualizzazione.|1 al numero di nodi di calcolo nell'appliance moltiplicato per il numero di distribuzioni per nodo di calcolo.|  
|pdw_node_id|**int**|ID del nodo in questa distribuzione.|Vedere in pdw_node_id [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|name|**nvarchar(32)**|Stringa identificatore associato alla distribuzione, utilizzata come un suffisso in tabelle distribuite.|Stringa di risultato di 'A-Z', 'a-z','0-9', '_','-'.|  
|position|**int**|Posizione della distribuzione all'interno di un nodo rispetto al altre distribuzioni su tale nodo.|1 al numero di distribuzioni per nodo.|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
