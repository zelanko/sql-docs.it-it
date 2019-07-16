---
title: sp_add_alert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_alert
- sp_add_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b16fe1f29d132b900eeb4c8f450fcdbd66eb22b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942388"
---
# <a name="spaddalert-transact-sql"></a>sp_add_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un avviso.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_alert [ @name = ] 'name'   
     [ , [ @message_id = ] message_id ]   
     [ , [ @severity = ] severity ]   
     [ , [ @enabled = ] enabled ]  
     [ , [ @delay_between_responses = ] delay_between_responses ]   
     [ , [ @notification_message = ] 'notification_message' ]   
     [ , [ @include_event_description_in = ] include_event_description_in ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @event_description_keyword = ] 'event_description_keyword_pattern' ]   
     [ , { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ]   
     [ , [ @raise_snmp_trap = ] raise_snmp_trap ]   
     [ , [ @performance_condition = ] 'performance_condition' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name = ] 'name'` Il nome dell'avviso. Tale nome viene visualizzato nel messaggio di posta elettronica o di cercapersone inviato in risposta all'avviso. Deve essere univoco e può contenere la percentuale ( **%** ) caratteri. *nome* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @message_id = ] message_id` Il numero di errore di messaggio che definisce l'avviso. (Corrisponde in genere a un numero di errore il **sysmessages** tabella.) *message_id* viene **int**, il valore predefinito è **0**. Se *severity* viene usato per l'avviso, definire *message_id* deve essere **0** o NULL.  
  
> [!NOTE]  
>  Solo **sysmessages** errori scritti nel registro applicazioni di Microsoft Windows possono causare un avviso da inviare.  
  
`[ @severity = ] severity` Il livello di gravità (da **1** attraverso **25**) che definisce l'avviso. Eventuali [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] messaggio archiviato nel **sysmessages** inviata alla tabella il [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro applicazioni di Windows con indicazione della gravità provoca l'avviso da inviare. *livello di gravità* viene **int**, con un valore predefinito è 0. Se *message_id* viene usato per l'avviso, definire *gravità* deve essere **0**.  
  
`[ @enabled = ] enabled` Indica lo stato corrente dell'avviso. *abilitata* viene **tinyint**, con un valore predefinito è 1 (abilitato). Se **0**, l'avviso non è abilitato e non venga attivato.  
  
`[ @delay_between_responses = ] delay_between_responses` Periodo di attesa, espresso in secondi, tra le risposte all'avviso. *delay_between_responses*viene **int**, il valore predefinito è **0**, non ovvero non esiste alcun intervallo di attesa tra le risposte (ogni occorrenza dell'avviso genera una risposta). La risposta può assumere una delle due forme seguenti:  
  
-   Una o più notifiche inviate tramite posta elettronica o cercapersone.  
  
-   Un processo da eseguire.  
  
 L'impostazione di tale valore impedisce, ad esempio, l'invio di più messaggi di posta elettronica quando un avviso viene generato ripetutamente in un breve periodo di tempo.  
  
`[ @notification_message = ] 'notification_message'` Messaggio aggiuntivo facoltativo inviato all'operatore come parte del messaggio di posta elettronica, **net send**, o notifica tramite cercapersone. *notification_message* viene **nvarchar(512)** , con un valore predefinito è NULL. Che specifica *notification_message* è utile per aggiungere note speciali, ad esempio procedure correttive.  
  
`[ @include_event_description_in = ] include_event_description_in` È se la descrizione del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] errore debba essere inclusi come parte del messaggio di notifica. *include_event_description_in*viene **tinyint**, il valore predefinito è **5** (messaggio di posta elettronica e **net send**) e può avere uno o più dei valori seguenti combinati con un **o** operatore logico.  
  
> [!IMPORTANT]
>  Le opzioni Cercapersone e **net send** verranno rimosse da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare pertanto di utilizzarle in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui sono state implementate.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Nessuna|  
|**1**|Posta elettronica|  
|**2**|Cercapersone|  
|**4**|**net send**|  
  
