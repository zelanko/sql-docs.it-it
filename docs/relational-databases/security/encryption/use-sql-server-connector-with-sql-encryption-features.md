---
title: Usare Connettore SQL Server con le funzionalità di crittografia SQL | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, using
- EKM, with SQL Server Connector
ms.assetid: 58fc869e-00f1-4d7c-a49b-c0136c9add89
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: b6f47c0b1139e78119a345cfbb7565500dc346a1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401084"
---
# <a name="use-sql-server-connector-with-sql-encryption-features"></a>Usare Connettore SQL Server con le funzionalità di crittografia SQL
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]
  Le attività di crittografia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comuni che usano una chiave asimmetrica protetta dall'insieme di credenziali delle chiavi di Azure includono le tre aree seguenti.  
  
-   Transparent Data Encryption con una chiave asimmetrica dell'insieme di credenziali delle chiavi di Azure  
  
-   Crittografia dei backup tramite una chiave asimmetrica dell'insieme di credenziali delle chiavi  
  
-   Crittografia a livello di colonna tramite una chiave asimmetrica dell'insieme di credenziali delle chiavi  
  
 Completare le parti dalla 1 alla 4 dell'argomento [Procedura di installazione di Extensible Key Management con l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)prima di seguire la procedura di questo argomento.  
 
> [!NOTE]  
>  Le versioni 1.0.0.440 e precedenti sono state sostituite e non sono più supportate negli ambienti di produzione. Eseguire l'aggiornamento alla versione 1.0.1.0 o successiva visitando l'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=45344) e seguendo le istruzioni nella pagina [Manutenzione e risoluzione dei problemi di Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) in "Aggiornamento del Connettore SQL Server".  
  
## <a name="transparent-data-encryption-by-using-an-asymmetric-key-from-azure-key-vault"></a>Transparent Data Encryption con una chiave asimmetrica dell'insieme di credenziali delle chiavi di Azure  
 Dopo aver completato le parti dalla 1 alla 4 dell'argomento Procedura di installazione di Extensible Key Management con l'insieme di credenziali delle chiavi di Azure, usare la chiave dell'insieme di credenziali delle chiavi di Azure per crittografare la chiave di crittografia del database con TDE.  
