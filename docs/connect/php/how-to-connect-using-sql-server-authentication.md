---
title: "Procedura: Connessione con l'autenticazione di SQL Server | Microsoft Docs"
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, SQL Server Authentication
ms.assetid: 8d298830-3186-47e7-aef6-586b457901c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7d894b48fc6ec82450c42599f13725f0cd8ee1a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993554"
---
# <a name="how-to-connect-using-sql-server-authentication"></a>Procedura: Connessione con l'autenticazione di SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] supporta l'autenticazione di SQL Server quando ci si connette a SQL Server.  
  
L'autenticazione di SQL Server deve essere usata solo quando l'autenticazione di Windows non è possibile. Per informazioni sulla connessione con l'autenticazione di Windows, vedere [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Quando si usa l'autenticazione di SQL Server per la connessione a SQL Server è necessario considerare i seguenti punti:  
  
-   Nel server deve essere abilitata l'autenticazione in modalità mista di SQL Server.  
  
-   L'ID utente e la password (gli attributi di connessione *UID* e *PWD* nel driver SQLSRV) devono essere impostati quando si tenta di stabilire una connessione. L'ID utente e password devono corrispondere a un utente e a una password di SQL Server validi.  
  
> [!NOTE]  
> Le password che contengono una parentesi graffa di chiusura (}) devono essere precedute da una seconda parentesi graffa di chiusura come carattere di escape. Ad esempio, se la password di SQL Server è "pass}word", il valore dell'attributo di connessione *PWD* deve essere impostato su "pass}}word".  
  
Quando si usa l'autenticazione di SQL Server per la connessione a SQL Server è necessario adottare le precauzioni seguenti:  
  
-   Proteggere (crittografare) le credenziali trasmesse in rete dal server Web al database. Le credenziali vengono crittografate per impostazione predefinita a partire da SQL Server 2005. Per maggiore sicurezza, impostare l'attributo di connessione Encrypt su "on" per crittografare tutti i dati inviati al server.  
  
> [!NOTE]  
> Impostare l'attributo di connessione Encrypt su "on" può rallentare le prestazioni poiché la crittografia dei dati può richiedere notevoli risorse di elaborazione.  
  
-   Negli script PHP non includere valori per gli attributi di connessione *UID* e *PWD* in testo normale. Questi valori devono essere archiviati in una directory specifica dell'applicazione con autorizzazioni limitate appropriate.  
  
-   Evitare l'uso dell'account *sa* . Eseguire il mapping dell'applicazione a un utente del database che dispone dei privilegi desiderati e usare una password complessa.  
  
> [!NOTE]  
> Quando si stabilisce una connessione è possibile impostare altri attributi di connessione oltre a ID utente e password. Per un elenco completo degli attributi di connessione supportati, vedere [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="example"></a>Esempio  
L'esempio seguente usa il driver SQLSRV con l'autenticazione di SQL Server per connettersi a un'istanza locale di SQL Server. I valori per gli attributi di connessione *UID* e *PWD* richiesti sono ricavati da file di testo specifici dell'applicazione, *uid.txt* e *pwd.txt*, nella directory *C:\AppData*. Dopo aver stabilito la connessione, viene eseguita una query nel server per verificare l'accesso dell'utente.  
  
Nell'esempio si presuppone che SQL Server e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando l'esempio viene eseguito dal browser, tutto l'output viene scritto nel browser.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
  
/* Get UID and PWD from application-specific files.  */  
$uid = file_get_contents("C:\AppData\uid.txt");  
$pwd = file_get_contents("C:\AppData\pwd.txt");  
$connectionInfo = array( "UID"=>$uid,  
                         "PWD"=>$pwd,  
                         "Database"=>"AdventureWorks");  
  
/* Connect using SQL Server Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Esempio  
Questo esempio usa il driver PDO_SQLSRV per illustrare la procedura di connessione con l'autenticazione di SQL Server.  
  
```  
<?php  
   $serverName = "(local)";   
   $database = "AdventureWorks";  
  
   // Get UID and PWD from application-specific files.   
   $uid = file_get_contents("C:\AppData\uid.txt");  
   $pwd = file_get_contents("C:\AppData\pwd.txt");  
  
   try {  
      $conn = new PDO( "sqlsrv:server=$serverName;Database = $database", $uid, $pwd);   
      $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
   }  
  
   catch( PDOException $e ) {  
      die( "Error connecting to SQL Server" );   
   }  
  
   echo "Connected to SQL Server\n";  
  
   $query = 'select * from Person.ContactType';   
   $stmt = $conn->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
      print_r( $row );   
   }  
  
   // Free statement and connection resources.   
   $stmt = null;   
   $conn = null;   
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Procedura: Connessione con l'autenticazione di SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)

[Guida alla programmazione per i driver Microsoft per PHP per SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Informazioni sugli esempi di codice nella documentazione](../../connect/php/about-code-examples-in-the-documentation.md)

[SUSER_SNAME (Transact-SQL)](../../t-sql/functions/suser-sname-transact-sql.md)

[Procedura: Creare un account di accesso di SQL Server](../../relational-databases/security/authentication-access/create-a-login.md)

[Procedura: Creare un utente del database](../../relational-databases/security/authentication-access/create-a-database-user.md)

[Gestione di utenti, ruoli e account di accesso](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[Separazione tra schema e utente](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[GRANT - autorizzazioni per oggetti (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
