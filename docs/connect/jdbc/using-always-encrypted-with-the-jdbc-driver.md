---
title: Utilizzo di Always Encrypted con il driver JDBC | Microsoft Docs
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
ms.openlocfilehash: f19878f73397b9146765fecd879dad07ebb73dc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916454"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Uso di Always Encrypted con il driver JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

In questa pagina vengono fornite informazioni su come sviluppare applicazioni Java utilizzando [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e Microsoft JDBC Driver 6,0 (o versione successiva) per SQL Server.

Always Encrypted consente ai client di eseguire la crittografia dei dati sensibili senza mai rivelare i dati o le chiavi di crittografia a SQL Server o al database SQL di Azure. Di tutto ciò si occupa un driver abilitato per Always Encrypted, come Microsoft JDBC Driver 6.0 (o versione successiva) per SQL Server, che esegue in modo trasparente la crittografia e la decrittografia dei dati sensibili nell'applicazione client. Il driver determina automaticamente i parametri di query corrispondenti alle colonne di database Always Encrypted e crittografa i valori di tali parametri prima di inviarli al SQL Server o al database SQL di Azure. Analogamente, il driver esegue in modo trasparente la decrittografia dei dati, recuperati dalle colonne di database crittografate nei risultati delle query. Per ulteriori informazioni, vedere [Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [Always Encrypted riferimento API per il driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

## <a name="prerequisites"></a>Prerequisites
- Assicurarsi che Microsoft JDBC Driver 6,0 (o versione successiva) per SQL Server sia installato nel computer di sviluppo. 
- Scaricare e installare Java Cryptography Extension (JCE) Unlimited Strenght Jurisdiction Policy Files.  Leggere il file leggimi incluso nel file ZIP per istruzioni sull'installazione e dettagli rilevanti sui possibili problemi di importazione/esportazione.  

    - Se si usa mssql-jdbc-X.X.X.jre7.jar o sqljdbc41.jar, i file dei criteri possono essere scaricati da [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 7 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - Se si usa mssql-jdbc-X.X.X.jre8.jar o sqljdbc42.jar, i file dei criteri possono essere scaricati da [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - Se si usa mssql-jdbc-X.X.X.jre9.jar, non è necessario scaricare alcun file di criteri. I criteri di giurisdizione in Java 9 sono predefiniti per la crittografia di forza illimitata.

## <a name="working-with-column-master-key-stores"></a>Uso degli archivi delle chiavi master delle colonne
Per crittografare o decrittografare i dati delle colonne crittografate, SQL Server gestisce le chiavi di crittografia della colonna. Le chiavi di crittografia di colonna vengono archiviate in forma crittografata nei metadati del database. Ogni chiave di crittografia di colonna ha una chiave master corrispondente che viene usata per crittografare la chiave di crittografia della colonna. I metadati del database non contengono le chiavi master della colonna. Tali chiavi vengono utilizzate solo dal client. Tuttavia, i metadati del database contengono informazioni sulla posizione in cui vengono archiviate le chiavi master della colonna relative al client. I metadati del database, ad esempio, possono indicare che l'archivio chiavi contenente una chiave master della colonna è l'archivio certificati di Windows e il certificato specifico usato per crittografare e decrittografare si trova in un percorso specifico all'interno dell'archivio certificati di Windows. Se il client ha accesso a tale certificato nell'archivio certificati di Windows, può ottenere il certificato. Il certificato può quindi essere usato per decrittografare la chiave di crittografia della colonna. La chiave di crittografia può quindi essere usata per decrittografare o crittografare i dati per le colonne crittografate che usano la chiave di crittografia della colonna.

Microsoft JDBC driver per SQL Server comunica con un archivio chiavi utilizzando un provider dell'archivio chiavi master della colonna, che è un'istanza di una classe derivata da **SQLServerColumnEncryptionKeyStoreProvider**.

### <a name="using-built-in-column-master-key-store-providers"></a>Uso dei provider predefiniti di archivio delle chiavi master delle colonne
Microsoft JDBC driver per SQL Server viene fornita con i seguenti provider predefiniti di archivio delle chiavi master della colonna. Alcuni di questi provider sono pre-registrati con i nomi di provider specifici (usati per cercare il provider) e alcuni richiedono credenziali aggiuntive o una registrazione esplicita.

| Classe                                                 | Descrizione                                        | Nome del provider (ricerca)  | È già registrato? |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- |
| **SQLServerColumnEncryptionAzureKeyVaultProvider**    | Provider per un archivio chiavi per la Azure Key Vault. | AZURE_KEY_VAULT         | no                 |
| **SQLServerColumnEncryptionCertificateStoreProvider** | Un provider per l'archivio certificati Windows.      | MSSQL_CERTIFICATE_STORE | Sì                |
| **SQLServerColumnEncryptionJavaKeyStoreProvider**     | Un provider per l'archivio chiavi Java                   | MSSQL_JAVA_KEYSTORE     | Sì                |

Per i provider dell'archivio chiavi preregistrati, non è necessario apportare modifiche al codice dell'applicazione per usare questi provider, ma tenere presenti gli elementi seguenti:

- È necessario che l'utente (o l'amministratore del database) verifichi che il nome del provider, configurato nei metadati della chiave master della colonna, sia corretto e che il percorso della chiave master sia conforme al formato del percorso della chiave valido per un determinato provider. È consigliabile configurare le chiavi usando strumenti come SQL Server Management Studio, che genera automaticamente i nomi di provider e i percorsi di chiave validi quando viene eseguita l'istruzione CREATE COLUMN MASTER KEY (Transact-SQL).
- Verificare che l'applicazione possa accedere alla chiave nell'archivio chiavi. Questa attività potrebbe comportare l'accesso da parte dell'applicazione alla chiave e/o all'archivio chiavi, a seconda dell'archivio, o l'esecuzione di altri passaggi di configurazione specifici dell'archivio chiavi. Ad esempio, per usare SQLServerColumnEncryptionJavaKeyStoreProvider, è necessario specificare il percorso e la password dell'archivio chiavi nelle proprietà di connessione. 

Tutti questi provider dell'archivio chiavi sono descritti in modo più dettagliato nelle sezioni seguenti. È sufficiente implementare un provider dell'archivio chiavi per usare Always Encrypted.

### <a name="using-azure-key-vault-provider"></a>Uso del provider dell'insieme di credenziali delle chiavi di Azure
Azure Key Vault rappresenta una scelta valida per archiviare e gestire le chiavi master delle colonne per Always Encrypted, soprattutto se l'applicazione è ospitata in Azure. Microsoft JDBC driver per SQL Server include un provider predefinito, SQLServerColumnEncryptionAzureKeyVaultProvider, per le applicazioni che dispongono di chiavi archiviate in Azure Key Vault. Il nome di questo provider è AZURE_KEY_VAULT. Per usare il provider di Azure Key Vault Store, uno sviluppatore di applicazioni deve creare l'insieme di credenziali e le chiavi in Azure Key Vault e creare una registrazione dell'app in Azure Active Directory. All'applicazione registrata devono essere concesse le autorizzazioni Get, Decrypt, encrypt, Unwrap Key, wrap Key e verify nei criteri di accesso definiti per l'insieme di credenziali delle chiavi creato per l'uso con Always Encrypted. Per altre informazioni su come configurare l'insieme di credenziali delle chiavi e creare una chiave master della colonna, vedere [Azure Key Vault: passaggio per passaggio](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) e [creazione di chiavi master della colonna in Azure Key Vault](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault).

Per gli esempi in questa pagina, se è stata creata una chiave master della colonna basata su Azure Key Vault e una chiave di crittografia della colonna usando SQL Server Management Studio, lo script T-SQL per ricrearli potrebbe essere simile a questo esempio con il proprio **KEY_PATH** specifico e **ENCRYPTED_VALUE**:

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

Per usare la Azure Key Vault, le applicazioni client devono creare un'istanza di SQLServerColumnEncryptionAzureKeyVaultProvider e registrarla nel driver.

Di seguito è riportato un esempio di inizializzazione di SQLServerColumnEncryptionAzureKeyVaultProvider:  

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**ClientID** è l'ID dell'applicazione per la registrazione di un'app in un'istanza di Azure Active Directory. **clientkey vuoto** è una password chiave registrata in tale applicazione, che fornisce l'accesso all'API all'Azure Key Vault.

Dopo che l'applicazione ha creato un'istanza di SQLServerColumnEncryptionAzureKeyVaultProvider, l'applicazione deve registrare l'istanza con il driver usando il metodo SQLServerConnection. registerColumnEncryptionKeyStoreProviders (). Si consiglia vivamente di registrare l'istanza usando il nome di ricerca predefinito, AZURE_KEY_VAULT, che può essere ottenuto chiamando l'API SQLServerColumnEncryptionAzureKeyVaultProvider. GetName (). L'uso del nome predefinito consente di usare strumenti come SQL Server Management Studio o PowerShell per il provisioning e la gestione delle chiavi di Always Encrypted (gli strumenti usano il nome predefinito per generare l'oggetto di metadati nella chiave master della colonna). Nell'esempio seguente viene illustrata la registrazione del provider Azure Key Vault. Per ulteriori informazioni sul metodo SQLServerConnection. registerColumnEncryptionKeyStoreProviders (), vedere [Always Encrypted riferimento API per il driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Se si usa il provider dell'archivio chiavi Azure Key Vault, l'implementazione Azure Key Vault del driver JDBC presenta dipendenze da queste librerie (da GitHub) che devono essere incluse nell'applicazione:
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java libraries](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Per un esempio di come includere queste dipendenze in un progetto Maven, vedere [scaricare le dipendenze ADAL4J e AKV con Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Uso del provider per l'archivio certificati Windows
SqlColumnEncryptionCertificateStoreProvider consente di archiviare le chiavi master della colonna nell'archivio certificati Windows. Utilizzare la procedura guidata Always Encrypted SQL Server Management Studio (SSMS) o altri strumenti supportati per creare le definizioni delle chiavi master della colonna e della chiave di crittografia della colonna nel database. È possibile usare la stessa procedura guidata per generare un certificato autofirmato nell'archivio certificati di Windows che può essere usato come chiave master della colonna per i dati always Encrypted. Per ulteriori informazioni sulla sintassi T-SQL della chiave master della colonna e della chiave di crittografia della colonna, vedere rispettivamente creazione della chiave [Master](../../t-sql/statements/create-column-master-key-transact-sql.md) della colonna e [creazione della chiave di crittografia](../../t-sql/statements/create-column-encryption-key-transact-sql.md) della colonna.

Il nome di SQLServerColumnEncryptionCertificateStoreProvider è MSSQL_CERTIFICATE_STORE e può essere sottoposto a query dall'API GetName () dell'oggetto provider. Viene automaticamente registrato dal driver e può essere utilizzato senza alcuna modifica dell'applicazione.

Per gli esempi in questa pagina, se è stata creata una chiave master della colonna basata sull'archivio certificati Windows e una chiave di crittografia della colonna usando SQL Server Management Studio, lo script T-SQL per ricrearli potrebbe essere simile a questo esempio con il proprio **KEY_ specifico PERCORSO** e **ENCRYPTED_VALUE**:

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
> Mentre gli altri provider dell'archivio chiavi in questo articolo sono disponibili su tutte le piattaforme supportate dal driver, l'implementazione di SQLServerColumnEncryptionCertificateStoreProvider del driver JDBC è disponibile solo nei sistemi operativi Windows. Ha una dipendenza da sqljdbc_auth. dll disponibile nel pacchetto driver. Per usare questo provider, copiare il file sqljdbc_auth.dll in una directory nel percorso di sistema Windows nel computer in cui è installato il driver JDBC. In alternativa è possibile impostare la proprietà di sistema java.library.path in modo da specificare la directory di sqljdbc_auth.dll. Se si esegue Java Virtual Machine (JVM) a 32 bit, utilizzare il file sqljdbc_auth.dll nella cartella x86, anche se la versione del sistema operativo è x64. Se si esegue JVM a 64 bit in un processore x64, utilizzare il file sqljdbc_auth.dll nella cartella x64. Ad esempio, se si usa il driver JVM a 32 bit e il driver JDBC è installato nella directory predefinita, specificare il percorso della DLL tramite l'argomento seguente della VM (Virtual Machine) quando l'applicazione Java viene avviata: `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Uso del provider dell'archivio chiavi Java
Il driver JDBC è disponibile in un’implementazione predefinita del provider dell’archivio chiavi per l’archivio chiavi Java. Se la proprietà della stringa di connessione **keyStoreAuthentication** è presente nella stringa di connessione ed è impostata su "JavaKeyStorePassword", il driver crea automaticamente un'istanza del provider per l'archivio chiavi Java e lo registra. Il nome del provider dell'archivio chiavi Java è MSSQL_JAVA_KEYSTORE. È anche possibile eseguire query su questo nome usando l'API SQLServerColumnEncryptionJavaKeyStoreProvider. GetName (). 

Sono disponibili tre proprietà della stringa di connessione che consentono a un'applicazione client di specificare le credenziali necessarie per l'autenticazione da parte del driver nell'archivio chiavi Java. Il driver Inizializza il provider in base ai valori di queste tre proprietà nella stringa di connessione.

**keyStoreAuthentication:** Identifica l'archivio chiavi Java da usare. Con Microsoft JDBC Driver 6,0 e versioni successive per SQL Server, è possibile eseguire l'autenticazione all'archivio chiavi Java solo tramite questa proprietà. Per l'archivio chiavi Java, il valore di questa proprietà deve essere `JavaKeyStorePassword`.

**keyStoreLocation:** Percorso del file dell'archivio chiavi Java in cui è archiviata la chiave master della colonna. Il percorso include il nome file dell'archivio chiavi.

**keyStoreSecret:** La password o il segreto da usare per l'archivio chiavi e per la chiave. Per l'uso dell'archivio chiavi Java, l'archivio chiavi e la password della chiave devono essere uguali.

Di seguito è riportato un esempio di come fornire queste credenziali nella stringa di connessione:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

È anche possibile ottenere o impostare queste impostazioni usando l'oggetto SQLServerDataSource. Per ulteriori informazioni, vedere [Always Encrypted riferimento API per il driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

Il driver JDBC crea automaticamente un'istanza di SQLServerColumnEncryptionJavaKeyStoreProvider quando queste credenziali sono presenti nelle proprietà di connessione.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Creazione di una chiave master della colonna per l'archivio chiavi Java
SQLServerColumnEncryptionJavaKeyStoreProvider può essere usato con i tipi di archivio chiavi JKS o PKCS12. Per creare o importare una chiave da usare con questo provider, usare l'utilità per la [chiave Java.](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) La chiave deve avere la stessa password dell'archivio chiavi. Di seguito è riportato un esempio di come creare una chiave pubblica e la relativa chiave privata associata usando l'utilità di chiave:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

Questo comando crea una chiave pubblica e ne esegue il wrapping in un certificato autofirmato X. 509, che viene archiviato nell'archivio chiavi "keystore. JKS" insieme alla relativa chiave privata associata. Questa voce nell'archivio chiavi è identificata dall'alias ' AlwaysEncryptedKey '.

Di seguito è riportato un esempio dello stesso utilizzo di un tipo di archivio PKCS12:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

Se l'archivio chiavi è di tipo PKCS12, l'utilità per la chiave non richiede una password della chiave e la password della chiave deve essere fornita con l'opzione-Key Pass perché il SQLServerColumnEncryptionJavaKeyStoreProvider richiede che l'archivio chiavi e la chiave abbiano lo stesso valore password.

È anche possibile esportare un certificato dall'archivio certificati di Windows in formato pfx e usarlo con SQLServerColumnEncryptionJavaKeyStoreProvider. Il certificato esportato può anche essere importato nell'archivio chiavi Java come tipo di archivio chiavi di JKS.

Dopo aver creato la voce dello strumento chiave, creare i metadati della chiave master della colonna nel database, che richiede il nome del provider dell'archivio chiavi e il percorso della chiave. Per altre informazioni su come creare i metadati della chiave master della colonna, vedere [creare una chiave master della colonna](../../t-sql/statements/create-column-master-key-transact-sql.md). Per SQLServerColumnEncryptionJavaKeyStoreProvider, il percorso della chiave è semplicemente l'alias della chiave e il nome di SQLServerColumnEncryptionJavaKeyStoreProvider è' MSSQL_JAVA_KEYSTORE '. È anche possibile eseguire una query su questo nome usando l'API pubblica GetName () della classe SQLServerColumnEncryptionJavaKeyStoreProvider. 

La sintassi T-SQL per la creazione della chiave master della colonna è:

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

Per il ' AlwaysEncryptedKey ' creato in precedenza, la definizione della chiave master della colonna sarà:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> La funzionalità incorporata di SQL Server Management Studio non è in grado di creare definizioni della chiave master della colonna per l'archivio chiavi Java. È necessario usare i comandi T-SQL a livello di codice.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Creazione di una chiave di crittografia della colonna per l'archivio chiavi Java
Il SQL Server Management Studio o qualsiasi altro strumento non può essere usato per creare le chiavi di crittografia della colonna usando le chiavi master della colonna nell'archivio chiavi Java. L'applicazione client deve creare la chiave di crittografia della colonna a livello di codice utilizzando la classe SQLServerColumnEncryptionJavaKeyStoreProvider. Per altre informazioni, vedere [uso dei provider dell'archivio chiavi master della colonna per il provisioning delle chiavi a livello di](#using-column-master-key-store-providers-for-programmatic-key-provisioning)codice.

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
Quando si accede a colonne crittografate, Microsoft JDBC Driver per SQL Server trova in modo trasparente e chiama il provider corretto di archivio chiavi master delle colonne per decrittografare le chiavi di crittografia delle colonne. In genere, il codice dell'applicazione normale non chiama direttamente i provider di archivio delle chiavi master delle colonne. È possibile, tuttavia, creare un'istanza e chiamare un provider a livello di codice per il provisioning e la gestione delle chiavi Always Encrypted. Questo passaggio può essere eseguito per generare una chiave di crittografia della colonna crittografata e decrittografare una chiave di crittografia della colonna come rotazione della chiave master della colonna parte, ad esempio. Per altre informazioni, vedere [Panoramica della gestione delle chiavi per Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

Se si usa un provider dell'archivio chiavi personalizzato, potrebbe essere necessario implementare gli strumenti di gestione delle chiavi. Quando si usano chiavi archiviate nell'archivio certificati di Windows o in Azure Key Vault, è possibile usare gli strumenti esistenti, ad esempio SQL Server Management Studio o PowerShell, per gestire ed eseguire il provisioning delle chiavi. Quando si usano chiavi archiviate nell'archivio chiavi Java, è necessario eseguire il provisioning delle chiavi a livello di codice. Nell'esempio seguente viene illustrato l'uso della classe SQLServerColumnEncryptionJavaKeyStoreProvider per crittografare la chiave con una chiave archiviata nell'archivio chiavi Java.

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

Always Encrypted può anche essere abilitato per le singole query. Per altre informazioni, vedere [Controllo dell'impatto di Always Encrypted sulle prestazioni](#controlling-the-performance-impact-of-always-encrypted). Perché la crittografia o la decrittografia abbiano esito positivo, non è sufficiente l'abilitazione di Always Encrypted. È necessario anche assicurarsi che:
- L'applicazione abbia le autorizzazioni di database *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessarie per accedere ai metadati sulle chiavi Always Encrypted nel database. Per informazioni dettagliate, vedere [ Autorizzazioni in Always Encrypted (motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
- L'applicazione può accedere alla chiave master della colonna che protegge le chiavi di crittografia di colonna, le quali crittografano le colonne di database sottoposte a query. Per usare il provider dell'archivio chiavi Java, è necessario specificare credenziali aggiuntive nella stringa di connessione. Per altre informazioni, vedere [uso del provider dell'archivio chiavi Java](#using-java-key-store-provider).

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurazione della modalità di invio dei valori java.sql.Time al server
La proprietà di connessione **sendTimeAsDatetime** viene usata per configurare la modalità di invio del valore java.sql.Time al server. Se impostato su false, il valore dell'ora viene inviato come tipo di SQL Server tempo. Se impostato su true, il valore Time viene inviato come tipo DateTime. Se una colonna ora è crittografata, la proprietà **sendTimeAsDatetime** deve essere false, in quanto le colonne crittografate non supportano la conversione da Time a DateTime. Si noti inoltre che questa proprietà è impostata per impostazione predefinita su true, pertanto quando si utilizzano le colonne temporali crittografate è necessario impostarla su false. In caso contrario, il driver genererà un'eccezione. A partire dalla versione 6,0 del driver, la classe SQLServerConnection dispone di due metodi per configurare il valore di questa proprietà a livello di codice:
 
* public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

Per ulteriori informazioni su questa proprietà, vedere [configurazione della modalità di invio dei valori java. SQL. Time al server](configuring-how-java-sql-time-values-are-sent-to-the-server.md).

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>Configurazione della modalità di invio dei valori stringa al server
La proprietà di connessione **sendStringParametersAsUnicode** viene utilizzata per configurare la modalità di invio dei valori stringa a SQL Server. Se è impostata su True, i parametri String vengono inviati al server in formato Unicode. Se è impostato su false, i parametri di stringa vengono inviati in formato non Unicode, ad esempio ASCII o MBCS, anziché Unicode. Il valore predefinito di questa proprietà è True. Quando Always Encrypted è abilitato e viene crittografata una colonna char/varchar/varchar (max), il valore di **sendStringParametersAsUnicode** deve essere impostato su false. Se questa proprietà è impostata su true, il driver genererà un'eccezione durante la decrittografia dei dati da una colonna char/varchar/varchar (max) crittografata con caratteri Unicode. Per ulteriori informazioni su questa proprietà, vedere [impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recupero e modifica dei dati nelle colonne crittografate
Dopo aver abilitato Always Encrypted per le query dell'applicazione, è possibile utilizzare le API JDBC standard per recuperare o modificare i dati nelle colonne di database crittografate. Se l'applicazione dispone delle autorizzazioni necessarie per il database e può accedere alla chiave master della colonna, il driver eseguirà la crittografia di tutti i parametri di query destinati alle colonne crittografate e determinerà i dati recuperati dalle colonne crittografate.

Se Always Encrypted non è abilitato, le query con parametri destinati alle colonne crittografate avranno esito negativo. Le query possono comunque recuperare i dati dalle colonne crittografate, a condizione che non presentino parametri destinati alle colonne crittografate. Il driver non tenterà però di decrittografare i valori recuperati dalle colonne crittografate e l'applicazione riceverà dati crittografati binari, sotto forma di matrici di byte.

La tabella seguente riepiloga il comportamento delle query, a seconda che la funzionalità Always Encrypted sia abilitata o meno:

| Caratteristica della query                                                                           | Always Encrypted è abilitato e l'applicazione può accedere alle chiavi e ai metadati delle chiavi                                                                                                                        | Always Encrypted è abilitato e l'applicazione non può accedere alle chiavi o ai metadati delle chiavi | Always Encrypted è disabilitato                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| Query con parametri destinati alle colonne crittografate.                                           | I valori dei parametri vengono crittografati in modo trasparente.                                                                                                                                                           | Errore                                                                             | Errore                                                                                                               |
| Query che recuperano dati dalle colonne crittografate, senza parametri destinati alle colonne crittografate. | I risultati delle colonne vengono decrittografati in modo trasparente. L'applicazione riceve valori di testo non crittografato dei tipi di dati JDBC corrispondenti ai tipi di SQL Server configurati per le colonne crittografate. | Errore                                                                             | I risultati delle colonne crittografate non vengono decrittografati. L'applicazione riceve i valori crittografati come matrici di byte (byte[]). |

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Esempi di inserimento e recupero di dati crittografati

Gli esempi seguenti illustrano il recupero e la modifica dei dati nelle colonne crittografate. Gli esempi presuppongono la tabella di destinazione con lo schema seguente e le colonne di SSN e di nascita crittografate. Se è stata configurata una chiave master della colonna denominata "MyCMK" e una chiave di crittografia della colonna denominata "MyCEK", come descritto nelle sezioni precedenti dei provider dell'archivio chiavi, è possibile creare la tabella usando questo script:

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

Se si usa un provider Azure Key Vault keystore:

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Se si usa un provider di archivio chiavi dell'archivio certificati di Windows:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Se si usa un provider di archivio chiavi Java:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>Esempio di inserimento dei dati

Questo esempio illustra come inserire una riga nella tabella Patients. Si noti quanto segue:

- Il codice di esempio non contiene alcun elemento specifico per la crittografia. Microsoft JDBC driver per SQL Server rileva e crittografa automaticamente i parametri destinati alle colonne crittografate. In questo modo la crittografia diventa trasparente per l'applicazione.
- I valori inseriti nelle colonne di database, incluse le colonne crittografate, vengono passati come parametri utilizzando SQLServerPreparedStatement. Quando si inviano valori a colonne non crittografate, l'uso dei parametri è facoltativo, nonostante sia consigliabile per prevenire attacchi SQL injection. È invece necessario usare i parametri in presenza di valori destinati a colonne crittografate. Se i valori inseriti nelle colonne crittografate sono stati passati come valori letterali incorporati nell'istruzione di query, la query avrà esito negativo perché il driver non è in grado di determinare i valori nelle colonne crittografate di destinazione e i valori non vengono crittografati. Di conseguenza, il server li rifiuterà come incompatibili con le colonne crittografate.
- Tutti i valori stampati dal programma saranno in testo non crittografato perché Microsoft JDBC Driver per SQL Server possa decrittografare in modo trasparente i dati recuperati dalle colonne crittografate.
- Se si esegue una ricerca utilizzando una clausola WHERE, il valore utilizzato nella clausola WHERE deve essere passato come parametro in modo che il driver possa crittografarlo in modo trasparente prima di inviarlo al database. Nell'esempio seguente il codice SSN viene passato come parametro, ma il cognome viene passato come valore letterale perché LastName non è crittografato.
- Il metodo di impostazione usato per il parametro destinato alla colonna SSN è sestring (), che esegue il mapping al tipo di dati char/varchar SQL Server. Se per questo parametro il metodo setter usato era setNString(), che esegue il mapping a nchar/nvarchar, la query avrà esito negativo perché Always Encrypted non supporta le conversioni da valori nchar/nvarchar crittografati a valori char/varchar crittografati.

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

- usare i metodi setter appropriati quando si passano i valori per i parametri destinati alle colonne crittografate. Verificare che il SQL Server tipo di dati del parametro corrisponda esattamente al tipo della colonna di destinazione oppure che sia supportata una conversione del tipo di dati SQL Server del parametro nel tipo di destinazione della colonna. Sono stati aggiunti metodi API alle classi SQLServerPreparedStatement, SQLServerCallableStatement e SQLServerResultSet per passare parametri corrispondenti a tipi di dati di SQL Server specifici. Se, ad esempio, una colonna non è crittografata, è possibile usare il metodo setimestamp () per passare un parametro a un datetime2 o a una colonna DateTime. Tuttavia, quando una colonna è crittografata, è necessario utilizzare il metodo esatto che rappresenta il tipo della colonna nel database. Usare, ad esempio, setimestamp () per passare i valori a una colonna datetime2 crittografata e usare il valore di DateTime () per passare i valori a una colonna DateTime crittografata. Per un elenco completo delle nuove API, vedere informazioni di [riferimento sull'api always Encrypted per il driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) .
- La precisione e la scala dei parametri destinati alle colonne dei tipi di dati di SQL Server decimali e numerici sono uguali a quelle configurate per la colonna di destinazione. Sono stati aggiunti metodi API alle classi SQLServerPreparedStatement, SQLServerCallableStatement e SQLServerResultSet per accettare precisione e scalabilità insieme ai valori di dati per parametri/colonne che rappresentano tipi di dati Decimal e numeric. Per un elenco completo delle API nuove/sottocaricate, vedere informazioni di [riferimento sulle API di Always Encrypted per il driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) .  
- la precisione/scala dei secondi frazionari dei parametri destinati alle colonne di tipo datetime2, DateTimeOffset o time SQL Server non è maggiore della precisione/scala dei secondi frazionari per la colonna di destinazione nelle query che modificano i valori della colonna di destinazione. . Sono stati aggiunti metodi API alle classi SQLServerPreparedStatement, SQLServerCallableStatement e SQLServerResultSet per accettare la scala e la precisione dei secondi frazionari insieme ai valori di dati per i parametri che rappresentano questi tipi di dati. Per un elenco completo delle API nuove/in overload, vedere informazioni di [riferimento sulle api always Encrypted per il driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

### <a name="errors-due-to-incorrect-connection-properties"></a>Errori causati da proprietà di connessione non corrette

In questa sezione viene descritto come configurare correttamente le impostazioni di connessione per utilizzare i dati Always Encrypted. Poiché i tipi di dati crittografati supportano le conversioni limitate, le impostazioni di connessione **sendTimeAsDatetime** e **sendStringParametersAsUnicode** richiedono una configurazione appropriata quando si utilizzano colonne crittografate. Assicurarsi che:

- l'impostazione di connessione [sendTimeAsDatetime](setting-the-connection-properties.md) è impostata su false quando si inseriscono dati in colonne temporali crittografate. Per ulteriori informazioni, vedere [configurazione della modalità di invio dei valori java. SQL. Time al server](configuring-how-java-sql-time-values-are-sent-to-the-server.md).
- l'impostazione di connessione [sendStringParametersAsUnicode](setting-the-connection-properties.md) è impostata su true (o viene lasciato come valore predefinito) quando si inseriscono dati in colonne di tipo char/varchar/varchar (max) crittografate.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Errori causati dal passaggio di testo non crittografato anziché di valori crittografati

Qualsiasi valore destinato a una colonna crittografata deve essere crittografato all'interno dell'applicazione. Il tentativo di inserire, modificare o filtrare in base a un valore di testo non crittografato in una colonna crittografata genererà un errore simile al seguente:

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Per evitare tali errori, verificare che:

- Always Encrypted sia abilitato per le query dell'applicazione destinate alle colonne crittografate (per la stringa di connessione o per una query specifica).
- per inviare i dati destinati alle colonne crittografate, è possibile utilizzare istruzioni e parametri preparati. L'esempio seguente illustra una query che filtra in modo errato in base a un valore letterale o costante in una colonna crittografata (SSN), anziché passare il valore letterale all'interno sotto forma di parametro. Questa query avrà esito negativo:

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>Forza crittografia sui parametri di input

La funzionalità di crittografia forzata impone la crittografia di un parametro quando si usa Always Encrypted. Se si usa la crittografia forzata e SQL Server indica al driver che il parametro non deve essere crittografato, la query che usa il parametro avrà esito negativo. Questa proprietà fornisce protezione aggiuntiva contro attacchi alla sicurezza in cui un SQL Server compromesso fornisce al client metadati di crittografia non corretti, con conseguente rischio di divulgazione dei dati. I metodi set * nelle classi SQLServerPreparedStatement e SQLServerCallableStatement e i metodi Update\* della classe SQLServerResultSet sono sottoposti a overload per accettare un argomento booleano per specificare l'impostazione di crittografia forzata. Se il valore di questo argomento è false, il driver non forza la crittografia sui parametri. Se la crittografia forzata è impostata su true, il parametro di query viene inviato solo se la colonna di destinazione è crittografata e Always Encrypted è abilitata per la connessione o per l'istruzione. L'uso di questa proprietà offre un ulteriore livello di sicurezza, assicurando che il driver non invii erroneamente i dati a SQL Server come testo non crittografato quando si prevede che venga crittografato.

Per ulteriori informazioni sui metodi SQLServerPreparedStatement e SQLServerCallableStatement che vengono sottoposti a overload con l'impostazione Force Encryption, vedere [Always Encrypted riferimento API per il driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controllo dell'impatto di Always Encrypted sulle prestazioni

Considerato che Always Encrypted è una tecnologia di crittografia lato client, la maggior parte del sovraccarico delle prestazioni si verifica sul lato client, non nel database. A parte il costo delle operazioni di crittografia e decrittografia, le altre origini di sovraccarico delle prestazioni sul lato client sono le seguenti:

- Round trip aggiuntivi al database per recuperare i metadati per i parametri di query.
- Chiamate a un archivio delle chiavi master delle colonne per accedere alla chiave master di una colonna.

Questa sezione descrive le ottimizzazioni delle prestazioni predefinite in Microsoft JDBC Driver per SQL Server e come controllare l'impatto sulle prestazioni esercitato dai due fattori descritti.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controllo dei round trip per recuperare i metadati per i parametri di query

Se la funzionalità Always Encrypted è abilitata per una connessione, per impostazione predefinita il driver chiamerà [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) per ogni query con parametri, passando l'istruzione di query (senza i valori dei parametri) a SQL Server. [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) analizza l'istruzione di query per verificare se sono presenti parametri da crittografare e, in tal caso, restituisce le informazioni relative alla crittografia che consentiranno al driver di crittografare i valori dei parametri. Il comportamento descritto garantisce all'applicazione client un elevato livello di trasparenza. Finché l'applicazione utilizza parametri per passare valori destinati a colonne crittografate al driver, l'applicazione (e lo sviluppatore dell'applicazione) non devono essere in grado di stabilire quali query accedono alle colonne crittografate.

### <a name="setting-always-encrypted-at-the-query-level"></a>Impostazione di Always Encrypted a livello di query

Per controllare l'impatto sulle prestazioni del recupero dei metadati di crittografia per le query con parametri, è possibile abilitare Always Encrypted per singole query, anziché l'impostare la funzionalità per la connessione. In questo modo, è possibile assicurarsi che sys.sp_describe_parameter_encryption venga richiamato solo per le query con parametri destinati a colonne crittografate. Si noti, tuttavia, che in tal modo si riduce la trasparenza della crittografia. Se si modificano le proprietà di crittografia delle colonne di database, potrebbe essere necessario modificare il codice dell'applicazione per allinearlo alle modifiche dello schema.

Per controllare il comportamento di Always Encrypted delle singole query, è necessario configurare singoli oggetti istruzione passando un enum, SQLServerStatementColumnEncryptionSetting, che specifica come verranno inviati e ricevuti i dati durante la lettura e la scrittura. colonne crittografate per l'istruzione specifica. Di seguito sono riportate alcune linee guida utili:

- Se la maggior parte delle query che un'applicazione client invia alla connessione del database accede alle colonne crittografate, seguire queste linee guida:

    - Impostare la parola chiave della stringa di connessione **columnEncryptionSetting** su **Enabled**.
    - Impostare SQLServerStatementColumnEncryptionSetting.Disabled per le singole query che non accedono a colonne crittografate. In questo modo verranno disabilitati sia la chiamata di sys.sp_describe_parameter_encryption chiamante che il tentativo di decrittografare i valori nel set di risultati.
    - Impostare SQLServerStatementColumnEncryptionSetting.ResultSet per le singole query che non presentano parametri da crittografare, ma che recuperano i dati dalle colonne crittografate. In questo modo verranno disabilitate la chiamata di sys.sp_describe_parameter_encryption e la crittografia dei parametri. La query potrà decrittografare i risultati delle colonne di crittografia.

- Se la maggior parte delle query che un'applicazione client invia alla connessione del database non accede alle colonne crittografate, seguire queste linee guida:

    - Impostare la parola chiave della stringa di connessione **columnEncryptionSetting** su **Disabled**.
    - Impostare SQLServerStatementColumnEncryptionSetting.Enabled per le singole query che presentano parametri da crittografare. In questo modo verranno abilitate sia la chiamata di sys.sp_describe_parameter_encryption che la decrittografia dei risultati di query recuperati da colonne crittografate.
    - Impostare SQLServerStatementColumnEncryptionSetting.ResultSet per le query che non presentano parametri da crittografare, ma che recuperano i dati dalle colonne crittografate. In questo modo verranno disabilitate la chiamata di sys.sp_describe_parameter_encryption e la crittografia dei parametri. La query potrà decrittografare i risultati delle colonne di crittografia.

Le impostazioni SQLServerStatementColumnEncryptionSetting non possono essere usate per ignorare la crittografia e ottenere l'accesso ai dati in testo non crittografato. Per ulteriori informazioni sulla configurazione della crittografia di colonna in un'istruzione, vedere [Always Encrypted riferimento API per il driver JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

Nell'esempio seguente la funzionalità Always Encrypted è disabilitata per la connessione di database. La query eseguita dall'applicazione ha un parametro la cui destinazione è la colonna LastName non crittografata. La query recupera i dati dalle colonne SSN e BirthDate, che sono entrambe crittografate. In tal caso, la chiamata di sys.sp_describe_parameter_encryption per recuperare i metadati di crittografia non è necessaria. È tuttavia necessario abilitare la decrittografia dei risultati della query in modo che l'applicazione possa ricevere i valori di testo non crittografato dalle due colonne crittografate. L'impostazione SQLServerStatementColumnEncryptionSetting. ResultSet viene utilizzata per garantire che.

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

È possibile configurare un valore di durata (TTL) per le voci della chiave di crittografia della colonna nella cache usando l'API setColumnEncryptionKeyCacheTtl () nella classe SQLServerConnection. Il valore di durata (TTL) predefinito per le voci della chiave di crittografia della colonna nella cache è di due ore. Per disattivare la memorizzazione nella cache, utilizzare un valore pari a 0. Per impostare un valore di durata (TTL), usare l'API seguente:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

Ad esempio, per impostare un valore di durata (TTL) di 10 minuti, usare:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

Come unità di tempo sono supportati solo giorni, ore, minuti o secondi.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Copia dei dati crittografati con SQLServerBulkCopy

Con SQLServerBulkCopy, è possibile copiare dati già crittografati e archiviati in una tabella in un'altra tabella, senza eseguire la decrittografia dei dati. Per eseguire questa operazione:

- Assicurarsi che la configurazione di crittografia della tabella di destinazione sia identica alla configurazione della tabella di origine. In particolare, le due le tabelle devono avere le stesse colonne crittografate e le colonne devono essere crittografate usando gli stessi tipi di crittografia e le stesse chiavi di crittografia. Se una delle colonne di destinazione è crittografata in modo diverso dalla relativa colonna di origine corrispondente, non sarà possibile decrittografare i dati nella tabella di destinazione dopo l'operazione di copia. I dati risulteranno danneggiati.
- Configurare le due connessioni di database alla tabella di origine e la tabella di destinazione, senza abilitare Always Encrypted.
- Impostare l'opzione allowEncryptedValueModifications. Per ulteriori informazioni, vedere [utilizzo della copia bulk con il driver JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

> [!NOTE]
> Prestare attenzione quando si specifica AllowEncryptedValueModifications. Questa opzione può danneggiare il database perché Microsoft JDBC Driver per SQL Server non verifica se i dati vengono effettivamente crittografati o se vengono crittografati correttamente usando lo stesso tipo di crittografia, l'algoritmo e la chiave della colonna di destinazione.

## <a name="see-also"></a>Vedere anche

[Always Encrypted (Motore di database)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
