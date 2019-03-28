---
title: sys.sp_cdc_add_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_add_job_TSQL
- sys.sp_cdc_add_job
- sys.sp_cdc_add_job_TSQL
- sp_cdc_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_add_job
ms.assetid: c4458738-ed25-40a6-8294-a26ca5a05bd9
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 533f37252fa16e2e139f29ac843d6d4a933f13de
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532143"
---
# <a name="sysspcdcaddjob-transact-sql"></a>sys.sp_cdc_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di creare un processo di pulizia dell'acquisizione dei dati delle modifiche o un processo di acquisizione nel database corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.sp_cdc_add_job [ @job_type = ] 'job_type'  
    [ , [ @start_job = ] start_job ]   
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ , [ @threshold ] = 'delete_threshold' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_type = ] 'job\_type'` Tipo di processo da aggiungere. *job_type* viene **nvarchar(20)** e non può essere NULL. Gli input validi sono **'capture'** e **'cleanup'**.  
  
`[ @start_job = ] start_job` Flag che indica se il processo deve essere avviato immediatamente dopo l'aggiunta. *start_job* viene **bit** con valore predefinito è 1.  
  
`[ @maxtrans ] = max_trans` Numero massimo di transazioni da elaborare in ogni ciclo di analisi. *max_trans* viene **int** con valore predefinito è 500. Se specificato, il valore deve essere un numero intero positivo.  
  
 *max_trans* è valida solo per i processi di acquisizione.  
  
`[ @maxscans ] = max\_scans_` Numero massimo di cicli di analisi da eseguire per estrarre tutte le righe dal log. *max_scans* viene **int** con valore predefinito è 10.  
  
 *max_scan* è valida solo per i processi di acquisizione.  
  
`[ @continuous ] = continuous_` Indica se il processo di acquisizione deve essere eseguito continuamente (1), o eseguire una sola volta (0). *Continuous* viene **bit** con valore predefinito è 1.  
  
 Quando *continui* = 1, il [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) processo analizza il log ed elabora fino a (*max_trans* \* *max_scans*) transazioni. Attende quindi il numero di secondi specificato nel *polling_interval* prima di iniziare l'analisi del log successivo.  
  
 Quando *continui* = 0, il **sp_cdc_scan** processo esegue fino a *max_scans* analisi del log, elaborando fino a *max_trans* delle transazioni durante ogni analisi e quindi viene chiusa.  
  
 *Continua* è valida solo per i processi di acquisizione.  
  
`[ @pollinginterval ] = polling\_interval_` Numero di secondi tra cicli di analisi di log. *polling_interval* viene **bigint** con valore predefinito è 5.  
  
 *polling_interval* è valido solo per l'acquisizione processi quando *continua* è impostato su 1. Se specificato, il valore non può essere negativo e non può superare 24 ore. Se viene specificato il valore 0, non esiste alcun intervallo di attesa tra le analisi del log.  
  
`[ @retention ] = retention_` Numero di minuti che modificano i dati le righe devono essere conservate nelle tabelle delle modifiche. *conservazione* viene **bigint** con valore predefinito è 4320 (72 ore). Il valore massimo è 52494800 (100 anni). Se specificato, il valore deve essere un numero intero positivo.  
  
 *conservazione* è valida solo per i processi di pulizia.  
  
`[ @threshold = ] 'delete\_threshold'` Numero massimo di voci che possono essere eliminate utilizzando un'unica istruzione nel processo di pulizia. *delete_threshold* viene **bigint** con valore predefinito è 5000.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Un processo di pulizia viene creato utilizzando i valori predefiniti quando la prima tabella nel database è abilitata per Change Data Capture. Un processo di acquisizione viene creato utilizzando i valori predefiniti quando la prima tabella nel database è abilitata per Change Data Capture e per il database non esistono pubblicazioni transazionali. Se esiste una pubblicazione transazionale, per attivare il meccanismo di acquisizione viene utilizzato l'agente di lettura del log delle transazioni. Non è quindi necessario né consentito un processo di acquisizione separato.  
  
 Poiché i processi di pulizia e di acquisizione vengono creati per impostazione predefinita, questa stored procedure è necessaria solo quando un processo è stato eliminato in modo esplicito e deve essere ricreato.  
  
 Il nome del processo è **cdc.**  _\<database\_name\>_**\_pulizia** oppure **cdc.**  _\<database\_name\>_**\_acquisire**, dove *< database_name >* corrisponde al nome del database corrente. Se un processo con lo stesso nome esiste già, il nome viene aggiunto un punto (**.**) seguita da un identificatore univoco, ad esempio: **cdc. AdventureWorks_capture. A1ACBDED-13FC-428C-8302-10100EF74F52**.  
  
 Per visualizzare la configurazione corrente di un processo di pulizia o di acquisizione, usare [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md). Per modificare la configurazione di un processo, usare [sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **db_owner** ruolo predefinito del database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-creating-a-capture-job"></a>A. Creazione di un processo di acquisizione  
 Nell'esempio seguente viene creato un processo di acquisizione. Questo esempio presuppone che il processo di pulizia esistente sia stato eliminato in modo esplicito e debba essere ricreato. Il processo viene creato utilizzando i valori predefiniti.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job @job_type = N'capture';  
GO  
```  
  
### <a name="b-creating-a-cleanup-job"></a>B. Creazione di un processo di pulizia  
 Nell'esempio seguente viene creato un processo di pulizia nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Il parametro `@start_job` è impostato su 0 e `@retention` è impostato su 5760 minuti (96 ore). Questo esempio presuppone che il processo di pulizia esistente sia stato eliminato in modo esplicito e debba essere ricreato.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job  
     @job_type = N'cleanup'  
    ,@start_job = 0  
    ,@retention = 5760;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [dbo.cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [Informazioni su Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
