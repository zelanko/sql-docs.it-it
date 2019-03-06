---
title: Azure Active Directory | Microsoft Docs
ms.date: 02/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- azure active directory, authentication, access token
author: david-puglielli
ms.author: v-dapugl
manager: mbarwin
ms.openlocfilehash: 30423cd7c15a920d99fad4c0ea08e074beaece0b
ms.sourcegitcommit: 8664c2452a650e1ce572651afeece2a4ab7ca4ca
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56828051"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Connessione con l'autenticazione di Azure Active Directory
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) è una tecnologia di gestione ID utente centrale che opera come alternativa alla [autenticazione di SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md). Azure AD consente le connessioni al Database SQL di Microsoft Azure e SQL Data Warehouse con le identità federate in Azure AD usando un nome utente e password, autenticazione integrata di Windows o un token di accesso di Azure AD. Il driver PHP per SQL Server offre il supporto parziale per queste funzionalità.

Per usare Azure AD, usare il **Authentication** oppure **AccessToken** parole chiave (che si escludono a vicenda), come illustrato nella tabella seguente. Per informazioni tecniche più dettagliate, consultare [tramite Azure Active Directory con il Driver ODBC](../../connect/odbc/using-azure-active-directory.md).

|Parola chiave|Valori|Descrizione|
|-|-|-|
|**AccessToken**|Non impostato (valore predefinito)|Modalità di autenticazione determinata da altre parole chiave. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md). |
||Una stringa di byte|Il Azure AD Access Token estratti da una risposta OAuth JSON. La stringa di connessione non deve contenere ID utente, password o la parola chiave Authentication (richiede il Driver ODBC versione 17 o versione successiva in Linux o macOS). |
|**Autenticazione**|Non impostato (valore predefinito)|Modalità di autenticazione determinata da altre parole chiave. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|L'autenticazione diretta a un'istanza di SQL Server, che può essere un'istanza di Azure, usando un nome utente e password. Il nome utente e la password deve essere passati nella stringa di connessione usando il **UID** e **PWD** parole chiave. |
||`ActiveDirectoryPassword`|Eseguire l'autenticazione con un'identità di Azure Active Directory usando un nome utente e password. Il nome utente e la password deve essere passati nella stringa di connessione usando il **UID** e **PWD** parole chiave. |
||`ActiveDirectoryMsi`|L'autenticazione usando un'identità gestita assegnato dal sistema o un'identità gestita assegnata dall'utente (Driver ODBC versione 17.3.1.1 richiede o versione successiva). Per una panoramica e le esercitazioni, vedere [What ' s identità gestita per le risorse di Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).|

Il **autenticazione** (parola chiave) riguarda le impostazioni di sicurezza della connessione. Se è impostato nella stringa di connessione, quindi per impostazione predefinita il **Encrypt** parola chiave viene impostata su true, il che significa che il client richiederà la crittografia. Inoltre, il certificato del server verrà da convalidare indipendentemente dall'impostazione di crittografia, a meno che **TrustServerCertificate** è impostata su true (**false** per impostazione predefinita). Questa funzionalità si differenzia dal precedente, meno metodo di accesso sicuro, in cui il certificato del server viene convalidato solo quando specificamente richiesto crittografia nella stringa di connessione.

Quando si usa Azure AD con il driver PHP per SQL Server in Windows, potrebbe essere richiesto di installare il [Microsoft Online Services Sign-In Assistant](https://www.microsoft.com/download/details.aspx?id=41950) (non necessario per ODBC 17 +).

#### <a name="limitations"></a>Limitazioni

In Windows, il driver ODBC sottostante supporta un maggior valore per il **autenticazione** parola chiave **ActiveDirectoryIntegrated**, ma il driver PHP non supportano questo valore su qualsiasi piattaforma.

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>Esempio - connettersi con ActiveDirectoryPassword e SqlPassword

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = array("UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword');

$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=SqlPassword.\n";
    sqlsrv_close($conn);
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = array("Database"=>$azureDatabase,
                        "UID"=>$azureUsername,
                        "PWD"=>$azurePassword,
                        "Authentication"=>'ActiveDirectoryPassword');

$conn = sqlsrv_connect($azureServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    sqlsrv_close($conn);
}

?>
```

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>Esempio - connettersi usando il driver PDO_SQLSRV

```php
<?php
// First connect to a local SQL Server instance by setting Authentication to SqlPassword
$serverName = "myserver.mydomain";

$connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

try {
    $conn = new PDO("sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword);
    echo "Connected successfully with Authentication=SqlPassword.\n";
    $conn = null;
} catch (PDOException $e) {
    echo "Could not connect with Authentication=SqlPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}

// Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
$azureServer = "myazureserver.database.windows.net";
$azureDatabase = "myazuredatabase";
$azureUsername = "myuid";
$azurePassword = "mypassword";
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword);
    echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-azure-ad-access-token"></a>Esempio - connettersi usando Token di accesso di Azure AD

### <a name="sqlsrv-driver"></a>Driver SQLSRV

```php
<?php
// Using an access token to connect: do not use UID or PWD connection options
// Assume $accToken is the valid byte string extracted from an OAuth JSON response
$connectionInfo = array("Database"=>$azureAdDatabase, "AccessToken"=>$accToken);
$conn = sqlsrv_connect($azureAdServer, $connectionInfo);
if ($conn === false) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Azure AD Access Token.\n";
    sqlsrv_close($conn);
}
?>
```

### <a name="pdosqlsrv-driver"></a>Driver PDO_SQLSRV

```php
<?php
try {
    // Using an access token to connect: do not pass in $uid or $pwd
    // Assume $accToken is the valid byte string extracted from an OAuth JSON response
    $connectionInfo = "Database = $azureAdDatabase; AccessToken = $accToken;";
    $conn = new PDO("sqlsrv:server = $azureAdServer; $connectionInfo");
    echo "Connected successfully with Azure AD Access Token\n";
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Azure AD Access Token.\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>Esempio - connettersi usando identità gestite per le risorse di Azure

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>Usando l'identità gestita assegnato dal sistema con il driver SQLSRV

Quando ci si connette utilizzando l'assegnato dal sistema Gestione identità, non usare le opzioni UID e PWD.

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$connectionInfo = array('Database'=>$azureDatabase,
                        'Authentication'=>'ActiveDirectoryMsi');
$conn = sqlsrv_connect($azureServer, $connectionInfo);

if ($conn === false) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    print_r(sqlsrv_errors());
} else {
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (system-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    $stmt = sqlsrv_query($conn, $tsql);
    if ($stmt === false) {
        echo "Failed to run the simple query (system-assigned).\n";
        print_r(sqlsrv_errors());
    } else {
        while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
            echo $row['SQL_VERSION'] . PHP_EOL;
        }

        sqlsrv_free_stmt($stmt);
    }
    
    sqlsrv_close($conn);
}
?>
```

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>Usando l'identità gestito assegnata dall'utente con il driver PDO_SQLSRV

Un'identità gestita assegnata dall'utente viene creata come risorsa di Azure autonoma. Azure crea un'identità nel tenant di Azure AD considerata attendibile dalla sottoscrizione in uso. Dopo aver creato l'identità, l'identità deve appartenere a uno o più istanze del servizio di Azure. Copia il `Object ID` dell'identità e set come utente del nome nella stringa di connessione. 

Pertanto, quando ci si connette utilizzando l'assegnata dall'utente gestito identità, specificare l'ID di oggetto come nome utente, ma omette la password.

```php
<?php

$azureServer = 'myazureserver.database.windows.net';
$azureDatabase = 'myazuredatabase';
$azureUser = '2d68f56e-9547-4dae-aee8-f3g28ab9674x';    // Object ID of the identity
$connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryMsi;";

try {
    $conn = new PDO("sqlsrv:server = $azureServer; $connectionInfo", $azureUser);
    echo "Connected successfully with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    
    $tsql = "SELECT @@Version AS SQL_VERSION";
    
    try {
        $stmt = $conn->query($tsql);
        $result = $stmt->fetchall(PDO::FETCH_ASSOC);
        print_r($result);

        unset($stmt);
    } catch (PDOException $e) {
        echo "Failed to run the simple query (user-assigned).\n";
    }
    unset($conn);
} catch (PDOException $e) {
    echo "Could not connect with Authentication=ActiveDirectoryMsi (user-assigned).\n";
    print_r($e->getMessage());
    echo "\n";
}
?>
```

## <a name="see-also"></a>Vedere anche
[Uso di Azure Active Directory con ODBC Driver](https://docs.microsoft.com/sql/connect/odbc/using-azure-active-directory)

[Che cos'è l'identità gestita per le risorse di Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
