---
title: Risolvere i problemi relativi agli utenti isolati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- orphaned users [SQL Server]
- logins [SQL Server], orphaned users
- troubleshooting [SQL Server], user accounts
- user accounts [SQL Server], orphaned users
- failover [SQL Server], managing metadata
- database mirroring [SQL Server], metadata
- users [SQL Server], orphaned
ms.assetid: 11eefa97-a31f-4359-ba5b-e92328224133
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38a33b34b64cf285e94f66c547b2309b8daf1ae8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63035668"
---
# <a name="troubleshoot-orphaned-users-sql-server"></a>Risolvere i problemi relativi agli utenti isolati (SQL Server)
  Per accedere a un'istanza di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario che un'entità disponga di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valido. Tale account di accesso viene utilizzato nel processo di autenticazione che verifica se l'entità è autorizzata a connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli account di accesso in un'istanza del server sono visibili nel **Sys. server_principals** vista del catalogo e il **Sys. syslogins** visualizzazione compatibilità.  
  
 Gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consentono di accedere a database singoli mediante un utente del database di cui viene eseguito il mapping all'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sono previste due eccezioni a questa regola:  
  
-   Account Guest.  
  
     Si tratta di un account che, se attivato nel database, consente agli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di cui non viene eseguito il mapping ad alcun utente del database di accedere al database come utente guest.  
  
-   Appartenenza ai gruppi di Microsoft Windows.  
  
     Un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creato da un utente di Windows può accedere a un database se tale utente di Windows è membro di un gruppo di Windows a sua volta utente del database.  
  
 Le informazioni relative al mapping di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un utente del database sono archiviate all'interno del database. Includono il nome dell'utente del database e il SID dell'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrispondente. Le autorizzazioni di tale utente del database vengono utilizzate come autorizzazioni nel database.  
  
 Un utente del database il cui account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrispondente non è definito o è definito in modo errato in un'istanza del server non potrà accedere a tale istanza. Questo utente viene definito *utente orfano* del database nell'istanza del server. Un utente del database può diventare isolato (orfano) se l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrispondente viene rimosso oppure dopo il ripristino di un database in un'istanza diversa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il collegamento del database a tale istanza. È possibile che si verifichi l'isolamento se l'utente del database è sottoposto a mapping a un SID non presente nella nuova istanza del server.  
  
> [!NOTE]  
>  Oggetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso non è possibile accedere a un database in cui Manca un corrispondente utente del database, a meno che **guest** in tale database è abilitato. Per informazioni sulla creazione di un account utente del database, vedere [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql).  
  
## <a name="to-detect-orphaned-users"></a>Per rilevare gli utenti isolati (orfani)  
 Per rilevare gli utenti isolati (orfani), eseguire le istruzioni Transact-SQL seguenti:  
  
```  
USE <database_name>;  
GO;   
sp_change_users_login @Action='Report';  
GO;  
```  
  
 Nell'output sono elencati gli utenti e gli identificatori di sicurezza (SID) corrispondenti disponibili nel database corrente e non collegati ad alcun account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [sp_change_users_login &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql).  
  
> [!NOTE]  
>  **sp_change_users_login** non può essere usato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli account di accesso creati da Windows.  
  
## <a name="to-resolve-an-orphaned-user"></a>Per risolvere un utente isolato (orfano)  
 Per risolvere un utente isolato (orfano), eseguire la procedura seguente:  
  
1.  Il comando seguente consente di ricollegare l'account di accesso server specificato da *< login_name >* con l'utente del database specificato da *< database_user >*.  
  
    ```  
    USE <database_name>;  
    GO  
    sp_change_users_login @Action='update_one', @UserNamePattern='<database_user>', @LoginName='<login_name>';  
    GO  
  
    ```  
  
     Per altre informazioni, vedere [sp_change_users_login &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql).  
  
2.  Al termine dell'esecuzione del codice riportato nel passaggio precedente, l'utente sarà in grado di accedere al database. L'utente potrà quindi modificare la password del *< login_name >* account di accesso tramite il **sp_password** stored procedure, come indicato di seguito:  
  
    ```  
    USE master   
    GO  
    sp_password @old=NULL, @new='password', @loginame='<login_name>';  
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  Solo gli account di accesso con autorizzazione ALTER ANY LOGIN possono modificare la password dell'account di accesso di un altro utente. Solo i membri del ruolo **sysadmin** possono tuttavia modificare le password dei membri del ruolo **sysadmin** .  
  
    > [!NOTE]  
    >  **sp_password** non può essere usato per [!INCLUDE[msCoName](../../includes/msconame-md.md)] gli account di Windows. L'autenticazione degli utenti che si connettono a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in base al corrispondente account di rete di Windows viene eseguita da Windows. Le password di tali utenti sono pertanto modificabili solo in Windows.  
  
     Per altre informazioni, vedere [sp_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [sp_change_users_login &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)   
 [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)   
 [sp_grantlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-grantlogin-transact-sql)   
 [sp_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)   
 [sys.sysusers &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysusers-transact-sql)   
 [sys.syslogins &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)  
  
  
