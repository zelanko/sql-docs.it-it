---
title: Sys. sp_cdc_change_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_change_job_TSQL
- sys.sp_cdc_change_job
- sp_cdc_change_job_TSQL
- sp_cdc_change_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_change_job
ms.assetid: ea918888-0fc5-4cc1-b301-26b2a9fbb20d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cfbf93fc858f52cd35401bd80fe5ede7dee86a3d
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591745"
---
# <a name="sysspcdcchangejob-transact-sql"></a>sys.sp_cdc_change_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica la configurazione di un processo di pulizia dell'acquisizione dei dati delle modifiche o di un processo di acquisizione nel database corrente. Per visualizzare la configurazione corrente di un processo, eseguire una query di [dbo. cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) tabella oppure utilizzare [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.sp_cdc_change_job [ [ @job_type = ] 'job_type' ]  
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ @threshold = ] 'delete threshold'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@job_type=** ] **'**_job_type_**'**  
 Tipo di processo da modificare. *job_type* viene **nvarchar(20)** con valore predefinito è 'capture'. Gli input validi sono 'capture' e 'cleanup'.  
  
 [ **@maxtrans** ] **=** _max_trans_  
 Numero massimo di transazioni da elaborare in ogni ciclo di analisi. *max_trans* viene **int** con un valore predefinito è NULL, che indica nessuna modifica per questo parametro. Se specificato, il valore deve essere un numero intero positivo.  
  
 *max_trans* è valida solo per i processi di acquisizione.  
  
 [ **@maxscans** ] **=** _max_scans_  
 Numero massimo di cicli di analisi da eseguire per estrarre tutte le righe dal log. *max_scans* viene **int** con un valore predefinito è NULL, che indica nessuna modifica per questo parametro.  
  
 *max_scan* è valida solo per i processi di acquisizione.  
  
 [ **@continuous** ] **=** _continua_  
 Viene indicato se il processo di acquisizione deve essere eseguito continuamente (1) o solo una volta (0). *Continuous* viene **bit** con un valore predefinito è NULL, che indica nessuna modifica per questo parametro.  
  
 Quando *continui* = 1, il [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) processo analizza il log ed elabora fino a (*max_trans* \* *max_scans*) transazioni. Attende quindi il numero di secondi specificato nel *polling_interval* prima di iniziare l'analisi del log successivo.  
  
 Quando *continui* = 0, il **sp_cdc_scan** processo esegue fino a *max_scans* analisi del log, elaborando fino a *max_trans* transazioni durante ogni analisi e quindi viene chiusa.  
  
 Se **@continuous** viene modificato da 1 a 0, **@pollinginterval** viene impostata automaticamente su 0. Un valore specificato per **@pollinginterval** diverso da 0 viene ignorato.  
  
 Se **@continuous** viene omesso o impostato esplicitamente su NULL e **@pollinginterval** è impostata esplicitamente su un valore maggiore di 0 **@continuous** viene automaticamente Impostare su 1.  
  
 *Continua* è valida solo per i processi di acquisizione.  
  
 [ **@pollinginterval** ] **=** _polling_interval_  
 Numero di secondi tra cicli di analisi del log. *polling_interval* viene **bigint** con un valore predefinito è NULL, che indica nessuna modifica per questo parametro.  
  
 *polling_interval* è valido solo per l'acquisizione processi quando *continua* è impostato su 1.  
  
 [ **@retention** ] **=** _conservazione_  
 Numero di minuti in base al quale le righe delle modifiche devono essere conservate nelle tabelle delle modifiche. *conservazione* viene **bigint** con un valore predefinito è NULL, che indica nessuna modifica per questo parametro. Il valore massimo è 52494800 (100 anni). Se specificato, il valore deve essere un numero intero positivo.  
  
 *conservazione* è valida solo per i processi di pulizia.  
  
 [  **@threshold=** ] **'**_eliminare soglia_**'**  
 Numero massimo di voci che possono essere eliminate utilizzando un'unica istruzione nel processo di pulizia. *soglia di eliminazione* viene **bigint** con un valore predefinito è NULL, che indica nessuna modifica per questo parametro. *soglia di eliminazione* è valida solo per i processi di pulizia.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Se si omette un parametro, il valore associato nella [dbo. cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) tabella non viene aggiornata. Un parametro impostato esplicitamente su NULL viene considerato come se fosse stato omesso.  
  
 Se si specifica un parametro non valido per il tipo di processo, l'istruzione avrà esito negativo.  
  
 Le modifiche apportate a un processo non diventano effettive fino a quando il processo viene arrestato utilizzando [sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md) e riavviato tramite [sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **db_owner** ruolo predefinito del database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-changing-a-capture-job"></a>A. Modifica di un processo di acquisizione  
 L'esempio seguente aggiorna il `@job_type`, `@maxscans`, e `@maxtrans` i parametri di un processo di acquisizione nel `AdventureWorks2012` database. Gli altri parametri validi per un processo di acquisizione, `@continuous` e `@pollinginterval`, sono omessi e i relativi valori non vengono modificati.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'capture',  
    @maxscans = 1000,  
    @maxtrans = 15;  
GO  
```  
  
### <a name="b-changing-a-cleanup-job"></a>b. Modifica di un processo di pulizia  
 Nell'esempio seguente viene aggiornato un processo di pulizia nel database `AdventureWorks2012`. Tutti i parametri validi per questo tipo di processo, tranne **@threshold**, vengono specificati. Il valore di **@threshold** non viene modificato.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [dbo. cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
