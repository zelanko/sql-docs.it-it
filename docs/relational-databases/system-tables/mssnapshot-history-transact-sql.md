---
title: MSsnapshot_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshot_history
- MSsnapshot_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_history system table
ms.assetid: 56bf4128-1689-4963-9343-432dd0898d31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca24fdce036c4f63e49e7d0eb12054d2d67aa6aa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800723"
---
# <a name="mssnapshothistory-transact-sql"></a>MSsnapshot_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSsnapshot_history** tabella contiene righe di cronologia per gli agenti Snapshot associati al server di distribuzione locale. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ID dell'agente snapshot.|  
|**runstatus**|**int**|Stato di esecuzione:<br /><br /> **1** = avvio.<br /><br /> **2** = esito positivo.<br /><br /> **3** = in corso.<br /><br /> **4** = inattivo.<br /><br /> **5** = nuovo tentativo.<br /><br /> **6** = esito negativo.|  
|**start_time**|**datetime**|Ora di inizio dell'esecuzione del processo.|  
|**time**|**datetime**|Ora di registrazione del messaggio.|  
|**duration**|**int**|Durata espressa in secondi della sessione del messaggio.|  
|**Commenti**|**nvarchar(255)**|Testo del messaggio.|  
|**delivered_transactions**|**int**|Numero totale di transazioni recapitate durante la sessione.|  
|**delivered_commands**|**int**|Numero di comandi recapitati al secondo.|  
|**delivery_rate**|**float(53)**|Numero medio dei comandi recapitati al secondo.|  
|**error_id**|**int**|L'ID dell'errore nella [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) tabella di sistema.|  
|**timestamp**|**timestamp**|Colonna timestamp della tabella.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
