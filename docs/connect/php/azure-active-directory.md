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
manager: v-mabarw
ms.openlocfilehash: 8712681a244e969d230b0b7099acd4aa56334f11
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265184"
---
# <a name="connect-using-azure-active-directory-authentication"></a>Connessione con l'autenticazione di Azure Active Directory
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) (Azure AD) è una tecnologia di gestione degli ID utente centrale che opera in alternativa all' [autenticazione SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md). Azure AD consente le connessioni ai database SQL di Microsoft Azure e SQL Data Warehouse con le identità federate in Azure AD usando un nome utente e una password, l'autenticazione integrata di Windows o un token di accesso Azure AD. I driver PHP per SQL Server offrono un supporto parziale per queste funzionalità.

Per utilizzare Azure AD, utilizzare le parole chiave **Authentication** o **AccessToken** (si escludono a vicenda), come illustrato nella tabella seguente. Per informazioni più tecniche, vedere [utilizzo di Azure Active Directory con il driver ODBC](../../connect/odbc/using-azure-active-directory.md).

|Parola chiave|Valori|Descrizione|
|-|-|-|
|**AccessToken**|Non impostato (impostazione predefinita)|Modalità di autenticazione determinata da altre parole chiave. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md). |
||Una stringa di byte|Il token di accesso Azure AD Estratto da una risposta JSON OAuth. La stringa di connessione non deve contenere l'ID utente, la password o la parola chiave di autenticazione (richiede il driver ODBC versione 17 o successiva in Linux o macOS). |
|**Autenticazione**|Non impostato (impostazione predefinita)|Modalità di autenticazione determinata da altre parole chiave. Per altre informazioni, vedere [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|Eseguire l'autenticazione direttamente in un'istanza di SQL Server (che potrebbe essere un'istanza di Azure) usando un nome utente e una password. Il nome utente e la password devono essere passati nella stringa di connessione usando le parole chiave **UID** e **pwd** . |
||`ActiveDirectoryPassword`|Eseguire l'autenticazione con un'identità Azure Active Directory usando un nome utente e una password. Il nome utente e la password devono essere passati nella stringa di connessione usando le parole chiave **UID** e **pwd** . |
||`ActiveDirectoryMsi`|Eseguire l'autenticazione tramite un'identità gestita assegnata dal sistema o un'identità gestita assegnata dall'utente (richiede il driver ODBC versione 17.3.1.1 o successiva). Per una panoramica ed esercitazioni, vedere informazioni sulle [identità gestite per le risorse di Azure](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).|

La parola chiave **Authentication** influiscono sulle impostazioni di sicurezza della connessione. Se è impostato nella stringa di connessione, per impostazione predefinita la parola chiave **Encrypt** è impostata su true, il che significa che il client richiede la crittografia. Inoltre, il certificato del server verrà convalidato indipendentemente dall'impostazione della crittografia, a meno che **TrustServerCertificate** non sia impostato su true (**false** per impostazione predefinita). Questa funzionalità si distingue dal metodo di accesso precedente, meno sicuro, in cui il certificato server viene convalidato solo quando la crittografia è richiesta in modo specifico nella stringa di connessione.

Quando si usa Azure AD con i driver PHP per SQL Server in Windows, è possibile che venga richiesto di installare l'assistente per l' [accesso ai Microsoft Online Services](https://www.microsoft.com/download/details.aspx?id=41950) (non necessario per ODBC 17 +).

#### <a name="limitations"></a>Limitazioni

In Windows, il driver ODBC sottostante supporta un valore maggiore per la parola chiave **Authentication** , **ActiveDirectoryIntegrated**, ma i driver php non supportano questo valore in nessuna piattaforma.

## <a name="example---connect-using-sqlpassword-and-activedirectorypassword"></a>Esempio: connettersi usando sqlpassword e ActiveDirectoryPassword

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

## <a name="example---connect-using-the-pdosqlsrv-driver"></a>Esempio: connettersi usando il driver PDO_SQLSRV

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

## <a name="example---connect-using-azure-ad-access-token"></a>Esempio: connettersi con Azure AD token di accesso

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

## <a name="example---connect-using-managed-identities-for-azure-resources"></a>Esempio: connettersi usando identità gestite per le risorse di Azure

### <a name="using-the-system-assigned-managed-identity-with-sqlsrv-driver"></a>Uso dell'identità gestita assegnata dal sistema con il driver SQLSRV

Quando ci si connette usando l'identità gestita assegnata dal sistema, non usare le opzioni UID o PWD.

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

### <a name="using-the-user-assigned-managed-identity-with-pdosqlsrv-driver"></a>Uso dell'identità gestita assegnata dall'utente con il driver PDO_SQLSRV

Un'identità gestita assegnata dall'utente viene creata come risorsa di Azure autonoma. Azure crea un'identità nel tenant di Azure AD considerata attendibile dalla sottoscrizione in uso. Dopo la creazione dell'identità, l'identità può essere assegnata a una o più istanze del servizio di Azure. Copiare l' `Object ID` oggetto di questa identità e impostarlo come nome utente nella stringa di connessione. 

Pertanto, quando ci si connette utilizzando l'identità gestita assegnata dall'utente, fornire l'ID oggetto come nome utente, ma omettere la password.

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

[Che cosa sono le identità gestite per le risorse di Azure?](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
