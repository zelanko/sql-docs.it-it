---
title: sysmail_add_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b41b0c0ae805923a10d0ee9c4fd066b1202fa94
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537893"
---
# <a name="sysmailaddaccountsp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un nuovo account di Posta elettronica database contenente informazioni su un account SMTP.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_add_account_sp  [ @account_name = ] 'account_name',  
    [ @email_address = ] 'email_address' ,  
    [ [ @display_name = ] 'display_name' , ]  
    [ [ @replyto_address = ] 'replyto_address' , ]  
    [ [ @description = ] 'description' , ]  
    [ @mailserver_name = ] 'server_name'   
    [ , [ @mailserver_type = ] 'server_type' ]  
    [ , [ @port = ] port_number ]  
    [ , [ @username = ] 'username' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @use_default_credentials = ] use_default_credentials ]  
    [ , [ @enable_ssl = ] enable_ssl ]  
    [ , [ @account_id = ] account_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @account_name = ] 'account_name'` Il nome dell'account da aggiungere. *account_name* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @email_address = ] 'email_address'` L'indirizzo di posta elettronica da cui inviare il messaggio. Deve essere un indirizzo di posta elettronica Internet. *email_address* viene **nvarchar (128)**, non prevede alcun valore predefinito. Ad esempio, un account per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può inviare posta elettronica dall'indirizzo **SqlAgent@Adventure-Works.com**.  
  
`[ @display_name = ] 'display_name'` Il nome visualizzato da utilizzare nei messaggi di posta elettronica da questo account. *DISPLAY_NAME* viene **nvarchar (128)**, con un valore predefinito è NULL. Ad esempio, un account per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può visualizzare il nome **SQL Server Agent Automated Mailer** nei messaggi di posta elettronica.  
  
`[ @replyto_address = ] 'replyto_address'` L'indirizzo che vengono inviate le risposte ai messaggi da questo account a. *replyto_address* viene **nvarchar (128)**, con un valore predefinito è NULL. Ad esempio, risposte a un account per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente possono essere indirizzate all'amministratore del database **danw@Adventure-Works.com**.  
  
`[ @description = ] 'description'` È una descrizione per l'account. *Descrizione* viene **nvarchar(256)**, con un valore predefinito è NULL.  
  
`[ @mailserver_name = ] 'server_name'` Il nome o indirizzo IP del server di posta SMTP da utilizzare per questo account. Il computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere in grado di risolvere le *server_name* a un indirizzo IP. *nome_server* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @mailserver_type = ] 'server_type'` Tipo di server di posta elettronica. *server_type* viene **sysname**, il valore predefinito è **'SMTP'**...  
  
`[ @port = ] port_number` Il numero di porta per il server di posta elettronica. *port_number* viene **int**, con un valore predefinito pari a 25.  
  
`[ @username = ] 'username'` Il nome utente da utilizzare per accedere al server di posta elettronica. *nome utente* viene **nvarchar (128)**, con un valore predefinito è NULL. Se questo parametro è NULL, Posta elettronica database non utilizza l'autenticazione per questo account. Se il server di posta elettronica non richiede l'autenticazione, specificare NULL per il nome utente.  
  
`[ @password = ] 'password'` La password da utilizzare per accedere al server di posta elettronica. *la password* viene **nvarchar (128)**, con un valore predefinito è NULL. Non è necessario specificare una password se non si specifica un nome utente.  
  
`[ @use_default_credentials = ] use_default_credentials` Specifica se inviare la posta elettronica al server SMTP utilizzando le credenziali del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** è di tipo bit e il valore predefinito è 0. Se questo parametro è 1, Posta elettronica database utilizza le credenziali di [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Quando questo parametro è 0, posta elettronica Database invia il **@username** e **@password** parametri, se presente, in caso contrario invia il messaggio senza **@username**e **@password** parametri.  
  
`[ @enable_ssl = ] enable_ssl` Specifica se posta elettronica Database consente di crittografare le comunicazioni mediante SSL (Secure Sockets Layer). **Enable_ssl** è di tipo bit e il valore predefinito è 0.  
  
`[ @account_id = ] account_id OUTPUT` Restituisce l'id per il nuovo account. *account_id* viene **int**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 Posta elettronica database sono disponibili parametri distinti per **@email_address**, **@display_name**, e **@replyto_address**. Il **@email_address** parametro è l'indirizzo da cui viene inviato il messaggio. Il **@display_name** parametro è il nome visualizzato nel **da:** campo del messaggio di posta elettronica. Il **@replyto_address** parametro è l'indirizzo di cui verranno inviate le risposte al messaggio di posta elettronica. Un account utilizzato per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, ad esempio, potrebbe inviare messaggi di posta elettronica da un indirizzo di posta elettronica che viene utilizzato solo per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. I messaggi provenienti da tale indirizzo dovrebbero includere un nome descrittivo, in modo che i destinatari possano stabilire con facilità che il mittente è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se un destinatario risponde al messaggio, la risposta dovrebbe arrivare all'amministratore del database e non all'indirizzo utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per questo scenario, l'account utilizza **SqlAgent@Adventure-Works.com** come indirizzo di posta elettronica. Il nome visualizzato è impostato su **SQL Server Agent Automated Mailer**. L'account viene utilizzato **danw@Adventure-Works.com** come indirizzo per le risposte, pertanto le risposte ai messaggi inviati dall'account passare per l'amministratore del database anziché all'indirizzo di posta elettronica per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'agente. Grazie alla possibilità di specificare impostazioni indipendenti per questi tre parametri, con Posta elettronica database è possibile configurare i messaggi in base alle proprie esigenze.  
  
 Il **@mailserver_type** parametro supporta il valore **'SMTP'**.  
  
 Quando **@use_default_credentials** è 1, il messaggio viene inviato al server SMTP utilizzando le credenziali del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Quando **@use_default_credentials** è 0 e un **@username** e **@password** vengono specificati per un account, l'account utilizza l'autenticazione SMTP. Il **@username** e **@password** sono le credenziali dell'account viene utilizzato per il server SMTP, non le credenziali per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o della rete che il computer sia acceso.  
  
 La stored procedure **sysmail_add_account_sp** nel **msdb** database ed è di proprietà di **dbo** dello schema. La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni per questa routine per impostazione predefinita ai membri di esecuzione per il **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creato un account denominato `AdventureWorks Administrator`. L'account utilizza l'indirizzo di posta elettronica `dba@Adventure-Works.com` e invia la posta al server di posta elettronica SMTP `smtp.Adventure-Works.com`. Messaggi inviati da questo account viene visualizzato `AdventureWorks Automated Mailer` nella **da:** riga del messaggio. Le risposte ai messaggi vengono indirizzate a `danw@Adventure-Works.com`.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Creare un Account di posta elettronica Database](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Stored procedure di posta elettronica database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