È necessario creare le credenziali e un account di accesso, nonché una chiave di crittografia del database che consente di crittografare i dati e i log nel database. Per crittografare un database è necessaria l'autorizzazione **CONTROL** per il database. L'immagine seguente mostra la gerarchia della chiave di crittografia quando si usa l'insieme di credenziali delle chiavi di Azure.  
  
 ![ekm&#45;key&#45;hierarchy&#45;with&#45;akv](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-with-akv.png "ekm-key-hierarchy-with-akv")  
  
1.  **Creare credenziali di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per il motore di database da usare per TDE**  
  
     Il motore di Database usa le credenziali per accedere all'insieme di credenziali delle chiavi durante il caricamento del database. Si consiglia di creare un altro **ID client** e un altro **segreto** di Azure Active Directory nella parte 1 per [!INCLUDE[ssDE](../../../includes/ssde-md.md)]per limitare le autorizzazioni concesse per l'insieme di credenziali delle chiavi.  
  
     Modificare lo script [!INCLUDE[tsql](../../../includes/tsql-md.md)] sottostante nei modi seguenti:  
  
    -   Modificare l'argomento `IDENTITY` (`ContosoDevKeyVault`) in modo che punti all'insieme di credenziali delle chiavi di Azure.
        - Se si usa **Azure pubblico**, sostituire l'argomento `IDENTITY` con il nome dell'insieme di credenziali delle chiavi di Azure della parte II.
        - Se si usa un **cloud privato di Azure** , ad esempio Azure per enti pubblici, Azure Cina o Azure Germania, sostituire l'argomento `IDENTITY` con l'URI dell'insieme di credenziali restituito nella parte II, passaggio 3. Non includere "https://" nell'URI dell'insieme di credenziali.   
  
    -   Sostituire la prima parte dell'argomento `SECRET` con l'**ID client** di Azure Active Directory della parte 1. In questo esempio l'**ID client** è `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  È necessario rimuovere i trattini dall'**ID client**.  
  
    -   Completare la seconda parte dell'argomento `SECRET` con il **segreto client** della parte I. In questo esempio il **segreto client** della parte I è `Replace-With-AAD-Client-Secret`. La stringa finale dell'argomento `SECRET` sarà una lunga sequenza di lettere e numeri *senza trattini*.  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
    ```  
  
2.  **Creare un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per [!INCLUDE[ssDE](../../../includes/ssde-md.md)] per TDE**  
  
     Creare un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e aggiungere le credenziali del passaggio 1. Questo esempio di [!INCLUDE[tsql](../../../includes/tsql-md.md)] usa la stessa chiave importata in precedenza.  
  
    ```sql  
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  **Creare la chiave di crittografia del database (DEK)**  
  
     La chiave DEK crittografa i file di dati e di log nell'istanza del database e a sua volta viene crittografata dalla chiave asimmetrica dell'insieme di credenziali delle chiavi di Azure. La chiave DEK può essere creata usando qualsiasi lunghezza dell'algoritmo o della chiave supportata da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    ```sql  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
    ```  
  
4.  **Attivare TDE**  
  
    ```sql  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON;  
    GO  
    ```  
  
     Con [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], verificare che TDE sia attivato connettendo il database con Esplora oggetti. Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Gestisci crittografia del database**.  
  
     ![ekm&#45;tde&#45;object&#45;explorer](../../../relational-databases/security/encryption/media/ekm-tde-object-explorer.png "ekm-tde-object-explorer")  
  
     Nella finestra di dialogo **Gestisci crittografia del database** confermare che TDE è attivo e specificare la chiave asimmetrica che sta crittografando DEK.  
  
     ![ekm&#45;tde&#45;dialog&#45;box](../../../relational-databases/security/encryption/media/ekm-tde-dialog-box.png "ekm-tde-dialog-box")  
  
     In alternativa, è possibile eseguire lo script [!INCLUDE[tsql](../../../includes/tsql-md.md)] seguente. Uno stato di crittografia 3 indica un database crittografato.  
  
    ```sql  
    USE MASTER  
    SELECT * FROM sys.asymmetric_keys  
  
    -- Check which databases are encrypted using TDE  
    SELECT d.name, dek.encryption_state   
    FROM sys.dm_database_encryption_keys AS dek  
    JOIN sys.databases AS d  
         ON dek.database_id = d.database_id;  
    ```  
  
    > [!NOTE]  
    >  Il database `tempdb` viene crittografato automaticamente ogni volta che un database abilita TDE.  
  
## <a name="encrypting-backups-by-using-an-asymmetric-key-from-the-key-vault"></a>Crittografia dei backup tramite una chiave asimmetrica dell'insieme di credenziali delle chiavi  
 I backup crittografati sono supportati a partire da [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. L'esempio seguente crea e ripristina un backup crittografato di una chiave DEK protetta dalla chiave asimmetrica nell'insieme di credenziali delle chiavi.  
[!INCLUDE[ssDE](../../../includes/ssde-md.md)] richiede le credenziali quando si accede all'insieme di credenziali delle chiavi durante il caricamento del database. Si consiglia di creare un altro ID client e un altro segreto di Azure Active Directory nella parte 1 per il motore di database per limitare le autorizzazioni concesse per l'insieme di credenziali delle chiavi.  
  
1.  **Creare credenziali di SQL Server per il motore di database da usare per la crittografia dei backup**  
  
     Modificare lo script [!INCLUDE[tsql](../../../includes/tsql-md.md)] sottostante nei modi seguenti:  
  
    -   Modificare l'argomento `IDENTITY` (`ContosoDevKeyVault`) in modo che punti all'insieme di credenziali delle chiavi di Azure.
        - Se si usa **Azure pubblico**, sostituire l'argomento `IDENTITY` con il nome dell'insieme di credenziali delle chiavi di Azure della parte II.
        - Se si usa un **cloud privato di Azure** , ad esempio Azure per enti pubblici, Azure Cina o Azure Germania, sostituire l'argomento `IDENTITY` con l'URI dell'insieme di credenziali restituito nella parte II, passaggio 3. Non includere "https://" nell'URI dell'insieme di credenziali.    
  
    -   Sostituire la prima parte dell'argomento `SECRET` con l'**ID client** di Azure Active Directory della parte 1. In questo esempio l'**ID client** è `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  È necessario rimuovere i trattini dall'**ID client**.  
  
    -   Completare la seconda parte dell'argomento `SECRET` con il **segreto client** della parte I. In questo esempio il **segreto client** della parte I è `Replace-With-AAD-Client-Secret`. La stringa finale dell'argomento `SECRET` sarà una lunga sequenza di lettere e numeri *senza trattini*.   
  
        ```sql  
        USE master;  
  
        CREATE CREDENTIAL Azure_EKM_Backup_cred   
            WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
            SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;    
        ```  
  
2.  **Creare un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per [!INCLUDE[ssDE](../../../includes/ssde-md.md)] per la crittografia dei backup**  
  
     Creare un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da usare per [!INCLUDE[ssDE](../../../includes/ssde-md.md)]e per i backup di crittografia e aggiungere le credenziali del passaggio 1. Questo esempio di [!INCLUDE[tsql](../../../includes/tsql-md.md)] usa la stessa chiave importata in precedenza.  
  
    > [!IMPORTANT]  
    >  Non è possibile usare la stessa chiave asimmetrica per la crittografia dei backup se è già stata usata per la crittografia TDE (esempio precedente) o per la crittografia a livello di colonna (esempio successivo).  
  
     Questo esempio usa la chiave asimmetrica `CONTOSO_KEY_BACKUP` archiviata nell'insieme di credenziali delle chiavi che può essere importato o creato in precedenza per il database master, come descritto nel passaggio 5 della parte 4 precedente.  
  
    ```sql  
    USE master;  
  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it is encrypting the backup.  
    CREATE LOGIN Backup_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY_BACKUP;  
    GO   
  
    -- Alter the Encrypted Backup Login to add the credential for use by   
    -- the Database Engine to access the key vault  
    ALTER LOGIN Backup_Login   
    ADD CREDENTIAL Azure_EKM_Backup_cred ;  
    GO  
    ```  
  
3.  **Eseguire il backup del database**  
  
     Eseguire il backup del database specificando la crittografia con la chiave simmetrica archiviata nell'insieme di credenziali delle chiavi.
     
     Nell'esempio seguente si noti che se il database è stato già crittografato con TDE e la chiave asimmetrica `CONTOSO_KEY_BACKUP` è diversa dalla chiave asimmetrica TDE, il backup verrà crittografato sia con la chiave asimmetrica TDE che con `CONTOSO_KEY_BACKUP`. L'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di destinazione dovrà disporre di entrambe le chiavi per decrittografare il backup.
  
    ```sql  
    USE master;  
  
    BACKUP DATABASE [DATABASE_TO_BACKUP]  
    TO DISK = N'[PATH TO BACKUP FILE]'   
    WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
    ENCRYPTION(ALGORITHM = AES_256,   
    SERVER ASYMMETRIC KEY = [CONTOSO_KEY_BACKUP]);  
    GO  
    ```  
  
4.  **Ripristinare il database**  
    
    Per ripristinare un backup del database crittografato con TDE, l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di destinazione deve prima di tutto disporre di una copia della chiave dell'insieme di credenziali asimmetrica usata per la crittografia. Ecco come si ottiene questo risultato:  
    
    - Se la chiave asimmetrica originale usata per TDE non è più nell'insieme di credenziali chiave, ripristinare il backup della chiave dell'insieme di credenziali chiave o reimportare la chiave da un modulo HSM locale. **Importante:** per fare in modo che l'identificazione digitale della chiave corrisponda all'identificazione digitale registrata nel backup del database, la chiave deve avere lo **stesso nome della chiave dell'insieme di credenziali delle chiavi** originale.
    
    - Applicare i passaggi 1 e 2 nell'istanza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di destinazione.
    
    - Quando l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di destinazione ha accesso alle chiavi asimmetriche usate per crittografare il backup, ripristinare il database nel server.
    
     Esempio del codice di ripristino:  
  
    ```sql  
    RESTORE DATABASE [DATABASE_TO_BACKUP]  
    FROM DISK = N'[PATH TO BACKUP FILE]'   
        WITH FILE = 1, NOUNLOAD, REPLACE;  
    GO  
    ```  
  
     Per altre informazioni sulle opzioni di backup, vedere [BACKUP (Transact-SQL)](../../../t-sql/statements/backup-transact-sql.md).  
  
## <a name="column-level-encryption-by-using-an-asymmetric-key-from-the-key-vault"></a>Crittografia a livello di colonna tramite una chiave asimmetrica dell'insieme di credenziali delle chiavi  
 L'esempio seguente crea una chiave simmetrica protetta dalla chiave asimmetrica nell'insieme di credenziali delle chiavi. La chiave simmetrica viene quindi usata per crittografare i dati nel database.  
  
> [!IMPORTANT]  
>  Non è possibile usare la stessa chiave asimmetrica per la crittografia dei backup se è già stata usata per la crittografia TDE o dei backup (esempi precedenti).  
  
 Questo esempio usa la chiave asimmetrica `CONTOSO_KEY_COLUMNS` archiviata nell'insieme di credenziali delle chiavi che può essere importata o creata in precedenza, come descritto nel passaggio 3 della sezione 3 di [Procedura di installazione di Extensible Key Management con l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md). Per usare questa chiave asimmetrica nel database `ContosoDatabase` , è necessario eseguire nuovamente l'istruzione `CREATE ASYMMETRIC KEY` in modo da fornire al database `ContosoDatabase` un riferimento alla chiave.  
  
```sql  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY_COLUMNS   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoDevRSAKey2',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY  
    (  
    KEY_GUID('DATA_ENCRYPTION_KEY'),   
    CONVERT(VARBINARY,'Plain text data to encrypt')  
    );  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di installazione di Extensible Key Management con l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)   
 [Extensible Key Management tramite l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [Opzione di configurazione del server EKM provider enabled](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [Manutenzione e risoluzione dei problemi del Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
