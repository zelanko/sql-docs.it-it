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
ms.openlocfilehash: 4db6a29d92fe093e9704f88fcc528c9fa687ccff
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768953"
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'`Nome della pubblicazione. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`Nome del processo di snapshot da modificare. *dynamic_snapshot_jobname*è di **tipo sysname**e il valore predefinito è n'%'. Se viene specificato *dynamic_snapshot_jobid* , è necessario usare il valore predefinito per *dynamic_snapshot_jobname*.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`ID del processo di snapshot da modificare. *dynamic_snapshot_jobid* è di tipo **uniqueidentifier**e il valore predefinito è null. Se viene specificato *dynamic_snapshot_jobname*, è necessario usare il valore predefinito per *dynamic_snapshot_jobid*.  
  
`[ @frequency_type = ] frequency_type`Frequenza con cui pianificare l'agente. *frequency_type* è di **tipo int**. i possibili valori sono i seguenti.  
  
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
  
`[ @frequency_interval = ] frequency_interval`Giorni in cui viene eseguito l'agente. *frequency_interval* è di **tipo int**. i possibili valori sono i seguenti.  
  
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
  
`[ @frequency_subday = ] frequency_subday`Frequenza di ripianificazione durante il periodo definito. *frequency_subday* è di **tipo int**. i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4**|Minuto|  
|**8**|Ora|  
|NULL (predefinito)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`Intervallo di *frequency_subday*. *frequency_subday_interval* è di **tipo int**e il valore predefinito è null.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`Data di esecuzione del agente di merge. Questo parametro viene utilizzato quando *frequency_type* è impostato su **32** (mensile relativo). *frequency_relative_interval* è di **tipo int**. i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
|NULL (predefinito)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* è di **tipo int**e il valore predefinito è null.  
  
`[ @active_start_date = ] active_start_date`Data della prima pianificazione del agente di merge, formattata come AAAAMMGG. *active_start_date* è di **tipo int**e il valore predefinito è null.  
  
`[ @active_end_date = ] active_end_date`Data di arresto della agente di merge pianificata, formattata come AAAAMMGG. *active_end_date* è di **tipo int**e il valore predefinito è null.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`Ora del giorno in cui il agente di merge viene pianificato per la prima volta, formattato come HHMMSS. *active_start_time_of_day* è di **tipo int**e il valore predefinito è null.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`Ora del giorno in cui l'agente di merge viene arrestata, formattata come HHMMSS. *active_end_time_of_day* è di **tipo int**e il valore predefinito è null.  
  
`[ @job_login = ] 'job_login'`Account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per l'esecuzione del agente di snapshot durante la generazione dello snapshot per una sottoscrizione tramite un filtro di riga con parametri. *job_login* è di **tipo nvarchar (257)** e il valore predefinito è null.  
  
`[ @job_password = ] 'job_password'`Password per l'account di Windows con cui viene eseguito il agente di snapshot durante la generazione dello snapshot per una sottoscrizione utilizzando un filtro di riga con parametri. *job_password* è di **tipo nvarchar (257)** e il valore predefinito è null.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_changedynamicsnapshot_job** viene utilizzato nella replica di tipo merge per le pubblicazioni con filtri di riga con parametri.  
  
 Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_changedynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Snapshot per pubblicazioni di tipo merge con filtri con parametri](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
  
