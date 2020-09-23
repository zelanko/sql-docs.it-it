---
title: PDOStatement::bindColumn
description: Informazioni di riferimento sulle API per la funzione PDOStatement::bindColumn nel driver Microsoft PDO_SQLSRV per PHP per SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbdcea53-d23d-4769-89a0-95c7cf4d5390
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd62d4436c5718801dee7b273773b87f6b47eec6
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645881"
---
# <a name="pdostatementbindcolumn"></a>PDOStatement::bindColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Associa una variabile a una colonna in un set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
bool PDOStatement::bindColumn($column, &$param[, $type[, $maxLen[, $driverdata ]]] );  
```  
  
#### <a name="parameters"></a>Parametri  
$*column*: numero (misto) della colonna (indice in base 1) o nome della colonna nel set di risultati.  
  
&$*param*: nome (misto) della variabile PHP a cui verrà associata la colonna.  
  
$*type*: tipo di dati facoltativo del parametro, rappresentato da una costante PDO::PARAM_*.  
  
$*maxLen*: intero facoltativo, non usato dai driver Microsoft per PHP per SQL Server.  
  
$*driverdata*: parametro o parametri misti facoltativi per il driver. Ad esempio, è possibile specificare PDO::SQLSRV_ENCODING_UTF8 per associare la colonna a una variabile come stringa codificata in UTF-8.  
  
## <a name="return-value"></a>Valore restituito  
TRUE se ha esito positivo; in caso contrario, FALSE.  
  
## <a name="remarks"></a>Osservazioni  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
Questo esempio mostra l'associazione di una variabile a una colonna in un set di risultati.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "SELECT Title, FirstName, EmailAddress FROM Person.Contact where LastName = 'Estes'";  
$stmt = $conn->prepare($query);  
$stmt->execute();  
  
$stmt->bindColumn('EmailAddress', $email);  
while ( $row = $stmt->fetch( PDO::FETCH_BOUND ) ){  
   echo "$email\n";  
}  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
