---
title: sys.dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7d9e18284ac4d97efaa217802682fe79ebb2dfc5
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041522"
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Restituisce un elenco di tutte le credenziali di rete archiviato nel [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] appliance per tutti i server di destinazione. I risultati sono elencati per il nodo di controllo e ogni nodo di calcolo.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|Id numerico univoco associato al nodo.|  
|target_server_name|**nvarchar(32)**|Indirizzo IP del server di destinazione che [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] accederà usando le credenziali nome utente e password.|  
|username|**nvarchar(32)**|Nome utente per cui la password viene archiviata.|  
|LAST_MODIFIED|**datetime**|Data e ora dell'ultima operazione che modifica le credenziali.|  
  
## <a name="permissions"></a>Permissions  
 Richiede VIEW SERVER STATE.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 È la chiave per questa vista a gestione dinamica *pdw_node_id* plus *target_server_name*.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
