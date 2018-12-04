---
title: Uso di Always Encrypted con il driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4659c6571f8afbcdb757141e03df51ac54d0835e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510725"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Uso di Always Encrypted con il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questa pagina fornisce informazioni su come sviluppare applicazioni Java usando [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e Microsoft JDBC Driver 6.0 (o versione successiva) per SQL Server.

Always Encrypted consente ai client di eseguire la crittografia dei dati sensibili senza mai rivelare i dati o le chiavi di crittografia a SQL Server o al database SQL di Azure. Di tutto ciò si occupa un driver abilitato per Always Encrypted, come Microsoft JDBC Driver 6.0 (o versione successiva) per SQL Server, che esegue in modo trasparente la crittografia e la decrittografia dei dati sensibili nell'applicazione client. Il driver determina automaticamente la query che corrispondono alle colonne di database Always Encrypted, parametri e crittografa i valori di tali parametri prima che ne esegue l'invio a SQL Server o Database SQL di Azure. Analogamente, il driver esegue in modo trasparente la decrittografia dei dati, recuperati dalle colonne di database crittografate nei risultati delle query. Per altre informazioni, vedere [Always Encrypted (motore di Database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [Always Encrypted riferimento all'API per il Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

## <a name="prerequisites"></a>Prerequisites
- Assicurarsi che Microsoft JDBC Driver 6.0 (o versione successiva) per SQL Server sia installato nel computer di sviluppo. 
- Scaricare e installare Java Cryptography Extension (JCE) Unlimited Strenght Jurisdiction Policy Files.  Leggere il file leggimi incluso nel file ZIP per istruzioni sull'installazione e dettagli rilevanti sui possibili problemi di importazione/esportazione.  

    - Se si usa mssql-jdbc-X.X.X.jre7.jar o sqljdbc41.jar, i file dei criteri possono essere scaricati da [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 7 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - Se si usa mssql-jdbc-X.X.X.jre8.jar o sqljdbc42.jar, i file dei criteri possono essere scaricati da [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - Se si usa il mssql-jdbc-X.X.X.jre9.jar, non è necessario scaricare alcun file di criteri. I criteri di una giurisdizione in Java 9 viene impostato su un numero illimitato di livello di crittografia.

## <a name="working-with-column-master-key-stores"></a>Uso degli archivi delle chiavi master delle colonne
Per crittografare o decrittografare i dati per le colonne crittografate, SQL Server gestisce le chiavi di crittografia di colonna. Le chiavi di crittografia di colonna vengono archiviate in forma crittografata nei metadati del database. Ogni chiave di crittografia di colonna ha una chiave master corrispondente che viene usata per crittografare la chiave di crittografia della colonna. I metadati del database non contengano chiavi master della colonna. Tali chiavi vengono gestite solo dal client. Tuttavia i metadati del database contengono informazioni sulla posizione di archiviazione chiavi master della colonna rispetto al client. Ad esempio, i metadati del database potrebbero indicare che l'archivio chiavi contenente una chiave master della colonna è la Store di certificati di Windows e il certificato specifico utilizzato per crittografare e decrittografare si trova in un percorso specifico all'interno di Store di certificati di Windows. Se il client può accedere a tale certificato in Store il certificato di Windows, è possibile ottenere il certificato. Il certificato è quindi utilizzabile per decrittografare la chiave di crittografia di colonna. Tale chiave di crittografia può essere utilizzata per decrittografare o crittografare i dati per le colonne crittografate che usano tale chiave di crittografia di colonna.

Microsoft JDBC Driver per SQL Server comunica con un archivio chiavi usando un provider di archivio chiavi master di colonna, è un'istanza di una classe derivato da **SQLServerColumnEncryptionKeyStoreProvider**.

### <a name="using-built-in-column-master-key-store-providers"></a>Uso dei provider predefiniti di archivio delle chiavi master delle colonne
Microsoft JDBC Driver per SQL Server include i seguenti provider di archivio chiave master della colonna predefiniti. Alcuni di questi provider sono pre-registrati con i nomi di provider specifici (usati per cercare il provider) e alcune richiedono credenziali aggiuntive o registrazione esplicita.

| Classe                                                 | Descrizione                                        | Nome del provider (ricerca)  | È già registrato? |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- |
| **SQLServerColumnEncryptionAzureKeyVaultProvider**    | Un provider per un archivio chiavi per Azure Key Vault. | AZURE_KEY_VAULT         | no                 |
| **SQLServerColumnEncryptionCertificateStoreProvider** | Un provider per l'archivio certificati Windows.      | MSSQL_CERTIFICATE_STORE | Sì                |
| **SQLServerColumnEncryptionJavaKeyStoreProvider**     | Un provider dell'archivio chiavi Java                   | MSSQL_JAVA_KEYSTORE     | Sì                |

Per i provider dell'archivio chiavi pre-registrato, non è necessario apportare modifiche al codice dell'applicazione per utilizzare questi provider, ma tenere presente quanto segue:

- È necessario che l'utente (o l'amministratore del database) verifichi che il nome del provider, configurato nei metadati della chiave master della colonna, sia corretto e che il percorso della chiave master sia conforme al formato del percorso della chiave valido per un determinato provider. È consigliabile configurare le chiavi usando strumenti come SQL Server Management Studio, che genera automaticamente i nomi di provider e i percorsi di chiave validi quando viene eseguita l'istruzione CREATE COLUMN MASTER KEY (Transact-SQL).
- Verificare che l'applicazione possa accedere alla chiave nell'archivio chiavi. Questa attività potrebbe comportare l'accesso da parte dell'applicazione alla chiave e/o all'archivio chiavi, a seconda dell'archivio, o l'esecuzione di altri passaggi di configurazione specifici dell'archivio chiavi. Ad esempio, per l'uso di SQLServerColumnEncryptionJavaKeyStoreProvider, è necessario specificare la posizione e la password dell'archivio chiavi nelle proprietà di connessione. 

Tutti questi provider dell'archivio chiavi sono descritte più dettagliatamente nelle sezioni che seguono. È sufficiente implementare un provider dell'archivio chiavi per l'uso di Always Encrypted.

### <a name="using-azure-key-vault-provider"></a>Uso del provider dell'insieme di credenziali delle chiavi di Azure
Azure Key Vault rappresenta una scelta valida per archiviare e gestire le chiavi master delle colonne per Always Encrypted, soprattutto se l'applicazione è ospitata in Azure. Microsoft JDBC Driver per SQL Server include un provider predefinito, SQLServerColumnEncryptionAzureKeyVaultProvider, per le applicazioni che dispongono di chiavi archiviate in Azure Key Vault. Il nome di questo provider è AZURE_KEY_VAULT. Per usare il provider di archivio di Azure Key Vault, uno sviluppatore di applicazioni deve creare l'insieme di credenziali e le chiavi in Azure Key Vault e creare una registrazione dell'App in Azure Active Directory. L'applicazione registrata deve essere concesso ottenere, Decrypt, Encrypt, Unwrap Key, Wrap Key e verificare le autorizzazioni nei criteri di accesso definiti per l'insieme di credenziali delle chiavi creato per l'uso con crittografia sempre attiva. Per altre informazioni su come configurare l'insieme di credenziali delle chiavi e creare una chiave master della colonna, vedere [Azure Key Vault - passo a passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) e [creazione di chiavi Master della colonna in Azure Key Vault](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault).

Per gli esempi in questa pagina, se è stato creato un insieme di credenziali delle chiavi di Azure basato su chiave master della colonna e la chiave di crittografia di colonna usando SQL Server Management Studio, lo script T-SQL per ricrearle potrebbe essere simile a questo esempio con il proprio specifico **KEY_ PERCORSO** e **ENCRYPTED_VALUE**:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
)
```

Per usare Azure Key Vault, le applicazioni client devono creare un'istanza di SQLServerColumnEncryptionAzureKeyVaultProvider e registrarlo con il driver.

Di seguito è riportato un esempio di inizializzazione SQLServerColumnEncryptionAzureKeyVaultProvider:  

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID** è l'ID applicazione di registrazione di un'App in un'istanza di Azure Active Directory. **clientKey** è una Password della chiave registrata in tale applicazione, che fornisce l'accesso all'API di Azure Key Vault.

Dopo l'applicazione crea un'istanza di SQLServerColumnEncryptionAzureKeyVaultProvider, l'applicazione deve registrare l'istanza con il driver tramite il metodo registercolumnencryptionkeystoreproviders (). È consigliabile che l'istanza viene registrato usando il nome di ricerca predefinito, AZURE_KEY_VAULT, che può essere ottenuto chiamando l'API SQLServerColumnEncryptionAzureKeyVaultProvider.getName(). Il nome predefinito modo sarà possibile usare strumenti come SQL Server Management Studio o PowerShell per effettuare il provisioning e gestire le chiavi di Always Encrypted (strumenti di utilizzano il nome predefinito per generare l'oggetto di metadati di chiave master della colonna). L'esempio seguente illustra la registrazione del provider di Azure Key Vault. Per altre informazioni sul metodo registercolumnencryptionkeystoreproviders (), vedere [Always Encrypted riferimento all'API per il Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Se si usa il provider dell'archivio chiavi di Azure Key Vault, l'implementazione di Azure Key Vault del driver JDBC ha dipendenze su queste librerie (da GitHub) che devono essere incluse con l'applicazione:
>
>  [Azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [librerie di Azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Per un esempio di come includere queste dipendenze in un progetto Maven, vedere [scaricare ADAL4J AKV dipendenze e con Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Uso del provider per l'archivio certificati Windows
SqlColumnEncryptionCertificateStoreProvider consente di archiviare le chiavi master della colonna nell'archivio certificati Windows. Usare la procedura guidata Always Encrypted di SQL Server Management Studio (SSMS) o altri strumenti supportati per creare la chiave master della colonna e la crittografia di colonna definizioni chiave nel database. La stessa procedura guidata può essere utilizzata per generare un certificato autofirmato in Store il certificato di Windows che può essere utilizzato come chiave master della colonna per i dati sempre crittografati. Per altre informazioni sulla chiave master della colonna e sintassi T-SQL della colonna crittografia chiave, vedere [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) e [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) rispettivamente.

Il nome del SQLServerColumnEncryptionCertificateStoreProvider è MSSQL_CERTIFICATE_STORE e può eseguire query di getName() API dell'oggetto del provider. Viene automaticamente registrato dal driver ed è possibile usare facilmente senza apportare modifiche dell'applicazione.

Per gli esempi in questa pagina, se è stato creato un Store certificato Windows basato su chiave master della colonna e la chiave di crittografia di colonna usando SQL Server Management Studio, lo script T-SQL per ricrearle potrebbe essere simile a questo esempio con il proprio specifico **KEY_PATH** e **ENCRYPTED_VALUE**:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
)
```

> [!IMPORTANT]
> Mentre altri provider di archivio chiavi in questo articolo sono disponibili in tutte le piattaforme supportate dal driver, l'implementazione SQLServerColumnEncryptionCertificateStoreProvider del driver JDBC è disponibile Windows solo nei sistemi operativi. E presenta una dipendenza su sqljdbc_auth disponibile nel pacchetto di driver. Per usare questo provider, copiare il file sqljdbc_auth.dll in una directory nel percorso di sistema Windows nel computer in cui è installato il driver JDBC. In alternativa è possibile impostare la proprietà di sistema java.library.path in modo da specificare la directory di sqljdbc_auth.dll. Se si esegue Java Virtual Machine (JVM) a 32 bit, utilizzare il file sqljdbc_auth.dll nella cartella x86, anche se la versione del sistema operativo è x64. Se si esegue JVM a 64 bit in un processore x64, utilizzare il file sqljdbc_auth.dll nella cartella x64. Ad esempio, se si usa il driver JVM a 32 bit e il driver JDBC è installato nella directory predefinita, specificare il percorso della DLL tramite l'argomento seguente della VM (Virtual Machine) quando l'applicazione Java viene avviata: `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Usando Java Key Store provider
Il driver JDBC è disponibile in un’implementazione predefinita del provider dell’archivio chiavi per l’archivio chiavi Java. Se il **keyStoreAuthentication** proprietà della stringa di connessione è presente nella stringa di connessione e impostarlo su "JavaKeyStorePassword", il driver automaticamente crea un'istanza e registra il provider per Java Key Store. Il nome del provider di Java Key Store è MSSQL_JAVA_KEYSTORE. Questo nome è anche possibile eseguire query usando l'API SQLServerColumnEncryptionJavaKeyStoreProvider.getName(). 

Esistono tre proprietà di stringa di connessione che consentono a un'applicazione client specificare le credenziali che il driver deve eseguire l'autenticazione a Store la chiave di Java. Il driver Inizializza il provider in base ai valori di queste tre proprietà nella stringa di connessione.

**keyStoreAuthentication:** identifica la Store chiave Java da usare. Con Microsoft JDBC Driver 6.0 e versioni successive per SQL Server, è possibile eseguire l'autenticazione di Store chiave Java solo tramite questa proprietà. Per Store la chiave di Java, il valore di questa proprietà deve essere `JavaKeyStorePassword`.

**keyStoreLocation:** il percorso del file Java Key Store che archivia la chiave master della colonna. Il percorso include il nome del file dell'archivio chiavi.

**keyStoreSecret:** il segreto e la password da utilizzare per l'archivio chiavi nonché per la chiave. Per l'uso di Store chiave Java, l'archivio chiavi e la password della chiave deve essere lo stesso.

Di seguito è riportato un esempio di fornire queste credenziali nella stringa di connessione:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

È anche possibile ottenere o configurare queste impostazioni utilizzando l'oggetto SQLServerDataSource. Per altre informazioni, vedere [Always Encrypted riferimento all'API per il Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

Il driver JDBC crea automaticamente il SQLServerColumnEncryptionJavaKeyStoreProvider quando queste credenziali sono presenti nelle proprietà di connessione.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Creazione di una chiave master della colonna per la Store chiave Java
Il SQLServerColumnEncryptionJavaKeyStoreProvider è utilizzabile con i tipi di archivio chiavi JKS o PKCS12. Creare o importare una chiave da usare con questo provider Usa Java [dello strumento keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) utilità. La chiave deve avere la stessa password dell'archivio chiavi stesso. Di seguito è riportato un esempio di come creare una chiave pubblica e la relativa chiave privata associata tramite l'utilità keytool:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

Questo comando crea una chiave pubblica e ne esegue il wrapping in un X.509 autofirmato certificati, che viene archiviato nell'archivio chiavi 'keystore.jks' insieme alla relativa chiave privata associata. Questa voce nell'archivio chiavi è identificata dall'alias 'AlwaysEncryptedKey'.

Di seguito è riportato un esempio di un tipo di archivio PKCS12 utilizzando stesso:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

Se l'archivio chiavi è di tipo PKCS12, l'utilità keytool non visualizza una richiesta per una password della chiave e la password della chiave deve essere specificato con l'opzione - keypass come il SQLServerColumnEncryptionJavaKeyStoreProvider richiede che l'archivio chiavi e la chiave presentano lo stesso password.

È anche possibile esportare un certificato dall'archivio certificati di Windows nel formato PFX e usarlo con il SQLServerColumnEncryptionJavaKeyStoreProvider. Anche possibile importare il certificato esportato per la Store chiave Java come tipo di archivio chiavi JKS.

Dopo aver creato la voce dello strumento keytool, creare i metadati della chiave master della colonna nel database, che richiede il nome del provider dell'archivio chiavi e il percorso della chiave. Per altre informazioni su come creare i metadati chiave master della colonna, vedere [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md). Per SQLServerColumnEncryptionJavaKeyStoreProvider, il percorso della chiave è semplicemente l'alias della chiave e il nome del SQLServerColumnEncryptionJavaKeyStoreProvider è 'MSSQL_JAVA_KEYSTORE'. È anche possibile eseguire una query il nome mediante l'API pubblica getName() della classe SQLServerColumnEncryptionJavaKeyStoreProvider. 

La sintassi T-SQL per creare la chiave master della colonna è:

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

Per il 'AlwaysEncryptedKey' creato in precedenza, la definizione della chiave master della colonna sarà:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> La gestione di SQL Server predefinita funzionalità Studio non è possibile creare definizioni di chiave master della colonna per la Store chiave Java. I comandi T-SQL devono essere utilizzati a livello di codice.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Creazione di una chiave di crittografia di colonna per la Store chiave Java
SQL Server Management Studio o qualsiasi altro strumento non può essere utilizzato per creare colonna delle chiavi di crittografia con chiavi master della colonna in Store la chiave di Java. L'applicazione client deve creare la chiave di crittografia a livello di codice usando la classe SQLServerColumnEncryptionJavaKeyStoreProvider. Per altre informazioni, vedere [tramite provider di archivio chiavi master di colonna per il provisioning di chiavi a livello di codice](#using-column-master-key-store-providers-for-programmatic-key-provisioning).

### <a name="implementing-a-custom-column-master-key-store-provider"></a>Implementazione di un provider personalizzato di archivio delle chiavi master delle colonne
Se si vogliono archiviare le chiavi master delle colonne in un archivio chiavi che non è supportato da un provider esistente, è possibile implementare un provider personalizzato estendendo la classe SQLServerColumnEncryptionKeyStoreProvider e registrando il provider con il metodo SQLServerConnection.registerColumnEncryptionKeyStoreProviders().

```java
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)
    {
        // Logic for encrypting the column encryption key
    }

    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)
    {
        // Logic for decrypting the column encryption key
    }
}
```

Registrazione del provider:

```java
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>Uso di provider di archivio delle chiavi master delle colonne per il provisioning di chiavi a livello di codice
Quando si accede a colonne crittografate, Microsoft JDBC Driver per SQL Server trova in modo trasparente e chiama il provider corretto di archivio chiavi master delle colonne per decrittografare le chiavi di crittografia delle colonne. In genere, il codice dell'applicazione normale non chiama direttamente i provider di archivio delle chiavi master delle colonne. Si potrebbe, tuttavia, creare un'istanza e chiamare un provider a livello di codice per il provisioning e gestire le chiavi di Always Encrypted. Questo passaggio può essere eseguito per generare una chiave di crittografia di colonna crittografata e decrittografare una chiave di crittografia di colonna come parte rotazione della chiave master della colonna, ad esempio. Per altre informazioni, vedere [Panoramica della gestione delle chiavi per Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

Se si usa un provider dell'archivio chiavi personalizzato, potrebbe essere necessario implementare gli strumenti di gestione delle chiavi. Quando si usano chiavi archiviate in Windows Store di certificato o in Azure Key Vault, è possibile utilizzare gli strumenti esistenti, ad esempio SQL Server Management Studio o PowerShell, per gestire ed eseguire il provisioning delle chiavi. Quando si usano chiavi archiviate in Store la chiave di Java, è necessario effettuare il provisioning di chiavi a livello di codice. Nell'esempio seguente viene illustrato l'utilizzo della classe SQLServerColumnEncryptionJavaKeyStoreProvider per crittografare la chiave con una chiave archiviata in Store la chiave di Java.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted {
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<provide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of the column encryption key. The algorithm for the system providers must be
     * RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";

        try (Connection connection = DriverManager.getConnection(connectionUrl);
                Statement statement = connection.createStatement();) {

            // Instantiate the Java Key Store provider.
            SQLServerColumnEncryptionKeyStoreProvider storeProvider = new SQLServerColumnEncryptionJavaKeyStoreProvider(keyStoreLocation,
                    keyStoreSecret);

            byte[] encryptedCEK = getEncryptedCEK(storeProvider);

            /**
             * Create column encryption key For more details on the syntax, see:
             * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql Encrypted column encryption key first needs
             * to be converted into varbinary_literal from bytes, for which byteArrayToHex() is used.
             */
            String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                    + columnEncryptionKey
                    + " WITH VALUES ( "
                    + " COLUMN_MASTER_KEY = "
                    + columnMasterKeyName
                    + " , ALGORITHM =  '"
                    + algorithm
                    + "' , ENCRYPTED_VALUE =  0x"
                    + byteArrayToHex(encryptedCEK)
                    + " ) ";
            statement.executeUpdate(createCEKSQL);
            System.out.println("Column encryption key created with name : " + columnEncryptionKey);
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException {
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(keyAlias, algorithm, plainCEK);

        return encryptedCEK;
    }

    public static String byteArrayToHex(byte[] a) {
        StringBuilder sb = new StringBuilder(a.length * 2);
        for (byte b : a)
            sb.append(String.format("%02x", b).toUpperCase());
        return sb.toString();
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>Abilitazione di Always Encrypted per le query dell'applicazione
Il modo più semplice per abilitare la crittografia dei parametri e la decrittografia dei risultati delle query per le colonne crittografate consiste nell'impostare il valore della parola chiave della stringa di connessione **columnEncryptionSetting** su **Enabled**.

La stringa di connessione seguente è un esempio di abilitazione di Always Encrypted nel driver JDBC:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
```

Il codice seguente è un esempio equivalente che usa l'oggetto SQLServerDataSource:

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(<port>);
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

Always Encrypted può anche essere abilitato per le singole query. Per altre informazioni, vedere [controllare l'impatto sulle prestazioni di Always Encrypted](#controlling-the-performance-impact-of-always-encrypted). Perché la crittografia o la decrittografia abbiano esito positivo, non è sufficiente l'abilitazione di Always Encrypted. È necessario anche assicurarsi che:
- L'applicazione abbia le autorizzazioni di database *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessarie per accedere ai metadati sulle chiavi Always Encrypted nel database. Per informazioni dettagliate, vedere [ Autorizzazioni in Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
- L'applicazione può accedere alla chiave master della colonna che protegge le chiavi di crittografia di colonna, le quali crittografano le colonne di database sottoposte a query. Per usare il provider di Java Key Store, è necessario fornire altre credenziali nella stringa di connessione. Per altre informazioni, vedere [provider Using Java Key Store](#using-java-key-store-provider).

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurazione della modalità di invio dei valori java.sql.Time al server
La proprietà di connessione **sendTimeAsDatetime** viene usata per configurare la modalità di invio del valore java.sql.Time al server. Se impostato su false, il valore di ora viene inviato come un tipo time di SQL Server. Se impostato su true, l'ora di invio valore come tipo datetime. Se una colonna time è crittografata, il **sendTimeAsDatetime** proprietà deve essere impostato su false, come le colonne crittografate non supportano la conversione dall'ora in datetime. Si noti inoltre che questa proprietà è per valore predefinito true, in modo che quando si usano colonne crittografate ora è possibile impostarlo su false. In caso contrario, il driver genera un'eccezione. A partire dalla versione 6.0 del driver, la classe SQLServerConnection offre due metodi per configurare il valore di questa proprietà a livello di codice:
 
* public void setSendTimeAsDatetime (sendTimeAsDateTimeValue booleano)
* public boolean getSendTimeAsDatetime()

Per altre informazioni su questa proprietà, vedere [Java configurazione come valori vengono inviati al Server](configuring-how-java-sql-time-values-are-sent-to-the-server.md).

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>La configurazione come valori stringa vengono inviati al server
Il **sendStringParametersAsUnicode** proprietà di connessione viene usata per configurare come valori stringa vengono inviati a SQL Server. Se è impostata su True, i parametri String vengono inviati al server in formato Unicode. Se impostato su false, i parametri String viene inviato in formato non Unicode, ad esempio MBCS, invece di Unicode o ASCII. Il valore predefinito di questa proprietà è True. Quando è abilitato per Always Encrypted e una colonna char/varchar/varchar(max) viene crittografata, il valore della **sendStringParametersAsUnicode** deve essere impostata su false. Se questa proprietà è impostata su true, il driver genera un'eccezione durante la decrittografia di dati da una colonna crittografata char/varchar/varchar(max) con caratteri Unicode. Per altre informazioni su questa proprietà, vedere [impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recupero e modifica dei dati nelle colonne crittografate
Dopo aver abilitato Always Encrypted per le query dell'applicazione, è possibile usare le API JDBC standard per recuperare o modificare i dati in colonne crittografate del database. Se l'applicazione disponga delle autorizzazioni di database necessari e può accedere alla chiave master di colonna, il driver crittograferà eventuali parametri di query destinati alle colonne crittografate e per decrittografare i dati recuperati dalle colonne crittografate.

Se Always Encrypted non è abilitato, le query con parametri destinati alle colonne crittografate avranno esito negativo. Le query possono comunque recuperare i dati dalle colonne crittografate, a condizione che non presentino parametri destinati alle colonne crittografate. Il driver non tenterà però di decrittografare i valori recuperati dalle colonne crittografate e l'applicazione riceverà dati crittografati binari, sotto forma di matrici di byte.

La tabella seguente riepiloga il comportamento delle query, a seconda che la funzionalità Always Encrypted sia abilitata o meno:

| Caratteristica della query                                                                           | Always Encrypted è abilitato e l'applicazione può accedere alle chiavi e ai metadati delle chiavi                                                                                                                        | Always Encrypted è abilitato e l'applicazione non può accedere alle chiavi o ai metadati delle chiavi | Always Encrypted è disabilitato                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| Query con parametri destinati alle colonne crittografate.                                           | I valori dei parametri vengono crittografati in modo trasparente.                                                                                                                                                           | Errore                                                                             | Errore                                                                                                               |
| Query che recuperano dati dalle colonne crittografate, senza parametri destinati alle colonne crittografate. | I risultati delle colonne vengono decrittografati in modo trasparente. L'applicazione riceve valori di testo non crittografato dei tipi di dati JDBC corrispondenti ai tipi di SQL Server configurati per le colonne crittografate. | Errore                                                                             | I risultati delle colonne crittografate non vengono decrittografati. L'applicazione riceve i valori crittografati come matrici di byte (byte[]). |

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Inserimento e recupero di esempi di dati crittografati

Gli esempi seguenti illustrano il recupero e la modifica dei dati nelle colonne crittografate. Gli esempi presuppongono che la tabella di destinazione con lo schema seguente e le colonne SSN e Birthdate nascita crittografate. Se è stata configurata una chiave Master della colonna denominata "MyCMK" e una chiave di crittografia di colonna denominata "MyCEK" (come descritto nelle sezioni precedenti provider dell'archivio chiavi), è possibile creare la tabella con questo script:

```sql
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

Per ogni esempio di codice Java, è necessario inserire il codice specifico dell'archivio chiavi nel percorso indicato.

Se si usa un provider dell'archivio chiavi di Azure Key Vault:

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Se si usa un provider dell'archivio chiavi di Windows Store di certificato:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Se si usa un provider dell'archivio chiavi Java Key Store:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>Esempio di inserimento dei dati

Questo esempio illustra come inserire una riga nella tabella Patients. Si noti quanto segue:

- Il codice di esempio non contiene alcun elemento specifico per la crittografia. Microsoft JDBC Driver per SQL Server rileva automaticamente e crittografa i parametri destinati alle colonne crittografate. In questo modo la crittografia diventa trasparente per l'applicazione.
- I valori inseriti nelle colonne del database, incluse le colonne crittografate, vengono passati come parametri tramite SQLServerPreparedStatement. Quando si inviano valori a colonne non crittografate, l'uso dei parametri è facoltativo, nonostante sia consigliabile per prevenire attacchi SQL injection. È invece necessario usare i parametri in presenza di valori destinati a colonne crittografate. Se i valori inseriti nelle colonne crittografate sono stati passati come valori letterali incorporati nell'istruzione della query, la query avrà esito negativo perché il driver non sarebbe in grado di determinare i valori nelle colonne di destinazione crittografate e non sarebbe crittografare i valori. Di conseguenza, il server li rifiuterà come incompatibili con le colonne crittografate.
- Tutti i valori stampati dal programma saranno in testo non crittografato perché Microsoft JDBC Driver per SQL Server possa decrittografare in modo trasparente i dati recuperati dalle colonne crittografate.
- Se si sta eseguendo una ricerca usando una clausola WHERE, il valore usato nella clausola WHERE deve essere passata come parametro in modo che il driver possibile codificarli in modo trasparente prima dell'invio al database. Nell'esempio seguente, il codice fiscale viene passato come parametro, ma il cognome viene passato come valore letterale, come LastName non vengono crittografate.
- Il metodo set utilizzato per il parametro destinato alla colonna SSN è SetString (), che esegue il mapping per il tipo di dati di SQL Server char/varchar. Se per questo parametro il metodo setter usato era setNString(), che esegue il mapping a nchar/nvarchar, la query avrà esito negativo perché Always Encrypted non supporta le conversioni da valori nchar/nvarchar crittografati a valori char/varchar crittografati.

```java
// <Insert keystore-specific code here>
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement insertStatement = sourceConnection.prepareStatement("INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)")) {
    insertStatement.setString(1, "795-73-9838");
    insertStatement.setString(2, "Catherine");
    insertStatement.setString(3, "Abel");
    insertStatement.setDate(4, Date.valueOf("1996-09-10"));
    insertStatement.executeUpdate();
    System.out.println("1 record inserted.\n");
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>Esempio di recupero di dati di testo non crittografato

L'esempio seguente illustra come filtrare i dati in base ai valori crittografati e recuperare i dati in testo non crittografato da colonne crittografate. Si noti quanto segue:

- Il valore usato nella clausola WHERE per filtrare la colonna SSN deve essere passato come parametro, in modo che Microsoft JDBC Driver per SQL Server possa codificarlo in modo trasparente prima dell'invio al database.
- Tutti i valori stampati dal programma saranno in testo non crittografato perché Microsoft JDBC Driver per SQL Server possa decrittografare in modo trasparente i dati recuperati dalle colonne SSN e BirthDate.

> [!NOTE]
> Se le colonne sono crittografate tramite crittografia deterministica, le query possono eseguire confronti di uguaglianza nelle colonne. Per altre informazioni, vedere [Selezione della crittografia deterministica o casuale in Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```java
// <Insert keystore-specific code here>
try (Connection connection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection
                .prepareStatement("\"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;\"");) {
    selectStatement.setString(1, "795-73-9838");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-encrypted-data-example"></a>Esempio di recupero di dati crittografati

Se Always Encrypted non è abilitato, una query può comunque recuperare dati dalle colonne crittografate, a condizione che non presenti parametri destinati alle colonne crittografate.

L'esempio seguente illustra come recuperare dati crittografati binari da colonne crittografate. Si noti quanto segue:

- Considerato che Always Encrypted non è abilitato nella stringa di connessione, la query restituirà i valori crittografati di SSN e BirthDate come matrici di byte. Il programma converte i valori in stringhe.
- Una query che recupera dati dalle colonne crittografate con Always Encrypted disabilitato può avere parametri, a condizione che nessuno dei parametri sia destinato a una colonna crittografata. La query seguente filtra in base alla colonna LastName, che non è crittografata nel database. Se la query avesse filtrato per SSN o data di nascita, avrebbe avuto esito negativo.

```java
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = sourceConnection
                .prepareStatement("SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;");) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Come evitare i problemi comuni quando si eseguono query su colonne crittografate

Questa sezione descrive categorie di errori comuni che si verificano quando si eseguono query su colonne crittografate da applicazioni Java e contiene alcune linee guida su come correggere tali errori.

### <a name="unsupported-data-type-conversion-errors"></a>Errori di conversione dei tipi di dati non supportati

Always Encrypted supporta alcune conversioni per i tipi di dati crittografati. Per l'elenco dettagliato delle conversioni dei tipi supportati, vedere [Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Per evitare errori di conversione dei tipi di dati, procedere in questo modo. Assicurarsi che:

- Utilizzare i metodi di impostazione appropriato quando il passaggio di valori per parametri destinati alle colonne crittografate. Assicurarsi che il tipo di dati di SQL Server del parametro è esattamente uguale al tipo della colonna di destinazione o una conversione del tipo di dati SQL Server del parametro nel tipo di destinazione della colonna è supportata. Sono stati aggiunti i metodi API per le classi SQLServerPreparedStatement e SQLServerCallableStatement SQLServerResultSet per passare i parametri corrispondenti a specifici tipi di dati di SQL Server. Ad esempio, se una colonna non viene crittografata è possibile usare il metodo setTimestamp() per passare un parametro a un datetime2 o a una colonna datetime. Ma quando una colonna è crittografata è possibile usare il metodo esatto che rappresenta il tipo della colonna nel database. Ad esempio, usare setTimestamp() per passare valori a una colonna crittografata datetime2 e utilizzare setDateTime() per passare valori a una colonna di data e ora crittografati. Visualizzare [Always Encrypted riferimento all'API per il Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) per un elenco completo delle nuove API.
- La precisione e la scala dei parametri destinati alle colonne dei tipi di dati di SQL Server decimali e numerici sono uguali a quelle configurate per la colonna di destinazione. Sono stati aggiunti i metodi API per le classi SQLServerPreparedStatement e SQLServerCallableStatement SQLServerResultSet per accettare la precisione e scala insieme ai valori dei dati per i parametri o colonne che rappresentano i tipi di dati decimali e numerici. Visualizzare [Always Encrypted riferimento all'API per il Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) per un elenco completo delle API nuove o sottoposti a overload.  
- la precisione/scala di frazioni di parametri destinati alle colonne dei tipi di dati di SQL Server ora, datetime2 o datetimeoffset non è maggiore della precisione/scala di frazioni di secondo per la colonna di destinazione nelle query che modificano i valori della colonna di destinazione . Sono stati aggiunti i metodi API per le classi SQLServerPreparedStatement e SQLServerCallableStatement SQLServerResultSet per accettare i secondi frazionari precisione/scala insieme ai valori dei dati per i parametri che rappresentano i tipi di dati. Per un elenco completo delle API nuove o sottoposti a overload, vedere [Always Encrypted riferimento all'API per il Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

### <a name="errors-due-to-incorrect-connection-properties"></a>Errori a causa di proprietà di connessione non corrette

Questa sezione descrive come configurare le impostazioni di connessione in modo corretto per utilizzare dati Always Encrypted. Poiché i tipi di dati crittografati supportano le conversioni limitate, il **sendTimeAsDatetime** e **sendStringParametersAsUnicode** le impostazioni della connessione richiedano una configurazione appropriata quando si usano colonne crittografate. Assicurarsi che:

- [sendTimeAsDatetime](setting-the-connection-properties.md) impostazione di connessione è impostata su false quando si inseriscono dati in crittografato di colonne dell'ora. Per altre informazioni, vedere [come valori di Java vengono inviati al server di configurazione](configuring-how-java-sql-time-values-are-sent-to-the-server.md).
- [sendStringParametersAsUnicode](setting-the-connection-properties.md) connessione è impostato su true (o viene lasciato come impostazione predefinita) quando si inseriscono dati in crittografati char/varchar/varchar(max) colonne.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Errori causati dal passaggio di testo non crittografato anziché di valori crittografati

Qualsiasi valore destinato a una colonna crittografata deve essere crittografato all'interno dell'applicazione. Il tentativo di inserire, modificare o filtrare in base a un valore di testo non crittografato in una colonna crittografata genererà un errore simile al seguente:

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Per evitare tali errori, verificare che:

- Always Encrypted sia abilitato per le query dell'applicazione destinate alle colonne crittografate (per la stringa di connessione o per una query specifica).
- usare le istruzioni preparate e i parametri per inviare dati destinati alle colonne crittografate. L'esempio seguente illustra una query che filtra in modo errato in base a un valore letterale o costante in una colonna crittografata (SSN), anziché passare il valore letterale all'interno sotto forma di parametro. La query avrà esito negativo:

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>Forza crittografia su parametri di input

La funzionalità forza crittografia applica la crittografia di un parametro quando si usa Always Encrypted. Se si usa la crittografia forzata e SQL Server indica al driver che il parametro non deve essere crittografato, la query che usa il parametro avrà esito negativo. Questa proprietà fornisce protezione aggiuntiva contro attacchi alla sicurezza in cui un SQL Server compromesso fornisce al client metadati di crittografia non corretti, con conseguente rischio di divulgazione dei dati. I metodi set * nell'aggiornamento e le classi SQLServerPreparedStatement e SQLServerCallableStatement\* metodi della classe SQLServerResultSet sono sottoposti a overload per accettare un argomento booleano per specificare l'impostazione di crittografia force. Se il valore di questo argomento è false, il driver non forza la crittografia sui parametri. Se Forza crittografia è impostata su true, la query parametro verrà inviato solo se la colonna di destinazione è crittografata e Always Encrypted è abilitato per la connessione o per l'istruzione. Utilizzo di questa proprietà fornisce un ulteriore livello di sicurezza, garantendo che il driver non erroneamente invia dati a SQL Server come testo non crittografato quando che deve essere crittografato.

Per altre informazioni sui metodi di SQLServerPreparedStatement e SQLServerCallableStatement che sono sottoposti a overload con l'impostazione di crittografia forzata, vedere [Always Encrypted riferimento all'API per il Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controllo dell'impatto di Always Encrypted sulle prestazioni

Considerato che Always Encrypted è una tecnologia di crittografia lato client, la maggior parte del sovraccarico delle prestazioni si verifica sul lato client, non nel database. A parte il costo delle operazioni di crittografia e decrittografia, le altre origini di sovraccarico delle prestazioni sul lato client sono le seguenti:

- Round trip aggiuntivi al database per recuperare i metadati per i parametri di query.
- Chiamate a un archivio delle chiavi master delle colonne per accedere alla chiave master di una colonna.

Questa sezione descrive le ottimizzazioni delle prestazioni predefinite in Microsoft JDBC Driver per SQL Server e come controllare l'impatto sulle prestazioni esercitato dai due fattori descritti.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controllo dei round trip per recuperare i metadati per i parametri di query

Se la funzionalità Always Encrypted è abilitata per una connessione, per impostazione predefinita il driver chiamerà [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) per ogni query con parametri, passando l'istruzione di query (senza i valori dei parametri) a SQL Server. [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) analizza l'istruzione di query per verificare se sono presenti parametri da crittografare e, in tal caso, restituisce le informazioni relative alla crittografia che consentiranno al driver di crittografare i valori dei parametri. Il comportamento descritto garantisce all'applicazione client un elevato livello di trasparenza. Fino a quando l'applicazione usa i parametri per passare i valori destinati alle colonne crittografate del driver, l'applicazione (e lo sviluppatore dell'applicazione) non è necessario sapere quali query accedono alle colonne crittografate.

### <a name="setting-always-encrypted-at-the-query-level"></a>Impostazione di Always Encrypted a livello di query

Per controllare l'impatto sulle prestazioni del recupero dei metadati di crittografia per le query con parametri, è possibile abilitare Always Encrypted per singole query, anziché l'impostare la funzionalità per la connessione. In questo modo, è possibile assicurarsi che sys.sp_describe_parameter_encryption venga richiamato solo per le query con parametri destinati a colonne crittografate. Si noti, tuttavia, che in tal modo si riduce la trasparenza della crittografia. Se si modificano le proprietà di crittografia delle colonne di database, potrebbe essere necessario modificare il codice dell'applicazione per allinearlo alle modifiche dello schema.

Per controllare il comportamento di Always Encrypted delle singole query, è necessario configurare gli oggetti di singola istruzione passando un'enumerazione, SQLServerStatementColumnEncryptionSetting, che specifica come verranno inviati e ricevuti durante la lettura e scrittura di dati colonne crittografate per l'istruzione specifica. Di seguito sono riportate alcune linee guida utili:

- Se la maggior parte delle query che un'applicazione client invia alla connessione del database accede alle colonne crittografate, seguire queste linee guida:

    - Impostare la parola chiave della stringa di connessione **columnEncryptionSetting** su **Enabled**.
    - Impostare SQLServerStatementColumnEncryptionSetting.Disabled per le singole query che non accedono a colonne crittografate. In questo modo verranno disabilitati sia la chiamata di sys.sp_describe_parameter_encryption chiamante che il tentativo di decrittografare i valori nel set di risultati.
    - Impostare SQLServerStatementColumnEncryptionSetting.ResultSet per le singole query che non presentano parametri da crittografare, ma che recuperano i dati dalle colonne crittografate. In questo modo verranno disabilitate la chiamata di sys.sp_describe_parameter_encryption e la crittografia dei parametri. La query potrà decrittografare i risultati delle colonne di crittografia.

- Se la maggior parte delle query che un'applicazione client invia alla connessione del database non accede alle colonne crittografate, seguire queste linee guida:

    - Impostare la parola chiave della stringa di connessione **columnEncryptionSetting** su **Disabled**.
    - Impostare SQLServerStatementColumnEncryptionSetting.Enabled per le singole query che presentano parametri da crittografare. In questo modo verranno abilitate sia la chiamata di sys.sp_describe_parameter_encryption che la decrittografia dei risultati di query recuperati da colonne crittografate.
    - Impostare SQLServerStatementColumnEncryptionSetting.ResultSet per le query che non presentano parametri da crittografare, ma che recuperano i dati dalle colonne crittografate. In questo modo verranno disabilitate la chiamata di sys.sp_describe_parameter_encryption e la crittografia dei parametri. La query potrà decrittografare i risultati delle colonne di crittografia.

Le impostazioni SQLServerStatementColumnEncryptionSetting non possono essere usate per ignorare la crittografia e ottenere l'accesso ai dati di testo normale. Per altre informazioni su come configurare la crittografia di colonna in un'istruzione, vedere [Always Encrypted riferimento all'API per il Driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

Nell'esempio seguente la funzionalità Always Encrypted è disabilitata per la connessione di database. La query eseguita dall'applicazione ha un parametro la cui destinazione è la colonna LastName non crittografata. La query recupera i dati dalle colonne SSN e BirthDate, che sono entrambe crittografate. In tal caso, la chiamata di sys.sp_describe_parameter_encryption per recuperare i metadati di crittografia non è necessaria. È tuttavia necessario abilitare la decrittografia dei risultati della query in modo che l'applicazione possa ricevere i valori di testo non crittografato dalle due colonne crittografate. Consente di verificare che l'impostazione SQLServerStatementColumnEncryptionSetting.ResultSet.

```java
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>;" 
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=<keyStoreLocation>" 
        + "keyStoreSecret=<keyStoreSecret>;";

String filterRecord = "SELECT FirstName, LastName, SSN, BirthDate FROM " + tableName + " WHERE LastName = ?";

try (SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection.prepareStatement(filterRecord, ResultSet.TYPE_FORWARD_ONLY, ResultSet.CONCUR_READ_ONLY,
                connection.getHoldability(), SQLServerStatementColumnEncryptionSetting.ResultSetOnly);) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("First name: " + rs.getString("FirstName"));
        System.out.println("Last name: " + rs.getString("LastName"));
        System.out.println("SSN: " + rs.getString("SSN"));
        System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="column-encryption-key-caching"></a>Memorizzazione nella cache delle chiavi di crittografia della colonna

Per ridurre il numero di chiamate a un archivio chiavi master della colonna per decrittografare le chiavi di crittografia della colonna, Microsoft JDBC Driver per SQL Server memorizza nella cache le chiavi di crittografia della colonna di testo non crittografato. Dopo aver ricevuto il valore delle chiavi di crittografia della colonna crittografata dai metadati del database, il driver prova prima a trovare la chiave di crittografia della colonna di testo non crittografato corrispondente al valore della chiave crittografata. Il driver chiama l'archivio chiavi contenente la chiave master della colonna solo se non trova nella cache il valore della chiave di crittografia della colonna crittografata.

È possibile configurare un valore time-to-live per le voci di chiave di crittografia di colonna nella cache usando l'API, setColumnEncryptionKeyCacheTtl(), nella classe SQLServerConnection. Il valore predefinito di time-to-live per le voci chiave di crittografia di colonna nella cache è due ore. Per disabilitare la memorizzazione nella cache, usare un valore pari a 0. Per impostare qualsiasi valore di time-to-live, usare l'API seguente:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

Ad esempio, per impostare un valore time-to-live di 10 minuti, usare:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

Come unità di tempo sono supportati solo giorni, ore, minuti o secondi.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Copia dei dati crittografati usando SQLServerBulkCopy

Con SQLServerBulkCopy, è possibile copiare dati già crittografati e archiviati in una tabella in un'altra tabella, senza eseguire la decrittografia dei dati. Per eseguire questa operazione:

- Assicurarsi che la configurazione di crittografia della tabella di destinazione sia identica alla configurazione della tabella di origine. In particolare, le due le tabelle devono avere le stesse colonne crittografate e le colonne devono essere crittografate usando gli stessi tipi di crittografia e le stesse chiavi di crittografia. Se una delle colonne di destinazione è crittografata in modo diverso dalla relativa colonna di origine corrispondente, non sarà possibile decrittografare i dati nella tabella di destinazione dopo l'operazione di copia. I dati risulteranno danneggiati.
- Configurare le due connessioni di database alla tabella di origine e la tabella di destinazione, senza abilitare Always Encrypted.
- Impostare l'opzione allowEncryptedValueModifications. Per altre informazioni, vedere [usando la copia Bulk con il Driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

> [!NOTE]
> Prestare attenzione quando si specifica AllowEncryptedValueModifications. Questa opzione può danneggiare il database perché Microsoft JDBC Driver per SQL Server non verifica se i dati vengono effettivamente crittografati o se vengono crittografati correttamente usando lo stesso tipo di crittografia, l'algoritmo e la chiave della colonna di destinazione.

## <a name="see-also"></a>Vedere anche

[Always Encrypted (Motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
