---
title: MSsubscription_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_agents
- MSsubscription_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_agents system table
ms.assetid: 86ad5891-0bef-4963-9381-7d5b45245a0c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3354f69f92cbbbaa9d60ae8ed6352a0b3be6ab52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139791"
---
# <a name="mssubscriptionagents-transact-sql"></a>MSsubscription_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSsubscription_agents** tabella viene utilizzata dall'agente di distribuzione e trigger delle sottoscrizione aggiornabili per tenere traccia delle proprietà della sottoscrizione. Questa tabella è archiviata nel database di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID della riga|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database di pubblicazione.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> 0 = push<br /><br /> 1 = Pull.<br /><br /> 2 = Pull anonima.|  
|**queue_id**|**sysname**|L'ID del [!INCLUDE[msCoName](../../includes/msconame-md.md)] coda nel server di pubblicazione del messaggio. *queue_id* è impostata su **SQL** per basato su SQL ad aggiornamento in coda.|  
|**update_mode**|**tinyint**|Tipo di aggiornamento:<br /><br /> **0** = sola lettura.<br /><br /> **1** = aggiornamento immediato.<br /><br /> **2** = aggiornamento in coda tramite MSMQ.<br /><br /> **3** = immediato aggiornare con aggiornamento in coda come failover usando Accodamento messaggi.<br /><br /> **4** = aggiornamento in coda tramite una coda di SQL Server.<br /><br /> **5** = aggiornamento immediato con failover dell'aggiornamento in coda, tramite la coda SQL Server.|  
|**failover_mode**|**bit**|Se è stato specificato un aggiornamento di tipo failover, indica il tipo di failover selezionato:<br /><br /> **0** = immediato aggiornamento è in uso. Il failover non è attivato.<br /><br /> **1** = in coda aggiornamento è in uso. Il failover è attivato. La coda viene usata per il failover viene specificata nella *update_mode* valore.|  
|**spid**|**int**|ID del processo di sistema per la connessione utilizzata dall'agente di distribuzione appena eseguito o in esecuzione.|  
|**login_time**|**datetime**|Data e ora della connessione dell'agente di distribuzione appena eseguito o in esecuzione.|  
|**allow_subscription_copy**|**bit**|Specifica se consentire o meno la copia del database di sottoscrizione.|  
|**attach_state**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**attach_version**|**binary(16)**|Identificatore univoco che rappresenta la versione di una sottoscrizione allegata.|  
|**last_sync_status**|**int**|Ultimo stato di esecuzione dell'agente di distribuzione appena eseguito o in esecuzione. I possibili valori sono i seguenti.<br /><br /> **1** = avviato.<br /><br /> **2** = ha avuto esito positivo.<br /><br /> **3** = in corso.<br /><br /> **4** = inattivo.<br /><br /> **5** = nuovo tentativo.<br /><br /> **6** = esito negativo.|  
|**last_sync_summary**|**sysname**|Ultimo messaggio dell'agente di distribuzione appena eseguito o in esecuzione. I possibili valori sono i seguenti.<br /><br /> **Avviato.**<br /><br /> **È stata completata.**<br /><br /> **In corso.**<br /><br /> **Inattivo.**<br /><br /> **Ripetizione dei tentativi.**<br /><br /> **Esito negativo.**|  
|**last_sync_time**|**datetime**|La data e ora in cui il *last_sync_summary* e *last_sync_status* colonne sono state aggiornate. Gli agenti di distribuzione pull o anonimi eseguiti come processi del servizio SQL Server Agent non aggiornano queste colonne. Vengono invece registrate informazioni cronologiche nella tabella di cronologia processo.|  
|**queue_server**|**sysname**|Solo per uso interno.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)  
  
  
