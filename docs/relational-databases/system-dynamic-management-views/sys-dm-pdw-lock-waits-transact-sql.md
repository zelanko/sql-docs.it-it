---
title: sys. dm_pdw_lock_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 29a82daa2857177200bd76b738f92d65f6b26668
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899382"
---
# <a name="sysdm_pdw_lock_waits-transact-sql"></a>sys. dm_pdw_lock_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Include informazioni sulle richieste in attesa di blocchi.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Posizione della richiesta nell'elenco di attesa.|ordinale in base 0. Questa operazione non è univoca in tutte le voci di attesa.|  
|session_id|**nvarchar (32)**|ID della sessione in cui si è verificato lo stato di attesa.|Vedere session_id in [sys. dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|type|**nvarchar(255)**|Tipo di attesa rappresentata da questa voce.|Valori possibili:<br /><br /> Condiviso<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> Esclusivo|  
|object_type|**nvarchar(255)**|Tipo di oggetto interessato dall'attesa.|Valori possibili:<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar (386)**|Nome o GUID dell'oggetto specificato interessato dall'attesa.|Le tabelle e le viste vengono visualizzate con nomi in tre parti.<br /><br /> Gli indici e le statistiche vengono visualizzati con nomi in quattro parti.<br /><br /> Nomi, entità e database sono nomi di stringa.|  
|request_id|**nvarchar (32)**|ID della richiesta in cui si è verificato lo stato di attesa.|ID della richiesta.<br /><br /> Si tratta di un GUID per le richieste di caricamento.|  
|request_time|**datetime**|Ora in cui è stato richiesto il blocco o la risorsa.||  
|acquire_time|**datetime**|Ora in cui è stato acquisito il blocco o la risorsa.||  
|state|**nvarchar(50)**|Stato dello stato di attesa.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Priorità dell'elemento in attesa.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
