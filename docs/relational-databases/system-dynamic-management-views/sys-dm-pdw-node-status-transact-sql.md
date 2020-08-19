---
description: sys. dm_pdw_node_status (Transact-SQL)
title: sys. dm_pdw_node_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b93d177ad3f73982386407e019629401d70ec57f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447496"
---
# <a name="sysdm_pdw_node_status-transact-sql"></a>sys. dm_pdw_node_status (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Include informazioni aggiuntive (oltre a [sys. dm_pdw_nodes &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) sulle prestazioni e lo stato di tutti i nodi del dispositivo. Elenca una riga per nodo nell'appliance.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ID numerico univoco associato al nodo.<br /><br /> Chiave per questa visualizzazione.|Univoco nell'appliance, indipendentemente dal tipo.|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|Memoria allocata totale in questo nodo.||  
|available_memory|**bigint**|Memoria totale disponibile in questo nodo.||  
|process_cpu_usage|**bigint**|Utilizzo totale della CPU del processo, in cicli.||  
|total_cpu_usage|**bigint**|Utilizzo totale della CPU, in cicli.||  
|thread_count|**bigint**|Numero totale di thread in uso in questo nodo.||  
|handle_count|**bigint**|Numero totale di handle in uso in questo nodo.||  
|total_elapsed_time|**bigint**|Tempo totale trascorso dall'avvio o dal riavvio del sistema.|Tempo totale trascorso dall'avvio o dal riavvio del sistema. Se total_elapsed_time supera il valore massimo per un numero intero (24,8 giorni in millisecondi), si verificherà un errore di materializzazione causato da un overflow.<br /><br /> Il valore massimo in millisecondi equivale a 24,8 giorni.|  
|is_available|**bit**|Flag che indica se il nodo è disponibile.||  
|sent_time|**datetime**|Ultima volta in cui un pacchetto di rete è stato inviato da questo nodo.||  
|received_time|**datetime**|Ora dell'ultima ricezione di un pacchetto di rete da questo nodo.||  
|error_id|**nvarchar (36)**|Identificatore univoco dell'ultimo errore che si è verificato in questo nodo.||  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
