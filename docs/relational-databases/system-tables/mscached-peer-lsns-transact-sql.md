---
title: MScached_peer_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MScached_peer_lsns_TSQL
- MScached_peer_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MScached_peer_lsns system table
ms.assetid: f8b6089a-0230-45f9-8c34-9fe0d2a3a74e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2134429ae9d14e00e99c88f1596b1216170e5b66
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078147"
---
# <a name="mscachedpeerlsns-transact-sql"></a>MScached_peer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MScached_peer_lsns** tabella viene utilizzata per rilevare gli LSN nel log delle transazioni che vengono usate per determinare i comandi da restituire a un determinato sottoscrittore nella replica peer-to-peer. Questa tabella è archiviata nel database di distribuzione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ID dell'agente di distribuzione.|  
|**originator**|**sysname**|Nome del server di pubblicazione di origine.|  
|**originator_db**|**sysname**|Nome del database di pubblicazione di origine.|  
|**originator_publication_id**|**int**|Identifica la pubblicazione di origine.|  
|**originator_db_version**|**int**|Identifica il numero di versione del database di origine.|  
|**originator_lsn**|**varbinary(16)**|LSN della transazione di origine.|  
  
## <a name="remarks"></a>Note  
 Gli LSN vengono utilizzati solo immediatamente dopo l'inserimento e non hanno un significato permanente nel sistema.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
