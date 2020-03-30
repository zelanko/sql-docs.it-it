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
ms.openlocfilehash: 11da2b4eca130eafe93a01315aaa1f6d9919632c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015046"
---
# <a name="sqlsrv_connect"></a>sqlsrv_connect
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Crea una risorsa di connessione e apre una connessione. Per impostazione predefinita, viene eseguito un tentativo di connessione usando l'autenticazione di Windows.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sqlsrv_connect( string $serverName [, array $connectionInfo])  
```  
  
#### <a name="parameters"></a>Parametri  
*$serverName*: stringa che specifica il nome del server con cui viene stabilita la connessione. Nella stringa può essere incluso un nome di istanza (ad esempio, "myServer\instanceName") o un numero di porta (ad esempio, "myServer, 1521"). Per una descrizione completa delle opzioni disponibili per questo parametro, vedere la parola chiave Server nella sezione Parole chiave delle stringhe di connessione per il driver ODBC di [Uso delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
A partire dalla versione 3.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è inoltre possibile specificare un'istanza di LocalDB con `"(localdb)\instancename"`. Per altre informazioni, vedere [Supporto per Local DB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).  
  
In più, a partire dalla versione 3.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], è possibile specificare un nome di rete virtuale per connettersi a un gruppo di disponibilità AlwaysOn. Per altre informazioni sul supporto di [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] per [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vedere [Supporto per disponibilità elevata e ripristino di emergenza](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).  
  
*$connectionInfo* [facoltativo]: una **matrice** associativa che contiene attributi di connessione (ad esempio, **array**("Database" => "AdventureWorks")). Vedere [Connection Options](../../connect/php/connection-options.md) per un elenco delle chiavi supportate per la matrice.  
  
## <a name="return-value"></a>Valore restituito  
Una risorsa di connessione PHP. Se non è possibile creare e aprire correttamente una connessione, verrà restituito **false** .  
  
## <a name="remarks"></a>Osservazioni  
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

[Connessione al server](../../connect/php/connecting-to-the-server.md)

[Informazioni sugli esempi di codice nella documentazione](../../connect/php/about-code-examples-in-the-documentation.md)  
  
