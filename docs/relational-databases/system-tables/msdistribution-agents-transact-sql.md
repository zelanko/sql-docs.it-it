---
title: MSdistribution_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_agents_TSQL
- MSdistribution_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_agents system table
ms.assetid: 0e8f0653-1351-41d1-95d2-40f6d5a050ca
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5c138f2e97bf80f00f77c519bb4b9467c715f95b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907409"
---
# <a name="msdistributionagents-transact-sql"></a>MSdistribution_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSdistribution_agents** tabella contiene una riga per ogni agente di distribuzione in esecuzione nel server di distribuzione locale. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID dell'agente di distribuzione.|  
|**name**|**nvarchar(100)**|Nome dell'agente di distribuzione.|  
|**publisher_database_id**|**int**|ID del database del server di pubblicazione.|  
|**publisher_id**|**smallint**|ID del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione.|  
|**subscriber_id**|**smallint**|ID del Sottoscrittore, utilizzato solo da agenti noti. Per gli agenti anonimi questa colonna è riservata.|  
|**subscriber_db**|**sysname**|Nome del database di sottoscrizione.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push.<br /><br /> **1** = pull.<br /><br /> **2** = anonimo.|  
|**local_job**|**bit**|Indica se è presente un processo di SQL Server Agent nel server di distribuzione locale.|  
|**job_id**|**binary(16)**|Numero di identificazione del processo.|  
|**subscription_guid**|**binary(16)**|ID delle sottoscrizioni dell'agente.|  
|**profile_id**|**int**|L'ID di configurazione di [MSagent_profiles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) tabella.|  
|**anonymous_subid**|**uniqueidentifier**|ID di un agente anonimo.|  
|**subscriber_name**|**sysname**|Nome del Sottoscrittore utilizzato solo dagli agenti anonimi.|  
|**virtual_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**anonymous_agent_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**creation_date**|**datetime**|Data e ora in cui è stato creato l'agente di distribuzione o di merge.|  
|**queue_id**|**sysname**|Identificatore per l'individuazione della coda per le sottoscrizioni ad aggiornamento in coda. Per le sottoscrizioni non impostate per l'aggiornamento in coda il valore è NULL. Per le pubblicazioni basate sul servizio di accodamento messaggi [!INCLUDE[msCoName](../../includes/msconame-md.md)], corrisponde a un valore GUID che identifica in modo univoco la coda da utilizzare per la sottoscrizione. Per le pubblicazioni in coda basate su SQL Server, la colonna contiene il valore **SQL**.<br /><br /> Nota: Usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] Accodamento messaggi è stato deprecato e non è più supportata.|  
|**queue_status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offload_enabled**|**bit**|Indica se è possibile attivare l'agente in remoto.<br /><br /> **0** specifica che l'agente non può essere attivato in remoto.<br /><br /> **1** specifica che l'agente verrà attivato in remoto nel computer remoto specificato nella *offload_server* proprietà.|  
|**offload_server**|**sysname**|Nome di rete del server da utilizzare per l'attivazione remota dell'agente.|  
|**dts_package_name**|**sysname**|Nome del pacchetto DTS. Ad esempio, per un pacchetto denominato **DTSPub_Package**, specificare `@dts_package_name = N'DTSPub_Package'`.|  
|**dts_package_password**|**nvarchar(524)**|Password del pacchetto.|  
|**dts_package_location**|**int**|Posizione del pacchetto. La posizione del pacchetto può essere **distributore** oppure **sottoscrittore**.|  
|**sid**|**varbinary(85)**|ID di sicurezza (SID) dell'agente di distribuzione o di merge durante la prima esecuzione dell'agente.|  
|**queue_server**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**subscriber_security_mode**|**smallint**|Modalità di sicurezza utilizzata dall'agente per la connessione al Sottoscrittore. I possibili valori sono i seguenti:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticazione di SQL Server<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] l'autenticazione di Windows.|  
|**subscriber_login**|**sysname**|Account di accesso utilizzato per la connessione al Sottoscrittore.|  
|**subscriber_password**|**nvarchar(524)**|Valore crittografato della password utilizzata per la connessione al Sottoscrittore.|  
|**reset_partial_snapshot_progress**|**bit**|Indica se uno snapshot scaricato parzialmente deve essere scartato in modo da consentire il riavvio dell'intero processo di snapshot.|  
|**job_step_uid**|**uniqueidentifier**|ID univoco del processo di SQL Server Agent passaggio in cui l'agente viene avviato.|  
|**subscriptionstreams**|**tinyint**|Imposta il numero di connessioni consentite per ogni agente di distribuzione per l'applicazione parallela di più batch di modifiche in un Sottoscrittore. È supportato un intervallo di valori compreso tra 1 e 64.|  
|**memory_optimized**|**bit**|1 indica il sottoscrittore può essere utilizzato per le tabelle ottimizzate per la memoria.|  
|**job_login**|**sysname**||  
|**job_password**|**nvarchar(524)**||  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
