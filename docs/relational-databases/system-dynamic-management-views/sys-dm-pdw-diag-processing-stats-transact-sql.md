---
title: sys. dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a765e591e3b55bb4be2e2b6d7431873702910f6f
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394356"
---
# <a name="sysdm_pdw_diag_processing_stats-transact-sql"></a>sys. dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Visualizza le informazioni relative a tutti gli eventi di diagnostica interni che possono essere incorporati nelle sessioni di diagnostica definite dall'amministratore. Eseguire una query su questa vista per comprendere le statistiche alla base dei sottosistemi di diagnostica e di eventi che determinano il popolamento di tutti gli altri DMV. È disponibile un gruppo di code per ogni processo in ogni nodo.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|Nodo del dispositivo da cui è presente il log.|  
|**process_id**|**int**|Identificatore del processo che esegue l'invio di questa statistica.|  
|**target_name**|**nvarchar(255)**|Nome della coda.|  
|**queue_size**|**int**|Numero di elementi nella coda dei processi. Le dimensioni della coda sono in genere pari a 0. Un numero positivo indica che il sistema è sottoposto a stress e sta creando un backlog di eventi. Un conteggio positivo nelle altre colonne significa che il sistema è stato danneggiato per la coda specifica e per eventuali DMV correlati.|  
|**lost_events_count**|**bigint**|Il numero di eventi persi.|  
  
## <a name="see-also"></a>Vedi anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
