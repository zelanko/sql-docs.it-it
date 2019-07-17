---
title: sp_addpushsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords:
- sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
author: stevestein
ms.author: sstein
ms.openlocfilehash: b0d17e4bc16340e0e913f48549f697eaabc8ec1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031053"
---
# <a name="spaddpushsubscriptionagent-transact-sql"></a>sp_addpushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Aggiunge un nuovo processo di agente pianificato per sincronizzare una sottoscrizione push di una pubblicazione transazionale. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]  
>  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addpushsubscription_agent [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @distribution_job_name = ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @subscriber_provider = ] 'subscriber_provider' ]   
    [ , [ @subscriber_datasrc = ] 'subscriber_datasrc' ]   
    [ , [ @subscriber_location = ] 'subscriber_location' ]  
    [ , [ @subscriber_provider_string = ] 'subscriber_provider_string' ]   
    [ , [ @subscriber_catalog = ] 'subscriber_catalog' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'` È il nome del database di sottoscrizione. *subscriber_db* viene **sysname**, con un valore predefinito è NULL. Per un non - SQL Server sottoscrittore, specificare un valore pari **(destinazione predefinita)** per *subscriber_db*.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode` È la modalità di sicurezza da utilizzare quando ci si connette a un sottoscrittore durante la sincronizzazione. *subscriber_security_mode* viene **int**, con un valore predefinito è 1. **0** specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. **1** specifica l'autenticazione di Windows.  
  
> [!IMPORTANT]  
>  Per le sottoscrizioni ad aggiornamento in coda utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le connessioni ai Sottoscrittori e specificare un account diverso per la connessione a ogni Sottoscrittore. Per tutte le altre sottoscrizioni utilizzare l'autenticazione di Windows.  
  
`[ @subscriber_login = ] 'subscriber_login'` È l'account di accesso da utilizzare quando ci si connette a un sottoscrittore durante la sincronizzazione. *subscriber_login* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subscriber_password = ] 'subscriber_password'` È la password del sottoscrittore. *subscriber_password* è obbligatorio se *subscriber_security_mode* è impostata su **0**. *subscriber_password* viene **sysname**, con un valore predefinito è NULL. Le password del Sottoscrittore vengono crittografate automaticamente.  
  
> [!IMPORTANT]  
>  Non usare una password vuota. Usare una password complessa. Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
`[ @job_login = ] 'job_login'` È l'account di accesso per l'account con cui viene eseguito l'agente. Usare un account di SQL Server in istanza gestita di Azure SQL Database. *job_login* viene **nvarchar(257)** , con un valore predefinito NULL. Questo account di Windows viene sempre utilizzato per le connessioni dell'agente al server di distribuzione e per le connessioni al Sottoscrittore quando si utilizza l'autenticazione integrata di Windows.  
  
`[ @job_password = ] 'job_password'` È la password per l'account con cui viene eseguito l'agente. *job_password* viene **sysname**, non prevede alcun valore predefinito.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
`[ @job_name = ] 'job_name'` È il nome di un processo dell'agente esistente. *nome_processo* viene **sysname**, con un valore predefinito NULL. Questo parametro viene specificato solo quando la sottoscrizione verrà sincronizzata mediante un processo esistente anziché un nuovo processo creato (impostazione predefinita). Se non si è un membro del **sysadmin** ruolo predefinito del server, è necessario specificare *job_login* e *job_password* quando si specifica *job_name*.  
  
`[ @frequency_type = ] frequency_type` È la frequenza con cui pianificare l'agente di distribuzione. *frequency_type* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Su richiesta|  
|**4**|Ogni giorno|  
|**8**|Settimanale|  
|**16**|Mensile|  
|**32**|Mensile relativa|  
|**64** (impostazione predefinita)|Avvio automatico|  
|**128**|Periodica|  
  
> [!NOTE]  
>  Se si specifica un valore di **64** fa sì che l'agente di distribuzione per l'esecuzione in modalità continua. Corrisponde all'impostazione di **-continua** parametro per l'agente. Per altre informazioni, vedere [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
`[ @frequency_interval = ] frequency_interval` Il valore da applicare alla frequenza impostata *frequency_type*. *frequency_interval* viene **int**, con un valore predefinito è 1.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` È la data dell'agente di distribuzione. Questo parametro viene utilizzato quando *frequency_type* è impostata su **32** (frequenza mensile relativa). *frequency_relative_interval* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1** (impostazione predefinita)|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, con un valore predefinito è 0.  
  
`[ @frequency_subday = ] frequency_subday` È la frequenza di ripianificazione durante il periodo definito. *frequency_subday* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4** (impostazione predefinita)|Minuto|  
|**8**|Ora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, con un valore predefinito è 5.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` È l'ora del giorno quando l'agente di distribuzione è primo pianificata, nel formato HHMMSS. *active_start_time_of_day* viene **int**, con un valore predefinito è 0.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` L'ora del giorno quando si arresta l'agente di distribuzione è pianificata, nel formato HHMMSS. *active_end_time_of_day* viene **int**, con un valore predefinito è 235959.  
  
`[ @active_start_date = ] active_start_date` È la data della prima l'agente di distribuzione pianificata, nel formato YYYYMMDD. *active_start_date* viene **int**, con un valore predefinito è 0.  
  
`[ @active_end_date = ] active_end_date` La data di arresto dell'agente di distribuzione è pianificata, nel formato aaaammgg. *active_end_date* viene **int**, con un valore predefinito è 99991231.  
  
`[ @dts_package_name = ] 'dts_package_name'` Specifica il nome del pacchetto Data Transformation Services (DTS). *dts_package_name* è un **sysname** con valore predefinito è NULL. Per specificare, ad esempio, il nome di pacchetto `DTSPub_Package`, il parametro deve essere `@dts_package_name = N'DTSPub_Package'`.  
  
`[ @dts_package_password = ] 'dts_package_password'` Specifica la password necessaria per eseguire il pacchetto. *dts_package_password* viene **sysname** con valore predefinito è NULL.  
  
> [!NOTE]  
>  È necessario specificare una password se *dts_package_name* è specificato.  
  
`[ @dts_package_location = ] 'dts_package_location'` Specifica il percorso del pacchetto. *dts_package_location* è un **nvarchar (12)** , con un valore predefinito del server di distribuzione. La posizione del pacchetto può essere **distributore** oppure **sottoscrittore**.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` È se la sottoscrizione può essere sincronizzata tramite [!INCLUDE[msCoName](../../includes/msconame-md.md)] Gestione sincronizzazione. *enabled_for_syncmgr* viene **nvarchar(5**, con un valore predefinito è FALSE. Se **false**, la sottoscrizione non è registrata con Gestione sincronizzazione Microsoft. Se **true**, la sottoscrizione viene registrata con Gestione sincronizzazione e può essere sincronizzata senza avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
`[ @distribution_job_name = ] 'distribution_job_name'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito NULL.  
  
`[ @subscriber_provider = ] 'subscriber_provider'` È l'identificatore univoco a livello di codice (PROGID) con cui il provider OLE DB per non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origine dati viene registrata. *subscriber_provider* viene **sysname**, con valore predefinito è NULL. *subscriber_provider* deve essere univoco per il provider OLE DB installato nel server di distribuzione. *subscriber_provider* è supportata solo per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori.  
  
`[ @subscriber_datasrc = ] 'subscriber_datasrc'` È il nome dell'origine dati riconosciuto dal provider OLE DB. *subscriber_datasrc* viene **nvarchar (4000)** , con un valore predefinito NULL. *subscriber_datasrc* viene passato come proprietà DBPROP_INIT_DATASOURCE per inizializzare il provider OLE DB. *subscriber_datasrc* è supportata solo per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori.  
  
`[ @subscriber_location = ] 'subscriber_location'` È il percorso del database riconosciuto dal provider OLE DB. *subscriber_location* viene **nvarchar (4000)** , con un valore predefinito NULL. *subscriber_location* viene passato come proprietà DBPROP_INIT_LOCATION per inizializzare il provider OLE DB. *subscriber_location* è supportata solo per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori.  
  
`[ @subscriber_provider_string = ] 'subscriber_provider_string'` È la stringa di connessione specifica del provider OLE DB che identifica l'origine dati. *subscriber_provider_string* viene **nvarchar (4000)** , con un valore predefinito NULL. *subscriber_provider_string* viene passato a IDataInitialize o impostato come proprietà DBPROP_INIT_PROVIDERSTRING per inizializzare il provider OLE DB. *subscriber_provider_string* è supportata solo per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori.  
  
`[ @subscriber_catalog = ] 'subscriber_catalog'` È il catalogo da utilizzare durante la connessione al provider OLE DB. *subscriber_catalog* viene **sysname**, con valore predefinito è NULL. *subscriber_catalog* viene passato come proprietà DBPROP_INIT_CATALOG per inizializzare il provider OLE DB. *subscriber_catalog* è supportata solo per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addpushsubscription_agent** viene utilizzata nella replica snapshot e transazionale.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addpushsubscription_agent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Creare una sottoscrizione per un Sottoscrittore non SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Sottoscrivere le pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
