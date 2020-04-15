---
title: sysmail_update_account_sp (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3dd772a1519ea856cac0302d31be9eb7d0f9d782
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283164"
---
# <a name="sysmail_update_account_sp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica le informazioni di un account di Posta elettronica database esistente.  
 
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_update_account_sp [ [ @account_id = ] account_id ] [ , ] [ [ @account_name = ] 'account_name' ] ,  
    [ @email_address = ] 'email_address' ,   
    [ @display_name = ] 'display_name' ,   
    [ @replyto_address = ] 'replyto_address' ,  
    [ @description = ] 'description' ,   
    [ @mailserver_name = ] 'server_name' ,   
    [ @mailserver_type = ] 'server_type' ,   
    [ @port = ] port_number ,   
    [ @timeout = ] 'timeout' ,  
    [ @username = ] 'username' ,  
    [ @password = ] 'password' ,  
    [ @use_default_credentials = ] use_default_credentials ,  
    [ @enable_ssl = ] enable_ssl   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @account_id = ] account_id`ID dell'account da aggiornare. *account_id* è **int**, con un valore predefinito NULL. È necessario specificare almeno uno *account_id* o *un account_name.* Se si specificano entrambi, la stored procedure modifica il nome dell'account.  
  
`[ @account_name = ] 'account_name'`Nome dell'account da aggiornare. *account_name* è **sysname**, con un valore predefinito NULL. È necessario specificare almeno uno *account_id* o *un account_name.* Se si specificano entrambi, la stored procedure modifica il nome dell'account.  
  
`[ @email_address = ] 'email_address'`Nuovo indirizzo di posta elettronica da cui inviare il messaggio. Deve essere un indirizzo di posta elettronica Internet. Il nome del server nell'indirizzo è il server utilizzato da Posta elettronica database per l'invio di posta da questo account. *email_address* è **di tipo nvarchar(128)** e il valore predefinito è NULL.  
  
`[ @display_name = ] 'display_name'`Nuovo nome visualizzato da utilizzare nei messaggi di posta elettronica provenienti da questo account. *display_name* è **di tipo nvarchar(128)** e non prevede alcun valore predefinito.  
  
`[ @replyto_address = ] 'replyto_address'`Nuovo indirizzo da utilizzare nell'intestazione Rispondi a dei messaggi di posta elettronica provenienti da questo account. *replyto_address* è **di tipo nvarchar(128)** e non prevede alcun valore predefinito.  
  
`[ @description = ] 'description'`Nuova descrizione per l'account. *description* è **di tipo nvarchar(256)** e il valore predefinito è NULL.  
  
`[ @mailserver_name = ] 'server_name'`Nuovo nome del server di posta SMTP da utilizzare per questo account. Il computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione deve essere in grado di risolvere il *server_name* in un indirizzo IP. *server_name* è **sysname**, senza alcun valore predefinito.  
  
`[ @mailserver_type = ] 'server_type'`Nuovo tipo di server di posta. *server_type* è **sysname**, senza alcun valore predefinito. È supportato solo il valore **'SMTP'.**  
  
`[ @port = ] port_number`Nuovo numero di porta del server di posta. *port_number* è **int**, senza alcun valore predefinito.  
  
`[ @timeout = ] 'timeout'`Parametro Timeout per SmtpClient.Send di un singolo messaggio di posta elettronica. *Timeout* è **int** in secondi, senza alcun valore predefinito.  
  
`[ @username = ] 'username'`Nuovo nome utente da utilizzare per accedere al server di posta. *Il nome utente* è **sysname**, senza alcun valore predefinito.  
  
`[ @password = ] 'password'`Nuova password da utilizzare per accedere al server di posta. *password* è **di tipo sysname**, senza alcun valore predefinito.  
  
`[ @use_default_credentials = ] use_default_credentials`Specifica se inviare la posta al server SMTP [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilizzando le credenziali del servizio. **use_default_credentials** è bit, senza alcun valore predefinito. Se questo parametro è 1, Posta elettronica database utilizza le credenziali di [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Quando questo parametro è 0, ** \@** Posta elettronica database utilizza il ** \@nome utente** e la password per l'autenticazione sul server SMTP. Se ** \@nome utente** e ** \@password** sono NULL, verrà utilizzata l'autenticazione anonima. Prima di specificare questo parametro consultare l'amministratore del server SMTP.  
  
`[ @enable_ssl = ] enable_ssl`Specifica se Posta elettronica database crittografa le comunicazioni utilizzando Transport Layer Security (TLS), precedentemente noto come Secure Sockets Layer (SSL). Utilizzare questa opzione se TLS è richiesto sul server SMTP. **enable_ssl** è bit, senza alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Osservazioni  
 Se si specificano sia il nome dell'account che l'ID dell'account, la stored procedure modifica il nome dell'account, oltre ad aggiornare le informazioni relative all'account. Questo può essere utile se è necessario correggere un errore nel nome dell'account.  
  
 La stored procedure **sysmail_update_account_sp** si trova nel database **msdb** ed è di proprietà dello schema **dbo.** La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-changing-the-information-for-an-account"></a>R. Modifica delle informazioni di un account  
 Nell'esempio seguente `AdventureWorks Administrator` viene aggiornato l'account nel database **msdb.** Le informazioni dell'account vengono impostate in base ai valori specificati.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_name = 'AdventureWorks Administrator'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>B. Modifica del nome e delle informazioni di un account  
 Nell'esempio seguente vengono modificati il nome e le informazioni dell'account con ID `125`. Il nuovo nome dell'account è `Backup Mail Server`.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_id = 125  
    ,@account_name = 'Backup Mail Server'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp-backup.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Creare un account di posta elettronica del database](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail Stored Procedure &#40;&#41;Transact-SQLDatabase Mail Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
