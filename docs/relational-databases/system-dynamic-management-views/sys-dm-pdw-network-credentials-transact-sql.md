---
description: sys.dm_pdw_network_credentials (Transact-SQL)
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
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 7d94853e62c1e9e97ddd65ad973e9e481d90bcb0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472742"
---
# <a name="sysdm_pdw_network_credentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Restituisce un elenco di tutte le credenziali di rete archiviate nell' [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Appliance per tutti i server di destinazione. I risultati sono elencati per il nodo di controllo e per ogni nodo di calcolo.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|ID numerico univoco associato al nodo.|  
|target_server_name|**nvarchar(32)**|Indirizzo IP del server di destinazione [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] a cui si accederà utilizzando le credenziali di nome utente e password.|  
|username|**nvarchar(32)**|Nome utente per il quale è archiviata la password.|  
|last_modified|**datetime**|Data/ora dell'ultima operazione che ha modificato la credenziale.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede lo stato del SERVER di visualizzazione.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 La chiave per questa vista a gestione dinamica è *pdw_node_id* più *target_server_name*.  
  
## <a name="see-also"></a>Vedere anche  
 [Analisi delle sinapsi di Azure e DMV Parallel data warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
