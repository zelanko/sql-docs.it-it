---
title: sys. dm _exec_dms_services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DMS_SERVICES_TSQL
- SYS.DM_EXEC_DMS_SERVICES_TSQL
- DM_EXEC_DMS_SERVICES
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_services management view
- sys.dm_exec_dms_services management view
ms.assetid: 6ac47eef-4293-46b8-8555-07a614837504
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11e353af23c2331cd8f2bef5b439c967512e7323
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532929"
---
# <a name="sysdm_exec_dms_services-transact-sql"></a>sys. dm _exec_dms_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Include informazioni su tutti i servizi DMS in esecuzione nei nodi di calcolo di base. Viene elencata una riga per ogni istanza del servizio.  
  
|Nome colonna|tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|`int`|ID numerico univoco associato al core DMS. Chiave per questa visualizzazione.|ID univoco.|  
|compute_node_id|`int`|ID del nodo in cui è in esecuzione il servizio DMS|Vedere *compute_node_id* in [sys. dm _EXEC_COMPUTE_NODES &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|status|`nvarchar(32)`|Stato corrente del servizio DMS||
|compute_pool_id|`int`|Identificatore univoco per il pool.|

## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi di base con viste a gestione dinamica](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-SQL delle viste &#40;a gestione dinamica relative ai database&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
