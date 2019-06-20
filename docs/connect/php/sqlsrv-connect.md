---
title: sqlsrv_connect | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_connect
apitype: NA
helpviewer_keywords:
- connecting to the server
- API Reference, sqlsrv_connect
- connection pooling support
- sqlsrv_connect
ms.assetid: 37836b49-258e-45ce-9549-b8bd85d6952d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a5cb52f4e27ea933b4988c3c8f2daee6fb90147d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796897"
---
# <a name="sqlsrvconnect"></a>sqlsrv_connect
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Crea una risorsa di connessione e apre una connessione. Per impostazione predefinita, viene eseguito un tentativo di connessione usando l'autenticazione di Windows.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sqlsrv_connect( string $serverName [, array $connectionInfo])  
```  
  
#### <a name="parameters"></a>Parametri  
*$serverName*: stringa che specifica il nome del server con cui viene stabilita la connessione. Nella stringa può essere incluso un nome di istanza (ad esempio, "myServer\instanceName") o un numero di porta (ad esempio, "myServer, 1521"). Per una descrizione completa delle opzioni disponibili per questo parametro, vedere la parola chiave Server nella sezione Parole chiave delle stringhe di connessione per il driver ODBC di [Uso delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
A partire dalla versione 3.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è inoltre possibile specificare un'istanza di LocalDB con `"(localdb)\instancename"`. Per altre informazioni, vedere [supporto per LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).  
  
In più, a partire dalla versione 3.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], è possibile specificare un nome di rete virtuale per connettersi a un gruppo di disponibilità AlwaysOn. Per altre informazioni sulle [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Sopporto [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vedere [supporto per la disponibilità elevata, ripristino di emergenza](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).  
  
*$connectionInfo* [facoltativo]: una **matrice** associativa che contiene attributi di connessione (ad esempio, **array**("Database" => "AdventureWorks")). Vedere [Connection Options](../../connect/php/connection-options.md) per un elenco delle chiavi supportate per la matrice.  
  
## <a name="return-value"></a>Valore restituito  
Una risorsa di connessione PHP. Se non è possibile creare e aprire correttamente una connessione, verrà restituito **false** .  
  
## <a name="remarks"></a>Remarks  
Se i valori per le chiavi *UID* e *PWD* non sono specificati nel parametro *$connectionInfo* facoltativo, verrà eseguito un tentativo di connessione viene usando l'autenticazione di Windows. Per altre informazioni sulla connessione al server, vedere [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md) e [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md).  
  
## <a name="example"></a>Esempio  
L'esempio seguente permette di creare e aprire una connessione usando l'autenticazione di Windows. Nell'esempio si presuppone che SQL Server e il database [AdventureWorks](https://www.codeplex.com/SqlServerSamples) siano installati nel computer locale. Quando si esegue l'esempio dalla riga di comando, tutto l'output viene scritto nel browser.  
  
```  
<?php  
/*  
Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. To connect using  
SQL Server Authentication, set values for the "UID" and "PWD"  
 attributes in the $connectionInfo parameter. For example:  
$connectionInfo = array("UID" => $uid, "PWD" => $pwd, "Database"=>"AdventureWorks");  
*/  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if( $conn )  
{  
     echo "Connection established.\n";  
}  
else  
{  
     echo "Connection could not be established.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Connecting to the Server](../../connect/php/connecting-to-the-server.md)

[Informazioni sugli esempi di codice nella documentazione](../../connect/php/about-code-examples-in-the-documentation.md)  
  
