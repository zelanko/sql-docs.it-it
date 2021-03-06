---
description: MSrepl_identity_range (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8099f50052fdb41d2e5136b6644e6f016d05ab71
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540255"
---
# <a name="msrepl_identity_range-transact-sql"></a>MSrepl_identity_range (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSrepl_identity_range** fornisce supporto per la gestione degli intervalli di valori Identity. Questa tabella è archiviata nei database di pubblicazione, distribuzione e sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**pubblicazione**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database di pubblicazione.|  
|**TableName**|**sysname**|Nome della tabella.|  
|**identity_support**|**int**|Specifica se è attivata la gestione automatica degli intervalli di valori Identity. 0 specifica che tale gestione non è attivata.|  
|**next_seed**|**bigint**|Se la gestione automatica degli intervalli di valori Identity è attivata, indica il punto iniziale dell'intervallo successivo.|  
|**pub_range**|**bigint**|Dimensioni dell'intervallo di valori Identity del server di pubblicazione.|  
|**range**|**bigint**|Dimensioni dei valori Identity consecutivi che verrebbero assegnati nei Sottoscrittori durante un intervento di regolazione.|  
|**max_identity**|**bigint**|Limite massimo dell'intervallo di valori Identity.|  
|**threshold**|**int**|Percentuale di soglia dell'intervallo di valori Identity.|  
|**current_max**|**bigint**|Valore massimo corrente che è possibile assegnare, ma che non viene necessariamente assegnato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
