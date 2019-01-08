---
title: syssubscriptions (vista di sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 529572f02568cb7e13ff8821ab8d48a86d908141
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52783453"
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions (vista di sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **syssubscriptions** Vista espone le informazioni sulla sottoscrizione. Questa vista è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|ID univoco di un articolo sottoscritto.|  
|**srvid**|**smallint**|ID del Sottoscrittore.|  
|**dest_db**|**sysname**|Nome del database di sottoscrizione.|  
|**status**|**tinyint**|Stato della sottoscrizione:<br /><br /> **0** = inattiva.<br /><br /> **1** = sottoscritta.<br /><br /> **2** = attivo.|  
|**sync_type**|**tinyint**|Tipo di sincronizzazione iniziale:<br /><br /> **1** = automatic.<br /><br /> **2** = none.|  
|**login_name**|**sysname**|Nome dell'account di accesso utilizzato per la connessione al server di pubblicazione per l'aggiunta della sottoscrizione.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push: l'agente di distribuzione viene eseguito nel server di distribuzione.<br /><br /> **1** = pull: l'agente di distribuzione viene eseguito nel Sottoscrittore.|  
|**distribution_jobid**|**binary(16)**|Identifica il processo dell'agente di distribuzione utilizzato per sincronizzare la sottoscrizione.|  
|**timestmap**|**timestamp**|Data e ora di creazione della sottoscrizione.|  
|**update_mode**|**tinyint**|Modalità di aggiornamento:<br /><br /> **0** = sola lettura.<br /><br /> **1** = aggiornamento immediato.|  
|**loopback_detection**|**bit**|Si applica alle sottoscrizioni che fanno parte di una topologia di replica transazionale bidirezionale. Il rilevamento di loopback determina se l'agente di distribuzione deve inviare nuovamente al Sottoscrittore le transazioni provenienti dal Sottoscrittore:<br /><br /> **0** = restituisce le transazioni.<br /><br /> **1** = non restituisce le transazioni.|  
|**queued_reinit**|**bit**|Specifica se l'articolo è contrassegnato per l'inizializzazione o la reinizializzazione. Un valore pari **1** specifica che l'articolo sottoscritto è contrassegnato per l'inizializzazione o la reinizializzazione.|  
|**nosync_type**|**tinyint**|Tipo di inizializzazione della sottoscrizione:<br /><br /> **0** = automatica (snapshot)<br /><br /> **1** = solo supporto replica<br /><br /> **2** = inizializzazione con backup<br /><br /> **3** = inizializzazione dal numero di sequenza del log (LSN)<br /><br /> Per altre informazioni, vedere la **@sync_type** parametro [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).<br /><br /> **3** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|Nome del Sottoscrittore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
