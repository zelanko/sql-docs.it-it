---
title: Extensible Key Management tramite l'insieme di credenziali delle chiavi di Azure (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault
- TDE, EKM and key vault
- Extensible Key Management with key vault
- Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: c9fc8df6878c40d49ffc1b4efd3e118fb59f716f
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798062"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Extensible Key Management tramite l'insieme di credenziali delle chiavi di Azure (SQL Server)
  Il connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Key Vault consente la crittografia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per sfruttare il servizio Azure Key Vault come provider [EKM &#40;&#41; di Extensible Key Management](extensible-key-management-ekm.md) per proteggere le chiavi di crittografia.  
  
 Contenuto dell'argomento:  
  
-   [Utilizzi di EKM](#Uses)  
  
-   [Passaggio 1: configurazione della Key Vault per l'uso da parte di SQL Server](#Step1)  
  
-   [Passaggio 2: installazione del Connettore SQL Server](#Step2)  
  
-   [Passaggio 3: configurare SQL Server per l'uso di un provider EKM per il Key Vault](#Step3)  
  
-   [Esempio A: Transparent Data Encryption usando una chiave asimmetrica della Key Vault](#ExampleA)  
  
-   [Esempio B: crittografia dei backup tramite una chiave asimmetrica dalla Key Vault](#ExampleB)  
  
-   [Esempio C: crittografia a livello di colonna tramite una chiave asimmetrica dalla Key Vault](#ExampleC)  
  
##  <a name="Uses"></a>Utilizzi di EKM  
 Un'organizzazione può usare la crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per proteggere i dati sensibili. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crittografia include [Transparent Data Encryption &#40;&#41;](transparent-data-encryption.md)Transparent Data Encryption, [crittografia a livello di colonna](/sql/t-sql/functions/cryptographic-functions-transact-sql) (CLE) e crittografia dei [backup](../../backup-restore/backup-encryption.md). In tutti questi casi, i dati vengono crittografati tramite una chiave DEK simmetrica. Per proteggerla ulteriormente, tale chiave viene crittografata con una gerarchia di chiavi archiviate in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. In alternativa, l'architettura del provider EKM consente a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di proteggere le chiavi DEK tramite una chiave asimmetrica archiviata all'esterno di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un provider del servizio di crittografia esterno. L'utilizzo dell'architettura del provider EKM aggiunge un ulteriore livello di sicurezza consentendo alle organizzazioni di separare la gestione delle chiavi e dei dati.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector per l'insieme di credenziali delle chiavi di Azure consente a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di sfruttare il servizio dell'insieme di credenziali delle chiavi scalabile, ad alte prestazioni e a disponibilità elevata come provider EKM per la protezione delle chiavi di crittografia. Il servizio dell'insieme di credenziali delle chiavi può essere usato con le installazioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nelle macchine virtuali di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e per i server locali. Il servizio dell'insieme di credenziali delle chiavi consente inoltre di usare i moduli di protezione hardware (HSM) controllati e monitorati rigorosamente per un livello di protezione maggiore per le chiavi di crittografia asimmetriche. Per altre informazioni sull'insieme di credenziali delle chiavi, vedere [Insieme di credenziali delle chiavi di Azure](https://go.microsoft.com/fwlink/?LinkId=521401).  
  
 L'immagine seguente illustra il flusso di processo di EKM con l'insieme di credenziali delle chiavi. I numeri dei passaggi del processo nell'immagine non sono concepiti per corrispondere ai numeri dei passaggi della configurazione riportati di seguito.  
  
 ![SQL Server EKM utilizzando il Azure Key Vault](../../../database-engine/media/ekm-using-azure-key-vault.png "SQL Server EKM utilizzando il Azure Key Vault")  
  
##  <a name="Step1"></a>Passaggio 1: configurare la Key Vault per l'uso da parte di SQL Server  
 Completare i passaggi seguenti per configurare un insieme di credenziali delle chiavi da usare con il [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] per la protezione delle chiavi di crittografia. È possibile che per l'organizzazione sia già in uso un insieme di credenziali. Se non esiste un insieme di credenziali, l'amministratore di Azure incaricato della gestione delle chiavi di crittografia può creare un insieme di credenziali, generare una chiave asimmetrica nell'insieme di credenziali e quindi autorizzare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a usare la chiave. Per acquisire familiarità con il servizio dell'insieme di credenziali delle chiavi, consultare [Introduzione all'insieme di credenziali delle chiavi di Azure](https://go.microsoft.com/fwlink/?LinkId=521402)e il riferimento di PowerShell [Cmdlet per l'insieme di credenziali delle chiavi di Azure](https://docs.microsoft.com/powershell/module/azurerm.keyvault) .  
  
> [!IMPORTANT]  
>  Se sono disponibili più sottoscrizioni di Azure, è necessario usare la sottoscrizione contenente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
1.  **Creare un insieme di credenziali:** creare un insieme di credenziali seguendo le istruzioni presenti nella sezione **Creare un insieme di credenziali delle chiavi** dell'articolo [Introduzione all'insieme di credenziali delle chiavi di Azure](https://go.microsoft.com/fwlink/?LinkId=521402). Registrare il nome dell'insieme di credenziali. Questo argomento usa **ContosoKeyVault** come nome dell'insieme di credenziali delle chiavi.  
  
2.  **Generare una chiave asimmetrica nell'insieme di credenziali:** la chiave asimmetrica nell'insieme di credenziali delle chiavi viene usata per proteggere le chiavi di crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Solo la parte pubblica della chiave asimmetrica lascia sempre l'insieme di credenziali, la parte privata non viene mai esportata dall'insieme di credenziali. Tutte le operazioni crittografiche che usano la chiave asimmetrica vengono delegate all'insieme di credenziali delle chiavi di Azure e sono protette dalla sicurezza dell'insieme di credenziali delle chiavi.  
  
     Esistono diversi modi per generare una chiave asimmetrica e archiviarla nell'insieme di credenziali. È possibile generare una chiave esternamente e importarla nell'insieme di credenziali come file con estensione pfx oppure creare la chiave direttamente nell'insieme di credenziali mediante le API dell'insieme di credenziali delle chiavi.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector richiede che le chiavi asimmetriche siano di tipo RSA a 2048 bit e il nome della chiave può usare solo i caratteri "a-z", "A-Z", "0-9" e "-". In questo documento il nome della chiave asimmetrica viene definito **ContosoMasterKey**. Sostituire questo nome con il nome univoco da usare per la chiave.  
  
    > [!IMPORTANT]  
    >  L'importazione della chiave asimmetrica è consigliata per gli scenari di produzione in quanto consente all'amministratore di depositare la chiave in un sistema di deposito delle chiavi. Se la chiave asimmetrica viene creata nell'insieme di credenziali, non potrà essere depositata perché la chiave privata non può mai lasciare l'insieme di credenziali. È consigliabile depositare le chiavi usate per proteggere i dati critici. Se si perde una chiave asimmetrica, non sarà più possibile recuperare i dati.  
  
    > [!IMPORTANT]  
    >  L'insieme di credenziali delle chiavi supporta più versioni della stessa chiave denominata. È consigliabile non eseguire il controllo delle versioni né il rollback delle chiavi che vengono usate da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector. Se l'amministratore vuole eseguire il rollback della chiave usata per la crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , sarà necessario creare una nuova chiave con un nome diverso nell'insieme di credenziali e usarla per crittografare la chiave DEK.  
  
     Per altre informazioni su come importare una chiave nell'insieme di credenziali delle chiavi o creare una chiave nell'insieme di credenziali delle chiavi (non consigliato per un ambiente di produzione), vedere la sezione **Aggiungere una chiave o un segreto nell'insieme di credenziali delle chiavi** in [Introduzione all'insieme di credenziali delle chiavi di Azure](https://go.microsoft.com/fwlink/?LinkId=521402).  
  
3.  **Ottenere le entità servizio di Azure Active Directory da usare per SQL Server:** quando l'organizzazione esegue la registrazione per un servizio cloud Microsoft, ottiene un'istanza di Azure Active Directory. Creare le **entità servizio** nell'istanza di Azure Active Directory per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (per l'autenticazione in Azure Active Directory) per l'accesso all'insieme di credenziali delle chiavi.  
  
    -   Un' **entità servizio** sarà necessaria per consentire a un amministratore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di accedere all'insieme di credenziali per configurare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in modo da usare la crittografia.  
  
    -   Un'altra **entità servizio** sarà necessaria per consentire al [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] di accedere all'insieme di credenziali per eseguire l'operazione unwrap per le chiavi usate nella crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Per altre informazioni su come registrare un'applicazione e generare un'entità servizio, vedere la sezione **Registrare un'applicazione con Azure Active Directory** in [Introduzione all'insieme di credenziali delle chiavi di Azure](https://go.microsoft.com/fwlink/?LinkId=521402). Il processo di registrazione restituisce un **ID applicazione** (noto anche come **ID CLIENT**) e una **Chiave di autenticazione** (nota anche come **Segreto**) per ogni **entità servizio**di Azure Active Directory. Se utilizzata nell'istruzione `CREATE CREDENTIAL`, il trattino deve essere rimosso dall' **ID client**. Registrare questi valori da usare negli script seguenti:  
  
    -   **Entità servizio** per un account di accesso **sysadmin** : **CLIENTID_sysadmin_login** e **SECRET_sysadmin_login**  
  
    -   **Entità servizio** per il [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]: **CLIENTID_DBEngine** e **SECRET_DBEngine**.  
  
4.  **Concedere le autorizzazioni per le entità servizio per accedere al Key Vault:** Entrambe le entità **CLIENTID_sysadmin_login** e **CLIENTID_DBEngineService** richiedono le autorizzazioni **Get**, **List**, **wrapKey**e **unwrapKey** nell'insieme di credenziali delle chiavi. Se si intende creare chiavi tramite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , è necessario concedere anche l'autorizzazione **create** nell'insieme di credenziali delle chiavi.  
  
    > [!IMPORTANT]  
    >  Gli utenti devono avere almeno le operazioni **wrapKey** e **unwrapKey** per l'insieme di credenziali delle chiavi.  
  
     Per altre informazioni sulla concessione delle autorizzazioni all'insieme di credenziali, vedere la sezione **Autorizzare l'applicazione a usare la chiave o il segreto** in [Introduzione all'insieme di credenziali delle chiavi di Azure](https://go.microsoft.com/fwlink/?LinkId=521402).  
  
     Collegamenti alla documentazione dell'insieme di credenziali delle chiavi di Azure  
  
    -   [Informazioni sull'insieme di credenziali delle chiavi di Azure](https://go.microsoft.com/fwlink/?LinkId=521401)  
  
    -   [Introduzione all'insieme di credenziali delle chiavi di Azure](https://go.microsoft.com/fwlink/?LinkId=521402)  
  
    -   Riferimento di PowerShell [Cmdlet per l'insieme di credenziali delle chiavi di Azure](https://docs.microsoft.com/powershell/module/azurerm.keyvault)  
  
##  <a name="Step2"></a>Passaggio 2: installare il Connettore SQL Server  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector viene scaricato e installato dall'amministratore del computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . È possibile scaricare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector dalla pagina [Microsoft Download Center](https://go.microsoft.com/fwlink/p/?LinkId=521700).  Cercare **SQL Server Connector per l'insieme di credenziali delle chiavi di Microsoft Azure**, esaminare i dettagli, i requisiti di sistema e le istruzioni di installazione e scegliere di scaricare il connettore e avviare l'installazione con il pulsante **Scarica**. Esaminare la licenza e accettarne le condizioni, quindi continuare.  
  
 Per impostazione predefinita, il connettore viene installato in **C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault**. Questo percorso può essere modificato durante l'installazione. Se si modifica il percorso, apportare la modifica negli script riportati di seguito.  
  
 Dopo aver completato l'installazione, nel computer vengono installati gli elementi seguenti:  
  
-   **Microsoft.AzureKeyVaultService.EKM.dll**: si tratta della DLL del provider di crittografia EKM che deve essere registrata con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante l'istruzione CREATE CRYPTOGRAPHIC PROVIDER.  
  
-   **SQL Server Connector per l'insieme di credenziali delle chiavi di Azure**: si tratta di un servizio di Windows che consente al provider di crittografia EKM di comunicare con l'insieme di credenziali delle chiavi.  
  
 L'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector consente anche di scaricare facoltativamente gli script di esempio per la crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
##  <a name="Step3"></a>Passaggio 3: configurare SQL Server per l'uso di un provider EKM per il Key Vault  
  
###  <a name="Permissions"></a> Permissions  
 Per completare l'intero processo è necessaria l'autorizzazione CONTROL SERVER o l'appartenenza al ruolo predefinito del server **sysadmin** . Le azioni specifiche richiedono le autorizzazioni seguenti:  
  
-   Per creare un provider di crittografia è necessaria l'autorizzazione CONTROL SERVER o l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
-   Per modificare un'opzione di configurazione ed eseguire l'istruzione RECONFIGURE, è necessario disporre dell'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
-   Per creare le credenziali, è necessaria l'autorizzazione ALTER ANY CREDENTIAL.  
  
-   Per aggiungere le credenziali per un account di accesso, è necessaria l'autorizzazione ALTER ANY LOGIN.  
  
-   Per creare una chiave asimmetrica, è necessaria l'autorizzazione CREATE ASYMMETRIC KEY.  
  
###  <a name="TsqlProcedure"></a>Per configurare SQL Server per l'utilizzo di un provider di crittografia  
  
1.  Configurare il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] per usare EKM e registrare (creare) il provider di crittografia con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    ```sql
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
  
    -- Create a cryptographic provider, using the SQL Server Connector  
    -- which is an EKM provider for the Azure Key Vault. This example uses   
    -- the name AzureKeyVault_EKM_Prov.  
  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO
    ```  
  
2.  Configurare le credenziali di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per un account di accesso di amministratore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per usare l'insieme di credenziali delle chiavi in modo da configurare e gestire gli scenari di crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!IMPORTANT]  
    >  L'argomento **Identity** di `CREATE CREDENTIAL` richiede il nome dell'insieme di credenziali delle chiavi. L'argomento **Secret** di `CREATE CREDENTIAL` richiede l' *ID client\<* (senza trattini) e *\<Secret >* essere passati insieme senza uno spazio tra di essi.  
  
     Nell'esempio seguente l' **ID client** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) viene immesso con tutti i trattini rimossi come stringa `EF5C8E094D2A4A769998D93440D8115D` e il **Segreto** è rappresentato dalla stringa *SECRET_sysadmin_login*.  
  
    ```sql
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_sysadmin_login'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
  
    -- Add the credential to the SQL Server administrators domain login   
    ALTER LOGIN [<domain>/<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     Per un esempio dell'uso delle variabili per gli argomenti di `CREATE CREDENTIAL` e della rimozione dei trattini dall'ID client a livello di codice, vedere [ &#40;create&#41;Credential Transact-SQL](/sql/t-sql/statements/create-credential-transact-sql).  
  
3.  Se è stata importata una chiave asimmetrica come descritto in precedenza nella sezione 3 del passaggio 1, aprire la chiave, fornendo il nome della chiave nell'esempio seguente.  
  
    ```sql
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
  
     Sebbene non consigliabile per un ambiente di produzione (perché la chiave non può essere esportata), è possibile creare una chiave asimmetrica direttamente nell'insieme di credenziali da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se in precedenza non è stata importata alcuna chiave, creare una chiave asimmetrica nell'insieme di credenziali delle chiavi ai fini del test usando lo script seguente. Eseguire lo script, usando un account di accesso di cui è stato effettuato il provisioning con le credenziali **sysadmin_ekm_cred** .  
  
    ```sql
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH ALGORITHM = RSA_2048,  
    PROVIDER_KEY_NAME = 'ContosoMasterKey';  
    ```  
  
> [!TIP]  
>  Gli utenti che ricevono l'errore **Non è stato possibile esportare la chiave pubblica dal provider. Codice di errore del provider: 2053.** devono verificare le autorizzazioni **get**, **list**, **wrapKey**e **unwrapKey** nell'insieme di credenziali della chiave.  
  
 Per ulteriori informazioni, vedere quanto segue:  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
## <a name="examples"></a>Esempi  
  
###  <a name="ExampleA"></a>Esempio A: Transparent Data Encryption usando una chiave asimmetrica della Key Vault  
 Dopo aver completato i passaggi precedenti, creare le credenziali e un account di accesso e quindi creare una chiave di crittografia del database protetta dalla chiave asimmetrica nell'insieme di credenziali delle chiavi. Usare la chiave di crittografia del database per crittografare un database con TDE.  
  
 Per crittografare un database è necessaria l'autorizzazione CONTROL per il database.  
  
##### <a name="to-enable-tde-using-ekm-and-the-key-vault"></a>Per abilitare TDE tramite EKM e l'insieme di credenziali delle chiavi  
  
1.  Creare le credenziali di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] da usare per l'accesso a EKM con l'insieme di credenziali delle chiavi durante il caricamento del database.  
  
    > [!IMPORTANT]  
    >  L'argomento **Identity** di `CREATE CREDENTIAL` richiede il nome dell'insieme di credenziali delle chiavi. L'argomento **Secret** di `CREATE CREDENTIAL` richiede l' *ID client\<* (senza trattini) e *\<Secret >* essere passati insieme senza uno spazio tra di essi.  
  
     Nell'esempio seguente l' **ID client** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) viene immesso con tutti i trattini rimossi come stringa `EF5C8E094D2A4A769998D93440D8115D` e il **Segreto** è rappresentato dalla stringa *SECRET_DBEngine*.  
  
    ```sql
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
    ```  
  
2.  Creare un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che verrà usato dal [!INCLUDE[ssDE](../../../includes/ssde-md.md)] per TDE e aggiungervi le credenziali. Questo esempio usa la chiave asimmetrica CONTOSO_KEY archiviata nell'insieme di credenziali delle chiavi importato o creato in precedenza per il database master, come sopra descritto nella [sezione 3 del passaggio 3](#Step3) .  
  
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
  
3.  Creare la chiave di crittografia del database (DEK) che verrà usata per TDE. La chiave DEK può essere creata usando qualsiasi algoritmo supportato da SQL Server o la lunghezza della chiave. La chiave DEK verrà protetta dalla chiave asimmetrica nell'insieme di credenziali delle chiavi.  
  
     Questo esempio usa la chiave asimmetrica CONTOSO_KEY archiviata nell'insieme di credenziali delle chiavi importato o creato in precedenza, come sopra descritto nella [sezione 3 del passaggio 3](#Step3) .  
  
    ```sql
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_128   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
     Per ulteriori informazioni, vedere quanto segue:  
  
    -   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
    -   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
###  <a name="ExampleB"></a>Esempio B: crittografia dei backup tramite una chiave asimmetrica dalla Key Vault  
 I backup crittografati sono supportati a partire da [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. L'esempio seguente crea e ripristina un backup crittografato di una chiave DEK protetta dalla chiave asimmetrica nell'insieme di credenziali delle chiavi.  
  
```sql
USE master;  
BACKUP DATABASE [DATABASE_TO_BACKUP]  
TO DISK = N'[PATH TO BACKUP FILE]'   
WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);  
GO  
```  
  
 Esempio del codice di ripristino.  
  
```sql
RESTORE DATABASE [DATABASE_TO_BACKUP]  
FROM DISK = N'[PATH TO BACKUP FILE]' WITH FILE = 1, NOUNLOAD, REPLACE;  
GO  
```  
  
 Per ulteriori informazioni sulle opzioni di backup, [vedere &#40;backup Transact-&#41;SQL](/sql/t-sql/statements/backup-transact-sql).  
  
###  <a name="ExampleC"></a>Esempio C: crittografia a livello di colonna tramite una chiave asimmetrica dalla Key Vault  
 L'esempio seguente crea una chiave simmetrica protetta dalla chiave asimmetrica nell'insieme di credenziali delle chiavi. La chiave simmetrica viene quindi usata per crittografare i dati nel database.  
  
 Questo esempio usa la chiave asimmetrica CONTOSO_KEY archiviata nell'insieme di credenziali delle chiavi importato o creato in precedenza, come sopra descritto nella [sezione 3 del passaggio 3](#Step3) . Per usare questa chiave asimmetrica nel database `ContosoDatabase` , è necessario eseguire nuovamente l'istruzione CREATE ASYMMETRIC KEY in modo da fornire al database `ContosoDatabase` un riferimento alla chiave.  
  
```sql
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)   
 [Extensible Key Management &#40;EKM&#41;](extensible-key-management-ekm.md)   
 Abilitare Transparent Data [Encryption utilizzando EKM](enable-tde-on-sql-server-using-ekm.md)   
   di [crittografia dei backup](../../backup-restore/backup-encryption.md)  
 [Creare un backup crittografato](../../backup-restore/create-an-encrypted-backup.md)  
