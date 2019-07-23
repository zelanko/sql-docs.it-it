---
title: sqlsrv_field_metadata | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_field_metadata
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_field_metadata
- sqlsrv_field_metadata
ms.assetid: c02f6942-0484-4567-a78e-fe8aa2053536
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f378c080472ed9004311d0cc73724e2a8c5e263
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992709"
---
# <a name="sqlsrvfieldmetadata"></a>sqlsrv_field_metadata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera i metadati per i campi di un'istruzione preparata. Per informazioni sulla preparazione di un'istruzione, vedere [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md). Si noti che **sqlsrv_field_metadata** può essere chiamato in qualsiasi istruzione preparata, pre-esecuzione o post-esecuzione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sqlsrv_field_metadata( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parametri  
*$stmt*: risorsa di istruzione per la quale sono richiesti i metadati del campo.  
  
## <a name="return-value"></a>Valore restituito  
Una **matrice** di matrici oppure **false**. La matrice è costituita da una singola matrice per ogni campo nel set di risultati. Ogni matrice secondaria include le chiavi elencate nella tabella seguente. Se si verifica un errore durante il recupero dei metadati del campo, viene restituito **false** .  
  
|Key|Descrizione|  
|-------|---------------|  
|nome|Nome della colonna a cui corrisponde il campo.|  
|Tipo|Valore numerico che corrisponde a un tipo SQL.|  
|Dimensione|Numero di caratteri per i campi di tipo carattere (char(n), varchar(n), nchar(n), nvarchar(n), XML). Numero di byte per i campi di tipo binario (binary(n), varbinary(n), tipo definito dall'utente). **NULL** per altri tipi di dati di SQL Server.|  
|Precisione|Precisione per i tipi di precisione delle variabili (real, numeric, decimal, datetime2, datetimeoffset e time). **NULL** per altri tipi di dati di SQL Server.|  
|Scala|Scala per i tipi di scala delle variabili (numeric, decimal, datetime2, datetimeoffset e time). **NULL** per altri tipi di dati di SQL Server.|  
|Ammette valori Null|Valore enumerato che indica se la colonna è nullable (**SQLSRV_NULLABLE_YES**), non è nullable (**SQLSRV_NULLABLE_NO**) o non è noto se la colonna è nullable (**SQLSRV_NULLABLE_UNKNOWN**).|  
  
Nella tabella seguente vengono fornite altre informazioni sulle chiavi di ogni matrice secondaria (per informazioni sui tipi, vedere la documentazione di SQL Server):  
  
|Tipo di dati di SQL Server 2008|Tipo|Precisione min/max|Scala min/max|Dimensione|  
|-----------------------------|--------|----------------------|------------------|--------|  
|BIGINT|SQL_BIGINT (-5)|||8|  
|BINARY|SQL_BINARY (-2)|||0 < *n* < 8000 <sup>1</sup>|  
|bit|SQL_BIT (-7)||||  
|char|SQL_CHAR (1)|||0 < *n* < 8000 <sup>1</sup>|  
|Data|SQL_TYPE_DATE (91)|10/10|0/0||  
|DATETIME|SQL_TYPE_TIMESTAMP (93)|23/23|3/3||  
|datetime2|SQL_TYPE_TIMESTAMP (93)|19/27|0/7||  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET (-155)|26/34|0/7||  
|Decimal|SQL_DECIMAL (3)|1/38|0/valore precisione||  
|FLOAT|SQL_FLOAT (6)|4/8|||  
|image|SQL_LONGVARBINARY (-4)|||2 GB|  
|INT|SQL_INTEGER (4)||||  
|money|SQL_DECIMAL (3)|19/19|4/4||  
|NCHAR|SQL_WCHAR (-8)|||0 < *n* < 4000 <sup>1</sup>|  
|ntext|SQL_WLONGVARCHAR (-10)|||1 GB|  
|NUMERIC|SQL_NUMERIC (2)|1/38|0/valore precisione||  
|NVARCHAR|SQL_WVARCHAR (-9)|||0 < *n* < 4000 <sup>1</sup>|  
|REAL|SQL_REAL (7)|4/4|||  
|smalldatetime|SQL_TYPE_TIMESTAMP (93)|16/16|0/0||  
|SMALLINT|SQL_SMALLINT (5)|||2 byte|  
|Smallmoney|SQL_DECIMAL (3)|10/10|4/4||  
|text|SQL_LONGVARCHAR (-1)|||2 GB|  
|time|SQL_SS_TIME2 (-154)|8/16|0/7||  
|TIMESTAMP|SQL_BINARY (-2)|||8 byte|  
|TINYINT|SQL_TINYINT (-6)|||1 byte|  
|udt|SQL_SS_UDT (-151)|||variabile|  
|UNIQUEIDENTIFIER|SQL_GUID (-11)|||16|  
|varbinary|SQL_VARBINARY (-3)|||0 < *n* < 8000 <sup>1</sup>|  
|varchar|SQL_VARCHAR (12)|||0 < *n* < 8000 <sup>1</sup>|  
|xml|SQL_SS_XML (-152)|||0|  
  
(1) Zero (0) indica che la dimensione massima è consentita.  
  
La chiave nullable può essere yes o no.  
  
## <a name="example"></a>Esempio  
Nell'esempio seguente viene creata una risorsa di istruzione, quindi vengono recuperati e visualizzati i metadati dei campi. Nell'esempio si presuppone che SQL Server e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando si esegue l'esempio dalla riga di comando, tutto l'output viene scritto nel browser.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Prepare the statement. */  
$tsql = "SELECT ReviewerName, Comments FROM Production.ProductReview";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
  
/* Get and display field metadata. */  
foreach( sqlsrv_field_metadata( $stmt) as $fieldMetadata)  
{  
      foreach( $fieldMetadata as $name => $value)  
      {  
           echo "$name: $value\n";  
      }  
      echo "\n";  
}  
  
/* Note: sqlsrv_field_metadata can be called on any statement  
resource, pre- or post-execution. */  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

[Informazioni sugli esempi di codice nella documentazione](../../connect/php/about-code-examples-in-the-documentation.md)  
  
