---
title: Connessione con l'autenticazione di Azure Active Directory | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b596936010fcdce4eb5c0701c5f0c6631cd9687e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028118"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Connessione con l'autenticazione di Azure Active Directory

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questo articolo fornisce informazioni su come sviluppare applicazioni Java per usare la funzionalità di autenticazione di Azure Active Directory con Microsoft JDBC Driver for SQL Server.

È possibile usare l'autenticazione di Azure Active Directory (AAD), che è un meccanismo di connessione alla versione 12 del database SQL di Azure usando le identità in Azure Active Directory. Usare l'autenticazione di Azure Active Directory per gestire centralmente le identità degli utenti del database e come alternativa all'autenticazione di SQL Server. Il driver JDBC consente di specificare le credenziali di Azure Active Directory nella stringa di connessione JDBC per connettersi al database SQL di Azure. Per informazioni su come configurare Azure Active Directory autenticazione, vedere [connessione al database SQL tramite l'autenticazione Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Le proprietà di connessione per supportare l'autenticazione Azure Active Directory in Microsoft JDBC driver per SQL Server sono:
*   **Authentication**: usare questa proprietà per indicare quale metodo di autenticazione SQL usare per la connessione. I valori possibili sono: 
    * **ActiveDirectoryMSI**
        * Supportato a partire dalla versione **7.2**del `authentication=ActiveDirectoryMSI` driver, può essere usato per connettersi a un database SQL di Azure/Data warehouse dall'interno di una risorsa di Azure con il supporto "Identity" abilitato. Facoltativamente, è possibile specificare **msiClientId** anche nelle proprietà Connection/DataSource insieme a questa modalità di autenticazione, che deve contenere l'ID client di un identità del servizio gestita da usare per acquisire il **AccessToken** per la definizione connessione.
    * **ActiveDirectoryIntegrated**
        * Supportato a partire dalla versione **6.0**del `authentication=ActiveDirectoryIntegrated` driver, può essere usato per connettersi a un database SQL di Azure/Data Warehouse usando l'autenticazione integrata. Per utilizzare questa modalità di autenticazione, è necessario federare il Active Directory Federation Services locale (ADFS) con Azure Active Directory nel cloud. Una volta configurato, è possibile connettersi aggiungendo la libreria nativa ' sqljdbc_auth. dll ' al percorso della classe dell'applicazione nel sistema operativo Windows o impostando un ticket Kerberos per il supporto dell'autenticazione multipiattaforma. È possibile accedere al database SQL di Azure/DW senza che vengano richieste le credenziali quando si è connessi a un computer aggiunto al dominio.
    * **ActiveDirectoryPassword**
        * Supportato a partire dalla versione **6.0**del `authentication=ActiveDirectoryPassword` driver, può essere usato per connettersi a un database SQL di Azure/Data Warehouse usando un nome di Azure ad principale e una password.
    * **SqlPassword**
        * Usare `authentication=SqlPassword` per connettersi a un SQL Server usando le proprietà Username/user e password.
    * **NotSpecified**
        * Usare `authentication=NotSpecified` o lasciare il valore predefinito quando non è necessario nessuno di questi metodi di autenticazione.

*   **AccessToken**: usare questa proprietà di connessione per connettersi a un database SQL usando un token di accesso. accessToken può essere impostato solo usando il parametro Properties del metodo GetConnection () nella classe DriverManager. Non può essere usato nell'URL di connessione.  

Per ulteriori informazioni, vedere la proprietà Authentication nell' [impostazione della pagina Proprietà connessione](../../connect/jdbc/setting-the-connection-properties.md) .  


## <a name="client-setup-requirements"></a>Requisiti di configurazione client
Per l'autenticazione **ActiveDirectoryMSI** , i componenti seguenti devono essere installati nel computer client:
* Java 8 o versione successiva
* Microsoft JDBC driver 7,2 (o versione successiva) per SQL Server
* L'ambiente client deve essere una risorsa di Azure e deve essere abilitato il supporto della funzionalità "Identity".
* Un utente del database indipendente che rappresenta l'identità gestita assegnata al sistema della risorsa di Azure o l'identità gestita assegnata dall'utente o uno dei gruppi a cui appartiene il file MSI deve esistere nel database di destinazione e deve disporre dell'autorizzazione CONNECT.

