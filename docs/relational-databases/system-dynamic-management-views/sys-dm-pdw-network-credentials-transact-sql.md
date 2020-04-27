---
title: sys. dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b75eb53da9961025e3310f27e4a12608dd4fda78
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899354"
---
# <a name="sysdm_pdw_network_credentials-transact-sql"></a>sys. dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Restituisce un elenco di tutte le credenziali di rete archiviate nell' [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Appliance per tutti i server di destinazione. I risultati sono elencati per il nodo di controllo e per ogni nodo di calcolo.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|ID numerico univoco associato al nodo.|  
|target_server_name|**nvarchar(32)**|Indirizzo IP del server di destinazione a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] cui si accederà utilizzando le credenziali di nome utente e password.|  
|nomeutente|**nvarchar(32)**|Nome utente per il quale è archiviata la password.|  
|last_modified|**datetime**|Data/ora dell'ultima operazione che ha modificato la credenziale.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede lo stato del SERVER di visualizzazione.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 La chiave per questa vista a gestione dinamica è *pdw_node_id* più *target_server_name*.  
  
## <a name="see-also"></a>Vedi anche  
 [SQL Data Warehouse e Parallel data warehouse viste a gestione dinamica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
