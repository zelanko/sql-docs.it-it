---
title: sp_addqreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addqreader_agent_TSQL
- sp_addqreader_agent
helpviewer_keywords:
- sp_addqreader_agent
ms.assetid: dc9f591a-e67e-4ba8-bf47-defd5eda0822
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a1e37004d15d8758160edb3558b2a69d30dae54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031017"
---
# <a name="spaddqreaderagent-transact-sql"></a>sp_addqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un agente di lettura coda per un server di distribuzione specificato. Questa stored procedure viene eseguita nel database di distribuzione del server di distribuzione o nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addqreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name'  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_login = ] 'job_login'` Account di accesso per il [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows dell'account con cui verrà eseguito l'agente. *job_login* viene **nvarchar(257)** , non prevede alcun valore predefinito. Questo account di Windows viene sempre utilizzato per le connessioni dell'agente al server di distribuzione.  
  
`[ @job_password = ] 'job_password'` È la password per l'account di Windows con cui viene eseguito l'agente. *job_password* viene **sysname**, non prevede alcun valore predefinito.  
  
> [!IMPORTANT]  
>  Non archiviare informazioni di autenticazione in file script. Per una sicurezza ottimale, i nomi e le password degli account di accesso dovrebbero essere passati in fase di esecuzione.  
  
`[ @job_name = ] 'job_name'` È il nome di un processo dell'agente esistente. *nome_processo* viene **sysname**, con un valore predefinito NULL. Questo parametro viene specificato solo quando l'agente viene creato con un processo esistente anziché con un nuovo processo creato (impostazione predefinita).  
  
`[ @frompublisher = ] frompublisher` Specifica se la procedura viene eseguita nel server di pubblicazione. *frompublisher* è di tipo bit e il valore predefinito **0**. Un valore pari **1** significa che la procedura viene eseguita dal server di pubblicazione nel database di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_addqreader_agent** viene utilizzata nella replica transazionale.  
  
 **sp_addqreader_agent** deve essere eseguita almeno una volta in un server di distribuzione che supporta in coda l'aggiornamento dopo [sp_adddistributiondb](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) ma prima [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
 Il processo di agente di lettura coda viene rimosso quando si esegue [sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_addqreader_agent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare le sottoscrizioni aggiornabili per le pubblicazioni transazionali](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Aggiornare gli script di replica &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_changeqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md)   
 [sp_helpqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)  
  
  