Per altre modalità di autenticazione, è necessario che i componenti seguenti siano installati nel computer client:
* Java 7 o versione successiva
* Microsoft JDBC Driver 6,0 (o versione successiva) per SQL Server
* Se si usa la modalità di autenticazione basata su token di accesso, è necessario [Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e le relative dipendenze per eseguire gli esempi di questo articolo. Per ulteriori informazioni, vedere la sezione **connessione utilizzando il token di accesso** .
* Se si usa la modalità di autenticazione **ActiveDirectoryPassword** , sono necessari [Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e le relative dipendenze. Per ulteriori informazioni, vedere la sezione **connessione mediante la modalità di autenticazione ActiveDirectoryPassword** .
* Se si usa la modalità **ActiveDirectoryIntegrated** , sono necessari Azure-ActiveDirectory-Library-for-Java e le relative dipendenze. Per ulteriori informazioni, vedere la sezione **connessione mediante la modalità di autenticazione ActiveDirectoryIntegrated** .

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>Connessione tramite la modalità di autenticazione ActiveDirectoryMSI
L'esempio seguente illustra come usare la modalità `authentication=ActiveDirectoryMSI`. Eseguire questo esempio dall'interno di una risorsa di Azure, e, g una macchina virtuale di Azure, un servizio app o un app per le funzioni federato con Azure Active Directory.

Prima di eseguire l'esempio, sostituire il nome del server o del database con il nome del server o del database nelle righe seguenti:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

Esempio di utilizzo della modalità di autenticazione ActiveDirectoryMSI:

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

Eseguendo questo esempio in una macchina virtuale di Azure, viene recuperato un token di accesso dall'identità gestita assegnata dal _sistema_ o dall'identità _gestita assegnata dall'utente_ (se **msiClientId** è specificato) e viene stabilita una connessione tramite l'accesso recuperato. token. Se viene stabilita una connessione, verrà visualizzato il messaggio seguente:

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Connessione tramite la modalità di autenticazione ActiveDirectoryIntegrated
Con la versione 6,4, Microsoft JDBC driver aggiunge il supporto per l'autenticazione ActiveDirectoryIntegrated usando un ticket Kerberos su più piattaforme (Windows, Linux e macOS).
Per altre informazioni, vedere [impostare un ticket Kerberos per Windows, Linux e Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) . In alternativa, in Windows sqljdbc_auth. dll può essere utilizzato anche per l'autenticazione ActiveDirectoryIntegrated con il driver JDBC.

> [!NOTE]
>  Se si utilizza una versione precedente del driver, selezionare questo [collegamento](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) per le rispettive dipendenze necessarie per utilizzare questa modalità di autenticazione. 

L'esempio seguente illustra come usare la modalità `authentication=ActiveDirectoryIntegrated`. Eseguire questo esempio in un computer aggiunto a un dominio federato con Azure Active Directory. Un utente del database indipendente che rappresenta il Azure AD entità o uno dei gruppi a cui si appartiene deve esistere nel database e deve disporre dell'autorizzazione CONNECT. 

Prima di compilare ed eseguire l'esempio, nel computer client in cui si vuole eseguire l'esempio, scaricare la [libreria Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e le relative dipendenze e includerle nel percorso di compilazione Java

Prima di eseguire l'esempio, sostituire il nome del server o del database con il nome del server o del database nelle righe seguenti:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

Esempio di utilizzo della modalità di autenticazione ActiveDirectoryIntegrated:
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

L'esecuzione di questo esempio in un computer client usa automaticamente il ticket Kerberos e non è richiesta alcuna password. Se viene stabilita una connessione, verrà visualizzato il messaggio seguente:

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Imposta ticket Kerberos in Windows, Linux e Mac

È necessario configurare un ticket Kerberos che collega l'utente corrente a un account di dominio di Windows. Di seguito è riportato un riepilogo dei passaggi principali.

#### <a name="windows"></a>Windows
JDK viene fornita `kinit`con, che è possibile usare per ottenere un TGT da centro distribuzione chiavi (KDC) in un computer aggiunto al dominio che è federato con Azure Active Directory.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Passaggio 1: ticket che concede il recupero di ticket
- **Esegui in**: Windows
- **Azione**:
  - Usare il comando `kinit username@DOMAIN.COMPANY.COM` per ottenere un TGT da KDC, quindi verrà richiesta la password del dominio.
  - Usare `klist` per visualizzare i ticket disponibili. Se il kinit ha avuto esito positivo, verrà visualizzato un ticket da krbtgt/DOMAIN. COMPANY. COM @ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Potrebbe essere necessario specificare un `.ini` file con `-Djava.security.krb5.conf` l'applicazione per individuare il KDC.

#### <a name="linux-and-mac"></a>Linux e Mac

##### <a name="requirements"></a>Requisiti
Accesso a un computer aggiunto a un dominio di Windows per eseguire una query sul controller di dominio Kerberos.

##### <a name="step-1-find-kerberos-kdc"></a>Passaggio 1: trovare il KDC Kerberos
- **Esegui in**: riga di comando di Windows
- **Azione**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (dove "Domain.Company.com" esegue il mapping al nome del dominio)
- **Esempio di output**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Informazioni da estrarre** Nome del controller di dominio, in questo caso`co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Passaggio 2: configurazione di KDC in krb5. conf
- **Esegui in**: Linux/Mac
- **Azione**: modificare il/etc/krb5.conf in un editor di propria scelta. Configurare le chiavi seguenti
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  Salvare quindi il file krb5.conf e uscire

> [!NOTE]
>  Il dominio deve essere in lettere MAIUSCOLE.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>Passaggio 3: test del recupero del Ticket Granting Ticket
- **Esegui in**: Linux/Mac
- **Azione**:
  - Usare il comando `kinit username@DOMAIN.COMPANY.COM` per ottenere un TGT da KDC, quindi verrà richiesta la password del dominio.
  - Usare `klist` per visualizzare i ticket disponibili. Se il kinit ha avuto esito positivo, verrà visualizzato un ticket da krbtgt/DOMAIN. COMPANY. COM @ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Connessione tramite la modalità di autenticazione ActiveDirectoryPassword
L'esempio seguente illustra come usare la modalità `authentication=ActiveDirectoryPassword`.

Prima di compilare ed eseguire l'esempio:
1.  Nel computer client in cui si vuole eseguire l'esempio, scaricare la [libreria Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e le relative dipendenze e includerle nel percorso di compilazione Java
2.  Individuare le righe di codice seguenti e sostituire il nome del server/database con il nome del server o del database.
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Individuare le righe di codice seguenti e sostituire nome utente con il nome dell'utente di AAD a cui si vuole connettersi.
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

Esempio di utilizzo della modalità di autenticazione ActiveDirectoryPassword:
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
Se viene stabilita la connessione, verrà visualizzato il messaggio seguente come output:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Un database utente indipendente deve esistere e un utente del database indipendente che rappresenta l'utente Azure AD specificato o uno dei gruppi, l'utente Azure AD specificato appartiene a, deve esistere nel database e deve disporre dell'autorizzazione CONNECT (ad eccezione di Azure Active Directory amministratore del server o gruppo)

## <a name="connecting-using-access-token"></a>Connessione tramite il token di accesso
Le applicazioni e i servizi possono recuperare un token di accesso dal Azure Active Directory e usarlo per connettersi al database SQL di Azure/data warehouse.

> [!NOTE] 
> **AccessToken** può essere impostato solo usando il parametro Properties del metodo GetConnection () nella classe DriverManager. Non può essere usato nella stringa di connessione.

L'esempio seguente contiene una semplice applicazione Java che si connette al database SQL di Azure/data warehouse usando l'autenticazione basata su token di accesso. Prima di compilare ed eseguire l'esempio, seguire questa procedura:
1.  Creare un account dell'applicazione in Azure Active Directory per il servizio.
    1. Accedere al portale di Azure.
    2. Fare clic su Azure Active Directory nel percorso di spostamento a sinistra.
    3. Fare clic sulla scheda "Registrazioni app".
    4. Nel cassetto fare clic su "registrazione nuova applicazione".
    5. Immettere mytokentest come nome descrittivo per l'applicazione e selezionare "app Web/API".
    6. L'URL di accesso non è necessario. Basta fornire qualsiasi elemento: https://mytokentest"".
    7. Fare clic su "Crea" nella parte inferiore.
    9. Sempre nella portale di Azure fare clic sulla scheda "Impostazioni" dell'applicazione e aprire la scheda "proprietà".
    10. Trovare il valore "ID applicazione" (noto anche come ID client) e copiarlo a parte. questa operazione è necessaria in un secondo momento durante la configurazione dell'applicazione (ad esempio, 1846943b-ad04-4808-aa13-4702d908b5c1). Vedere gli snapshot seguenti.
    11. Nella sezione "chiavi" creare una chiave compilando il campo nome, selezionando la durata della chiave e salvando la configurazione (lasciare vuoto il campo valore). Dopo il salvataggio, il campo del valore deve essere compilato automaticamente, copiare il valore generato. Questo è il segreto client.
    12. Fare clic su Azure Active Directory nel pannello sul lato sinistro. In "registrazioni per l'app" trovare la scheda "endpoint punti". Copiare l'URL in "GIURAmento 2,0 TOKEN ENDPOINT", ovvero l'URL STS.
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Accedere al database utente di Azure SQL Server come amministratore Azure Active Directory e usare un comando T-SQL effettuare il provisioning di un utente di database indipendente per l'entità applicazione. Per ulteriori informazioni su come creare un amministratore Azure Active Directory e un utente del database indipendente, vedere la pagina relativa alla [connessione al database SQL o SQL data warehouse tramite l'autenticazione Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) .

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  Nel computer client in cui si vuole eseguire l'esempio, scaricare la libreria [Azure-ActiveDirectory-Library-for-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e le relative dipendenze e includerle nel percorso di compilazione Java. Si noti che Azure-ActiveDirectory-Library-for-Java è necessario solo per eseguire questo esempio specifico. L'esempio usa le API di questa libreria per recuperare il token di accesso da Azure AAD. Se si dispone già di un token di accesso, è possibile ignorare questo passaggio. Si noti che è necessario anche rimuovere la sezione nell'esempio che recupera il token di accesso.

Nell'esempio seguente sostituire l'URL del servizio token di identità, l'ID client, il segreto client, il nome del server e del database con i valori.

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

Se la connessione ha esito positivo, verrà visualizzato il messaggio seguente come output:

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
