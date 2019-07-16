---
title: sysmail_help_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2b5f416d1f2989cd9392ecac0279e792477cca8d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909179"
---
# <a name="sysmailhelpaccountsp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza un elenco di informazioni (eccetto le password) sugli account di Posta elettronica database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @account_id = ] account_id` ID dell'account dell'account da elenco di informazioni. *account_id* viene **int**, con un valore predefinito è NULL.  
  
`[ @account_name = ] 'account_name'` Il nome dell'account da elenco di informazioni. *account_name* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce un set di risultati contenente le colonne elencate di seguito.  
  
||||  
|-|-|-|  
|Nome colonna|Tipo di dati|Descrizione|  
|**account_id**|**int**|ID dell'account.|  
|**name**|**sysname**|Nome dell'account.|  
|**description**|**nvarchar(256)**|Descrizione dell'account.|  
|**email_address**|**nvarchar(128)**|Indirizzo di posta elettronica da cui inviare i messaggi.|  
|**display_name**|**nvarchar(128)**|Nome visualizzato dell'account.|  
|**replyto_address**|**nvarchar(128)**|Indirizzo a cui vengono inviate le risposte ai messaggi da questo account.|  
|**servertype**|**sysname**|Tipo di server di posta elettronica per l'account.|  
|**servername**|**sysname**|Nome del server di posta elettronica per l'account.|  
|**port**|**int**|Numero della porta del server di posta elettronica.|  
|**username**|**nvarchar(128)**|Nome utente da utilizzare per accedere al server di posta elettronica se il server di posta elettronica utilizza l'autenticazione. Quando **username** è NULL, posta elettronica Database non utilizza l'autenticazione per questo account.|  
|**use_default_credentials**|**bit**|Specifica se inviare la posta elettronica al server SMTP utilizzando le credenziali di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** è di tipo bit e non prevede alcun valore predefinito. Se questo parametro è 1, Posta elettronica database utilizza le credenziali del servizio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Quando questo parametro è 0, posta elettronica Database utilizza il **@username** e **@password** per l'autenticazione nel server SMTP. Se **@username** e **@password** sono NULL e quindi posta elettronica Database utilizza l'autenticazione anonima. Prima di specificare questo parametro consultare l'amministratore del server SMTP.|  
|**enable_ssl**|**bit**|Specifica l'utilizzo della crittografia mediante SSL (Secure Sockets Layer) da parte di Posta elettronica database. Utilizzare questa opzione se SSL è obbligatorio per il server SMTP. **enable_ssl** è di tipo bit e non prevede alcun valore predefinito. 1 indica che le comunicazioni vengono crittografate mediante SSL. 0 indica che i messaggi vengono inviati senza utilizzare la crittografia SSL.|  
  
## <a name="remarks"></a>Note  
 Se non si specifica *account_id* oppure *account_name* viene fornito **sysmail_help_account** Elenca le informazioni su tutti gli account di posta elettronica Database nell'istanza di Microsoft SQL Server.  
  
 La stored procedure **sysmail_help_account_sp** nel **msdb** database ed è di proprietà di **dbo** dello schema. La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni per questa routine per impostazione predefinita ai membri di esecuzione per il **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 **A. Elenco di informazioni per tutti gli account**  
  
 Nell'esempio seguente viene visualizzato un elenco di informazioni per tutti gli account nell'istanza.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp ;  
```  
  
 Quello che segue è un set di risultati di esempio, modificato per adattarlo alla lunghezza di riga.  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- --------------------------------------- ------------------------- -------------------------------- --------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
149         Audit Account                Account for audit e-mail.               audit@Adventure-Works.com Automated Mailer (Audit)         NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
```  
  
 **B. Elenco di informazioni per un account specifico**  
  
 Nell'esempio seguente viene visualizzato un elenco di informazioni di account per l'account denominato `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
 Quello che segue è un set di risultati di esempio, modificato per adattarlo alla lunghezza di riga.  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- ------------------------------------------------------ ------------------------- ---------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL     0                       0       
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Creare un Account di posta elettronica Database](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Stored procedure di posta elettronica database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
