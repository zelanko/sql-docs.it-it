---
title: MSrepl_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_identity_range_TSQL
- MSrepl_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_identity_range system table
ms.assetid: 6e92a8e8-7667-4c98-b1c4-46735bac50d8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 38f5037598e240585333d246a99c29c5fd8f40fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079166"
---
# <a name="msreplidentityrange-transact-sql"></a>MSrepl_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSrepl_identity_range** tabella fornisce il supporto di gestione di identità intervallo. Questa tabella è archiviata nei database di pubblicazione, distribuzione e sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database di pubblicazione.|  
|**TableName**|**sysname**|Nome della tabella.|  
|**identity_support**|**int**|Specifica se è attivata la gestione automatica degli intervalli di valori Identity. 0 specifica che tale gestione non è attivata.|  
|**next_seed**|**bigint**|Se la gestione automatica degli intervalli di valori Identity è attivata, indica il punto iniziale dell'intervallo successivo.|  
|**pub_range**|**bigint**|Dimensioni dell'intervallo di valori Identity del server di pubblicazione.|  
|**Intervallo**|**bigint**|Dimensioni dei valori Identity consecutivi che verrebbero assegnati nei Sottoscrittori durante un intervento di regolazione.|  
|**max_identity**|**bigint**|Limite massimo dell'intervallo di valori Identity.|  
|**threshold**|**int**|Percentuale di soglia dell'intervallo di valori Identity.|  
|**current_max**|**bigint**|Valore massimo corrente che è possibile assegnare, ma che non viene necessariamente assegnato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
