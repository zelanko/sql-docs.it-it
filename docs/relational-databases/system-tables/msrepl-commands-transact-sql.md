---
title: MSrepl_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_commands
- MSrepl_commands_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_commands system table
ms.assetid: 53b9f9cd-9429-47a0-aba2-908fc60e7036
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a4a55e595f925c8b542f14e34c8c88110472df89
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822095"
---
# <a name="msreplcommands-transact-sql"></a>MSrepl_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSrepl_commands** tabella contiene righe di comandi replicati. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|ID del database del server di pubblicazione.|  
|**xact_seqno**|**varbinary(16)**|Numero di sequenza della transazione.|  
|**type**|**int**|Tipo di comando.|  
|**article_id**|**int**|ID dell'articolo.|  
|**originator_id**|**int**|ID dell'origine.|  
|**command_id**|**int**|ID del comando.|  
|**che**|**bit**|Indica se si tratta di un comando parziale.|  
|**comando**|**varbinary(1024)**|Valore del comando.|  
|**hashKey**|**int**|Solo per uso interno.|  
|**originator_lsn**|**varbinary(16)**|Identifica il numero di sequenza del file di log (LSN) per il comando nella pubblicazione di origine. Viene utilizzato nella replica transazionale peer-to-peer.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
