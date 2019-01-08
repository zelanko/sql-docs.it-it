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
manager: craigg
ms.openlocfilehash: 27906e593020d45a9fb5e79be6ac53bc0e7fafcc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791553"
---
# <a name="msmergeidentityrange-transact-sql"></a>MSmerge_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSmerge_identity_range** tabella viene utilizzata per tenere traccia degli intervalli numerici assegnati alle colonne di identità per la sottoscrizione delle pubblicazioni in cui la replica gestisce automaticamente tali assegnazioni di intervalli. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|Numero di identificazione univoco per la sottoscrizione specificata.|  
|**artid**|**uniqueidentifier**|Identificatore univoco per l'articolo specificato.|  
|**range_begin**|**Numeric(38)**|Valore Identity all'inizio dell'intervallo corrente.|  
|**range_end**|**Numeric(38)**|Valore Identity alla fine dell'intervallo corrente.|  
|**next_range_begin**|**Numeric(38)**|Valore Identity all'inizio dell'intervallo successivo da assegnare.|  
|**next_range_end**|**Numeric(38)**|Valore Identity alla fine dell'intervallo successivo da assegnare.|  
|**is_pub_range**|**bit**|Un valore pari **1** se l'intervallo di valori identity viene assegnato alla pubblicazione.|  
|**max_used**|**Numeric(38)**|Valore Identity massimo che può essere assegnato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
