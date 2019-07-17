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
ms.openlocfilehash: 51ab87c830d27a2749fdb332c5a13a5b5dd85542
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139708"
---
# <a name="mssubscriptions-transact-sql"></a>MSsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSsubscriptions** tabella contiene una riga per ogni articolo pubblicato in una sottoscrizione gestita dal server di distribuzione locale. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|ID del database del server di pubblicazione.|  
|**publisher_id**|**smallint**|ID del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**publication_id**|**int**|ID della pubblicazione.|  
|**article_id**|**int**|ID dell'articolo.|  
|**subscriber_id**|**smallint**|ID del Sottoscrittore.|  
|**subscriber_db**|**sysname**|Nome del database di sottoscrizione.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push.<br /><br /> **1** = pull.<br /><br /> **2** = anonimo.|  
|**sync_type**|**tinyint**|Tipo di sincronizzazione:<br /><br /> **1** = automatic.<br /><br /> **2** non = Nessuna sincronizzazione.|  
|**status**|**tinyint**|Stato della sottoscrizione:<br /><br /> **0** = inattiva.<br /><br /> **1** = sottoscritta.<br /><br /> **2** = attivo.|  
|**subscription_seqno**|**varbinary(16)**|Numero di sequenza della transazione snapshot.|  
|**snapshot_seqno_flag**|**bit**|Indica l'origine del numero di sequenza delle transazioni snapshot, dove il valore **1** significa che **subscription_seqno** è il numero di sequenza dello snapshot.|  
|**independent_agent**|**bit**|Indica se per questa pubblicazione è disponibile un agente di distribuzione autonomo.|  
|**subscription_time**|**datetime**|Solo per uso interno.|  
|**loopback_detection**|**bit**|Si applica alle sottoscrizioni che fanno parte di una topologia di replica transazionale bidirezionale. Il rilevamento di loopback determina se l'agente di distribuzione deve inviare nuovamente al Sottoscrittore le transazioni provenienti dal Sottoscrittore:<br /><br /> **1** = non restituisce le transazioni.<br /><br /> **0** = restituisce le transazioni.<br /><br /> Nota: Questa colonna è supportata solo per garantire la compatibilità con la funzionalità di replica bidirezionale [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Con le versioni più recenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è consigliabile utilizzare la replica peer-to-peer. Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|**agent_id**|**int**|ID dell'agente.|  
|**update_mode**|**tinyint**|Tipo di aggiornamento.|  
|**publisher_seqno**|**varbinary(16)**|Numero di sequenza della transazione nel server di pubblicazione per questa sottoscrizione.|  
|**ss_cplt_seqno**|**varbinary(16)**|Numero di sequenza utilizzato per indicare il completamento dell'elaborazione simultanea degli snapshot.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
