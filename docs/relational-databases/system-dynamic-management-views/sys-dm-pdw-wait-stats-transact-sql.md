---
description: sys. dm_pdw_wait_stats (Transact-SQL)
title: sys. dm_pdw_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f5a8d40b7181f932f5e42192224e91f5c6aa4c8a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88397827"
---
# <a name="sysdm_pdw_wait_stats-transact-sql"></a>sys. dm_pdw_wait_stats (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Include informazioni correlate allo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stato del sistema operativo correlate alle istanze in esecuzione nei diversi nodi. Per un elenco dei tipi di attesa e della relativa descrizione, vedere [sys. dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx).  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|ID del nodo a cui si riferisce questa voce.||  
|**wait_name**|**nvarchar(255)**|Nome del tipo di attesa.||  
|**max_wait_time**|**bigint**|Tempo massimo di attesa per questo tipo di attesa.||  
|**request_count**|**bigint**|Numero di attese in attesa del tipo di attesa.||  
|**signal_time**|**bigint**|Differenza tra il momento in cui è stato rilevato il thread in attesa e quello in cui è stata avviata l'esecuzione del thread.||  
|**completed_count**|**bigint**|Numero totale di attese di questo tipo completate dopo l'ultimo riavvio del server.||  
|**wait_time**|**bigint**|Tempo di attesa totale per questo tipo di attesa in millisecons. Inclusione di signal_time.||  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys. dm_pdw_waits &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
