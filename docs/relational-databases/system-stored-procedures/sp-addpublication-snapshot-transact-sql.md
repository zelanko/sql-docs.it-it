---
title: sp_addpublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4fbba559eceae58483419c0f1e3826b9db79bef5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061828"
---
# <a name="spaddpublicationsnapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Crea l'agente snapshot per la pubblicazione specificata. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]  
>  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @frequency_type = ] frequency_type` È la frequenza con cui viene eseguito l'agente Snapshot. *frequency_type* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Singola occorrenza.|  
|**4** (impostazione predefinita)|Giornaliera.|  
|**8**|Settimanale.|  
|**16**|Mensile.|  
|**32**|Mensile relativa, in base all'intervallo di frequenza.|  
|**64**|All'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|**128**|Quando il computer è inattivo|  
  
`[ @frequency_interval = ] frequency_interval` Il valore da applicare alla frequenza impostata *frequency_type*. *frequency_interval* viene **int**, e può essere uno dei valori seguenti.  
  
|Valore di frequency_type|Effetto su frequency_interval|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval* risulta inutilizzato.|  
|**4** (impostazione predefinita)|Ogni *frequency_interval* giorni, con un valore predefinito di ogni giorno.|  
|**8**|*frequency_interval* corrisponde a uno o più dei valori seguenti (combinato con un [ &#124; (OR bit per bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) operatore logico):<br /><br /> **1** = domenica&#124;<br /><br /> **2** = lunedì&#124;<br /><br /> **4** = martedì&#124;<br /><br /> **8** = mercoledì&#124;<br /><br /> **16** = giovedì&#124;<br /><br /> **32** = venerdì&#124;<br /><br /> **64** = sabato|  
|**16**|Nel *frequency_interval* giorno del mese.|  
|**32**|*frequency_interval* è uno dei seguenti:<br /><br /> **1** = domenica&#124;<br /><br /> **2** = lunedì&#124;<br /><br /> **3** = martedì&#124;<br /><br /> **4** = mercoledì&#124;<br /><br /> **5** = giovedì&#124;<br /><br /> **6** = venerdì&#124;<br /><br /> **7** = sabato&#124;<br /><br /> **8** = giorno&#124;<br /><br /> **9** = giorno feriale&#124;<br /><br /> **10** = giorno festivo|  
|**64**|*frequency_interval* risulta inutilizzato.|  
|**128**|*frequency_interval* risulta inutilizzato.|  
  
`[ @frequency_subday = ] frequency_subday` È l'unità per *freq_subday_interval*. *frequency_subday* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4** (impostazione predefinita)|Minuto|  
|**8**|Ora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, con un valore predefinito è 5, ovvero ogni 5 minuti.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` È la data che viene eseguito l'agente Snapshot. *frequency_relative_interval* viene **int**, con un valore predefinito è 1.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, con un valore predefinito è 0.  
  
`[ @active_start_date = ] active_start_date` È la data della prima l'agente Snapshot pianificata, nel formato YYYYMMDD. *active_start_date* viene **int**, con un valore predefinito è 0.  
  
`[ @active_end_date = ] active_end_date` La data di arresto dell'agente Snapshot viene pianificata, nel formato aaaammgg. *active_end_date* viene **int**, con un valore predefinito è 99991231, che corrisponde al 31 dicembre 9999.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` È l'ora del giorno quando l'agente Snapshot è primo pianificata, nel formato HHMMSS. *active_start_time_of_day* viene **int**, con un valore predefinito è 0.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` L'ora del giorno quando si arresta l'agente Snapshot viene pianificata, nel formato HHMMSS. *active_end_time_of_day* viene **int**, con un valore predefinito è 235959, che significa 59: 11:59 P.M. nel formato 24 ore.  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'` È il nome di un processo dell'agente Snapshot esistente se viene utilizzato un processo esistente. *snapshot_agent_name* viene **nvarchar(100)** con un valore predefinito NULL. Questo parametro è per uso interno e non deve essere specificato per la creazione di una nuova pubblicazione. Se *snapshot_agent_name* è specificato, quindi *job_login* e *job_password* deve essere NULL.  
  
`[ @publisher_security_mode = ] publisher_security_mode` La modalità di sicurezza utilizzata dall'agente quando ci si connette al server di pubblicazione. *publisher_security_mode* viene **smallint**, con un valore predefinito è 1. **0** specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, e **1** specifica l'autenticazione di Windows. Un valore pari **0** deve essere specificato per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` L'account di accesso utilizzata per la connessione al server di pubblicazione. *publisher_login* viene **sysname**, con un valore predefinito è NULL. *publisher_login* deve essere specificato quando *publisher_security_mode* viene **0**. Se *publisher_login* è NULL e *publisher_security_mode* viene **1**, quindi l'account specificato nella *job_login* verrà usato quando la connessione al server di pubblicazione.  
  
`[ @publisher_password = ] 'publisher_password'` Password utilizzata durante la connessione al server di pubblicazione. *publisher_password* viene **sysname**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  Non archiviare informazioni di autenticazione in file script. Per migliorare la sicurezza, si consiglia di specificare nomi e password di accesso in fase di esecuzione.  
  
`[ @job_login = ] 'job_login'` È l'account di accesso per l'account con cui viene eseguito l'agente. SQL Database istanza gestita di Azure, usare un account di SQL Server. *job_login* viene **nvarchar(257)** , con un valore predefinito è NULL. Questo account viene sempre utilizzato per le connessioni dell'agente al server di distribuzione. È necessario specificare questo parametro per la creazione di un nuovo processo per l'agente snapshot.  
  
> [!NOTE]
>  Per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione deve essere l'account di accesso specificato [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md).  
  
`[ @job_password = ] 'job_password'` È la password per l'account di Windows con cui viene eseguito l'agente. *job_password* viene **sysname**, non prevede alcun valore predefinito. È necessario specificare questo parametro per la creazione di un nuovo processo per l'agente snapshot.  
  
> [!IMPORTANT]  
>  Non archiviare informazioni di autenticazione in file script. Per migliorare la sicurezza, si consiglia di specificare nomi e password di accesso in fase di esecuzione.  
  
`[ @publisher = ] 'publisher'` Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere usata durante la creazione di un agente Snapshot in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addpublication_snapshot** viene utilizzata nella replica snapshot, la replica transazionale e di tipo merge.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addpublication_snapshot**.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Creare e applicare lo snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
