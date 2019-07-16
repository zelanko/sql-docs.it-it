---
title: sp_notify_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_notify_operator_TSQL
- sp_notify_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_notify_operator
ms.assetid: c440f5c9-9884-4196-b07c-55d87afb17c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 74558320df59414a756e1655bb073e9bf0d7d73c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107983"
---
# <a name="spnotifyoperator-transact-sql"></a>sp_notify_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Invia un messaggio di posta elettronica a un operatore tramite Posta elettronica database.  
  
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_notify_operator  
    [ @profile_name = ] 'profilename' ,  
    [ @id = ] id ,  
    [ @name = ] 'name' ,  
    [ @subject = ] 'subject' ,  
    [ @body = ] 'message' ,  
    [ @file_attachments = ] 'attachment'  
    [ @mail_database = ] 'mail_host_database'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @profile_name = ] 'profilename'` Il nome del profilo di posta elettronica Database da usare per inviare il messaggio. *ProfileName* viene **nvarchar (128)** . Se *profilename* viene omesso, viene utilizzato il profilo di posta elettronica Database predefinito.  
  
`[ @id = ] id` L'identificatore per l'operatore a cui inviare il messaggio. *ID* viene **int**, con un valore predefinito è NULL. Uno dei *id* oppure *nome* deve essere specificato.  
  
`[ @name = ] 'name'` Il nome dell'operatore a cui inviare il messaggio. *nome* viene **nvarchar (128)** , con un valore predefinito è NULL. Uno dei *id* oppure *nome* deve essere specificato.  
  
> **NOTA:** Indirizzo di posta elettronica debba essere definito per l'operatore possa ricevere messaggi.  
  
`[ @subject = ] 'subject'` Oggetto per il messaggio di posta elettronica. *Subject* viene **nvarchar(256)** non prevede alcun valore predefinito.  
  
`[ @body = ] 'message'` Il corpo del messaggio di posta elettronica. *messaggio* viene **nvarchar (max)** non prevede alcun valore predefinito.  
  
`[ @file_attachments = ] 'attachment'` Il nome di un file da allegare al messaggio di posta elettronica. *allegato* viene **nvarchar(512)** , non prevede alcun valore predefinito.  
  
`[ @mail_database = ] 'mail_host_database'` Specifica il nome del database host della posta elettronica. *mail_host_database* viene **nvarchar (128)** . Se nessun *mail_host_database* è specificato, il **msdb** database viene utilizzato per impostazione predefinita.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 Invia il messaggio specificato all'indirizzo di posta elettronica dell'operatore. Se non è stato configurato un indirizzo di posta elettronica per l'operatore, viene restituito un errore.  
  
 Per poter inviare una notifica a un operatore, è necessario innanzitutto configurare Posta elettronica database e un database host della posta elettronica.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene inviato un messaggio di notifica all'operatore `François Ajenstat` tramite il profilo `AdventureWorks Administrator` di Posta elettronica database. L'oggetto del messaggio di posta elettronica è `Test Notification`. The e-mail message contains the sentence, "This is a test of notification via e-mail."  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_notify_operator  
   @profile_name = N'AdventureWorks Administrator',  
   @name = N'François Ajenstat',  
   @subject = N'Test Notification',  
   @body = N'This is a test of notification via e-mail.' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  
