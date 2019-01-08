---
title: sp_add_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobstep_TSQL
- sp_add_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobstep
ms.assetid: 97900032-523d-49d6-9865-2734fba1c755
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1832768a98dff17b0b59d9b3cf81f40f03ab34ad
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538153"
---
# <a name="spaddjobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un passaggio (operazione) a un processo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_jobstep [ @job_id = ] job_id | [ @job_name = ] 'job_name'   
     [ , [ @step_id = ] step_id ]   
     { , [ @step_name = ] 'step_name' }   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @command = ] 'command' ]   
     [ , [ @additional_parameters = ] 'parameters' ]   
          [ , [ @cmdexec_success_code = ] code ]   
     [ , [ @on_success_action = ] success_action ]   
          [ , [ @on_success_step_id = ] success_step_id ]   
          [ , [ @on_fail_action = ] fail_action ]   
          [ , [ @on_fail_step_id = ] fail_step_id ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @database_user_name = ] 'user' ]   
     [ , [ @retry_attempts = ] retry_attempts ]   
     [ , [ @retry_interval = ] retry_interval ]   
     [ , [ @os_run_priority = ] run_priority ]   
     [ , [ @output_file_name = ] 'file_name' ]   
     [ , [ @flags = ] flags ]   
     [ , { [ @proxy_id = ] proxy_id   
         | [ @proxy_name = ] 'proxy_name' } ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@job_id =** ] *job_id*  
 Numero di identificazione del processo a cui aggiungere il passaggio. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
 [  **@job_name =** ] **'**_job_name_**'**  
 Nome del processo a cui aggiungere il passaggio. *nome_processo* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *job_id* oppure *job_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
 [ **@step_id =** ] *step_id*  
 Numero di identificazione sequenziale per il passaggio del processo. Passaggio di numeri di identificazione partono **1** e aumentano in modo sequenziale. Se viene inserito un passaggio nella sequenza esistente, i numeri di sequenza vengono automaticamente adeguati. Viene fornito un valore se *step_id* non è specificato. *step_id*viene **int**, con un valore predefinito è NULL.  
  
 [  **@step_name =** ] **'**_step_name_**'**  
 Nome del passaggio. *step_name*viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@subsystem =** ] **'**_sottosistema_**'**  
 Sottosistema utilizzato dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio agente per eseguire *comando*. *sottosistema* viene **nvarchar (40)**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|«**ACTIVESCRIPTING**»|Script ActiveX<br /><br /> **\*\* Importante \*\*** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|«**CMDEXEC**»|Comando del sistema operativo o programma eseguibile|  
|«**DISTRIBUZIONE**»|Processo di Agente distribuzione repliche|  
|«**SNAPSHOT**»|Processo di Agente snapshot repliche|  
|«**LOGREADER**»|Processo di Agente lettura log repliche|  
|«**MERGE**»|Processo di Agente merge repliche|  
|«**QueueReader**»|Processo di Agente di lettura coda repliche|  
|«**ANALYSISQUERY**»|Query di Analysis Services (MDX, DMX).|  
|«**ANALYSISCOMMAND**»|Comando di Analysis Services (XMLA).|  
|«**Dts**»|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] esecuzione del pacchetto|  
|«**PowerShell**»|Script di PowerShell|  
|«**TSQL**' (impostazione predefinita)|[!INCLUDE[tsql](../../includes/tsql-md.md)] - istruzione|  
  
 [  **@command=** ] **'**_comando_**'**  
 I comandi da eseguire tramite **SQLServerAgent** servizio attraverso *sottosistema*. *comando* viene **nvarchar (max)**, con un valore predefinito è NULL. SQL Server Agent consente di eseguire la sostituzione dei token, che garantisce la stessa flessibilità assicurata dalle variabili durante la scrittura dei programmi software.  
  
> [!IMPORTANT]  
>  È necessario inserire una macro di escape con tutti i token utilizzati nei passaggi di processo. In caso contrario, questi passaggi avranno esito negativo. È ora necessario inoltre racchiudere tra parentesi i nomi dei token e inserire il simbolo di dollaro (`$`) all'inizio della sintassi del token, Ad esempio:  
>   
>  `$(ESCAPE_` *Nome della macro* `(DATE))`  
  
 Per altre informazioni su questi token e passaggi di processo per usare la nuova sintassi dei token di aggiornamento, vedere [usare i token nei passaggi del processo](../../ssms/agent/use-tokens-in-job-steps.md).  
  
