---
title: MSsubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriptions_TSQL
- MSsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriptions system table
ms.assetid: b7e8301d-d115-41f6-8d4f-e0d25f453b25
author: stevestein
ms.author: sstein
ms.openlocfilehash: ca4364709462eee9df62baa8193dec9f8ea36241
ms.sourcegitcommit: 722f2ec5a1af334f5bcab8341bc744d16a115273
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74866040"
---
# <a name="mssubscriptions-transact-sql"></a>MSsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella **MSsubscriptions** contiene una riga per ogni articolo pubblicato in una sottoscrizione gestita dal server di distribuzione locale. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|ID del database del server di pubblicazione.|  
|**publisher_id**|**smallint**|ID del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**publication_id**|**int**|ID della pubblicazione.|  
|**article_id**|**int**|ID dell'articolo.|  
|**subscriber_id**|**smallint**|ID del Sottoscrittore.|  
|**subscriber_db**|**sysname**|Nome del database di sottoscrizione.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push.<br /><br /> **1** = pull.<br /><br /> **2** = anonimo.|  
|**sync_type**|**tinyint**|Tipo di sincronizzazione:<br /><br /> **1** = automatico.<br /><br /> **2** = nessuna sincronizzazione.|  
|**stato**|**tinyint**|Stato della sottoscrizione:<br /><br /> **0** = inattivo.<br /><br /> **1** = sottoscritto.<br /><br /> **2** = attivo.|  
|**subscription_seqno**|**varbinary (16)**|Numero di sequenza della transazione snapshot.|  
|**snapshot_seqno_flag**|**po'**|Indica l'origine del numero di sequenza della transazione snapshot, dove il valore **1** indica che **subscription_seqno** è il numero di sequenza dello snapshot.|  
|**independent_agent**|**po'**|Indica se per questa pubblicazione è disponibile un agente di distribuzione autonomo.|  
|**subscription_time**|**DateTime**|Solo per uso interno.|  
|**loopback_detection**|**po'**|Si applica alle sottoscrizioni che fanno parte di una topologia di replica transazionale bidirezionale. Il rilevamento di loopback determina se l'agente di distribuzione deve inviare nuovamente al Sottoscrittore le transazioni provenienti dal Sottoscrittore:<br /><br /> **1** = non viene restituito.<br /><br /> **0** = restituisce.<br /><br />|  
|**agent_id**|**int**|ID dell'agente.|  
|**update_mode**|**tinyint**|Tipo di aggiornamento.|  
|**publisher_seqno**|**varbinary (16)**|Numero di sequenza della transazione nel server di pubblicazione per questa sottoscrizione.|  
|**ss_cplt_seqno**|**varbinary (16)**|Numero di sequenza utilizzato per indicare il completamento dell'elaborazione simultanea degli snapshot.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste di replica &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
