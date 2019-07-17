---
title: sp_help_downloadlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_downloadlist_TSQL
- sp_help_downloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_downloadlist
ms.assetid: 745b265b-86e8-4399-b928-c6969ca1a2c8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40345ed8ad1a10da0088c5c1388c44fa24cad929
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055188"
---
# <a name="sphelpdownloadlist-transact-sql"></a>sp_help_downloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elenca tutte le righe di **sysdownloadlist** tabella di sistema per il processo specificato oppure tutte le righe se viene specificato alcun processo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_downloadlist { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }   
     [ , [ @operation = ] 'operation' ]   
     [ , [ @object_type = ] 'object_type' ]   
     [ , [ @object_name = ] 'object_name' ]   
     [ , [ @target_server = ] 'target_server' ]   
     [ , [ @has_error = ] has_error ]   
     [ , [ @status = ] status ]   
     [ , [ @date_posted = ] date_posted ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @job_id = ] job_id` ID del processo per cui restituire informazioni. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` Il nome del processo. *nome_processo* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *job_id* oppure *job_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @operation = ] 'operation'` Operazione valida per il processo specificato. *operazione* viene **varchar(64)** , con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**DEFECT**|Operazione server che richiede l'esclusione del server di destinazione Master **SQLServerAgent** servizio.|  
|**DELETE**|Operazione del processo che rimuove un intero processo.|  
|**INSERT**|Operazione del processo che inserisce un intero processo o ne aggiorna uno esistente. Include tutti i passaggi e le pianificazioni del processo, se applicabile.|  
|**REINTEGRARSI**|Operazione del server con cui viene attivato il rinvio delle informazioni di integrazione del server di destinazione, tra cui l'intervallo di polling e il fuso orario per il dominio multiserver. Il server di destinazione redownloads anche il **MSXOperator** dettagli.|  
|**SET-POLL**|Operazione del server con cui viene impostato l'intervallo di tempo in secondi per il polling del dominio multiserver eseguito dai server di destinazione. Se specificato, *valore* viene interpretato come valore di intervallo obbligatorio e può essere un valore compreso **10** al **28.800**.|  
|**START**|Operazione del processo con cui viene richiesto l'avvio dell'esecuzione del processo.|  
|**STOP**|Operazione del processo con cui viene richiesto l'arresto dell'esecuzione del processo.|  
|**SYNC-TIME**|Operazione del server con cui viene attivata la sincronizzazione del clock di sistema dei server di destinazione con il clock di sistema del dominio multiserver. Si tratta di un'operazione onerosa ed è pertanto consigliabile non eseguirla di frequente.|  
|**UPDATE**|Processo operazione che aggiorna solo le **sysjobs** informazioni per un processo, non i passaggi di processo o pianificazioni. Viene chiamato automaticamente dal **sp_update_job**.|  
  
`[ @object_type = ] 'object_type'` Il tipo di oggetto per il processo specificato. *object_type* viene **varchar(64)** , con un valore predefinito è NULL. *object_type* può essere JOB o SERVER. Per altre informazioni su validi *object_type*valori, vedere [sp_add_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md).  
  
`[ @object_name = ] 'object_name'` Il nome dell'oggetto. *object_name* viene **sysname**, con un valore predefinito è NULL. Se *object_type* è processo *object_name*è il nome del processo. Se *object_type*è SERVER, *object_name*è il nome del server.  
  
`[ @target_server = ] 'target_server'` Il nome del server di destinazione. *target_server* viene **nvarchar (128)** , con un valore predefinito è NULL.  
  
`[ @has_error = ] has_error` È se il processo deve segnalare gli errori. *has_error* viene **tinyint**, e il valore predefinito è NULL, che indica gli errori non devono essere segnalati. **1** indica che tutti gli errori devono essere segnalati.  
  
`[ @status = ] status` Lo stato per il processo. *lo stato* viene **tinyint**, con un valore predefinito NULL.  
  
`[ @date_posted = ] date_posted` Impostare la data e ora per tutte le voci apportate o dopo la data e ora specificate devono essere incluse nel risultato. *partire* viene **datetime**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Numero di identificazione univoco integer dell'istruzione.|  
|**source_server**|**nvarchar(30)**|Nome di computer del server da cui viene inviata l'istruzione. Nelle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 7.0, si tratta sempre il nome del computer del server master (MSX).|  
|**operation_code**|**nvarchar(4000)**|Codice di operazione dell'istruzione.|  
|**object_name**|**sysname**|Oggetto su cui viene eseguita l'istruzione.|  
|**object_id**|**uniqueidentifier**|Numero di identificazione dell'oggetto interessato dall'istruzione (**job_id** per un oggetto processo o 0x00 per un oggetto server) o un valore di dati specifico per il **operation_code**.|  
|**target_server**|**nvarchar(30)**|Server di destinazione in cui deve essere eseguito il download dell'istruzione.|  
|**error_message**|**nvarchar(1024)**|Eventuale messaggio di errore inviato dal server di destinazione se si verifica un problema durante l'elaborazione dell'istruzione.<br /><br /> Nota: Eventuali messaggi di errore impediscono ulteriori operazioni di download dal server di destinazione.|  
|**date_posted**|**datetime**|Data di inserimento dell'istruzione nella tabella.|  
|**date_downloaded**|**datetime**|Data di download dell'istruzione nel server di destinazione.|  
|**status**|**tinyint**|Stato del processo:<br /><br /> **0** = non ancora scaricato<br /><br /> **1** = scaricato correttamente.|  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni di esecuzione per questa procedura vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene visualizzato un elenco di righe in `sysdownloadlist` per il processo `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_downloadlist  
    @job_name = N'NightlyBackups',  
    @operation = N'UPDATE',   
    @object_type = N'JOB',   
    @object_name = N'NightlyBackups',  
    @target_server = N'SEATTLE2',   
    @has_error = 1,   
    @status = NULL,   
    @date_posted = NULL ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
