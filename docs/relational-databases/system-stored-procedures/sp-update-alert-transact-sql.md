---
title: sp_update_alert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
author: stevestein
ms.author: sstein
ms.openlocfilehash: baecdca82d7edcb27196c7c43d9d071a82adf792
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084954"
---
# <a name="spupdatealert-transact-sql"></a>sp_update_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiorna le impostazioni di un avviso esistente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_alert   
     [ @name =] 'name'   
     [ , [ @new_name =] 'new_name']   
     [ , [ @enabled =] enabled]   
     [ , [ @message_id =] message_id]   
     [ , [ @severity =] severity]   
     [ , [ @delay_between_responses =] delay_between_responses]   
     [ , [ @notification_message =] 'notification_message']   
     [ , [ @include_event_description_in =] include_event_description_in]   
     [ , [ @database_name =] 'database']   
     [ , [ @event_description_keyword =] 'event_description_keyword']   
     [ , [ @job_id =] job_id | [@job_name =] 'job_name']   
     [ , [ @occurrence_count = ] occurrence_count]   
     [ , [ @count_reset_date =] count_reset_date]   
     [ , [ @count_reset_time =] count_reset_time]   
     [ , [ @last_occurrence_date =] last_occurrence_date]   
     [ , [ @last_occurrence_time =] last_occurrence_time]   
     [ , [ @last_response_date =] last_response_date]   
     [ , [ @last_response_time =] last_response _time]  
     [ , [ @raise_snmp_trap =] raise_snmp_trap]  
     [ , [ @performance_condition =] 'performance_condition' ]   
     [ , [ @category_name =] 'category']  
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name = ] 'name'` Il nome dell'avviso che deve essere aggiornato. *nome* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @new_name = ] 'new_name'` Un nuovo nome per l'avviso. Il nome deve essere univoco. *new_name* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @enabled = ] enabled` Specifica se l'avviso è abilitato (**1**) o non abilitato (**0**). *abilitata* viene **tinyint**, con un valore predefinito è NULL. Per consentire la generazione di un avviso, è necessario che l'avviso sia abilitato.  
  
`[ @message_id = ] message_id` Un nuovo messaggio o errore numero per la definizione di avviso. In genere *message_id* corrisponde a un numero di errore il **sysmessages** tabella. *message_id* viene **int**, con un valore predefinito è NULL. Un messaggio ID può essere usato solo se è l'impostazione del livello di gravità dell'avviso **0**.  
  
`[ @severity = ] severity` Nuovo livello di gravità (da **1** attraverso **25**) per la definizione di avviso. Eventuali [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'avviso verranno attivato da messaggi inviati al registro applicazioni di Windows con il livello di gravità specificato. *livello di gravità* viene **int**, con un valore predefinito è NULL. Un livello di gravità può essere utilizzato solo se l'impostazione di ID di messaggio per l'avviso viene **0**.  
  
`[ @delay_between_responses = ] delay_between_responses` Nuovo intervallo di attesa, espresso in secondi, tra le risposte all'avviso. *delay_between_responses* viene **int**, con un valore predefinito è NULL.  
  
`[ @notification_message = ] 'notification_message'` Testo modificato di un messaggio aggiuntivo inviato all'operatore come parte del messaggio di posta elettronica, **net send**, o notifica tramite cercapersone. *notification_message* viene **nvarchar(512)** , con un valore predefinito è NULL.  
  
`[ @include_event_description_in = ] include_event_description_in` Specifica se la descrizione del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] errore nel registro applicazioni di Windows deve essere inclusi nel messaggio di notifica. *include_event_description_in* viene **tinyint**, con un valore predefinito è NULL, e può essere uno o più dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Nessuna|  
|**1**|Posta elettronica|  
|**2**|Cercapersone|  
|**4**|**net send**|  
|**7**|Tutti|  
  
`[ @database_name = ] 'database'` Il nome del database in cui deve verificarsi l'errore affinché l'avviso venga generato. *database* è **sysname.** I nomi racchiusi tra parentesi quadre ([ ]) non sono ammessi. Il valore predefinito è NULL.  
  
