---
title: sys. dm_pdw_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 61593522e09ed86ec10f08a6ad8ff7a941a2e10e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899351"
---
# <a name="sysdm_pdw_nodes-transact-sql"></a>sys. dm_pdw_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Include informazioni su tutti i nodi di [!INCLUDE[ssAPS](../../includes/ssaps-md.md)]. Elenca una riga per nodo nell'appliance.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|ID numerico univoco associato al nodo.<br /><br /> Chiave per questa visualizzazione.|Univoco nell'appliance, indipendentemente dal tipo.|  
|type|**nvarchar (32)**|Tipo del nodo.|' COMPUTE ',' CONTROL ',' MANAGEMENT '|  
|name|**nvarchar (32)**|Nome logico del nodo.|Qualsiasi stringa di lunghezza appropriata.|  
|address|**nvarchar (32)**|Indirizzo IP del nodo.|Nel formato [0-255]. [0-255]. [0-255]. [0-255].|  
|is_passive|**int**|Indica se la macchina virtuale che esegue il nodo è in esecuzione nel server assegnato oppure è stata sottoposta a failover sul server di riserva.|0-la macchina virtuale del nodo è in esecuzione nel server originale.<br /><br /> una macchina virtuale a 1 nodo è in esecuzione nel server di riserva.|  
|region|**nvarchar (32)**|Area in cui è in esecuzione il nodo.|' PDW ',' HDINSIGHT '|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
