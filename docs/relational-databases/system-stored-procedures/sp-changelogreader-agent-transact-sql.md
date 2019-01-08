---
title: sp_changelogreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changelogreader_agent
- sp_changelogreader_agent_TSQL
helpviewer_keywords:
- sp_changelogreader_agent
ms.assetid: 929b2fa7-1267-41d0-8b69-e9ab26a62c0f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 529ad27a4ebc220f8d17a58e9c05605e785237a7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807723"
---
# <a name="spchangelogreaderagent-transact-sql"></a>sp_changelogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Modifica le proprietà di sicurezza di un agente di lettura log. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]  
>  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changelogreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@job_login**=] **'***job_login***'**  
 È l'account di accesso per l'account con cui viene eseguito l'agente. *job_login* viene **nvarchar(257)**, con un valore predefinito è NULL. SQL Database istanza gestita di Azure, usare un account di SQL Server. *Non può essere modificato per non -* [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *server di pubblicazione.*  
  
 [ **@job_password**=] **'***job_password***'**  
 È la password per l'account con cui viene eseguito l'agente. *job_password* viene **sysname**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 Modalità di sicurezza utilizzata dall'agente per la connessione al server di pubblicazione. *publisher_security_mode* viene **smallint**, con un valore predefinito è NULL. **0** specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, e **1** specifica l'autenticazione di Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] **'***publisher_login***'**  
 Account di accesso utilizzato per la connessione al server di pubblicazione. *publisher_login* viene **sysname**, con un valore predefinito è NULL. *publisher_login* deve essere specificato quando *publisher_security_mode* viene **0**. Se *publisher_login* è NULL e *publisher_security_mode* viene **1**, quindi l'account Windows specificato nella *job_login* viene usato quando la connessione al server di pubblicazione.  
  
 [ **@publisher_password**=] **'***publisher_password***'**  
 Password utilizzata per la connessione al server di pubblicazione. *publisher_password* viene **sysname**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  Non usare una password vuota. Usare una password complessa. Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
 [ **@publisher**=] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL. Questo parametro è supportato solo per i server di pubblicazione non SQL Server.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changelogreader_agent** viene utilizzata nella replica transazionale.  
  
 **sp_changelogreader_agent** viene utilizzato per modificare l'account di Windows con cui viene eseguito un agente di lettura Log. È possibile cambiare la password di un account di accesso di Windows esistente oppure specificare un nuovo account di accesso di Windows e la password.  
  
 Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_changelogreader_agent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)   
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
