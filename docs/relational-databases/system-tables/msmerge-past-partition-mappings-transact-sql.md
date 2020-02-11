---
title: MSmerge_past_partition_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_past_partition_mappings
- MSmerge_past_partition_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_past_partition_mappings system table
ms.assetid: 06d54ff5-4d29-4eeb-b8be-64d032e53134
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d56debf540de7b1e7f33f741fdd4c3f52d3f04a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67984887"
---
# <a name="msmerge_past_partition_mappings-transact-sql"></a>MSmerge_past_partition_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella **MSmerge_past_partition_mappings** archivia una riga per ogni ID di partizione a cui appartiene una riga modificata specificata, ma non appartiene più a. Questa tabella è archiviata nel database di pubblicazione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|Numero di pubblicazione archiviato in **sysmergepublications**.|  
|**tablenick**|**int**|Nome alternativo della tabella pubblicata.|  
|**rowguid**|**uniqueidentifier**|Identificatore della riga specificata.|  
|**partition_id**|**int**|ID della partizione a cui appartiene la riga. Il valore è-1 se la modifica della riga è pertinente per tutti i sottoscrittori.|  
|**generazione**|**bigint**|Valore della generazione in cui si è verificata la modifica di partizione.|  
|**motivo**|**tinyint**|Solo per uso interno.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