`[ @event_description_keyword = ] 'event_description_keyword'` Una sequenza di caratteri che deve trovarsi nella descrizione dell'errore nel log dei messaggi di errore. È possibile utilizzare i caratteri dei criteri di ricerca dell'espressione LIKE [!INCLUDE[tsql](../../includes/tsql-md.md)]. *event_description_keyword* viene **nvarchar(100)** , con un valore predefinito è NULL. Questo parametro è utile per filtrare i nomi degli oggetti (ad esempio, **% customer_table %** ).  
  
`[ @job_id = ] job_id` ID del processo. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL. Se *job_id* omette *job_name* deve essere omessa.  
  
`[ @job_name = ] 'job_name'` Il nome del processo che viene eseguito in risposta all'avviso. *nome_processo* viene **sysname**, con un valore predefinito è NULL. Se *nome_processo* omette *job_id* deve essere omessa.  
  
`[ @occurrence_count = ] occurrence_count` Reimposta il numero di volte in cui che si è verificato l'avviso. *numero_occorrenze* viene **int**, con un valore predefinito è NULL e può essere impostata solo su **0**.  
  
`[ @count_reset_date = ] count_reset_date` Reimposta la data che dell'ultima reimpostazione il conteggio delle occorrenze. *count_reset_date* viene **int**, con un valore predefinito è NULL.  
  
`[ @count_reset_time = ] count_reset_time` Reimposta l'ora che dell'ultima reimpostazione il conteggio delle occorrenze. *count_reset_time* viene **int**, con un valore predefinito è NULL.  
  
`[ @last_occurrence_date = ] last_occurrence_date` Reimposta la data che dell'ultima occorrenza dell'avviso. *last_occurrence_date* viene **int**, con un valore predefinito è NULL e può essere impostata solo su **0**.  
  
`[ @last_occurrence_time = ] last_occurrence_time` Reimposta l'ora che dell'ultima occorrenza dell'avviso. *last_occurrence_time* viene **int**, con un valore predefinito è NULL e può essere impostata solo su **0**.  
  
`[ @last_response_date = ] last_response_date` Reimposta la data che di ultima risposta all'avviso dal servizio SQLServerAgent. *last_response_date* viene **int**, con un valore predefinito è NULL e può essere impostata solo su **0**.  
  
`[ @last_response_time = ] last_response_time` Reimposta l'ora che l'ultima risposta all'avviso dal servizio SQLServerAgent. *last_response_time* viene **int**, con un valore predefinito è NULL e può essere impostata solo su **0**.  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` Riservato.  
  
`[ @performance_condition = ] 'performance_condition'` Un valore espresso nel formato **»***itemcomparatorvalue***'** . *performance_condition* viene **nvarchar(512)** , con un valore predefinito è NULL ed è costituito da questi elementi.  
  
|Componente del formato|Descrizione|  
|--------------------|-----------------|  
|*Elemento*|Oggetto prestazioni, contatore delle prestazioni o istanza denominata del contatore|  
|*Criterio di confronto*|Uno degli operatori seguenti: **>** , **<** , **=**|  
|*Valore*|Valore numerico del contatore|  
  
`[ @category_name = ] 'category'` Il nome della categoria di avvisi. *categoria* viene **sysname** con valore predefinito è NULL.  
  
`[ @wmi_namespace = ] 'wmi_namespace'` Lo spazio dei nomi WMI per eseguire query per gli eventi. *wmi_namespace* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @wmi_query = ] 'wmi_query'` La query che specifica l'evento WMI per l'avviso. *Wmi_query* viene **nvarchar(512)** , con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 Solo **sysmessages** scritto il [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro applicazioni di Windows può essere generato un avviso.  
  
 **sp_update_alert** modificare solo le impostazioni di avviso per il parametro che vengono specificati i valori. Se si omette un parametro, viene mantenuta l'impostazione corrente.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa stored procedure, gli utenti devono essere un membro del **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente l'impostazione di abilitazione di `Test Alert` viene sostituita con `0`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_alert  
    @name = N'Test Alert',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
