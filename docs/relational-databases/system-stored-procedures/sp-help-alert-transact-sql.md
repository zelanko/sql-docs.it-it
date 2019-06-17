---
title: sp_help_alert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_alert
- sp_help_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_alert
ms.assetid: 850cef4e-6348-4439-8e79-fd1bca712091
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bca9c53780bb3258f73a274240c0bb5e63e126c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62796571"
---
# <a name="sphelpalert-transact-sql"></a>sp_help_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sugli avvisi definiti per il server.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_alert [ [ @alert_name = ] 'alert_name' ]   
     [ , [ @order_by = ] 'order_by' ]   
     [ , [ @alert_id = ] alert_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @legacy_format = ] legacy_format ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @alert_name = ] 'alert_name'` Il nome dell'avviso. *nome_avviso* viene **nvarchar (128)** . Se *nome_avviso* viene omesso, vengono restituite informazioni su tutti gli avvisi.  
  
`[ @order_by = ] 'order_by'` L'ordinamento da usare per produrre i risultati. *order_by*viene **sysname**, con un valore predefinito è N' '*nome*'.  
  
`[ @alert_id = ] alert_id` Il numero di identificazione dell'avviso per segnalare informazioni. *alert_id*viene **int**, con un valore predefinito è NULL.  
  
`[ @category_name = ] 'category'` La categoria dell'avviso. *categoria* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @legacy_format = ] legacy_format` Indica se generare un set di risultati legacy. *legacy_format* viene **bit**, il valore predefinito è **0**. Quando *legacy_format* viene **1**, **sp_help_alert** restituisce il set di risultati restituito da **sp_help_alert** in Microsoft SQL Server 2000.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Quando **@legacy_format** viene **0**, **sp_help_alert** produce il set di risultati seguente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificatore univoco di tipo integer assegnato dal sistema.|  
|**name**|**sysname**|Nome dell'avviso (ad esempio Demo: Completi **msdb** log).|  
|**event_source**|**nvarchar(100)**|Origine dell'evento. Sarà sempre **MSSQLServer** per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 7.0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|Numero dell'errore del messaggio che definisce l'avviso (In genere corrisponde a un numero di errore il **sysmessages** tabella). Se utilizzata per definire l'avviso, gravità **message_id** viene **0** o NULL.|  
|**severity**|**int**|Livello di gravità (da **9** attraverso **25**, **110**, **120**, **130**, o **140**) che definisce l'avviso.|  
|**enabled**|**tinyint**|Stato del fatto che l'avviso è abilitato (**1**) o No (**0**). Gli avvisi non abilitati non vengono inviati.|  
|**delay_between_responses**|**int**|Periodo di attesa in secondi tra risposte successive per l'avviso.|  
|**last_occurrence_date**|**int**|Data dell'ultima generazione dell'avviso.|  
|**last_occurrence_time**|**int**|Ora dell'ultima generazione dell'avviso.|  
|**last_response_date**|**int**|Data ultimo avviso ha risposto a per il **SQLServerAgent** servizio.|  
|**last_response_time**|**int**|Ora dell'ultima l'avviso ha risposto a per il **SQLServerAgent** servizio.|  
|**notification_message**|**nvarchar(512)**|Messaggio aggiuntivo facoltativo inviato all'operatore come parte della notifica tramite posta elettronica o cercapersone.|  
|**include_event_description**|**tinyint**|Indica se la descrizione dell'errore di SQL Server inclusa nel registro applicazioni di Microsoft Windows deve essere inserita nel messaggio di notifica.|  
|**database_name**|**sysname**|Database in cui deve verificarsi l'errore affinché l'avviso venga generato. Se il nome del database è NULL, l'avviso viene generato indipendentemente dal database in cui l'errore si verifica.|  
|**event_description_keyword**|**nvarchar(100)**|Descrizione dell'errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclusa nel registro applicazioni di Windows, che deve corrispondere alla sequenza di caratteri specificata.|  
|**occurrence_count**|**int**|Numero di volte che l'avviso è stato generato.|  
|**count_reset_date**|**int**|Data la **numero_occorrenze** ultima reimpostazione.|  
|**count_reset_time**|**int**|Ora il **numero_occorrenze** ultima reimpostazione.|  
|**job_id**|**uniqueidentifier**|Numero di identificazione del processo da eseguire in risposta a un avviso.|  
|**job_name**|**sysname**|Nome del processo da eseguire in risposta a un avviso.|  
|**has_notification**|**int**|È diverso da zero se uno o più operatori ricevono una notifica dell'avviso. Può essere uno o più d'uno dei valori seguenti uniti dall'operatore OR:<br /><br /> **1**= notifica tramite posta elettronica<br /><br /> **2**= notifica tramite cercapersone<br /><br /> **4**= ha **net send** notifica.|  
|**flags**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**performance_condition**|**nvarchar(512)**|Se **tipo** viene **2**, questa colonna Mostra la definizione della condizione delle prestazioni; in caso contrario, la colonna è NULL.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 è sempre '[Uncategorized]'.|  
|**wmi_namespace**|**sysname**|Se **tipo** viene **3**, questa colonna viene visualizzato lo spazio dei nomi per l'evento WMI.|  
|**wmi_query**|**nvarchar(512)**|Se **tipo** viene **3**, questa colonna viene visualizzata la query per l'evento WMI.|  
|**type**|**int**|Tipo dell'evento:<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avviso per evento<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avviso relativo alle prestazioni<br /><br /> **3** = avviso per evento WMI|  
  
 Quando **@legacy_format** viene **1**, **sp_help_alert** produce il set di risultati seguente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificatore univoco di tipo integer assegnato dal sistema.|  
