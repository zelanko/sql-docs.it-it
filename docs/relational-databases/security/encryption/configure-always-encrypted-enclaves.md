---
title: Configurare Always Encrypted con enclave sicuri | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 4ab035890dad4e51b6bc3a8d3f1c463e64143ac1
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670600"
---
# <a name="configure-always-encrypted-with-secure-enclaves"></a>Configurare Always Encrypted con enclave sicuri

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[Always Encrypted con enclave sicuri](always-encrypted-enclaves.md) estende la funzionalità [Always Encrypted](always-encrypted-database-engine.md) esistente per abilitare funzionalità più avanzate per i dati sensibili, mantenendo i dati riservati.

Per configurare Always Encrypted con enclave sicuri, usare il flusso di lavoro seguente:

1. Configurare l'attestazione del servizio Sorveglianza host (HGS).
2. Installare [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] nel computer SQL Server.
3. Installare gli strumenti nel computer client/di sviluppo.
4. Configurare il tipo di enclave nell'istanza di SQL Server.
5. Effettuare il provisioning delle chiavi abilitate per l'enclave.
6. Crittografare le colonne che contengono dati sensibili.

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

> [!NOTE]
> Per un'esercitazione dettagliata su come configurare l'ambiente di test e provare le funzionalità di Always Encrypted con enclave sicuri in SSMS, vedere [Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="configure-your-environment"></a>Configurare l'ambiente

Per usare gli enclave sicuri con Always Encrypted, per l'ambiente sono richiesti Windows Server 2019 Preview, SQL Server Management Studio (SSMS) 18.0, .NET Framework e vari altri componenti. Nelle sezioni seguenti sono disponibili altri dettagli e collegamenti per ottenere i componenti necessari.

### <a name="sql-server-computer-requirements"></a>Requisiti per il computer SQL Server

Il computer che esegue SQL Server deve disporre del sistema operativo e della versione di SQL Server seguenti:

*SQL Server*:

- [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] o versioni successive

*Windows*:

- Windows 10 Enterprise, versione 1809
- Windows Server DataCenter (canale semestrale), versione 1809
- Windows Server 2019 DataCenter

> [!IMPORTANT]
> Il computer SQL Server deve essere configurato come host sorvegliato, con attestazione del servizio HGS. L'attestazione TPM è il metodo di attestazione dell'enclave consigliato per gli ambienti di produzione e richiede che SQL Server venga eseguito in un computer fisico e non in una macchina virtuale. Le macchine virtuali sono adeguate solo per gli ambienti di pre-produzione.

### <a name="hgs-computer-requirements"></a>Requisiti per il computer HGS

Un singolo computer HGS è sufficiente durante la fase di test e prototipi. Per la produzione, è consigliato un cluster di failover Windows con tre computer.

Il servizio Sorveglianza host (HGS) di Windows deve essere installato in computer HGS separati e non nello stesso computer di SQL Server. Per informazioni dettagliate sui requisiti e la configurazione dei computer HGS, vedere [Configurazione del servizio Sorveglianza host per Always Encrypted in SQL Server](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server).


### <a name="determine-your-attestation-service-url"></a>Determinare l'URL del servizio di attestazione

Per determinare l'URL del servizio di attestazione, è necessario configurare gli strumenti e le applicazioni:

1. Accedere al computer SQL Server come amministratore.
2. Eseguire PowerShell come amministratore.
3. Eseguire [Get-HGSClientConfiguration](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsclientconfiguration).
4. Prendere nota della proprietà AttestationServerURL e salvarla. Dovrebbe essere simile a `https://x.x.x.x/Attestation`.

### <a name="install-tools"></a>Installare gli strumenti

Installare gli strumenti seguenti nel computer client/di sviluppo:

1. [.NET Framework 4.7.2](https://www.microsoft.com/net/download/dotnet-framework-runtime).
2. [SSMS 18.0 o versioni successive](../../../ssms/download-sql-server-management-studio-ssms.md).
3. [Modulo SQL Server PowerShell](../../../powershell/download-sql-server-ps-module.md) versione 21.1 o successiva.
4. [Visual Studio (2017 o versioni successive)](https://visualstudio.microsoft.com/downloads/).
5. [Developer Pack per .NET Framework 4.7.2](https://www.microsoft.com/net/download/visual-studio-sdks).
6. [Pacchetto NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider), versione 2.2.0 o successive.
7. [Pacchetto NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders](https://www.nuget.org/packages?q=Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders).

Usare i pacchetti NuGet nei progetti di Visual Studio per lo sviluppo di applicazioni tramite Always Encrypted con enclave sicuri. Il primo pacchetto è necessario solo se si archiviano le chiavi master della colonna in Azure Key Vault. Per altri dettagli, vedere [Sviluppare applicazioni](#develop-applications-issuing-rich-queries-in-visual-studio).

### <a name="configure-a-secure-enclave"></a>Configurare un enclave sicuro

Nel computer client/di sviluppo:

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server come amministratore di Active Directory (AD).
2. Per verificare che Always Encrypted con enclave sicuri sia supportato nell'istanza, eseguire la query seguente:

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```

    La query dovrebbe restituire una riga simile alla seguente:  

    | NAME                           | Valore | value_in_use |
    | ------------------------------ | ----- | -------------|
    | column encryption enclave type | 0     | 0            |

3. Configurare il tipo di enclave sicuro per gli enclave di tipo sicurezza basata su virtualizzazione.

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1;
   RECONFIGURE;
   ```

4. Riavviare l'istanza di SQL Server per rendere effettive le modifiche. Per riavviare l'istanza in SQL Server Management Studio, fare clic con il pulsante destro del mouse su di essa in Esplora oggetti e scegliere Riavvia. Dopo il riavvio dell'istanza, riconnettersi.

5. Verificare che l'enclave sicuro sia ora caricato eseguendo la query seguente:

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```   

    La query dovrebbe restituire una riga simile alla seguente:  

    | NAME                           | Valore | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | column encryption enclave type | 1     | 1              |

6. Per abilitare i calcoli avanzati sulle colonne crittografate, eseguire la query seguente:

   ```sql
   DBCC traceon(127,-1);
   ```

    > [!NOTE]
    > I calcoli avanzati sono disabilitati per impostazione predefinita in [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]. Devono essere abilitati tramite l'istruzione precedente dopo ogni riavvio dell'istanza di SQL Server.

## <a name="provision-enclave-enabled-keys"></a>Effettuare il provisioning delle chiavi abilitate per l'enclave

L'introduzione delle chiavi abilitate per l'enclave non cambia sostanzialmente i [flussi di lavoro per il provisioning e la gestione delle chiavi per Always Encrypted](overview-of-key-management-for-always-encrypted.md). L'unica modifica riguarda il flusso di lavoro di provisioning della chiave master della colonna. Ora è possibile contrassegnare la chiave come abilitata per l'enclave (per impostazione predefinita, le chiavi master della colonna non sono abilitate per l'enclave). Quando si imposta la nuova chiave master della colonna come abilitata per l'enclave (con SQL Server Management Studio o PowerShell), si verifica quanto segue:

- Viene impostata la proprietà `ENCLAVE_COMPUTATIONS` nei metadati della chiave master della colonna nel database.
- I valori delle proprietà della chiave master della colonna, inclusa l'impostazione di `ENCLAVE_COMPUTATIONS`, vengono firmati digitalmente. Lo strumento aggiunge la firma, che viene creata usando la chiave master della colonna effettiva, ai metadati. La firma impedisce la manomissione dell'impostazione `ENCLAVE_COMPUTATIONS`. I driver client SQL verificano le firme prima di consentire l'uso dell'enclave. In questo modo gli amministratori della sicurezza hanno il controllo sui dati di colonna che possono essere calcolati all'interno dell'enclave.

La proprietà `ENCLAVE_COMPUTATIONS` della chiave master della colonna non è modificabile. Non è possibile modificarla dopo che è stato eseguito il provisioning della chiave. È comunque possibile sostituire la chiave master della colonna con una nuova chiave con un valore diverso per la proprietà `ENCLAVE_COMPUTATIONS` rispetto a quello della chiave originale. Per sostituire la chiave master della colonna, [ruotare la chiave master della colonna](#make-columns-enclave-enabled-by-rotating-their-column-master-key). Per altre informazioni sulla proprietà `ENCLAVE_COMPUTATIONS`, vedere [CREATE COLUMN MASTER KEY](../../../t-sql/statements/create-column-master-key-transact-sql.md).

Per effettuare il provisioning di una chiave di crittografia di colonna abilitata per l'enclave, è necessario assicurarsi che la chiave master della colonna usata per la crittografia della chiave di crittografia della colonna sia abilitata per l'enclave.

Per il provisioning delle chiavi abilitate per l'enclave esistono attualmente le limitazioni seguenti:

- Le chiavi master della colonna abilitate per l'enclave devono essere archiviate in [Archivio certificati Windows](/windows/desktop/seccrypto/managing-certificates-with-certificate-stores) o in [Azure Key Vault](/azure/key-vault/key-vault-whatis/). L'archiviazione di chiavi master della colonna abilitate per l'enclave in altri tipi di archivi chiavi, ad esempio moduli di protezione hardware o archivi chiavi personalizzati, non è attualmente supportata.

### <a name="provision-enclave-enabled-keys-using-sql-server-management-studio-ssms"></a>Effettuare il provisioning di chiavi abilitate per l'enclave con SQL Server Management Studio (SSMS)

La procedura seguente crea le chiavi abilitate per l'enclave (richiede SQL Server Management Studio 18.0 o versioni successive):

1. Connettersi al database tramite SQL Server Management Studio.
2. In **Esplora oggetti** espandere il database e passare a **Sicurezza** > **Chiavi Always Encrypted**.
3. Effettuare il provisioning di una nuova chiave master della colonna abilitata per l'enclave:

    1. Fare clic con il pulsante destro del mouse su **Chiavi Always Encrypted** e scegliere **Nuova chiave master della colonna**.
    2. Selezionare il nome della chiave master della colonna.
    3. Assicurarsi di selezionare **Archivio certificati Windows (Utente corrente o Computer locale)** o **Azure Key Vault**.
    4. Selezionare **Consenti calcoli enclave**.
    5. Se si seleziona Azure Key Vault, accedere ad Azure e selezionare l'insieme di credenziali delle chiavi. Per altre informazioni su come creare un insieme di credenziali delle chiavi per Always Encrypted, vedere [Manage your key vaults from Azure portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/) (Gestire gli insiemi di credenziali delle chiavi dal portale di Azure).
    6. Selezionare la chiave se esiste già o seguire le istruzioni nel modulo per creare una nuova chiave.
    7. Fare clic su **OK**.

        ![Consenti calcoli enclave](./media/always-encrypted-enclaves/allow-enclave-computations.png)

4. Creare una nuova chiave di crittografia di colonna abilitata per l'enclave:

    1. Fare clic con il pulsante destro del mouse su **Chiavi Always Encrypted** e scegliere **Nuova chiave di crittografia della colonna**.
    2. Immettere un nome per la nuova chiave di crittografia della colonna.
    3. Nell'elenco a discesa **Chiave master della colonna** selezionare la chiave master della colonna creata nei passaggi precedenti.
    4. Fare clic su **OK**.

### <a name="provision-enclave-enabled-keys-using-powershell"></a>Effettuare il provisioning delle chiavi abilitate per l'enclave con PowerShell

Le sezioni seguenti forniscono esempi di script PowerShell per il provisioning delle chiavi abilitate per l'enclave. I passaggi specifici (nuovi) per Always Encrypted con enclave sicuri sono evidenziati. Per altre informazioni (non specifiche per Always Encrypted con enclave sicuri) sul provisioning delle chiavi tramite PowerShell, vedere [Configurare le chiavi di Always Encrypted con PowerShell](configure-always-encrypted-keys-using-powershell.md).

#### <a name="provisioning-enclave-enabled-keys---windows-certificate-store"></a>Effettuare il provisioning di chiavi abilitate per l'enclave - Archivio certificati Windows

Nel computer client/di sviluppo aprire Windows PowerShell ISE ed eseguire lo script seguente.

È importante notare l'uso del parametro `-AllowEnclaveComputations` nel cmdlet [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings).

```powershell
# Create a column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "\<Subject Name\>" -CertStoreLocation Cert:CurrentUser\\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Provide the server/db name. Modify the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key
# using the -AllowEnclaveComputations parameter.
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

#### <a name="provisioning-enclave-enabled-keys---azure-key-vault"></a>Effettuare il provisioning di chiavi abilitate per l'enclave - Azure Key Vault

Nel computer client/di sviluppo aprire Windows PowerShell ISE ed eseguire lo script seguente.

**Passaggio 1: Effettuare il provisioning di una chiave master della colonna in Azure Key Vault**

Questa operazione può essere eseguita anche tramite il portale di Azure. Per informazioni dettagliate, vedere [Manage your key vaults from Azure portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/) (Gestire gli insiemi di credenziali delle chiavi dal portale di Azure).


```powershell
Import-Module Az
Connect-AzAccount

# User values
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"

# Set the context to the specified subscription.
$azureCtx = Set-AzContext -SubscriptionId $SubscriptionId

# Create a new resource group - skip, if your desired group already exists.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation

# Create a new key vault - skip if your vault already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation

# Grant yourself permissions needed to create and use the column master key.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, list, update, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account

# Create a column master key in Azure Key Vault.
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"
```

**Passaggio 2: Creare i metadati della chiave master della colonna nel database, creare una chiave di crittografia della colonna e creare i metadati della chiave di crittografia della colonna nel database**


```powershell
# Import the SqlServer module.
Import-Module "SqlServer" -Version

# Connect to your database. Provide the server and db name. If needed, modify the connection string.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Authenticate to Azure before calling New-SqlAzureKeyVaultColumnMasterKeySettings,
# because -AllowEnclaveComputations causes a call to Azure Key Vault
# to generate the signature of the column master key.
Add-SqlAzureAuthenticationContext -Interactive

# Create a SqlColumnMasterKeySettings object for your column master key.
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="identify-enclave-enabled-keys-and-columns"></a>Identificare le colonne e le chiavi abilitate per l'enclave

Per visualizzare un elenco delle chiavi master della colonna configurate nel database, eseguire una query sulla vista del catalogo [column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md) (ad esempio, in SQL Server Management Studio). La nuova colonna **allow_enclave_computations** indica se una chiave master della colonna è abilitata per l'enclave.

```sql
SELECT name, allow_enclave_computations
FROM sys.column_master_keys;
```

Quando una chiave di crittografia della colonna è crittografata con chiavi di crittografia della colonna abilitate per l'enclave, è abilitata per l'enclave. Per restituire le chiavi di crittografia della colonna abilitate per l'enclave, la query seguente esegue un join di [sys.column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md), [sys.column_encryption_key_values](../../system-catalog-views/sys-column-encryption-key-values-transact-sql.md) e [sys.column_encryption_keys](../../system-catalog-views/sys-column-encryption-keys-transact-sql.md).

```sql
SELECT cek.name AS [cek_name]
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
FROM sys.column_master_keys cmk
JOIN sys.column_encryption_key_values cekv
   ON cmk.column_master_key_id = cekv.column_master_key_id
JOIN sys.column_encryption_keys cek
   ON cekv.column_encryption_key_id = cek.column_encryption_key_id;
```

Le colonne crittografate con chiavi abilitate per l'enclave sono abilitate per l'enclave. Per determinare quali colonne sono abilitate per l'enclave, usare la query seguente:

```sql
SELECT c.name AS column_name
, cek.name AS cek_name
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
from sys.columns c
JOIN sys.column_encryption_keys cek 
ON c.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_encryption_key_values cekv 
ON cekv.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_master_keys cmk 
ON cmk.column_master_key_id = cekv.column_master_key_id;
```

## <a name="manage-collations"></a>Gestire le regole di confronto

Always Encrypted limita le regole di confronto. Le regole di confronto non BIN2 non sono consentite per le colonne di tipo stringa di caratteri crittografate tramite crittografia deterministica. Questa restrizione si applica anche alle colonne di tipo stringa abilitate per l'enclave.

L'uso delle regole di confronto non BIN2 è consentito per le colonne di tipo stringa di caratteri crittografate con crittografia casuale e chiavi di crittografia di colonna abilitate per l'enclave. Tuttavia, l'unica nuova funzionalità abilitata per questo tipo di colonne è la crittografia sul posto. Per abilitare i calcoli avanzati (criteri di ricerca, operazioni di confronto), la colonna crittografata richiede regole di confronto BIN2.

La tabella seguente riepiloga le funzionalità per le colonne di tipo stringa abilitate per l'enclave, a seconda del tipo di crittografia e dell'ordinamento delle regole di confronto.

| **Ordinamento delle regole di confronto** | **Crittografia deterministica** | **Crittografia casuale**                 |
| ------------------------ | ---------------------------- | ----------------------------------------- |
| **Non BIN2**             | Non supportato                | Crittografia sul posto                       |
| **BIN2**                 | Confronto di uguaglianza          | Crittografia sul posto e calcoli avanzati |

### <a name="determining-and-changing-collations"></a>Determinazione e modifica delle regole di confronto

In SQL Server è possibile impostare le regole di confronto a livello di server, database o colonna. Per istruzioni generali su come determinare le regole di confronto correnti e modificare le regole di confronto a livello di server, database o colonna, vedere [Regole di confronto e supporto Unicode](../../collations/collation-and-unicode-support.md).

### <a name="special-considerations-for-non-unicode-string-columns"></a>Considerazioni speciali per le colonne di tipo stringa non UNICODE

La restrizione aggiuntiva seguente, imposta da una limitazione nei driver client SQL (non correlata ad Always Encrypted), si applica alle colonne di tipo stringa non UNICODE (ASCII). Se si sovrascrivono le regole di confronto del database per una colonna di tipo stringa non UNICODE (char, varchar), è necessario assicurarsi che le regole di confronto della colonna usino la stessa tabella codici delle regole di confronto del database.
Per elencare tutte le regole di confronto insieme ai relativi identificatori di tabella codici, usare la query seguente:

```sql
SELECT [Name]
   , [Description]
   , [CodePage] = COLLATIONPROPERTY([Name], 'CodePage')
FROM ::fn_helpcollations();
```

Ad esempio, `Chinese_Traditional_Stroke_Order_100_CI_AI_WS` e `Chinese_Traditional_Stroke_Order_100_BIN2` hanno la stessa tabella codici (950), ma `Chinese_Traditional_Stroke_Order_100_CI_AI_WS` e `Latin1_General_100_BIN2` hanno tabelle codici diverse (950 e 1252, rispettivamente). La restrizione precedente non si applica alle colonne di tipo stringa UNICODE (`nchar`, `nvarchar`). Prendere in considerazione l'impostazione del tipo di dati UNICODE per le nuove colonne crittografate create oppure la modifica del tipo in un tipo UNICODE prima della crittografia di una colonna esistente.

## <a name="create-a-new-table-with-enclave-enabled-columns"></a>Creare una nuova tabella con colonne abilitate per l'enclave

È possibile creare una nuova tabella con colonne crittografate usando l'istruzione [CREATE TABLE (Transact-SQL)](../../../t-sql/statements/create-table-transact-sql.md). Always Encrypted con enclave sicuri non modifica la sintassi dell'istruzione.

1. Usare SQL Server Management Studio per connettersi al database e aprire una finestra Query.

     > [!NOTE]
     > Always Encrypted non deve essere abilitato nella stringa di connessione per questa attività.

2. Nella finestra di query eseguire un'istruzione `CREATE TABLE` per creare la nuova tabella, specificando la clausola `ENCRYPTED WITH` nella [definizione di colonna](../../../t-sql/statements/alter-table-column-definition-transact-sql.md) per ogni colonna da crittografare. Per abilitare una colonna per l'enclave, assicurarsi di specificare una chiave di crittografia di colonna abilitata per l'enclave. Potrebbe anche essere necessario specificare regole di confronto BIN2 per le colonne di tipo stringa se le regole di confronto predefinite per il database non sono BIN2. Vedere la sezione dedicata alla configurazione delle regole di confronto per altri dettagli.

### <a name="example-of-creating-a-new-table-with-enclave-enabled-columns"></a>Esempio di creazione di una nuova tabella con colonne abilitate per l'enclave

L'istruzione seguente crea una nuova tabella con due colonne crittografate, SSN e Salary. Supponendo che CEK1 sia una chiave di crittografia di colonna abilitata per l'enclave, il motore di SQL Server supporta la crittografia sul posto e i calcoli avanzati per entrambe le colonne, perché usano la crittografia casuale. L'istruzione imposta le regole di confronto Latin1\_General\_BIN2 per la colonna SSN UNICODE, operazione necessaria supponendo che le regole di confronto predefinite del database non siano di tipo BIN2 Latin1.

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [int] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

## <a name="add-a-new-enclave-enabled-column-to-an-existing-table"></a>Aggiungere una nuova colonna abilitata per l'enclave a una tabella esistente

È possibile aggiungere una nuova colonna crittografia a una tabella esistente usando l'istruzione [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) / ADD. Always Encrypted con enclave sicuri non modifica la sintassi dell'istruzione.

1. Usare SQL Server Management Studio per connettersi al database e aprire una finestra Query.

   Always Encrypted non deve essere abilitato nella stringa di connessione per questa attività.

2. Nella finestra Query eseguire un'istruzione ALTER TABLE con la clausola ADD, specificando la clausola ENCRYPTED WITH nella [definizione di colonna](../../../t-sql/statements/alter-table-column-definition-transact-sql.md) e usando una chiave di crittografia di colonna abilitata per l'enclave. Potrebbe anche essere necessario specificare regole di confronto BIN2 se la nuova colonna è di tipo stringa e se le regole di confronto predefinite per il database non sono BIN2. Vedere la sezione dedicata alla configurazione delle regole di confronto per altri dettagli.

### <a name="example-of-adding-a-new-enclave-enabled-column-to-an-existing-table"></a>Esempio di aggiunta di una nuova colonna abilitata per l'enclave a una tabella esistente

Supponendo che CEK1 sia una chiave di crittografia di colonna abilitata per l'enclave, l'istruzione seguente aggiunge una nuova colonna crittografata, denominata BirthDate, che supporta sia query avanzate che la crittografia sul posto, perché la colonna usa la crittografia casuale.

```sql
ALTER TABLE [dbo].[Employees]
ADD [BirthDate] [Date] ENCRYPTED WITH (
COLUMN_ENCRYPTION_KEY = [CEK1],
ENCRYPTION_TYPE = Randomized,
ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL;
```


## <a name="prepare-an-ssms-query-window-with-always-encrypted-enabled"></a>Preparare una finestra di query di SQL Server Management Studio con Always Encrypted abilitato

Per aggiungere i parametri di connessione necessari per abilitare i calcoli dell'enclave:

1. Aprire SSMS.
2. Dopo aver specificato il nome del server e un nome di database nella finestra di dialogo Connetti al server, fare clic su **Opzioni**. Passare alla scheda **Always Encrypted** selezionare **Abilita Always Encrypted** e specificare l'URL di attestazione dell'enclave.
    
    ![Impostazione di crittografia di colonna](./media/always-encrypted-enclaves/column-encryption-setting.png)

3. Fare clic su Connetti.
4. Aprire una nuova finestra Query.

In alternativa, se è già aperta una finestra Query, questa è la procedura per aggiornare la connessione al database per abilitare Always Encrypted:

1. Fare clic con il pulsante destro del mouse in un punto qualsiasi all'interno di una finestra Query esistente.
2. Selezionare Connessione \> Cambia connessione.
3. Fare clic su **Opzioni**. Passare alla scheda **Always Encrypted** selezionare **Abilita Always Encrypted** e specificare l'URL di attestazione dell'enclave.
4. Fare clic su Connetti.

## <a name="work-with-encrypted-columns"></a>Usare colonne crittografate

### <a name="encrypt-an-existing-plaintext-column-in-place"></a>Crittografare una colonna esistente di testo non crittografato sul posto

È possibile crittografare una colonna esistente di testo non crittografato sul posto usando l'istruzione [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) / ALTER COLUMN, a condizione di usare una chiave di crittografia di colonna abilitata per l'enclave.

Per crittografare una colonna usando una chiave non abilitata per l'enclave, è necessario usare strumenti lato client, ad esempio la procedura guidata Always Encrypted in SQL Server Management Studio o il cmdlet Set-SqlColumnEncryption nel modulo SqlServer PowerShell. Per informazioni dettagliate, vedere:

- [Procedura guidata Always Encrypted](always-encrypted-wizard.md)
- [Configurare la crittografia della colonna tramite PowerShell](configure-column-encryption-using-powershell.md)


#### <a name="prerequisites-for-encrypting-an-existing-plaintext-column-in-place"></a>Prerequisiti per la crittografia di una colonna esistente di testo non crittografato sul posto

- La colonna esistente non è crittografata.
- È stato effettuato il provisioning delle chiavi abilitate per l'enclave.
- Si ha accesso alla chiave master della colonna.

#### <a name="steps-for-encrypting-existing-plaintext-column-in-place"></a>Passaggi per la crittografia di una colonna esistente di testo non crittografato sul posto

1. Preparare una finestra Query di SQL Server Management Studio con Always Encrypted e i calcoli dell'enclave abilitati nella connessione al database. Per informazioni dettagliate, vedere [Preparare una finestra Query di SQL Server Management Studio con Always Encrypted abilitato](#prepare-an-ssms-query-window-with-always-encrypted-enabled).
2. Nella finestra Query eseguire un'istruzione ALTER TABLE con la clausola ALTER COLUMN, specificando una chiave di crittografia di colonna abilitata per l'enclave nella clausola ENCRYPTED WITH. Se la colonna è una colonna di tipo stringa (ad esempio, char, varchar, nchar, nvarchar), potrebbe anche essere necessario modificare le regole di confronto impostando regole di confronto BIN2. Vedere la sezione dedicata alla configurazione delle regole di confronto per altri dettagli.
    
    > [!NOTE]
    > Se la chiave master della colonna è archiviata in Azure Key Vault, potrebbe essere richiesto di accedere ad Azure.

3. Cancellare la cache dei piani per tutti i batch e le stored procedure che accedono alla tabella per aggiornare le informazioni di crittografia dei parametri. 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > Se non si rimuove il piano per le query interessate dalla cache, la prima esecuzione della query dopo la crittografia potrebbe non riuscire.

    > [!NOTE]
    > Usare `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` o `DBCC FREEPROCCACHE` per cancellare la cache dei piani con attenzione, perché ciò potrebbe comportare una temporanea riduzione del livello delle prestazioni delle query. Per ridurre al minimo l'impatto negativo della cancellazione della cache, è possibile rimuovere selettivamente i piani solo per le query interessate.

4.  Chiamare [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) per aggiornare i metadati per i parametri di ogni modulo (stored procedure, funzione, vista, trigger) persistente in [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) e che potrebbe risultare invalidato in seguito alla crittografia delle colonne.

#### <a name="example-of-encrypting-existing-plaintext-column-in-place"></a>Esempio di crittografia di una colonna esistente di testo non crittografato sul posto

L'esempio seguente presuppone che:

- CEK1 sia una chiave di crittografia di colonna abilitata per l'enclave.

- La colonna SSN sia di testo non crittografato e usi attualmente regole di confronto Latin1 non BIN2 (ad esempio, Latin1\_General\_CI\_AI\_KS\_WS).

L'istruzione crittografa la colonna SSN mediante crittografia casuale e una chiave di crittografia di colonna abilitata per l'enclave. Sovrascrive anche le regole di confronto del database predefinite con regole di confronto BIN2 corrispondenti (nella stessa tabella codici).

L'operazione viene eseguita online (ONLINE = ON). Si noti anche la chiamata a **ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE** che ricrea i piani delle query interessate dalla modifica dello schema di tabella.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char] COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
WITH
(ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

### <a name="make-an-existing-encrypted-column-enclave-enabled"></a>Abilitare per l'enclave una colonna crittografata esistente

Esistono diversi modi per abilitare la funzionalità di enclave per una colonna esistente che non è abilitata per l'enclave. Il metodo scelto dipende da diversi fattori:

- **Ambito/granularità:** si vuole abilitare la funzionalità di enclave per un subset di colonne o per tutte le colonne protette con una chiave master della colonna specificata?
- **Dimensioni dei dati:** quali sono le dimensioni delle tabelle contenenti le colonne che si vuole abilitare per l'enclave?
- Si vuole modificare anche il tipo di crittografia per le colonne? Tenere presente che solo la crittografia casuale supporta i calcoli avanzati (criteri di ricerca, operatori di confronto). Se la colonna è crittografata con la crittografia deterministica, sarà necessario anche crittografarla di nuovo con la crittografia casuale per avere a disposizione le funzionalità complete dell'enclave.

Ecco i tre approcci per l'abilitazione degli enclave per colonne esistenti:

#### <a name="option-1-rotate-the-column-master-key-to-replace-it-with-an-enclave-enabled-column-master-key"></a>Opzione 1: ruotare la chiave master della colonna per sostituirla con una chiave master della colonna abilitata per l'enclave.
  
- Vantaggi:
  - Non richiede di crittografare di nuovo i dati, pertanto è in genere l'approccio più rapido. È un approccio consigliato per le colonne che contengono grandi quantità di dati, a condizione che tutte le colonne per cui è necessario abilitare i calcoli avanzati usino già la crittografia deterministica e, di conseguenza, non debbano essere crittografate di nuovo.
  - Consente di abilitare la funzionalità di enclave per più colonne su larga scala, perché abilita per l'enclave tutte le chiavi di crittografia di colonna e tutte le colonne crittografate, associate alla chiave master della colonna originale.
  
- Svantaggi:
  - Non supporta la modifica del tipo di crittografia da deterministica a casuale, quindi anche se rende disponibile la crittografia sul posto per le colonne crittografate in modo deterministico, non abilita i calcoli avanzati.
  - Non consente di convertire in modo selettivo alcune delle colonne, associate a una determinata chiave master della colonna.
  - Introduce l'overhead di gestione delle chiavi: è necessario creare una nuova chiave master della colonna e renderla disponibile per le applicazioni che eseguono query sulle colonne interessate.  

#### <a name="option-2-this-approach-involves-two-steps-1-rotating-the-column-master-key-as-in-option-1-and-2-re-encrypting-a-subset-of-deterministically-encrypted-columns-using-randomized-encryption-to-enable-rich-computations-for-those-columns"></a>Opzione 2: questo approccio comporta due passaggi: 1) ruotare la chiave master della colonna (come nell'opzione 1) e 2) crittografare nuovamente un subset di colonne crittografate in modo deterministico con la crittografia casuale, per abilitare i calcoli avanzati per tali colonne.
  
- Vantaggi:
  - Crittografa nuovamente i dati sul posto ed è pertanto un metodo consigliato per abilitare le query complesse per le colonne crittografate in modo deterministico che contengono grandi quantità di dati. Il passaggio 1 rende disponibile la crittografia sul posto per le colonne con crittografia deterministica, quindi il passaggio 2 può essere eseguito sul posto.
  - Consente di abilitare la funzionalità di enclave per più colonne su larga scala.
  
- Svantaggi:
  - Non consente di convertire in modo selettivo alcune delle colonne, associate a una determinata chiave master della colonna.
  - Introduce l'overhead di gestione delle chiavi: è necessario creare una nuova chiave master della colonna e renderla disponibile per le applicazioni che eseguono query sulle colonne interessate.

#### <a name="option-3-re-encrypting-selected-columns-with-a-new-enclave-enabled-column-encryption-key-and-randomized-encryption-if-needed-on-the-client-side"></a>Opzione 3: crittografare nuovamente le colonne selezionate con una nuova chiave di crittografia di colonna abilitata per l'enclave e la crittografia casuale, se necessario, sul lato client.
  
- Vantaggi:
  - Consente di abilitare la funzionalità di enclave in modo selettivo per una sola colonna o un piccolo subset di colonne.
  - È possibile abilitare i calcoli avanzati per una colonna crittografata in modo deterministico in un unico passaggio.
  - Non è richiesta la creazione di una nuova chiave master della colonna, quindi l'impatto sulle applicazioni è minore.
  
- Svantaggi:
  - L'intero contenuto della tabella che contiene la colonna deve essere spostato all'esterno del database per la riesecuzione della crittografia, pertanto è consigliabile solo per piccole tabelle.

Per ulteriori informazioni, vedere le sezioni seguenti:
  - [Abilitare le colonne per l'enclave tramite la rotazione delle chiavi master](#make-columns-enclave-enabled-by-rotating-their-column-master-key)
  - [Crittografare di nuovo le colonne sul posto](#re-encrypt-columns-in-place)
  - [Crittografare di nuovo le colonne sul lato client](#re-encrypt-columns-on-the-client-side)

### <a name="make-columns-enclave-enabled-by-rotating-their-column-master-key"></a>Abilitare le colonne per l'enclave tramite la rotazione delle chiavi master

La rotazione di una chiave master della colonna è il processo di sostituzione di una chiave master della colonna esistente con la nuova chiave. Comporta la riesecuzione della crittografia delle chiavi di crittografia della colonna associate alla chiave master precedente della colonna, usando la nuova chiave master della colonna. Questo flusso di lavoro esiste sin dalla versione iniziale di Always Encrypted per supportare la sostituzione di una chiave master della colonna per motivi di sicurezza o di conformità, in caso di compromissione della chiave master della colonna esistente.

Always Encrypted con gli enclave aggiunge un nuovo scopo per il flusso di lavoro di rotazione della chiave master della colonna. Supponendo che la vecchia chiave master della colonna non sia abilitata per l'enclave e che la nuova chiave master della colonna sia abilitata per l'enclave, il processo di rotazione rende effettivamente tutte le chiavi di crittografia di colonna, associate alla chiave master della colonna, abilitate per l'enclave. La rotazione di una chiave master della colonna non comporta la riesecuzione della crittografia dei dati e, pertanto, è un processo consigliato per l'abilitazione della funzionalità di enclave per le colonne esistenti.

La rotazione della chiave master della colonna non modifica il tipo di crittografia delle colonne interessate. Pertanto, è possibile solo rendere disponibile la crittografia sul posto per le colonne crittografate in modo deterministico. Per abilitare i calcoli avanzati per le colonne con crittografia deterministica, è necessario crittografarle nuovamente (sul posto) dopo la rotazione della chiave master della colonna.

Per rendere disponibili i calcoli avanzati, potrebbe anche essere necessario modificare le regole di confronto per le colonne stringa, usando la crittografia casuale, impostando regole di confronto BIN2. Vedere la sezione dedicata alla configurazione delle regole di confronto per altri dettagli.

Il processo di rotazione della chiave master della colonna è lo stesso, indipendentemente dal fatto che la chiave coinvolta sia abilitata per l'enclave. Negli articoli seguenti sono disponibili informazioni dettagliate su come ruotare la chiave master della colonna:

- [Ruotare una chiave master della colonna con SQL Server Management Studio](configure-always-encrypted-using-sql-server-management-studio.md)
- [Ruotare le chiavi di Always Encrypted con PowerShell](rotate-always-encrypted-keys-using-powershell.md)

Per praticità, di seguito viene fornito uno script di PowerShell di esempio per la rotazione di una chiave master della colonna.

#### <a name="prerequisites-of-rotating-the-column-master-key-for-enclave-enabled-columns"></a>Prerequisiti per la rotazione delle chiavi master di colonna per le colonne abilitate per l'enclave

- Aver effettuato il provisioning di una nuova chiave master della colonna abilitata per l'enclave.
- Avere accesso sia alla chiave master della colonna precedente che a quella nuova.
- Tutte le colonne di tipo stringa, protette con la chiave master della colonna precedente, usano regole di confronto BIN2.

> [!NOTE]
> In alternativa, è possibile modificare le regole di confronto delle colonne di tipo stringa dopo la rotazione della chiave master della colonna.

#### <a name="steps-for-rotating-the-column-master-key-for-enclave-enabled-columns"></a>Passaggi per la rotazione delle chiavi master di colonna per le colonne abilitate per l'enclave

Incollare lo script seguente in Windows PowerShell ISE, sostituendo i \<segnaposto\> con i valori specifici:

```powershell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Modify server/db name or/and the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " +
$databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Set the names of the old/current column master key and the new/target enclave-enabled column master key. (Change the names, if needed).
$oldCmkName = "<old column master key name>"
$newCmkName = "<new column master key name>"

# Authenticate to Azure. Needed only of either column master key is stored in Azure Key Vault.
Add-SqlAzureAuthenticationContext -Interactive

# Initiate the rotation from the current column master key to the new column master key.
Invoke-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName
-TargetColumnMasterKeyName $newCmkName -InputObject $database

# Complete the rotation of the old column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName
$oldCmkName -InputObject $database

# Remove the old column master key metadata.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```


### <a name="re-encrypt-columns-in-place"></a>Crittografare di nuovo le colonne sul posto

Dopo avere abilitato la colonna per l'enclave, è possibile eseguire le operazioni seguenti sul posto (all'interno dell'enclave, senza dover spostare i dati fuori dal database):

- Rotazione della chiave di crittografia di colonna (per sostituirla con una nuova chiave), ad esempio, al fine di rispettare normative di conformità che in alcuni casi richiedono la rotazione periodica delle chiavi, o per motivi di sicurezza in caso di compromissione della chiave di crittografia della colonna.
- Modifica del tipo di crittografia, ad esempio, dalla crittografia deterministica alla crittografia casuale, per rendere disponibili i calcoli avanzati per la colonna.

#### <a name="prerequisites-for-re-encrypting-columns-in-place"></a>Prerequisiti per crittografare di nuovo le colonne sul posto

- La colonna è crittografata con una chiave di crittografia di colonna abilitata per l'enclave.
- È stato eseguito il provisioning di una nuova chiave di crittografia di colonna abilitata per l'enclave (se l'obiettivo è sostituire la chiave di crittografia di colonna abilitata per l'enclave corrente per la protezione della colonna).
- Si ha accesso alla chiave master della colonna.

#### <a name="steps-for-re-encrypting-columns-in-place"></a>Passaggi per crittografare di nuovo le colonne sul posto

1. Preparare una finestra Query di SQL Server Management Studio con Always Encrypted e i calcoli dell'enclave abilitati per la connessione al database. Per informazioni dettagliate, vedere [Preparare una finestra Query di SQL Server Management Studio con Always Encrypted abilitato](#prepare-an-ssms-query-window-with-always-encrypted-enabled).

2. Nella finestra Query eseguire l'istruzione [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) con la clausola ALTER COLUMN, specificando quanto segue nella clausola ENCRYPTED WITH:
    
    1. Il nome della nuova chiave di crittografia di colonna abilitata per l'enclave se si intende ruotare la chiave corrente. Se non si intende modificare la chiave di crittografia di colonna, è necessario specificare il nome della chiave corrente.
    
    2. Il nuovo tipo di crittografia, se si vuole modificarlo. Se non si intende modificare il tipo di crittografia, è necessario specificare il tipo di crittografia corrente.
        
       Se la colonna da crittografare di nuovo usa regole di confronto (BIN2) diverse rispetto alle regole di confronto predefinite del database, è necessario includere la frase COLLATE e specificare le regole di confronto della colonna correnti nella definizione di colonna (per mantenere uguali le regole di confronto).
        
       > [!NOTE]
       > Se la chiave master della colonna è archiviata in Azure Key Vault, potrebbe essere richiesto di accedere ad Azure.

3. Cancellare la cache dei piani per tutti i batch e le stored procedure che accedono alla tabella per aggiornare le informazioni di crittografia dei parametri. 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > Se non si rimuove il piano per le query interessate dalla cache, la prima esecuzione della query dopo la crittografia potrebbe non riuscire.

    > [!NOTE]
    > Usare ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE o DBCC FREEPROCCACHE per cancellare la cache dei piani con attenzione, perché ciò potrebbe comportare una temporanea riduzione del livello delle prestazioni delle query. Per ridurre al minimo l'impatto negativo della cancellazione della cache, è possibile rimuovere selettivamente i piani solo per le query interessate.

4.  Chiamare [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) per aggiornare i metadati per i parametri di ogni modulo (stored procedure, funzione, vista, trigger) persistente in [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) e che potrebbe risultare invalidato in seguito alla riesecuzione della crittografia delle colonne.

#### <a name="examples-of-re-encrypting-columns-in-place"></a>Esempi di riesecuzione della crittografia delle colonne sul posto

Supponendo che la colonna SSN sia attualmente crittografata in modo deterministico con una chiave di crittografia di colonna abilitata per l'enclave denominata CEK1 e che le regole di confronto correnti impostate a livello di colonna siano Latin1\_General\_BIN2, l'istruzione seguente crittografa nuovamente la colonna con crittografia casuale e la stessa chiave.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

Supponendo che la colonna SSN sia attualmente crittografata in modo deterministico con una chiave di crittografia di colonna abilitata per l'enclave denominata CEK1 e che le regole di confronto predefinite del database siano di tipo BIN2 e non siano state impostate a livello di colonna, l'istruzione seguente crittografa nuovamente la colonna con una nuova chiave abilitata per l'enclave denominata CEK2 senza modificare il tipo di crittografia.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK2]
, ENCRYPTION\_TYPE = Deterministic
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

Supponendo che la colonna SSN sia attualmente crittografata in modo deterministico con una chiave di crittografia di colonna abilitata per l'enclave denominata CEK1 e che le regole di confronto predefinite del database siano di tipo BIN2 e non siano state impostate a livello di colonna, l'istruzione seguente crittografa nuovamente la colonna con una nuova chiave abilitata per l'enclave e la crittografia casuale. L'operazione viene inoltre eseguita nella modalità online.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL 
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

### <a name="re-encrypt-columns-on-the-client-side"></a>Crittografare di nuovo le colonne sul lato client

Il metodo legacy per rieseguire la crittografia (e per la crittografia o la decrittografia) delle colonne usa strumenti lato client, come la procedura guidata Always Encrypted o PowerShell. In generale, questo metodo non è consigliato, tranne se la tabella che contiene le colonne (di cui rieseguire la crittografia) è di piccole dimensioni e se l'obiettivo è combinare la riesecuzione della crittografia di una colonna con una nuova chiave abilitata per l'enclave e la modifica del tipo di crittografia (da deterministica a casuale).

Se si crittografa nuovamente una colonna usando la crittografia casuale, potrebbe essere necessario modificare le regole di confronto con regole di confronto BIN2 (prima o dopo la ricrittografia), per rendere disponibili i calcoli avanzati. Vedere la sezione dedicata alla configurazione delle regole di confronto per altri dettagli.

Per informazioni dettagliate, vedere:

  - Rotazione delle chiavi di crittografia della colonna con SQL Server Management Studio: <https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-wizard>
  - Rotazione delle chiavi di crittografia della colonna con PowerShell: <https://docs.microsoft.com/sql/relational-databases/security/encryption/configure-column-encryption-using-powershell>

### <a name="decrypt-a-column-in-place"></a>Decrittografare un colonna sul posto

Se la colonna è crittografata con una chiave di crittografia di colonna abilitata per l'enclave, è possibile decrittografarla (convertirla in colonna di testo non crittografato) sul posto usando l'istruzione ALTER TABLE. L'operazione viene inoltre eseguita nella modalità online.

#### <a name="prerequisites-for-decrypting-a-column-in-place"></a>Prerequisiti per la decrittografia di una colonna sul posto

- La colonna è crittografata con una chiave di crittografia di colonna abilitata per l'enclave.
- Si ha accesso alla chiave master della colonna.

#### <a name="steps-for-decrypting-a-column-in-place"></a>Passaggi per la decrittografia di una colonna sul posto

1. Preparare una finestra Query di SQL Server Management Studio con Always Encrypted e i calcoli dell'enclave abilitati per la connessione al database. Per informazioni dettagliate, vedere [Preparare una finestra Query di SQL Server Management Studio con Always Encrypted abilitato](#prepare-an-ssms-query-window-with-always-encrypted-enabled).

2. Nella finestra Query eseguire l'istruzione [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) con la clausola ALTER COLUMN, specificando la configurazione di colonna desiderata **senza** la clausola ENCRYPTED WITH.
    
    > [!NOTE]
    > Se la chiave master della colonna è archiviata in Azure Key Vault, potrebbe essere richiesto di accedere ad Azure.

3. Cancellare la cache dei piani per tutti i batch e le stored procedure che accedono alla tabella per aggiornare le informazioni di crittografia dei parametri. 

    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```

    > [!NOTE]
    > Se non si rimuove il piano per le query interessate dalla cache, la prima esecuzione della query dopo la crittografia potrebbe non riuscire.

    > [!NOTE]
    > Usare ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE o DBCC FREEPROCCACHE per cancellare la cache dei piani con attenzione, perché ciò potrebbe comportare una temporanea riduzione del livello delle prestazioni delle query. Per ridurre al minimo l'impatto negativo della cancellazione della cache, è possibile rimuovere selettivamente i piani solo per le query interessate.

4. Chiamare [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) per aggiornare i metadati per i parametri di ogni modulo (stored procedure, funzione, vista, trigger) persistente in [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) e che potrebbe risultare invalidato in seguito alla decrittografia delle colonne.

#### <a name="example-for-decrypting-a-column-in-place"></a>Esempio di decrittografia di una colonna sul posto

Supponendo che la colonna SSN sia crittografata e che le regole di confronto correnti impostate a livello di colonna siano Latin1\_General\_BIN2, l'istruzione seguente consente di decrittografare la colonna e mantenere invariate le regole di confronto. In alternativa, è possibile scegliere di modificare le regole di confronto, ad esempio, impostando regole di confronto non BIN2 nella stessa istruzione.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

## <a name="issue-rich-queries-against-encrypted-columns-using-ssms"></a>Eseguire query avanzate su colonne crittografate usando SQL Server Management Studio

Il modo più rapido per provare query avanzate sulle colonne abilitate per l'enclave è da una finestra Query di SQL Server Management Studio con la funzionalità Parametrizzazione per Always Encrypted abilitata. Per informazioni dettagliate su questa funzionalità utile in SQL Server Management Studio, vedere:

- [Parametrizzazione per Always Encrypted - Uso di SQL Server Management Studio per inserire, aggiornare e filtrare in base alle colonne crittografate](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/)
- [Esecuzione di query in colonne crittografate](configure-always-encrypted-using-sql-server-management-studio.md#querying-encrypted-columns)

### <a name="prerequisites-for-issuing-rich-queries-against-encrypted-columns-using-ssms"></a>Prerequisiti per l'esecuzione di query avanzate su colonne crittografate usando SQL Server Management Studio

- Le colonne di destinazione delle query sono abilitate per l'enclave.
- Si ha accesso alla chiave (o alle chiavi) master della colonna.

### <a name="steps-for-issuing-rich-queries-against-encrypted-columns-using-ssms"></a>Passaggi per l'esecuzione di query avanzate su colonne crittografate usando SQL Server Management Studio

1. Preparare una finestra Query di SQL Server Management Studio con Always Encrypted e i calcoli dell'enclave abilitati per la connessione al database. Per informazioni dettagliate, vedere [Preparare una finestra Query di SQL Server Management Studio con Always Encrypted abilitato](#prepare-an-ssms-query-window-with-always-encrypted-enabled).

2. Abilitare Parametrizzazione per Always Encrypted.

    1. Selezionare **Query** dal menu principale di SQL Server Management Studio.
    2. Selezionare **Opzioni query**.
    3. Passare a **Esecuzione** > **Avanzata**.
    4. Selezionare o deselezionare Abilita parametrizzazione per Always Encrypted.
    5. Fare clic su OK.

3. Creare ed eseguire le query usando calcoli avanzati sulle colonne crittografate. È necessario dichiarare una variabile Transact-SQL per ogni valore destinato a una colonna crittografata nella query. Le variabili devono usare le inizializzazioni inline (non possono essere impostate tramite l'istruzione SET).

    > [!NOTE]
    > Se la chiave master della colonna è archiviata in Azure Key Vault, potrebbe essere richiesto di accedere ad Azure.

### <a name="example-of-rich-queries-against-encrypted-columns"></a>Esempio di query avanzate su colonne crittografate

In questo esempio si presuppone che il database contenga una tabella creata usando l'istruzione seguente.

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [int] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

CEK1 sia una chiave di crittografia di colonna abilitata per l'enclave.

Di seguito è riportato un esempio di una query che rispetta le linee guida per la parametrizzazione, su tale tabella:

```sql
DECLARE @SSNPattern CHAR(11) = '%1111%'
DECLARE @MinSalary INT = 1000
SELECT *
FROM [dbo].[Employees]
WHERE SSN LIKE @SSNPattern
    AND [Salary] >= @MinSalary;
GO;
```

## <a name="create-and-use-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>Creare e usare indici sulle colonne abilitate per l'enclave tramite la crittografia casuale

Poiché un indice su una colonna abilitata per l'enclave che usa la crittografia casuale archivia i valori della chiave di indice crittografati mentre i valori sono ordinati in base al testo non crittografato, il motore di SQL Server deve usare l'enclave per qualsiasi operazione che comporta la creazione o aggiornamento di un indice, tra cui:

- Creazione o ricompilazione di un indice.
- Inserimento, aggiornamento o eliminazione di una riga nella tabella (contenente una colonna indicizzata/crittografata), che attiva l'inserimento e/o la rimozione di una chiave di indice nell'indice.
- Esecuzione di comandi DBCC che comportano la verifica dell'integrità degli indici, ad esempio [DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) oppure [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).
- Ripristino del database (ad esempio, dopo il riavvio di SQL Server in seguito a un errore), se SQL Server deve annullare eventuali modifiche all'indice (vedere di seguito).

Tutte le operazioni precedenti richiedono che l'enclave disponga della chiave di crittografia della colonna per la colonna indicizzata, in modo da poter decrittografare le chiavi di indice. In generale, l'enclave può ottenere una chiave di crittografia della colonna in due modi:
- Direttamente dall'applicazione client.
- Dalla cache delle chiavi di crittografia della colonna.

### <a name="invoke-indexing-operations-with-column-encryption-keys-provided-directly-by-the-client"></a>Richiamare operazioni di indicizzazione con chiavi di crittografia della colonna fornite direttamente dal client

Per il corretto funzionamento di questo metodo per richiamare le operazioni di indicizzazione, l'applicazione che esegue una query che attiva un'operazione su un indice deve:

- Connettersi al database con Always Encrypted e i calcoli dell'enclave abilitati nella connessione di database.
- L'applicazione deve avere accesso alla chiave master della colonna che protegge la chiave di crittografia della colonna per la colonna indicizzata.

Quando il motore di SQL Server analizza la query dell'applicazione e determina che sarà necessario aggiornare un indice su una colonna crittografata per eseguire la query, indica al driver client di fornire all'enclave la chiave CEK richiesta tramite un canale sicuro. Si tratta esattamente dello stesso meccanismo usato per fornire all'enclave le chiavi di crittografia della colonna per l'elaborazione delle query che non comportano operazioni di indicizzazione.

Questo metodo è utile per garantire che la presenza di indici su colonne crittografate sia trasparente per le applicazioni che si connettono già al database con Always Encrypted e i calcoli dell'enclave abilitati per la connessione e usano l'enclave per l'elaborazione delle query. Dopo aver creato un indice su una colonna, il driver all'interno dell'app fornirà in modo trasparente le chiavi di crittografia della colonna all'enclave per le operazioni di indicizzazione. Si noti che la creazione di indici può aumentare il numero di query che richiedono all'applicazione di inviare all'enclave le chiavi di crittografia della colonna.

Per istruzioni dettagliate su come usare questo metodo, vedere [Esercitazione: Creazione e uso di indici sulle colonne abilitate per l'enclave tramite la crittografia casuale](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md).

### <a name="invoke-indexing-operations-using-cached-column-encryption-keys"></a>Richiamare operazioni di indicizzazione mediante chiavi di crittografia di colonna memorizzate nella cache

Una volta che un'applicazione client invia all'enclave una chiave di crittografia della colonna (per l'elaborazione di qualsiasi query che richiede i calcoli dell'enclave), l'enclave memorizza la chiave di crittografia della colonna in una cache interna (posizionata all'interno dell'enclave e inaccessibile dall'esterno).

Se la stessa o un'altra applicazione client (usata dallo stesso o da un altro utente) attiva un'operazione su un indice senza specificare direttamente la crittografia della colonna richiesta, l'enclave cerca la chiave di crittografia della colonna nella cache. Di conseguenza, l'operazione sull'indice ha esito positivo, anche se l'applicazione client non ha fornito la chiave.

Per il corretto funzionamento di questo metodo di richiamo delle operazioni di indicizzazione, l'applicazione deve connettersi al database senza Always Encrypted abilitato per la connessione e la chiave di crittografia della colonna richiesta deve essere disponibile nella cache all'interno dell'enclave.

Questo metodo di richiamo delle operazioni è supportato solo per le query che non richiedono chiavi di crittografia della colonna per le altre operazioni non correlate agli indici. Ad esempio, un'applicazione che inserisce una riga tramite un'istruzione INSERT in una tabella che contiene una colonna crittografata deve connettersi al database con Always Encrypted abilitato nella stringa di connessione e deve avere accesso alle chiavi, indipendentemente dal fatto che la colonna crittografata contenga un indice o meno.

Questo metodo è utile per:

- Assicurare che la presenza di indici sulle colonne abilitate per l'enclave con crittografia casuale sia trasparente per le applicazioni e gli utenti che non hanno accesso alle chiavi e ai dati come testo non crittografato. Garantire che la creazione di un indice su una colonna crittografata non rallenti le query esistenti. In altre parole, se un'applicazione esegue una query su una tabella contenente colonne crittografate senza la necessità di avere accesso alle chiavi, l'applicazione può continuare a essere eseguita senza aver accesso alle chiavi dopo che un amministratore di database crea un indice. Si consideri ad esempio un'applicazione che esegue la query seguente sulla tabella **Employees** usata nell'esempio precedente, prima che un amministratore di database crei un indice su una colonna crittografata. 

   ```sql
   DELETE FROM [dbo].[Employees] WHERE [EmployeeID] = 1;
   GO
   ```

   Se l'applicazione invia la query tramite una connessione senza Always Encrypted e i calcoli dell'enclave abilitati, la query avrà esito positivo, perché non attiva alcun calcolo sulle colonne crittografate. Dopo che un amministratore di database crea un indice su colonne crittografate, la query attiva la rimozione dagli indici delle chiavi di indice, che sono richieste dall'enclave per le chiavi di crittografia della colonna. L'applicazione sarà comunque in grado di continuare a eseguire questa query tramite la stessa connessione, purché il proprietario dei dati abbia fornito all'enclave le chiavi di crittografia della colonna.

- Per ottenere la separazione dei ruoli durante la gestione degli indici, perché consente agli amministratori di database di creare e modificare gli indici su colonne crittografate senza dover accedere ai dati sensibili. 

Per istruzioni dettagliate su come usare questo metodo, vedere [Esercitazione: Creazione e uso di indici sulle colonne abilitate per l'enclave tramite la crittografia casuale](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md).

## <a name="develop-applications-issuing-rich-queries-in-visual-studio"></a>Sviluppare le applicazioni che eseguono query avanzate in Visual Studio

### <a name="set-up-your-visual-studio-project"></a>Configurare il progetto di Visual Studio

Per usare Always Encrypted con enclave sicuri in un'applicazione .NET Framework, è necessario assicurarsi che l'applicazione sia sviluppata in base a .NET Framework 4.7.2 e integrata con il pacchetto NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders. Inoltre, se la chiave master della colonna viene archiviata in Azure Key Vault, è anche necessario integrare l'applicazione con il pacchetto NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider, versione 2.2.0 o successiva. 

1. Aprire Visual Studio.
2. Creare un nuovo progetto Visual C\# o aprirne uno esistente.
3. Assicurarsi che il progetto sia destinato almeno a .NET Framework 4.7.2. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere Proprietà e impostare Framework di destinazione su .NET Framework 4.7.2.

4. Installare il pacchetto NuGet seguente passando a**Strumenti** (menu principale) > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**. Eseguire il codice seguente nella Console di Gestione pacchetti.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. Se si usa Azure Key Vault pe l'archiviazione delle chiavi master della colonna, installare i pacchetti NuGet seguenti passando a **Strumenti** (menu principale) > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**. Eseguire il codice seguente nella Console di Gestione pacchetti.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

6. Selezionare il progetto e fare clic su Installa.
7. Aprire il file di configurazione dal progetto (ad esempio, App.config o Web.config).
8. Individuare la sezione \<configuration\>. All'interno della sezione \<configuration\>, individuare la sezione \<configSections\>. Aggiungere la sezione seguente all'interno di \<configSections\>:

   ```xml
   <section name="SqlColumnEncryptionEnclaveProviders"  type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data,  Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
   ```

9. All'interno della sezione configuration, sotto la sezione \<configSections\>, aggiungere la sezione seguente, che specifica un provider di enclave da usare per attestare e interagire con gli enclave Intel SGX:

   ```xml
   <SqlColumnEncryptionEnclaveProviders>
       <providers>
           <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.VirtualizationBasedSecurityEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
       </providers>
   </SqlColumnEncryptionEnclaveProviders>
   ```

### <a name="develop-and-test-your-app"></a>Sviluppare e testare l'app

Per usare Always Encrypted e i calcoli dell'enclave, l'applicazione deve connettersi al database con le due parole chiave seguenti nella stringa di connessione: `Column Encryption Setting = Enabled; Enclave Attestation Url=https://x.x.x.x/Attestation` (dove xxxx può essere un indirizzo IP, un dominio e così via).

Inoltre, l'applicazione deve essere conforme alle linee guida comuni che si applicano alle applicazioni che usano Always Encrypted, ad esempio, l'applicazione deve avere accesso alle chiavi master della colonna associate alle colonne del database, a cui si fa riferimento nella query dell'applicazione.

Per informazioni dettagliate sullo sviluppo di applicazioni .NET Framework con Always Encrypted, vedere gli articoli seguenti:

- [Sviluppare con Always Encrypted e il provider di dati .NET Framework](develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Always Encrypted: proteggere i dati sensibili nel database SQL e archiviare le chiavi di crittografia in Azure Key Vault](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

#### <a name="example-of-simple-application"></a>Esempio di applicazione semplice

Il codice riportato di seguito è un esempio semplice di un'app console C\# che esegue una query LIKE sulla tabella con lo schema seguente:

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [int] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

Si presuppone che CEK1 sia una chiave di crittografia di colonna abilitata per l'enclave.

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.SqlClient;
using System.Data;
namespace ConsoleApp1
{
   class Program
   {
      static void Main(string\[\] args)
   {

   string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = https://10.193.16.185/Attestation/attestationservice.svc/signingCertificates; Integrated Security = true";

using (SqlConnection connection = new SqlConnection(connectionString))
{
   connection.Open();
   
   SqlCommand cmd = connection.CreateCommand();
   cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";
   
   SqlParameter paramSSNPattern = cmd.CreateParameter();
   
   paramSSNPattern.ParameterName = @"@SSNPattern";
   paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
   paramSSNPattern.Direction = ParameterDirection.Input;
   paramSSNPattern.Value = "%1111";
   paramSSNPattern.Size = 11;
   
   cmd.Parameters.Add(paramSSNPattern);
   
   SqlParameter MinSalary = cmd.CreateParameter();
   
   MinSalary.ParameterName = @"@MinSalary";
   MinSalary.DbType = DbType.Int32;
   MinSalary.Direction = ParameterDirection.Input;
   MinSalary.Value = 900;
   
   cmd.Parameters.Add(MinSalary);
   cmd.ExecuteNonQuery();
   
   SqlDataReader reader = cmd.ExecuteReader();
   while (reader.Read())
   
   {
     Console.WriteLine(reader);
     Console.WriteLine(reader\[0\] + ", " + reader\[1\] + ", " + reader\[2\] + ", " + reader\[3\]);
   }

   Console.ReadKey();

   }
  }
 }
}
```
