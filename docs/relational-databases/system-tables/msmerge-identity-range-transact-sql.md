---
title: MSmerge_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_TSQL
- MSmerge_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range system table
ms.assetid: 493a2028-88a0-4e83-ad89-ae5661d9f477
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9e62d2e8cf46de73bf8f0881b398437ab4ef58fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909040"
---
# <a name="msmergeidentityrange-transact-sql"></a>MSmerge_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSmerge_identity_range** tabella viene utilizzata per tenere traccia degli intervalli numerici assegnati alle colonne di identità per la sottoscrizione delle pubblicazioni in cui la replica gestisce automaticamente tali assegnazioni di intervalli. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|Numero di identificazione univoco per la sottoscrizione specificata.|  
|**artid**|**uniqueidentifier**|Identificatore univoco per l'articolo specificato.|  
|**range_begin**|**numeric(38)**|Valore Identity all'inizio dell'intervallo corrente.|  
|**range_end**|**numeric(38)**|Valore Identity alla fine dell'intervallo corrente.|  
|**next_range_begin**|**numeric(38)**|Valore Identity all'inizio dell'intervallo successivo da assegnare.|  
|**next_range_end**|**numeric(38)**|Valore Identity alla fine dell'intervallo successivo da assegnare.|  
|**is_pub_range**|**bit**|Un valore pari **1** se l'intervallo di valori identity viene assegnato alla pubblicazione.|  
|**max_used**|**numeric(38)**|Valore Identity massimo che può essere assegnato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