|**name**|**sysname**|Nome dell'avviso (ad esempio Demo: Completi **msdb** log).|  
|**event_source**|**nvarchar(100)**|Origine dell'evento. Sarà sempre **MSSQLServer** per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 7.0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|Numero dell'errore del messaggio che definisce l'avviso (In genere corrisponde a un numero di errore il **sysmessages** tabella). Se utilizzata per definire l'avviso, gravità **message_id** viene **0** o NULL.|  
|**severity**|**int**|Livello di gravità (da **9** attraverso **25**, **110**, **120**, **130**, o 1**40**) che definisce l'avviso.|  
|**enabled**|**tinyint**|Stato del fatto che l'avviso è abilitato (**1**) o No (**0**). Gli avvisi non abilitati non vengono inviati.|  
|**delay_between_responses**|**int**|Periodo di attesa in secondi tra risposte successive per l'avviso.|  
|**last_occurrence_date**|**int**|Data dell'ultima generazione dell'avviso.|  
|**last_occurrence_time**|**int**|Ora dell'ultima generazione dell'avviso.|  
|**last_response_date**|**int**|Data ultimo avviso ha risposto a per il **SQLServerAgent** servizio.|  
|**last_response_time**|**int**|Ora dell'ultima l'avviso ha risposto a per il **SQLServerAgent** servizio.|  
|**notification_message**|**nvarchar(512)**|Messaggio aggiuntivo facoltativo inviato all'operatore come parte della notifica tramite posta elettronica o cercapersone.|  
|**include_event_description**|**tinyint**|Indica se la descrizione dell'errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclusa nel registro applicazioni di Windows deve essere inserita nel messaggio di notifica.|  
|**database_name**|**sysname**|Database in cui deve verificarsi l'errore affinché l'avviso venga generato. Se il nome del database è NULL, l'avviso viene generato indipendentemente dal database in cui l'errore si verifica.|  
|**event_description_keyword**|**nvarchar(100)**|Descrizione dell'errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclusa nel registro applicazioni di Windows, che deve corrispondere alla sequenza di caratteri specificata.|  
|**occurrence_count**|**int**|Numero di volte che l'avviso è stato generato.|  
|**count_reset_date**|**int**|Data la **numero_occorrenze** ultima reimpostazione.|  
|**count_reset_time**|**int**|Ora il **numero_occorrenze** ultima reimpostazione.|  
|**job_id**|**uniqueidentifier**|Numero di identificazione del processo.|  
|**job_name**|**sysname**|Processo su richiesta da eseguire in risposta a un avviso.|  
|**has_notification**|**int**|È diverso da zero se uno o più operatori ricevono una notifica dell'avviso. Può essere uno o più d'uno dei valori seguenti uniti dall'operatore OR:<br /><br /> **1**= notifica tramite posta elettronica<br /><br /> **2**= notifica tramite cercapersone<br /><br /> **4**= ha **net send** notifica.|  
|**flags**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] (Indici per tabelle con ottimizzazione per la memoria).|  
|**performance_condition**|**nvarchar(512)**|Se **tipo** viene **2**, questa colonna Mostra la definizione della condizione delle prestazioni. Se **tipo** viene **3**, questa colonna viene visualizzata la query per l'evento WMI. Negli altri casi la colonna è NULL.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] Sarà sempre ' **[senza categoria]** ' per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.|  
|**type**|**int**|Tipo di avviso:<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avviso per evento<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avviso relativo alle prestazioni<br /><br /> **3** = avviso per evento WMI|  
  
## <a name="remarks"></a>Note  
 **sp_help_alert** deve essere eseguita la **msdb** database.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono appartenere al ruolo predefinito del database **SQLAgentOperatorRole** nel database **msdb** .  
  
 Per informazioni dettagliate sui **SQLAgentOperatorRole**, vedere [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sull'avviso `Demo: Sev. 25 Errors`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
