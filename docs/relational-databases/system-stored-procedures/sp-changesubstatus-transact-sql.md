---
title: sp_changesubstatus (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubstatus
- sp_changesubstatus_TSQL
helpviewer_keywords:
- sp_changesubstatus
ms.assetid: 9370e47a-d128-4f15-9224-1c3642770c39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa9452d7dc2e611b1b581c12cf33e88950eacc2a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212340"
---
# <a name="spchangesubstatus-transact-sql"></a>sp_changesubstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica lo stato di un Sottoscrittore esistente. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changesubstatus [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
        , [ @status = ] 'status'  
    [ , [ @previous_status = ] 'previous_status' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
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
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @distribution_jobid = ] distribution_jobid ]  
    [ , [ @from_auto_sync = ] from_auto_sync ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @offloadagent= ] remote_agent_activation ]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] dts_package_location ]  
    [ , [ @skipobjectactivation = ] skipobjectactivation  
  [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, il valore predefinito è **%**. Se *publication* non viene specificato, tutte le pubblicazioni sono interessate.  
  
 [  **@article=**] **'***articolo***'**  
 Nome dell'articolo. Deve essere univoco all'interno della pubblicazione. *articolo* viene **sysname**, il valore predefinito è **%**. Se *articolo* non viene specificato, tutti gli articoli sono interessati.  
  
 [  **@subscriber=**] **'***sottoscrittore***'**  
 Nome del Sottoscrittore di cui si desidera modificare lo stato. *Sottoscrittore* viene **sysname**, il valore predefinito è **%**. Se *sottoscrittore* non viene specificato, lo stato viene modificato per tutti i sottoscrittori per l'articolo specificato.  
  
 [  **@status =**] **'***stato***'**  
 Stato della sottoscrizione nella **syssubscriptions** tabella. *lo stato* viene **sysname**e non prevede alcun valore predefinito, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Attiva**|Il Sottoscrittore è sincronizzato e in fase di ricezione dei dati.|  
|**inattivo**|Alla voce relativa al Sottoscrittore non è associata alcuna sottoscrizione.|  
|**sottoscritto**|Il Sottoscrittore richiede dati, ma non è ancora sincronizzato.|  
  
 [  **@previous_status=**] **'***previous_status***'**  
 Stato precedente della sottoscrizione. *previous_status* viene **sysname**, con un valore predefinito è NULL. Questo parametro consente di modificare tutte le sottoscrizioni che hanno attualmente lo stato specificato, consentendo in tal modo le funzioni di gruppo in un set specifico di sottoscrizioni (ad esempio, impostando tutte attive verso le sottoscrizioni **sottoscritto**).  
  
 [  **@destination_db=**] **'***destination_db***'**  
 Nome del database di destinazione. *destination_db* viene **sysname**, il valore predefinito è **%**.  
  
 [  **@frequency_type=**] *frequency_type*  
 Frequenza di pianificazione dell'attività di distribuzione. *frequency_type* viene **int**, con un valore predefinito è NULL.  
  
 [  **@frequency_interval=**] *frequency_interval*  
 Il valore da applicare alla frequenza impostata *frequency_type*. *frequency_interval* viene **int**, con un valore predefinito è NULL.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Data dell'attività di distribuzione. Questo parametro viene utilizzato quando *frequency_type* è impostato su 32 (mensile relativa). *frequency_relative_interval* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
|NULL (predefinito)||  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, con un valore predefinito è NULL.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Frequenza di ripianificazione in minuti durante il periodo definito. *frequency_subday* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4**|Minuto|  
|**8**|Ora|  
|NULL (predefinito)||  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, con un valore predefinito è NULL.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Ora del giorno della prima esecuzione pianificata dell'attività di distribuzione, nel formato HHMMSS. *active_start_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Ora del giorno dell'ultima esecuzione pianificata dell'attività di distribuzione, nel formato HHMMSS. *active_end_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
 [  **@active_start_date=**] *active_start_date*  
 Data della prima esecuzione pianificata per l'attività di distribuzione, nel formato AAAAMMGG. *active_start_date* viene **int**, con un valore predefinito è NULL.  
  
 [  **@active_end_date=**] *active_end_date*  
 Data dell'ultima esecuzione pianificata dell'attività di distribuzione, nel formato AAAAMMGG. *active_end_date* viene **int**, con un valore predefinito è NULL.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 Riga di comando facoltativa. *optional_command_line* viene **nvarchar (4000)**, con un valore predefinito è NULL.  
  
 [  **@distribution_jobid=**] *distribution_jobid*  
 ID del processo dell'agente di distribuzione nel server di distribuzione per la sottoscrizione quando lo stato inattivo della sottoscrizione viene modificato da inattivo ad attivo. Negli altri casi non è definito. Se una chiamata a questa stored procedure richiede l'utilizzo di più agenti di distribuzione, il risultato non è definito. *distribution_jobid* viene **Binary (16)**, con un valore predefinito è NULL.  
  
 [  **@from_auto_sync=**] *from_auto_sync*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@offloadagent=** ] *remote_agent_activation*  
 > [!NOTE]  
>  L'attivazione remota dell'agente è deprecata e non è più supportata. Questo parametro è supportato solo per compatibilità con gli script di versioni precedenti. L'impostazione *remote_agent_activation* su un valore diverso da **0** genera un errore.  
  
 [  **@offloadserver=** ] **'***remote_agent_server_name***'**  
 > [!NOTE]  
>  L'attivazione remota dell'agente è deprecata e non è più supportata. Questo parametro è supportato solo per compatibilità con gli script di versioni precedenti. L'impostazione *remote_agent_server_name* su qualsiasi valore diverso da NULL genera un errore.  
  
 [ **@dts_package_name**=] **'***dts_package_name***'**  
 Specifica il nome del pacchetto Data Transformation Services (DTS). *dts_package_name* è un **sysname**, con un valore predefinito è NULL. Ad esempio, per un pacchetto denominato **DTSPub_Package** si specificherà `@dts_package_name = N'DTSPub_Package'`.  
  
 [ **@dts_package_password**=] **'***dts_package_password***'**  
 Specifica la password per il pacchetto. *dts_package_password* viene **sysname** con valore predefinito è NULL, che indica che la proprietà della password deve rimanere invariata.  
  
> [!NOTE]  
>  A ogni pacchetto DTS deve essere associata una password.  
  
 [ **@dts_package_location**=] *dts_package_location*  
 Specifica la posizione del pacchetto. *dts_package_location* è un **int**, il valore predefinito è **0**. Se **0**, il pacchetto si trova nel server di distribuzione. Se **1**, il percorso del pacchetto corrisponde al sottoscrittore. La posizione del pacchetto può essere **distributore** oppure **sottoscrittore**.  
  
 [ **@skipobjectactivation**=] *skipobjectactivation*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@distribution_job_name=** ] **'***job_name***'**  
 Nome del processo di distribuzione. *job_name* viene **sysname**, con un valore predefinito è NULL.  
  
 [ **@publisher**=] **'***publisher***'**  
 Specifica un non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzata quando si modificano le proprietà degli articoli in una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changesubstatus** viene utilizzata nella replica snapshot e transazionale.  
  
 **sp_changesubstatus** modificherà lo stato del sottoscrittore nel **syssubscriptions** tabella con lo stato modificato. Se necessario, aggiorna lo stato di articolo nel **sysarticles** tabella impostandolo su attivo o inattivo. Se necessario, imposta il flag di replica attiva o disattiva **sysobjects** tabella per la tabella replicata.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server **db_owner** ruolo predefinito del database o il creatore della sottoscrizione può eseguire **sp_changesubstatus**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
