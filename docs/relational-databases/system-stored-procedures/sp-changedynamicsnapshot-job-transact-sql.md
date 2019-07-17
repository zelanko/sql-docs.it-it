---
title: sp_changedynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7fc3b5e8fb8b6bc8d5d98d14ede475b8f5a3f75c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110853"
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di modificare il processo di agente che genera lo snapshot per una sottoscrizione di una pubblicazione con un filtro di riga con parametri. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changedynamicsnapshot_job [ @publication = ] 'publication'  
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'` Il nome del processo di snapshot viene modificato. *dynamic_snapshot_jobname*viene **sysname**, con il valore predefinito di N '% s'. Se *dynamic_snapshot_jobid* è specificato, è necessario usare il valore predefinito per *dynamic_snapshot_jobname*.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'` L'ID del processo di snapshot viene modificato. *dynamic_snapshot_jobid* viene **uniqueidentifier**, con valore predefinito è NULL. Se *dynamic_snapshot_jobname*è specificato, è necessario usare il valore predefinito per *dynamic_snapshot_jobid*.  
  
`[ @frequency_type = ] frequency_type` È la frequenza di pianificazione dell'agente. *frequency_type* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Su richiesta|  
|**4**|Ogni giorno|  
|**8**|Settimanale|  
|**16**|Mensile|  
|**32**|Mensile relativa|  
|**64**|Avvio automatico|  
|**128**|Periodica|  
|NULL (predefinito)||  
  
`[ @frequency_interval = ] frequency_interval` Giorni in cui viene eseguito l'agente. *frequency_interval* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Domenica|  
|**2**|Lunedì|  
|**3**|Martedì|  
|**4**|Mercoledì|  
|**5**|Giovedì|  
|**6**|Venerdì|  
|**7**|Sabato|  
|**8**|Day|  
|**9**|Giorni feriali|  
|**10**|Giorni festivi|  
|NULL (predefinito)||  
  
`[ @frequency_subday = ] frequency_subday` È la frequenza di ripianificazione durante il periodo definito. *frequency_subday* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4**|Minuto|  
|**8**|Ora|  
|NULL (predefinito)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, con un valore predefinito è NULL.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` È la data in cui viene eseguito l'agente di Merge. Questo parametro viene utilizzato quando *frequency_type* è impostata su **32** (frequenza mensile relativa). *frequency_relative_interval* viene **int**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
|NULL (predefinito)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_start_date = ] active_start_date` È la data della prima l'agente di Merge pianificata, nel formato YYYYMMDD. *active_start_date* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_end_date = ] active_end_date` La data di arresto dell'agente di Merge viene pianificata, nel formato aaaammgg. *active_end_date* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` È l'ora del giorno quando l'agente di Merge è primo pianificata, nel formato HHMMSS. *active_start_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` L'ora del giorno quando si arresta l'agente di Merge viene pianificata, nel formato HHMMSS. *active_end_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
`[ @job_login = ] 'job_login'` È il [!INCLUDE[msCoName](../../includes/msconame-md.md)] Account Windows con cui viene eseguito l'agente Snapshot durante la generazione dello snapshot per una sottoscrizione usando un filtro di riga con parametri. *job_login* viene **nvarchar(257)** , con un valore predefinito NULL.  
  
`[ @job_password = ] 'job_password'` Password per l'Account di Windows con cui viene eseguito l'agente Snapshot durante la generazione dello snapshot per una sottoscrizione tramite un filtro di riga con parametri. *job_password* viene **nvarchar(257)** , con un valore predefinito NULL.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changedynamicsnapshot_job** viene utilizzata nella replica di tipo merge per le pubblicazioni con filtri di riga con parametri.  
  
 Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_changedynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Snapshot per pubblicazioni di tipo merge con filtri con parametri](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
  
