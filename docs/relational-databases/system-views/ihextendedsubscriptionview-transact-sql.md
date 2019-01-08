---
title: IHextendedSubscriptionView (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedSubscriptionView_TSQL
- IHextendedSubscriptionView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedSubscriptionView view
ms.assetid: 124756a4-463a-4a81-bf5b-de7e8ffc7a62
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30ba4a0947f98ab34ed8c11ef0e8f3a25c3e453b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756983"
---
# <a name="ihextendedsubscriptionview-transact-sql"></a>IHextendedSubscriptionView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **IHextendedSubscriptionView** visualizzazione espone informazioni sulla sottoscrizione di una pubblicazione non SQL Server. Questa vista è archiviata nel **distribuzione** database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|ID univoco di un articolo.|  
|**dest_db**|**sysname**|Nome del database di destinazione.|  
|**srvid**|**smallint**|ID univoco di un Sottoscrittore.|  
|**login_name**|**sysname**|Account di accesso utilizzato per la connessione a un Sottoscrittore.|  
|**distribution_jobid**|**binary**|Identifica il processo dell'agente di distribuzione.|  
|**publisher_database_id**|**int**|Identifica il database di pubblicazione.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push: l'agente di distribuzione viene eseguito nel Sottoscrittore.<br /><br /> **1** = pull: l'agente di distribuzione viene eseguito nel server di distribuzione.|  
|**sync_type**|**tinyint**|Tipo di sincronizzazione iniziale:<br /><br /> **1** = automatica<br /><br /> **2** = nessuno|  
|**status**|**tinyint**|Stato della sottoscrizione:<br /><br /> **0** = inattivo<br /><br /> **1** = sottoscritta<br /><br /> **2** = attivo|  
|**snapshot_seqno_flag**|**bit**|Indica se viene utilizzato un numero di sequenza dello snapshot.|  
|**independent_agent**|**bit**|Specifica se per la pubblicazione è disponibile un agente di distribuzione autonomo.<br /><br /> **0** = la pubblicazione utilizza un agente di distribuzione condiviso, e ogni coppia database del server di pubblicazione/sottoscrittore del database ha un solo agente condiviso.<br /><br /> **1** = è disponibile un agente di distribuzione autonomo per la pubblicazione.|  
|**subscription_time**|**datetime**|Solo per uso interno.|  
|**loopback_detection**|**bit**|Si applica alle sottoscrizioni che fanno parte di una topologia di replica transazionale bidirezionale. Il rilevamento di loopback determina se l'agente di distribuzione deve inviare nuovamente al Sottoscrittore le transazioni provenienti dal Sottoscrittore:<br /><br /> **1** = non restituisce le transazioni.<br /><br /> **0** = restituisce le transazioni.|  
|**agent_id**|**int**|ID univoco dell'agente di distribuzione.|  
|**update_mode**|**tinyint**|Indica il tipo di modalità di aggiornamento. I possibili valori sono i seguenti:<br /><br /> **0** = sola lettura.<br /><br /> **1** = aggiornamento immediato.<br /><br /> **2** = aggiornamento in coda tramite MSMQ.<br /><br /> **3** = immediato aggiornare con aggiornamento in coda come failover usando Accodamento messaggi.<br /><br /> **4** = aggiornamento in coda tramite una coda di SQL Server.<br /><br /> **5** = aggiornamento immediato con failover dell'aggiornamento in coda, tramite la coda SQL Server.|  
|**publisher_seqno**|**varbinary(16)**|Numero di sequenza della transazione nel server di pubblicazione per questa sottoscrizione.|  
|**ss_cplt_seqno**|**varbinary(16)**|Numero di sequenza utilizzato per indicare il completamento dell'elaborazione simultanea degli snapshot.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