`[ @database_name = ] 'database'` Il database in cui deve verificarsi l'errore affinché l'avviso venga generato. Se *database*viene omesso, l'avviso viene attivato indipendentemente dalla posizione dell'errore. *database* viene **sysname**. I nomi racchiusi tra parentesi quadre ([ ]) non sono ammessi. Il valore predefinito è NULL.  
  
`[ @event_description_keyword = ] 'event_description_keyword_pattern'` La sequenza di caratteri che la descrizione del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] errore deve essere uguali. È possibile utilizzare i caratteri dei criteri di ricerca dell'espressione LIKE [!INCLUDE[tsql](../../includes/tsql-md.md)]. *event_description_keyword_pattern* viene **nvarchar(100)** , con un valore predefinito è NULL. Questo parametro è utile per filtrare i nomi degli oggetti (ad esempio, **% customer_table %** ).  
  
`[ @job_id = ] job_id` Il numero di identificazione del processo da eseguire in risposta all'avviso. *job_id* viene **uniqueidentifier**, con un valore predefinito è NULL.  
  
`[ @job_name = ] 'job_name'` Il nome del processo da eseguire in risposta all'avviso. *nome_processo*viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Entrambi *job_id* oppure *job_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` Non è implementata in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 7.0. *raise_snmp_trap* viene **tinyint**, con un valore predefinito è 0.  
  
`[ @performance_condition = ] 'performance_condition'` È un valore espresso nel formato '*itemcomparatorvalue*'. *performance_condition* viene **nvarchar(512)** con un valore predefinito è NULL ed è costituito da questi elementi.  
  
|Componente del formato|Descrizione|  
|--------------------|-----------------|  
|*Elemento*|Oggetto prestazioni, contatore delle prestazioni o istanza denominata del contatore|  
|*Criterio di confronto*|Uno degli operatori seguenti: >, <, o =|  
|*Valore*|Valore numerico del contatore|  
  
`[ @category_name = ] 'category'` Il nome della categoria di avvisi. *categoria* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @wmi_namespace = ] 'wmi_namespace'` Lo spazio dei nomi WMI per eseguire query per gli eventi. *wmi_namespace* viene **sysname**, con un valore predefinito è NULL. Sono supportati solo gli spazi di nomi nel server locale.  
  
`[ @wmi_query = ] 'wmi_query'` La query che specifica l'evento WMI per l'avviso. *Wmi_query* viene **nvarchar(512)** , con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 **sp_add_alert** deve essere eseguita la **msdb** database.  
  
 Di seguito sono descritti i casi in cui gli errori/messaggi generati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e da applicazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono inviati al registro applicazioni di Windows in modo da poter generare avvisi:  
  
-   Livello di gravità 19 o superiore **Sys. Messages** errori  
  
-   Qualsiasi istruzione RAISERROR richiamata con la clausola WITH LOG  
  
-   Eventuali **Sys. Messages** errore modificato o creato tramite **sp_altermessage**  
  
-   Qualsiasi evento registrato tramite **xp_logevent**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] include un semplice strumento grafico per la gestione del sistema di avvisi ed è lo strumento consigliato per la configurazione di un'infrastruttura di avvisi.  
  
 Se un avviso non funziona adeguatamente, controllare se:  
  
-   Il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è in esecuzione.  
  
-   L'evento è incluso nel registro applicazioni di Windows.  
  
-   L'avviso è attivato.  
  
-   Gli eventi generati con la stored procedure **xp_logevent** si verificano nel database master. Pertanto, **xp_logevent** genera un avviso solo se **@database_name** per l'avviso è **'master'** o NULL.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_add_alert**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene aggiunto un avviso (Test Alert) che esegue il processo `Back up the AdventureWorks2012 Database` quando viene generato.  
  
> [!NOTE]  
>  Nell'esempio si presuppone che il messaggio 55001 e il processo `Back up the AdventureWorks2012 Database` siano già esistenti. Questo esempio viene fornito solo a scopo illustrativo.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_alert  
    @name = N'Test Alert',  
    @message_id = 55001,   
   @severity = 0,   
   @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
   @job_name = N'Back up the AdventureWorks2012 Database' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
