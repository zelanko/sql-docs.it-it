---
title: Connessione con l'autenticazione di Azure Active Directory | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62892cebe5c3c709cedee94b620b2c0e4cfeb258
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737032"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Connessione con l'autenticazione di Azure Active Directory

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questo articolo fornisce informazioni su come sviluppare applicazioni Java da usare la funzionalità di autenticazione di Azure Active Directory con Microsoft JDBC Driver per SQL Server.

È possibile usare l'autenticazione di Azure Active Directory (AAD), che è un meccanismo di connessione alla versione 12 del Database SQL di Azure tramite identità in Azure Active Directory. Usare l'autenticazione di Azure Active Directory per gestire centralmente le identità degli utenti del database e come alternativa all'autenticazione di SQL Server. Il Driver JDBC consente di specificare le credenziali di Azure Active Directory nella stringa di connessione JDBC per connettersi al database SQL di Azure. Per informazioni su come configurare l'autenticazione di Azure Active Directory, visitare [la connessione a SQL Database usando Azure Active Directory l'autenticazione](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Proprietà di connessione per supportare l'autenticazione Azure Active Directory in Microsoft JDBC Driver per SQL Server sono:
*   **autenticazione**: usare questa proprietà per indicare il metodo di autenticazione SQL da usare per la connessione. I valori possibili sono: 
    * **ActiveDirectoryMSI**
        * Supportata a partire dalla versione del driver **versione 7.2**, `authentication=ActiveDirectoryMSI` può essere utilizzato per connettersi a un Azure SQL Database/Data Warehouse all'interno di una risorsa di Azure con supporto di "Identity" abilitato. Facoltativamente **msiClientId** possono anche essere specificati nelle proprietà della connessione o origine dati insieme a questa modalità di autenticazione, che deve contenere l'ID Client di un'identità del servizio gestito per essere usato per acquisire il  **accessToken** per stabilire la connessione.
    * **ActiveDirectoryIntegrated**
        * Supportata a partire dalla versione del driver **v6.0**, `authentication=ActiveDirectoryIntegrated` può essere usato per connettersi a un Azure SQL Database/Data Warehouse con l'autenticazione integrata. Per usare questa modalità di autenticazione, è necessario eseguire la federazione di locali Active Directory Federation Services (ADFS) con Azure Active Directory nel cloud. Dopo che è configurato, è possibile connettersi aggiungendo la libreria nativa 'sqljdbc_auth' al percorso della classe dell'applicazione nel sistema operativo Windows, o configurazione di un ticket Kerberos per supportare l'autenticazione multi-piattaforma. Sarà in grado di accedere a Azure SQL DB/DW senza che vengano richieste le credenziali quando è connessi a un computer appartenente al dominio.
    * **ActiveDirectoryPassword**
        * Supportata a partire dalla versione del driver **v6.0**, `authentication=ActiveDirectoryPassword` può essere usato per connettersi a un Azure SQL Database/Data Warehouse usando un nome dell'entità di Azure AD e una password.
    * **SqlPassword**
        * Usare `authentication=SqlPassword` per connettersi a SQL Server utilizzando le proprietà/utente di nome utente e password.
    * **NotSpecified**
        * Usare `authentication=NotSpecified` o lasciare il valore predefinito quando nessuno di questi metodi di autenticazione sono necessari.

*   **accessToken**: Usare questa proprietà di connessione per connettersi a un Database SQL usando un token di accesso. accessToken può essere impostato solo usando il parametro Properties del metodo getConnection () nella classe DriverManager. Non può essere utilizzato nell'URL della connessione.  

Per altre informazioni, vedere la proprietà di autenticazione sul [impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md) pagina.  


## <a name="client-setup-requirements"></a>Requisiti di installazione client
Per **ActiveDirectoryMSI** l'autenticazione, i seguenti componenti deve essere installato nel computer client:
* Java 8 o versione successiva
* Microsoft JDBC Driver versione 7.2 (o versioni successive) per SQL Server
* Ambiente client deve essere una risorsa di Azure e deve avere il supporto di funzionalità "Identity" abilitato.
* Un utente di database indipendente che rappresenta la risorsa di Azure gestiti identità assegnata di sistema o assegnato gestiti identità utente o uno dei gruppi a cui che appartiene l'identità del servizio gestito, deve esistere nel database di destinazione e deve disporre dell'autorizzazione CONNECT.

Per altre modalità di autenticazione, i seguenti componenti deve essere installato nel computer client:
* Java 7 o versione successiva
* Microsoft JDBC Driver 6.0 (o versione successiva) per SQL Server
* Se si usa la modalità di autenticazione basata su token di accesso, occorre [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e le relative dipendenze per eseguire gli esempi in questo articolo. Per altre informazioni, vedere la **la connessione tramite Token di accesso** sezione.
* Se si usa la **ActiveDirectoryPassword** modalità di autenticazione, è necessario [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e le relative dipendenze. Per altre informazioni, vedere la **la connessione Usa la modalità di autenticazione ActiveDirectoryPassword** sezione.
* Se si usa la **ActiveDirectoryIntegrated** modalità, è necessario azure-activedirectory-library-for-java e le relative dipendenze. Per altre informazioni, vedere la **la connessione Usa la modalità di autenticazione ActiveDirectoryIntegrated** sezione.

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>La connessione Usa la modalità di autenticazione ActiveDirectoryMSI
L'esempio seguente illustra come usare la modalità `authentication=ActiveDirectoryMSI`. Eseguire questo esempio all'interno di una risorsa di Azure, e, g una macchina virtuale di Azure, servizio App o un'App per le funzioni che è federato con Azure Active Directory.

Sostituire il nome del server/database con il nome del server/database nelle righe seguenti prima di eseguire l'esempio:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

L'esempio per usare la modalità di autenticazione ActiveDirectoryMSI:

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Esecuzione in una macchina virtuale di Azure di questo esempio recupera un token di accesso da _gestito identità assegnata di sistema_ o _identità gestita assegnata utente_ (se **msiClientId** è specificato) e stabilisce una connessione usando il token di accesso recuperato. Se viene stabilita una connessione, si dovrebbe vedere il messaggio seguente:

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>La connessione Usa la modalità di autenticazione ActiveDirectoryIntegrated
Con la versione 6.4, Microsoft JDBC Driver aggiunge il supporto per l'autenticazione ActiveDirectoryIntegrated mediante un ticket Kerberos su più piattaforme (Windows, Linux e macOS).
Per altre informazioni, vedere [ticket Kerberos impostato su Windows, Linux e Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) per altri dettagli. In alternativa, in Windows, sqljdbc_auth è anche utilizzabile per l'autenticazione ActiveDirectoryIntegrated con il Driver JDBC.

> [!NOTE]
>  Se si usa una versione precedente del driver, selezionare questa opzione [collegamento](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) per le rispettive dipendenze necessarie per usare questa modalità di autenticazione. 

L'esempio seguente illustra come usare la modalità `authentication=ActiveDirectoryIntegrated`. Eseguire questo esempio in un computer appartenente al dominio federato con Azure Active Directory. Un utente di database indipendente che rappresenta l'entità di Azure AD o a uno dei gruppi a cui che si appartiene, deve esistere nel database e deve disporre dell'autorizzazione CONNECT. 

Prima di compilare ed eseguire l'esempio, nel computer client (in cui, si desidera eseguire l'esempio), scaricare il [libreria di azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e le relative dipendenze e includerli nel percorso di compilazione Java

Sostituire il nome del server/database con il nome del server/database nelle righe seguenti prima di eseguire l'esempio:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

L'esempio per usare la modalità di autenticazione ActiveDirectoryIntegrated:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Esegue automaticamente in questo esempio in un computer client utilizza il ticket Kerberos e non è necessaria alcuna password. Se viene stabilita una connessione, si dovrebbe vedere il messaggio seguente:

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Impostare i ticket Kerberos per Windows, Linux e Mac

È necessario configurare un ticket Kerberos dell'utente corrente di collegamento a un account di dominio di Windows. Ecco un riepilogo dei passaggi principali.

#### <a name="windows"></a>Windows
È dotato di JDK `kinit`, che è possibile usare per ottenere un ticket TGT dal centro distribuzione chiavi (KDC) in un dominio aggiunto al computer in cui è federato con Azure Active Directory.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Passaggio 1: Recupero di ticket di concessione Ticket
- **Eseguire in**: Windows
- **Azione**:
  - Usare il comando `kinit username@DOMAIN.COMPANY.COM` per ottenere un ticket TGT dal KDC, quindi verrà richiesto di specificare la password di dominio.
  - Usare `klist` per visualizzare i ticket disponibili. Se il kinit ha esito positivo, si noterà un ticket da krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Potrebbe essere necessario specificare una `.ini` file con `-Djava.security.krb5.conf` dall'applicazione individuare KDC.

#### <a name="linux-and-mac"></a>Linux e Mac

##### <a name="requirements"></a>Requisiti
Accesso a un computer Windows aggiunti a un dominio per eseguire query sui Controller di dominio Kerberos.

##### <a name="step-1-find-kerberos-kdc"></a>Passaggio 1: Individuare KDC di Kerberos
- **Eseguire in**: riga di comando di Windows
- **Azione**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (dove "DOMAIN.COMPANY.COM" esegue il mapping al nome del dominio)
- **Esempio di output**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Per estrarre informazioni** denominare il controller di dominio, in questo caso `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Passaggio 2: La configurazione KDC in krb5.conf
- **Eseguire in**: Linux/Mac
- **Azione**: Modificare il /etc/krb5.conf in un editor di propria scelta. Configurare le chiavi seguenti
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  Quindi salvare il file krb5.conf ed Esci

> [!NOTE]
>  Dominio deve essere in lettere maiuscole.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>Passaggio 3: Test del recupero di Ticket di concessione Ticket
- **Eseguire in**: Linux/Mac
- **Azione**:
  - Usare il comando `kinit username@DOMAIN.COMPANY.COM` per ottenere un ticket TGT dal KDC, quindi verrà richiesto di specificare la password di dominio.
  - Usare `klist` per visualizzare i ticket disponibili. Se il kinit ha esito positivo, si noterà un ticket da krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>La connessione Usa la modalità di autenticazione ActiveDirectoryPassword
L'esempio seguente illustra come usare la modalità `authentication=ActiveDirectoryPassword`.

Prima di compilare ed eseguire l'esempio:
1.  Nel computer client (in cui, si desidera eseguire l'esempio), scaricare il [libreria di azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e le relative dipendenze e includerli nel percorso di compilazione Java
2.  Individuare le righe di codice seguente e sostituire il nome del server/database con il nome del server/database.
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Individuare le righe di codice seguente e sostituire nome utente, con il nome dell'utente di AAD che si desidera connettersi come.
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

L'esempio per usare la modalità di autenticazione ActiveDirectoryPassword:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
Se viene stabilita una connessione, si dovrebbe vedere il messaggio seguente come output:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Un database utente indipendente deve essere presente un utente di database indipendente che rappresenta l'oggetto specificato e utente di Azure AD o uno dei gruppi, di Azure specificato utente AD a cui appartiene, deve esistere nel database e deve disporre dell'autorizzazione CONNECT (ad eccezione di Azure Active Directory l'amministratore del server o gruppo)

## <a name="connecting-using-access-token"></a>La connessione tramite Token di accesso
Applicazioni/servizi può recuperare un token di accesso da Azure Active Directory e usarlo per connettersi ad Azure SQL Database/Data Warehouse.

> [!NOTE] 
> **accessToken** può essere impostato solo usando il parametro Properties del metodo getConnection () nella classe DriverManager. Non può essere utilizzato nella stringa di connessione.

L'esempio seguente contiene una semplice applicazione Java che si connette ad Azure SQL Database/Data Warehouse Usa l'autenticazione basata su token di accesso. Prima di compilare ed eseguire l'esempio, eseguire la procedura seguente:
1.  Creare un account dell'applicazione in Azure Active Directory per il servizio.
    1. Accedere al portale di Azure.
    2. Nel riquadro di spostamento a sinistra, fare clic su Azure Active Directory.
    3. Fare clic sulla scheda "Registrazioni per l'App".
    4. Nel pannello, fare clic su "Registrazione nuova applicazione".
    5. Immettere mytokentest come un nome descrittivo per l'applicazione, selezionare "App Web/API".
    6. Non è necessario l'URL di accesso. È sufficiente fornire qualsiasi elemento: "https://mytokentest".
    7. Fare clic su "Crea" nella parte inferiore.
    9. Nel portale di Azure, fare clic sulla scheda "Impostazioni" dell'applicazione e aprire la scheda "Proprietà".
    10. Trovare il valore "ID applicazione" (detto anche ID Client) e copiarlo a parte, è necessario in un secondo momento durante la configurazione dell'applicazione (ad esempio, 1846943b-ad04-4808-aa13-4702d908b5c1). Vedere lo snapshot seguente.
    11. Nella sezione "Chiavi", creare una chiave, specificando il campo nome, selezionando la durata della chiave e il salvataggio della configurazione (lasciare vuoto il campo valore). Dopo il salvataggio, il campo del valore deve essere compilato automaticamente, copiare il valore generato. Questo è il segreto client.
    12. Nel Pannello di sinistra, fare clic su Azure Active Directory. In "Registrazioni per l'App", trovare la scheda "Endpoint". Copiare l'URL in "OATH 2.0 TOKEN ENDPOINT", questo è l'URL del servizio token di sicurezza.
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Accedere al database utente del Server SQL Azure con un amministratore di Azure Active Directory e l'utilizzo di un utente del database una disposizione di comando di T-SQL per l'applicazione dell'entità. Per altre informazioni, vedere la [connessione al Database SQL oppure a SQL Data Warehouse da con Azure Active Directory l'autenticazione](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) per altri dettagli su come creare un amministratore di Azure Active Directory e un utente di database indipendente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  Nel computer client (in cui, si desidera eseguire l'esempio), scaricare il [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) libreria e le relative dipendenze e includerli nel percorso di compilazione Java. Si noti che il azure-activedirectory-library-for-java è necessaria solo per eseguire questo esempio specifico. L'esempio Usa le API da questa raccolta per recuperare il token di accesso da Azure Active Directory di Azure. Se si dispone già di un token di accesso, è possibile ignorare questo passaggio. Si noti che è necessario rimuovere anche la sezione nell'esempio che recupera i token di accesso.

Nell'esempio seguente, sostituire il nome di URL del servizio token di sicurezza, ID Client, segreto Client, server e database con i propri valori.

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

Se la connessione ha esito positivo, si dovrebbe vedere il seguente messaggio come output:

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
