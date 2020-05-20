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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 672715bb7bfa83767975c399f75595af04f23d57
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82825839"
---
# <a name="msmerge_identity_range-transact-sql"></a>MSmerge_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella **MSmerge_identity_range** viene utilizzata per tenere traccia degli intervalli numerici assegnati alle colonne Identity per la sottoscrizione di pubblicazioni in cui la replica gestisce automaticamente le assegnazioni di intervalli. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|Numero di identificazione univoco per la sottoscrizione specificata.|  
|**artid**|**uniqueidentifier**|Identificatore univoco per l'articolo specificato.|  
|**range_begin**|**numerico (38)**|Valore Identity all'inizio dell'intervallo corrente.|  
|**range_end**|**numerico (38)**|Valore Identity alla fine dell'intervallo corrente.|  
|**next_range_begin**|**numerico (38)**|Valore Identity all'inizio dell'intervallo successivo da assegnare.|  
|**next_range_end**|**numerico (38)**|Valore Identity alla fine dell'intervallo successivo da assegnare.|  
|**is_pub_range**|**bit**|Valore **1** se l'intervallo di valori Identity viene assegnato alla pubblicazione.|  
|**max_used**|**numerico (38)**|Valore Identity massimo che può essere assegnato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