> [!IMPORTANT]  
>  Qualsiasi utente di Windows con autorizzazioni di scrittura per il registro eventi di Windows è in grado di accedere ai passaggi di processo attivati dagli avvisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o di WMI. Per evitare rischi per la sicurezza, i token di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che possono essere utilizzati in processi attivati dagli avvisi sono disabilitati per impostazione predefinita. Questi token sono: **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG**., e **WMI (** _proprietà_**)**. Si noti che in questa versione l'utilizzo dei token è esteso a tutti gli avvisi.  
>   
>  Se si desidera utilizzare questi token, verificare innanzitutto che solo i membri di gruppi di sicurezza di Windows trusted, ad esempio il gruppo Administrators, dispongano delle autorizzazioni di scrittura per il registro eventi del computer in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A questo punto, fare clic con il pulsante destro del mouse su **SQL Server Agent** in Esplora oggetti, scegliere **Proprietà**e nella pagina **Sistema avvisi** selezionare **Sostituisci token per tutte le risposte del processo ad avvisi** per abilitare questi token.  
  
 [  **@additional_parameters=** ] **'**_parametri_**'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *i parametri* viene **ntext**, con un valore predefinito è NULL.  
  
 [  **@cmdexec_success_code =** ] *codice*  
 Il valore restituito da una **CmdExec** comando del sottosistema per indicare che *comando* eseguito correttamente. *codice*viene **int**, il valore predefinito è **0**.  
  
 [  **@on_success_action=** ] *success_action*  
 Azione da eseguire se il passaggio ha esito positivo. *success_action*viene **tinyint**, i possibili valori sono i seguenti.  
  
|Value|Descrizione (azione)|  
|-----------|----------------------------|  
|**1** (impostazione predefinita)|Uscita in caso di esito positivo|  
|**2**|Uscita in caso di esito negativo|  
|**3**|Esecuzione del passaggio successivo|  
|**4**|Andare al passaggio *on_success_step_id*|  
  
 [ **@on_success_step_id =** ] *success_step_id*  
 L'ID del passaggio del processo da eseguire se il passaggio ha esito positivo e *success_action*viene **4**. *success_step_id*viene **int**, il valore predefinito è **0**.  
  
 [  **@on_fail_action=** ] *fail_action*  
 Azione da eseguire se il passaggio non viene completato correttamente. *fail_action*viene **tinyint**, i possibili valori sono i seguenti.  
  
|Value|Descrizione (azione)|  
|-----------|----------------------------|  
|**1**|Uscita in caso di esito positivo|  
|**2** (impostazione predefinita)|Uscita in caso di esito negativo|  
|**3**|Esecuzione del passaggio successivo|  
|**4**|Andare al passaggio *on_fail_step_id*|  
  
 [  **@on_fail_step_id=** ] *fail_step_id*  
 L'ID del passaggio del processo da eseguire se il passaggio ha esito negativo e *fail_action*viene **4**. *fail_step_id*viene **int**, il valore predefinito è **0**.  
  
 [  **@server =**] **'**_server_**'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *server*viene **nvarchar(30)**, con un valore predefinito è NULL.  
  
 [  **@database_name=** ] **'**_database_**'**  
 Nome del database in cui eseguire un passaggio [!INCLUDE[tsql](../../includes/tsql-md.md)]. *database* viene **sysname**, il valore predefinito è NULL, nel qual caso il **master** database viene utilizzato. I nomi racchiusi tra parentesi quadre ([ ]) non sono ammessi. Per un passaggio di processo ActiveX, il *database* è il nome del linguaggio di script che usa il passaggio.  
  
 [  **@database_user_name=** ] **'**_utente_**'**  
 Nome dell'account utente da utilizzare quando viene eseguito un passaggio [!INCLUDE[tsql](../../includes/tsql-md.md)]. *utente* viene **sysname**, con un valore predefinito è NULL. Quando *utente* è NULL, il passaggio viene eseguito nel contesto utente del proprietario del processo sul *database*.  SQL Server Agent includerà questo parametro solo se il proprietario del processo è un sysadmin di SQL Server. In tal caso il passaggio del processo Transact-SQL specificato sarà eseguito nel contesto del nome utente di SQL Server specificato. Se il proprietario del processo non è un sysadmin di SQL Server, quindi il passaggio di Transact-SQL verrà sempre eseguito nel contesto dell'account di accesso proprietario del processo, e il @database_user_name parametro verrà ignorato.  
  
 [  **@retry_attempts=** ] *retry_attempts*  
 Numero di tentativi da eseguire in caso di esecuzione errata del passaggio. *retry_attempts*viene **int**, il valore predefinito è **0**, che indica nessun tentativo.  
  
 [  **@retry_interval=** ] *retry_interval*  
 Numero di minuti che devono trascorrere tra i tentativi. *retry_interval*viene **int**, il valore predefinito è **0**, che indica un **0**-intervallo di minuti.  
  
 [  **@os_run_priority =** ] *run_priority*  
 Riservato.  
  
 [  **@output_file_name=** ] **'**_file_name_**'**  
 Nome del file in cui salvare l'output del passaggio. *file_name*viene **nvarchar (200)**, con un valore predefinito è NULL. *file_name*può includere uno o più token elencati *comando*. Questo parametro è valido solo con i comandi eseguiti nel [!INCLUDE[tsql](../../includes/tsql-md.md)], **CmdExec**, **PowerShell**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sottosistemi.  
  
 [  **@flags=** ] *flag*  
 Opzione che consente di controllare il comportamento. *i flag* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0** (predefinito)|Il file di output viene sovrascritto|  
