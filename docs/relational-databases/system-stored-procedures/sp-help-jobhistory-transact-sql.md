---
title: sp_help_jobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobhistory_TSQL
- sp_help_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobhistory
ms.assetid: a944d44e-411b-4735-8ce4-73888d4262d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0b2ee476694098f4734c31439b48a7ec9efdc892
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534433"
---
# <a name="sphelpjobhistory-transact-sql"></a>sp_help_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sui processi per i server del dominio di amministrazione multiserver.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_jobhistory [ [ @job_id = ] job_id ]   
     [ , [ @job_name = ] 'job_name' ]   
     [ , [ @step_id = ] step_id ]   
     [ , [ @sql_message_id = ] sql_message_id ]   
     [ , [ @sql_severity = ] sql_severity ]   
     [ , [ @start_run_date = ] start_run_date ]   
     [ , [ @end_run_date = ] end_run_date ]   
     [ , [ @start_run_time = ] start_run_time ]   
     [ , [ @end_run_time = ] end_run_time ]   
     [ , [ @minimum_run_duration = ] minimum_run_duration ]   
     [ , [ @run_status = ] run_status ]   
     [ , [ @minimum_retries = ] minimum_retries ]   
     [ , [ @oldest_first = ] oldest_first ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @mode = ] 'mode' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] job_id` ID del processo. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` Il nome del processo. *nome_processo* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @step_id = ] step_id` Il numero di identificazione del passaggio. *step_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @sql_message_id = ] sql_message_id` Il numero di identificazione del messaggio di errore restituito da Microsoft SQL Server durante l'esecuzione del processo. *sql_message_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @sql_severity = ] sql_severity` Il livello di gravità del messaggio di errore restituito da SQL Server durante l'esecuzione del processo. *sql_severity* viene **int**, con un valore predefinito è NULL.  
  
`[ @start_run_date = ] start_run_date` Data che di avvio del processo. *start_run_date*viene **int**, con un valore predefinito è NULL. *start_run_date* deve essere immesso nel formato aaaammgg, dove YYYY è un anno di quattro caratteri, MM è un nome di un mese espressi con due cifre e GG è un nome di giorno di due caratteri.  
  
`[ @end_run_date = ] end_run_date` Data che di completamento del processo. *espresso* viene **int**, con un valore predefinito è NULL. *espresso*deve essere immesso nel formato aaaammgg, dove YYYY è l'anno a quattro cifre, MM è un nome di un mese espressi con due cifre e GG è un nome di giorno di due caratteri.  
  
`[ @start_run_time = ] start_run_time` Ora che di avvio del processo. *start_run_time* viene **int**, con un valore predefinito è NULL. *start_run_time*deve essere immesso nel formato HHMMSS, dove HH è l'ora, MM è un minuto espressi con due cifre del giorno e SS è il secondo espressi con due cifre del giorno.  
  
`[ @end_run_time = ] end_run_time` Ora che il processo completato la sua esecuzione. *end_run_time* viene **int**, con un valore predefinito è NULL. *end_run_time*deve essere immesso nel formato HHMMSS, dove HH è l'ora, MM è un minuto espressi con due cifre del giorno e SS è il secondo espressi con due cifre del giorno.  
  
`[ @minimum_run_duration = ] minimum_run_duration` La lunghezza minima di tempo per il completamento del processo. *minimum_run_duration* viene **int**, con un valore predefinito è NULL. *minimum_run_duration*deve essere immesso nel formato HHMMSS, dove HH è l'ora, MM è un minuto espressi con due cifre del giorno e SS è il secondo espressi con due cifre del giorno.  
  
`[ @run_status = ] run_status` Lo stato di esecuzione del processo. *run_status* viene **int**, con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Non riuscito|  
|**1**|Operazione completata|  
|**2**|Nuovo tentativo (solo passaggio)|  
|**3**|Canceled|  
|**4**|Messaggio di esecuzione in corso|  
|**5**|Unknown|  
  
`[ @minimum_retries = ] minimum_retries` Il numero minimo di volte in cui un processo di tentativi per l'esecuzione. *minimum_retries* viene **int**, con un valore predefinito è NULL.  
  
