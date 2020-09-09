---
title: MSmerge_generation_partition_mappings (T-SQL)
description: Viene descritto il MSmerge_generation_partition_mappings stored procedure utilizzato per tenere traccia delle modifiche apportate alle partizioni in una pubblicazione di tipo merge.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_generation_partition_mappings_TSQL
- MSmerge_generation_partition_mappings
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_generation_partition_mappings system table
ms.assetid: 443a4024-ce48-4772-9ee5-95bd6fb6476b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4ae8e89600a76da91ccf06d0a561319af9bec3f1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544512"
---
# <a name="msmerge_generation_partition_mappings-transact-sql"></a>MSmerge_generation_partition_mappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSmerge_generation_partition_mappings** viene utilizzata per tenere traccia delle modifiche apportate alle partizioni in una pubblicazione di tipo merge. Questa tabella viene archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|Identifica la pubblicazione di tipo merge.|  
|**generazione**|**bigint**|Valore di generazione.|  
|**partition_id**|**int**|Identifica la partizione.|  
|**changecount**|**int**|Numero di volte che la partizione è stata modificata.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
