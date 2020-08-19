---
description: sys. dm_exec_compute_node_status (Transact-SQL)
title: sys. dm_exec_compute_node_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODE_STATUS_TSQL
- DM_EXEC_COMPUTE_NODE_STATUS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_compute_node_status
- sys.dm_exec_compute_node_status management view
ms.assetid: b606f91f-3a08-4a4f-bb57-32ae155b3738
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 182a6fff7ff2cf0af1b009a3c5acc79e00c8365a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447631"
---
# <a name="sysdm_exec_compute_node_status-transact-sql"></a>sys. dm_exec_compute_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Include informazioni aggiuntive sulle prestazioni e lo stato di tutti i nodi di base. Elenca una riga per nodo.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|`int`|ID numerico univoco associato al nodo.|Univoco nel cluster con scalabilità orizzontale indipendentemente dal tipo.|  
|process_id|`int`|||  
|process_name|`nvarchar(255)`|Nome logico del nodo.|Qualsiasi stringa di lunghezza appropriata.|  
|allocated_memory|`bigint`|Memoria allocata totale in questo nodo.||  
|available_memory|`bigint`|Memoria totale disponibile in questo nodo.||  
|process_cpu_usage|`bigint`|Utilizzo totale della CPU del processo, in cicli.||  
|total_cpu_usage|`bigint`|Utilizzo totale della CPU, in cicli.||  
|thread_count|`bigint`|Numero totale di thread in uso in questo nodo.||  
|handle_count|`bigint`|Numero totale di handle in uso in questo nodo.||  
|total_elapsed_time|`bigint`|Tempo totale trascorso dall'avvio o dal riavvio del sistema.|Tempo totale trascorso dall'avvio o dal riavvio del sistema. Se total_elapsed_time supera il valore massimo per un numero intero (24,8 giorni in millisecondi), si verificherà un errore di materializzazione causato da un overflow. Il valore massimo in millisecondi equivale a 24,8 giorni.|  
|is_available|`bit`|Flag che indica se il nodo è disponibile.||  
|sent_time|`datetime`|Ora dell'ultima invio di un pacchetto di rete||  
|received_time|`datetime`|Ultima volta in cui un pacchetto di rete è stato inviato da questo nodo.||  
|error_id|`nvarchar(36)`|Identificatore univoco dell'ultimo errore che si è verificato in questo nodo.||
|compute_pool_id|`int`|Identificatore univoco per il pool.|

## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi di polibase con viste a gestione dinamica](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative ai database &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
