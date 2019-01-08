---
title: sp_addlogreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addlogreader_agent
- sp_addlogreader_agent_TSQL
helpviewer_keywords:
- sp_addlogreader_agent
ms.assetid: d83096b9-96ee-4789-bde0-940d4765b9ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6fdec3ada9bec27f6ecca2ea6a888d01640f6edb
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210840"
---
# <a name="spaddlogreaderagent-transact-sql"></a>sp_addlogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un agente di lettura log per un database specificato. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]  
>  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addlogreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@job_login**=] **'**_job_login_**'**  
 Account di accesso per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per l'esecuzione dell'agente. *job_login* viene **nvarchar(257)**, con un valore predefinito NULL. Questo account di Windows viene sempre utilizzato per le connessioni dell'agente al server di distribuzione.  
  
> [!NOTE]
>  Per non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione, deve essere l'account di accesso specificato [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md).  
  
 [ **@job_password**=] **'**_job_password_**'**  
 Password dell'account di Windows utilizzato per l'esecuzione dell'agente. *job_password* viene **sysname**, con un valore predefinito NULL.  
  
> [!IMPORTANT]  
>  Non archiviare informazioni di autenticazione in file script. Per una sicurezza ottimale, i nomi e le password degli account di accesso dovrebbero essere passati in fase di esecuzione.  
  
 [ **@job_name**=] **'**_job_name_**'**  
 Nome di un processo esistente dell'agente. *nome_processo* viene **sysname**, con un valore predefinito NULL. Questo parametro viene specificato solo quando l'agente viene avviato con un processo esistente anziché con un nuovo processo creato (impostazione predefinita).  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 Modalità di sicurezza utilizzata dall'agente per la connessione al server di pubblicazione. *publisher_security_mode* viene **smallint**, il valore predefinito è **1**. **0** specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, e **1** specifica l'autenticazione di Windows. Un valore pari **0** deve essere specificato per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione.  
  
 [ **@publisher_login**=] **'**_publisher_login_**'**  
 Account di accesso utilizzato per la connessione al server di pubblicazione. *publisher_login* viene **sysname**, con un valore predefinito è NULL. *publisher_login* deve essere specificato quando *publisher_security_mode* viene **0**. Se *publisher_login* è NULL e *publisher_security_mode* viene **1**, quindi l'account Windows specificato nella *job_login* verrà usato Quando ci si connette al server di pubblicazione.  
  
 [ **@publisher_password**=] **'**_publisher_password_**'**  
 Password utilizzata per la connessione al server di pubblicazione. *publisher_password* viene **sysname**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  Non archiviare informazioni di autenticazione in file script. Per una sicurezza ottimale, i nomi e le password degli account di accesso dovrebbero essere passati in fase di esecuzione.  
  
 [ **@publisher**=] **'**_editore_**'**  
 È il nome del non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Non specificare questo parametro per un server di pubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addlogreader_agent** viene utilizzata nella replica transazionale.  
  
 È necessario eseguire **sp_addlogreader_agent** per aggiungere un agente di lettura Log se è stato aggiornato un database in cui è stato abilitato per la replica in questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima della creazione di una pubblicazione che utilizza tale database.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_addlogreader_agent**.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addlogreader-agent-tr_1.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changelogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
