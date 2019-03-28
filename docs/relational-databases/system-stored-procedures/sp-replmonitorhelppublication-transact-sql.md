---
title: sp_replmonitorhelppublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublication_TSQL
- sp_replmonitorhelppublication
helpviewer_keywords:
- sp_replmonitorhelppublication
ms.assetid: 7928c50c-617f-41c5-9e0f-4e42e8be55dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 812ddd803d2a41695429902d6d8fc470ccef9576
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529217"
---
# <a name="spreplmonitorhelppublication-transact-sql"></a>sp_replmonitorhelppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sullo stato corrente per una o più pubblicazioni nel server di pubblicazione. Questa stored procedure, utilizzata per il monitoraggio della replica, viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replmonitorhelppublication [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db'   
    [ , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione viene monitorato lo stato dei quali. *server di pubblicazione* viene **sysname**, con un valore predefinito NULL. Se **null**, verranno restituite informazioni per tutti i server di pubblicazione che utilizzano il server di distribuzione.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del database pubblicato. *publisher_db* viene **sysname**, con un valore predefinito NULL. Se NULL, vengono restituite informazioni su tutti i database pubblicati nel server di pubblicazione.  
  
`[ @publication = ] 'publication'` Il nome della pubblicazione da monitorare. *pubblicazione* viene **sysname**, con un valore predefinito NULL.  
  
`[ @publication_type = ] publication_type` Se il tipo di pubblicazione. *publication_type* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Pubblicazione transazionale.|  
|**1**|Pubblicazione snapshot.|  
|**2**|Pubblicazione di tipo merge.|  
|NULL (predefinito)|La replica cerca di determinare il tipo di pubblicazione.|  
  
`[ @refreshpolicy = ] refreshpolicy` Solo uso interno.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher_db**|**sysname**|Nome del server di pubblicazione.|  
|**publication**|**sysname**|Nome di una pubblicazione.|  
|**publication_type**|**int**|Tipo di pubblicazione. I possibili valori sono i seguenti.<br /><br /> **0** = pubblicazione transazionale<br /><br /> **1** = pubblicazione snapshot<br /><br /> **2** = pubblicazione di tipo merge|  
|**status**|**int**|Stato massimo di tutti gli agenti di replica associati alla pubblicazione. I possibili valori sono i seguenti.<br /><br /> **1** = avviato<br /><br /> **2** = ha avuto esito positivo<br /><br /> **3** = in corso<br /><br /> **4** = inattivo<br /><br /> **5** = nuovo tentativo in corso<br /><br /> **6** = non è riuscita|  
|**warning**|**int**|Avviso correlato alla soglia massima generato da una sottoscrizione appartenente alla pubblicazione. Può essere il risultato OR logico di uno o più dei valori seguenti.<br /><br /> **1** = expiration - una sottoscrizione di una pubblicazione transazionale non sia stata sincronizzata entro la soglia di periodo di conservazione.<br /><br /> **2** = latency - il tempo necessario per replicare i dati da un server di pubblicazione transazionale al sottoscrittore supera la soglia, espresso in secondi.<br /><br /> **4** = mergeexpiration - una sottoscrizione a una pubblicazione di tipo merge non sia stata sincronizzata entro la soglia di periodo di conservazione.<br /><br /> **8** = mergefastrunduration - il tempo impiegato per completare la sincronizzazione di una sottoscrizione di tipo merge supera la soglia, espresso in secondi, tramite una connessione di rete veloce.<br /><br /> **16** = mergeslowrunduration - il tempo impiegato per completare la sincronizzazione di una sottoscrizione di tipo merge supera la soglia, espresso in secondi, tramite una connessione di rete lenta o remota.<br /><br /> **32** = mergefastrunspeed: la velocità di recapito delle righe durante la sincronizzazione di una sottoscrizione di tipo merge è minore della soglia, in righe al secondo, su una connessione di rete veloce.<br /><br /> **64** = mergeslowrunspeed: la velocità di recapito delle righe durante la sincronizzazione di una sottoscrizione di tipo merge è minore della soglia, in righe al secondo, su una connessione di rete lenta o remota.|  
|**worst_latency**|**int**|Latenza più alta, espressa in secondi, per le modifiche dei dati propagate dall'agente di lettura log o dagli agenti di distribuzione per una pubblicazione transazionale.|  
|**best_latency**|**int**|Latenza più bassa, espressa in secondi, per le modifiche dei dati propagate dall'agente di lettura log o dagli agenti di distribuzione per una pubblicazione transazionale.|  
|**average_latency**|**int**|Latenza media, espressa in secondi, per le modifiche dei dati propagate dall'agente di lettura log o dagli agenti di distribuzione per una pubblicazione transazionale.|  
|**last_distsync**|**datetime**|Data e ora dell'ultima esecuzione dell'agente di distribuzione.|  
|**retention**|**int**|Periodo di memorizzazione della pubblicazione.|  
|**latencythreshold**|**int**|Soglia della latenza impostato per la pubblicazione transazionale.|  
|**expirationthreshold**|**int**|Soglia della scadenza impostato per la pubblicazione di tipo merge.|  
|**agentnotrunningthreshold**|**int**|Soglia impostato per il periodo più lungo di mancata esecuzione di un agente.|  
|**subscriptioncount**|**int**|Numero di sottoscrizioni a una pubblicazione.|  
|**runningdistagentcount**|**int**|Numero di agenti di distribuzione in esecuzione per la pubblicazione.|  
|**snapshot_agentname**|**sysname**|Nome del processo dell'agente snapshot per la pubblicazione.|  
|**logreader_agentname**|**sysname**|Nome del processo dell'agente di lettura log per la pubblicazione transazionale.|  
|**qreader_agentname**|**sysname**|Nome del processo dell'agente di lettura coda per una pubblicazione transazionale che supporta l'aggiornamento in coda.|  
|**worst_runspeedPerf**|**int**|Tempo di sincronizzazione più lungo per la pubblicazione di tipo merge.|  
|**best_runspeedPerf**|**int**|Tempo minimo di sincronizzazione per la pubblicazione di tipo merge.|  
|**average_runspeedPerf**|**int**|Tempo medio di sincronizzazione per la pubblicazione di tipo merge.|  
|**retention_period_unit**|**int**|È l'unità utilizzata per esprimere *conservazione*.|  
|**publisher**|**sysname**|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite cui viene effettuata la pubblicazione.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_replmonitorhelppublication** viene utilizzato con tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **db_owner** oppure **replmonitor** ruolo predefinito del database nel database di distribuzione possono eseguire **sp_replmonitorhelppublication**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare la replica a livello di programmazione](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
