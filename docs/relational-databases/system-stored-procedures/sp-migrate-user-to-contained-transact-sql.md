---
title: sp_migrate_user_to_contained (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bdab8cd50a16913f37115f0d38c00c5c699bc0f
ms.sourcegitcommit: 113fa84148d6d475c7c1475666ea08ac6965e71c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2019
ms.locfileid: "66836306"
---
# <a name="spmigrateusertocontained-transact-sql"></a>sp_migrate_user_to_contained (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Converte un utente del database di cui è stato eseguito il mapping a un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un utente del database indipendente con password. In un database indipendente, utilizzare questa procedura per rimuovere le dipendenze nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui viene installato il database. **sp_migrate_user_to_contained** separa l'utente dall'originale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso, in modo che sia possibile amministrare separatamente impostazioni quali password e lingua predefinita per il database indipendente. **sp_migrate_user_to_contained** può essere usata prima di spostare il database indipendente in un'istanza diversa del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] per eliminare le dipendenze in corrente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli account di accesso dell'istanza.  
  
> [!NOTE]
> Prestare attenzione quando si usa **sp_migrate_user_to_contained**, come non sarà in grado di annullare l'effetto. Questa procedura viene utilizzata solo in un database indipendente. Per altre informazioni, vedere [Database indipendenti](../../relational-databases/databases/contained-databases.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@username =** ] **N'***user***'**  
 Nome di un utente nel database indipendente corrente di cui è stato eseguito il mapping a un account di accesso con autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il valore è **sysname**, il valore predefinito è **NULL**.  
  
 [ **@rename =** ] **N'***copy_login_name***'**  | **N'***keep_name***'**  
 Quando un utente di database basato su un account di accesso ha un nome utente diverso rispetto al nome di account di accesso, usare *keep_name* per mantenere il nome utente del database durante la migrazione. Uso *copy_login_name* per creare il nuovo utente di database indipendente con il nome dell'account di accesso, anziché sull'utente. Quando il nome utente di un utente del database basato su un account di accesso è uguale al nome dell'account di accesso, entrambe le opzioni consentono di creare l'utente del database indipendente senza la modifica del nome.  
  
 [ **@disablelogin =** ] **N'***disable_login***'**  | **N'***do_not_disable_login***'**  
 *disable_login* disabilita l'account di accesso nel database master. Per connettersi quando l'account di accesso è disabilitato, la connessione deve specificare il nome del database indipendente come le **catalogo iniziale** come parte della stringa di connessione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_migrate_user_to_contained** Crea utente del database indipendente con password, indipendentemente dalla proprietà o le autorizzazioni dell'account di accesso. Ad esempio, la procedura può avere esito positivo se l'account di accesso è disabilitato o se all'utente viene negato il **CONNECT** dell'autorizzazione per il database.  
  
 **sp_migrate_user_to_contained** presenta le restrizioni seguenti.  
  
-   Il nome utente non può essere già esistente nel database.  
  
-   Impossibile convertire gli utenti predefiniti, ad esempio dbo e guest.  
  
-   L'utente non è possibile specificare il **EXECUTE AS** clausola di una stored procedure firmata.  
  
-   L'utente non può disporre di una stored procedure che include il **EXECUTE AS OWNER** clausola.  
  
-   **sp_migrate_user_to_contained** non può essere utilizzato in un database di sistema.  
  
## <a name="security"></a>Sicurezza  
 Quando si esegue la migrazione di utenti, fare attenzione a non disabilitare o eliminare tutti gli account di accesso di amministratore dall'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se vengono eliminati tutti gli accessi, vedere [connettersi a SQL Server quando System Administrators vengono bloccati](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md).  
  
 Se il **BUILTIN\Administrators** account di accesso è presente, gli amministratori possono connettersi avviando l'applicazione mediante il **Esegui come amministratore** opzione.  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione **CONTROL SERVER** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-migrating-a-single-user"></a>A. Migrazione di un solo utente  
 Nell'esempio seguente viene eseguita la migrazione di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominato `Barry` a un database indipendente con password. L'esempio non modifica il nome utente e consente di mantenere l'account di accesso come abilitato.  
  
```sql  
sp_migrate_user_to_contained   
@username = N'Barry',  
@rename = N'keep_name',  
@disablelogin = N'do_not_disable_login' ;  
  
```  
  
### <a name="b-migrating-all-database-users-with-logins-to-contained-database-users-without-logins"></a>B. Migrazione di tutti gli utenti del database con account di accesso a utenti del database indipendente senza account di accesso  
 Nell'esempio seguente viene eseguita la migrazione di tutti gli utenti basati sugli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a utenti del database indipendente con password. Nell'esempio sono inclusi account di accesso non abilitati. L'esempio deve essere eseguito nel database indipendente.  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [Database indipendenti](../../relational-databases/databases/contained-databases.md)  
  
  
