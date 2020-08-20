---
description: sys. dm_pdw_os_performance_counters (Transact-SQL)
title: sys. dm_pdw_os_performance_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 08ef29f6fe47099bcbbdeb87fce0dfb5aa25a42a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474741"
---
# <a name="sysdm_pdw_os_performance_counters-transact-sql"></a>sys. dm_pdw_os_performance_counters (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contiene informazioni sui contatori delle prestazioni di Windows per i nodi in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ID del nodo che contiene il contatore.<br /><br /> pdw_node_id e counter_name formano la chiave per questa visualizzazione.|Vedere node_id in [sys. dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|counter_name|**nvarchar(255)**|Nome del contatore delle prestazioni di Windows.||  
|counter_category|**nvarchar(255)**|Nome della categoria del contatore delle prestazioni di Windows.||  
|nome_istanza|**nvarchar(255)**|Nome dell'istanza specifica del contatore.||  
|counter_value|**Decimali (38, 10)**|Valore corrente del contatore.||  
|last_update_time|**Datetime2 (3)**|Timestamp dell'ultima volta in cui il valore è stato aggiornato.||  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
