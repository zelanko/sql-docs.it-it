---
title: sqlsrv_num_rows | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- API Reference, sqlsrv_num_rows
- sqlsrv_num_rows
ms.assetid: c832210e-bb2a-47b5-a505-160b02d1d95e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e26c0e06ea9a71bdb6b9e39126e646d22ad40ea2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "68014981"
---
# <a name="sqlsrv_num_rows"></a>sqlsrv_num_rows
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Visualizza il numero di righe di un set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sqlsrv_num_rows( resource $stmt )  
```  
  
#### <a name="parameters"></a>Parametri  
*$stmt*: set di risultati per cui contare le righe.  
  
## <a name="return-value"></a>Valore restituito  
**false** se si è verificato un errore durante il calcolo del numero di righe. In caso contrario, restituisce il numero di righe del set di risultati.  
  
## <a name="remarks"></a>Osservazioni  
sqlsrv_num_rows richiede un cursore lato client, statico o keyset e restituisce **false** se si usa un cursore forward o un cursore dinamico. Un cursore forward è il valore predefinito. Per altre informazioni sui cursori, vedere [sqlsrv_query](../../connect/php/sqlsrv-query.md) e [Tipi di cursore &#40;driver SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md).  
  
## <a name="example"></a>Esempio  
  
```  
<?php  
   $server = "server_name";  
   $conn = sqlsrv_connect( $server, array( 'Database' => 'Northwind' ) );  
  
   $stmt = sqlsrv_query( $conn, "select * from orders where CustomerID = 'VINET'" , array(), array( "Scrollable" => SQLSRV_CURSOR_KEYSET ));  
  
   $row_count = sqlsrv_num_rows( $stmt );  
  
   if ($row_count === false)  
      echo "\nerror\n";  
   else if ($row_count >=0)  
      echo "\n$row_count\n";  
?>  
```  
  
L'esempio seguente mostra che in presenza di più set di risultati (query batch), il numero di righe è disponibile solo quando si usa un cursore lato client.  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
$tsql = "select * from HumanResources.Department";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
// works  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
  
// fails  
// $stmt = sqlsrv_query($conn, $tsql);  
// $stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"forward"));  
// $stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"static"));  
// $stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"keyset"));  
// $stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"dynamic"));  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
