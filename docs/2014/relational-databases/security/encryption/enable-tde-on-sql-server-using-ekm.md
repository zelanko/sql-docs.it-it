---
title: Abilitare Transparent Data Encryption con EKM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], TDE using an EKM
- TDE, EKM how to
- EKM, TDE how to
- Transparent Data Encryption, using EKM
ms.assetid: b892e7a7-95bd-4903-bf54-55ce08e225af
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 8b3f046017aa54f5db96878f8bfb6c435409d839
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74957233"
---
# <a name="enable-tde-using-ekm"></a>Abilitare TDE utilizzando EKM
  In questo argomento viene descritto come abilitare Transparent Data Encryption (TDE) in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] per proteggere una chiave di crittografia del database tramite una chiave asimmetrica archiviata in un modulo Extensible Key Management (EKM) con [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 TDE esegue la crittografia dell'archiviazione di un intero database usando una chiave simmetrica detta "chiave di crittografia del database". È inoltre possibile proteggere la chiave di crittografia del database utilizzando un certificato protetto dalla chiave master del database master. Per altre informazioni sulla protezione della chiave di crittografia del database tramite la chiave master del database, vedere [Transparent Data Encryption &#40;TDE&#41;](transparent-data-encryption.md). Per informazioni sulla configurazione di TDE quando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è in esecuzione in una macchina virtuale di Azure, vedere [Extensible Key Management con l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](extensible-key-management-using-azure-key-vault-sql-server.md).  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   [Per abilitare TDE utilizzando EKM tramite Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Per creare una chiave di crittografia del database e crittografare un database, è necessario essere un utente con privilegi elevati, ad esempio un amministratore di sistema, che possa essere autenticato dal modulo EKM.  
  
-   All'avvio il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve aprire il database. A tal fine, è necessario creare le credenziali che dovranno essere autenticate dal modulo EKM e aggiungerle a un account di accesso basato su una chiave asimmetrica. Gli utenti non possono eseguire l'accesso utilizzando tale account, ma il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] sarà in grado di effettuare l'autenticazione con il dispositivo EKM.  
  
-   In caso di perdita della chiave asimmetrica archiviata nel modulo EKM, il database non potrà essere aperto in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se il provider EKM consente di eseguire il backup della chiave asimmetrica, è consigliabile creare una copia di backup e archiviarla in una posizione sicura.  
  
-   Le opzioni e i parametri richiesti dal provider EKM possono differire da quanto indicato nell'esempio di codice seguente. Per altre informazioni, rivolgersi al provider EKM.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 In questo argomento vengono utilizzate le autorizzazioni seguenti:  
  
-   Per modificare un'opzione di configurazione ed eseguire l'istruzione RECONFIGURE, è necessario disporre dell'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
-   È richiesta l'autorizzazione ALTER ANY CREDENTIAL.  
  
-   È richiesta l'autorizzazione ALTER ANY LOGIN.  
  
-   È necessaria l'autorizzazione CREATE ASYMMETRIC KEY.  
  
-   È necessaria l'autorizzazione CONTROL nel database per crittografare il database.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-enable-tde-using-ekm"></a>Per abilitare Transparent Data Encryption tramite Extensible Key Management  
  
1.  Copiare i file forniti dal provider EKM in un percorso appropriato nel computer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . In questo esempio viene usata la cartella **C:\EKM** .  
  
2.  Installare i certificati nel computer in base a quanto richiesto dal provider EKM.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non fornisce un provider EKM. Ogni provider EKM può richiedere procedure diverse per l'installazione, la configurazione e l'autorizzazione degli utenti.  Per completare questo passaggio, consultare la documentazione del provider EKM.  
  
3.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
4.  Sulla barra Standard fare clic su **Nuova query**.  
  
5.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- Enable advanced options.  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Create a cryptographic provider, which we have chosen to call "EKM_Prov," based on an EKM provider  
  
    CREATE CRYPTOGRAPHIC PROVIDER EKM_Prov   
    FROM FILE = 'C:\EKM_Files\KeyProvFile.dll' ;  
    GO  
  
    -- Create a credential that will be used by system administrators.  
    CREATE CREDENTIAL sa_ekm_tde_cred   
    WITH IDENTITY = 'Identity1',   
    SECRET = 'q*gtev$0u#D1v'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
    GO  
  
    -- Add the credential to a high privileged user such as your   
    -- own domain login in the format [DOMAIN\login].  
    ALTER LOGIN Contoso\Mary  
    ADD CREDENTIAL sa_ekm_tde_cred ;  
    GO  
    -- create an asymmetric key stored inside the EKM provider  
    USE master ;  
    GO  
    CREATE ASYMMETRIC KEY ekm_login_key   
    FROM PROVIDER [EKM_Prov]  
    WITH ALGORITHM = RSA_512,  
    PROVIDER_KEY_NAME = 'SQL_Server_Key' ;  
    GO  
  
    -- Create a credential that will be used by the Database Engine.  
    CREATE CREDENTIAL ekm_tde_cred   
    WITH IDENTITY = 'Identity2'   
    , SECRET = 'jeksi84&sLksi01@s'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
  
    -- Add a login used by TDE, and add the new credential to the login.  
    CREATE LOGIN EKM_Login   
    FROM ASYMMETRIC KEY ekm_login_key ;  
    GO  
    ALTER LOGIN EKM_Login   
    ADD CREDENTIAL ekm_tde_cred ;  
    GO  
  
    -- Create the database encryption key that will be used for TDE.  
    USE AdventureWorks2012 ;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM  = AES_128  
    ENCRYPTION BY SERVER ASYMMETRIC KEY ekm_login_key ;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE AdventureWorks2012   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
 Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
-   [Extensible Key Management con l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](extensible-key-management-using-azure-key-vault-sql-server.md)  
  
-   [Transparent Data Encryption con il database SQL di Azure](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md)  
  
  