|**2**|L'output viene aggiunto alla fine del file di output.|  
|**4**|L'output del passaggio del processo [!INCLUDE[tsql](../../includes/tsql-md.md)] viene scritto nella cronologia dei passaggi|  
|**8**|Il log viene scritto nella tabella. La cronologia esistente viene sovrascritta|  
|**16**|Il log viene scritto nella tabella in aggiunta alla cronologia esistente|  
|**32**|Tutto l'output viene scritto nella cronologia processo|  
|**64**|Creare un evento Windows da utilizzare come segnale per l'interruzione dell'oggetto JobStep Cmd|  
  
 [ **@proxy_id** = ] *proxy_id*  
 ID del proxy in base al quale viene eseguito il passaggio del processo. *proxy_id* è di tipo **int**, con un valore predefinito è NULL. Se nessun *proxy_id* è specificato, nessun *proxy_name* viene specificato e non *user_name* viene specificato, il passaggio del processo viene eseguito come account del servizio per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
 [ **@proxy_name** =] **'**_proxy_name_**'**  
 Nome del proxy in base al quale viene eseguito il passaggio del processo. *proxy_name* è di tipo **sysname**, con un valore predefinito è NULL. Se nessun *proxy_id* è specificato, nessun *proxy_name* viene specificato e non *user_name* viene specificato, il passaggio del processo viene eseguito come account del servizio per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 **sp_add_jobstep** deve essere eseguita la **msdb** database.  
  
 SQL Server Management Studio include un semplice strumento grafico per la gestione dei processi ed è lo strumento consigliato per la creazione e gestione dell'infrastruttura dei processi.  
  
 Un passaggio di processo è necessario specificare un proxy, a meno che l'autore del passaggio del processo è un membro del **sysadmin** ruolo di sicurezza predefinito.  
  
 Un proxy può essere identificato da *nome_proxy* oppure *proxy_id*.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 L'autore del passaggio del processo deve avere accesso al proxy per il passaggio del processo. I membri del **sysadmin** ruolo predefinito del server ha accesso a tutti i proxy. Per quanto riguarda gli altri utenti, è necessario concedere esplicitamente l'accesso a un proxy.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creato un passaggio di processo che modifica l'accesso al database impostando la modalità sola lettura per il database Sales. In questo esempio, inoltre, vengono specificati 5 tentativi, con un intervallo di 5 minuti tra ognuno.  
  
> [!NOTE]  
>  In questo esempio si presuppone che il processo `Weekly Sales Data Backup` esista già.  
  
```  
USE msdb;  
GO  
EXEC sp_add_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_name = N'Set database to read only',  
    @subsystem = N'TSQL',  
    @command = N'ALTER DATABASE SALES SET READ_ONLY',   
    @retry_attempts = 5,  
    @retry_interval = 5 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare o modificare processi](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
