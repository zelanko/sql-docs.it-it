---
title: sysmail_help_account_sp (Transact-SQL) Documenti Microsoft
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
ms.openlocfilehash: ccb5cfd245148c97288a34b1857955f48f3efc73
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528415"
---
# <a name="sysmail_help_account_sp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza un elenco di informazioni (eccetto le password) sugli account di Posta elettronica database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @account_id = ] account_id`ID account dell'account per cui elencare le informazioni. *account_id* è **int**, con un valore predefinito NULL.  
  
`[ @account_name = ] 'account_name'`Nome dell'account di cui elencare le informazioni. *account_name* è **sysname**, con un valore predefinito NULL.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce un set di risultati contenente le colonne elencate di seguito.  
  
||||  
|-|-|-|  
|Nome colonna|Tipo di dati|Descrizione|  
|**account_id**|**int**|ID dell'account.|  
|**nome**|**sysname**|Nome dell'account.|  
|**Descrizione**|**nvarchar(256)**|Descrizione dell'account.|  
|**email_address**|**nvarchar(128)**|Indirizzo di posta elettronica da cui inviare i messaggi.|  
|**display_name**|**nvarchar(128)**|Nome visualizzato dell'account.|  
|**replyto_address**|**nvarchar(128)**|Indirizzo a cui vengono inviate le risposte ai messaggi da questo account.|  
|**Servertype**|**sysname**|Tipo di server di posta elettronica per l'account.|  
|**Nomeserver**|**sysname**|Nome del server di posta elettronica per l'account.|  
|**port**|**int**|Numero della porta del server di posta elettronica.|  
|**Nome utente**|**nvarchar(128)**|Nome utente da utilizzare per accedere al server di posta elettronica se il server di posta elettronica utilizza l'autenticazione. Quando **nomeutente** è NULL, Posta elettronica database non utilizza l'autenticazione per questo account.|  
|**use_default_credentials**|**bit**|Specifica se inviare la posta elettronica al server SMTP utilizzando le credenziali di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** è bit, senza alcun valore predefinito. Se questo parametro è 1, Posta elettronica database utilizza le credenziali del servizio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Quando questo parametro è 0, ** \@** Posta elettronica database utilizza il ** \@nome utente** e la password per l'autenticazione sul server SMTP. Se ** \@nomeutente** e ** \@password** sono NULL, Posta elettronica database utilizza l'autenticazione anonima. Prima di specificare questo parametro consultare l'amministratore del server SMTP.|  
|**enable_ssl**|**bit**|Specifica se Posta elettronica database crittografa le comunicazioni utilizzando Transport Layer Security (TLS), precedentemente noto come Secure Sockets Layer (SSL). Utilizzare questa opzione se TLS è richiesto sul server SMTP. **enable_ssl** è bit, senza alcun valore predefinito. 1 indica che Posta del database crittografa le comunicazioni utilizzando TLS. 0 indica che Posta elettronica database invia la posta senza crittografia TLS.|  
  
## <a name="remarks"></a>Osservazioni  
 Quando non viene fornita *alcuna account_id* o *account_name,* **sysmail_help_account** elenca le informazioni su tutti gli account di Posta elettronica database nell'istanza di Microsoft SQL Server.  
  
 La stored procedure **sysmail_help_account_sp** si trova nel database **msdb** ed è di proprietà dello schema **dbo.** La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Autorizzazioni  
 Le autorizzazioni di esecuzione per questa procedura vengono utilizzate per impostazione predefinita per i membri del ruolo predefinito del server **sysadmin.**  
  
## <a name="examples"></a>Esempi  
 **A. Visualizzazione di un elenco di informazioni per tutti gli account**  
  
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
  
 **B. Visualizzazione di un elenco di informazioni per un account specifico**  
  
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
 [Creare un account di posta elettronica del database](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail Stored Procedure &#40;&#41;Transact-SQLDatabase Mail Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