`[ @oldest_first = ] oldest_first` Indica se per primi nell'output con i processi meno recenti. *oldest_first* viene **int**, il valore predefinito è **0**, che presenta i processi più recenti prima di tutto. **1** presenta prima di tutto i processi meno recenti.  
  
`[ @server = ] 'server'` Il nome del server in cui è stato eseguito il processo. *server* viene **nvarchar(30)**, con un valore predefinito è NULL.  
  
`[ @mode = ] 'mode'` Indica se stampare tutte le colonne nel set di risultati (**completo**) o un riepilogo delle colonne. *modalità* viene **varchar(7)**, il valore predefinito è **riepilogo**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 L'elenco delle colonne dipende dal valore della *modalità*. Il set di colonne più completo è illustrato di seguito e viene restituito quando *modalità* è FULL.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Numero di identificazione della voce di cronologia.|  
|**job_id**|**uniqueidentifier**|Numero di identificazione del processo.|  
|**job_name**|**sysname**|Nome del processo.|  
|**step_id**|**int**|Numero di identificazione del passaggio (saranno **0** per la cronologia processo).|  
|**step_name**|**sysname**|Nome del passaggio (è NULL per la cronologia dei processi).|  
|**sql_message_id**|**int**|Per un passaggio [!INCLUDE[tsql](../../includes/tsql-md.md)], numero di errore [!INCLUDE[tsql](../../includes/tsql-md.md)] più recente restituito durante l'esecuzione del comando.|  
|**sql_severity**|**int**|Per un passaggio [!INCLUDE[tsql](../../includes/tsql-md.md)], gravità di errore [!INCLUDE[tsql](../../includes/tsql-md.md)] più elevata restituita durante l'esecuzione del comando.|  
|**message**|**nvarchar(1024)**|Messaggio della cronologia relativo al processo o al passaggio.|  
|**run_status**|**int**|Risultato del processo o del passaggio.|  
|**run_date**|**int**|Data di inizio dell'esecuzione del processo o del passaggio.|  
|**run_time**|**int**|Ora di inizio dell'esecuzione del processo o del passaggio.|  
|**run_duration**|**int**|Periodo trascorso, in formato HHMMSS, nella fase di esecuzione del processo o passaggio.|  
|**operator_emailed**|**nvarchar(20)**|Operatore che ha ricevuto la notifica relativa al processo tramite posta elettronica (è NULL per la cronologia dei passaggi).|  
|**operator_netsent**|**nvarchar(20)**|Operatore che ha ricevuto la notifica relativa al processo tramite un messaggio di rete (è NULL per la cronologia dei passaggi).|  
|**operator_paged**|**nvarchar(20)**|Operatore che ha ricevuto la notifica relativa al processo tramite cercapersone (è NULL per la cronologia dei passaggi).|  
|**retries_attempted**|**int**|Numero di tentativi di esecuzione del passaggio (è sempre 0 per la cronologia dei processi).|  
|**server**|**nvarchar(30)**|Server in cui viene eseguito il processo o il passaggio. È sempre (**locale**).|  
  
## <a name="remarks"></a>Note  
 **sp_help_jobhistory** restituisce un report con la cronologia dei processi pianificati specificati. Se non viene specificato alcun parametro, il report include la cronologia di tutti i processi pianificati.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 I membri del **SQLAgentUserRole** ruolo del database può solo visualizzare la cronologia dei processi di cui sono proprietari.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-all-job-information-for-a-job"></a>A. Visualizzazione di un elenco di tutte le informazioni di un processo  
 Nell'esempio seguente viene visualizzato un elenco di informazioni per il processo `NightlyBackups`  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobhistory   
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-that-match-certain-conditions"></a>B. Visualizzazione di un elenco di informazioni per i processi che corrispondono a determinate condizioni  
 Nell'esempio seguente vengono stampate tutte le colonne e tutte le informazioni relative ai processi e ai passaggi non eseguiti correttamente che hanno generato un messaggio di errore `50100` (messaggio di errore definito dall'utente) con livello di gravità `20`.  
  
```  
USE msdb  
GO  
  
EXEC dbo.sp_help_jobhistory  
    @sql_message_id = 50100,  
    @sql_severity = 20,  
    @run_status = 0,  
    @mode = N'FULL' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
