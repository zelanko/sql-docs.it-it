---
title: PDOStatement::columnCount
description: Informazioni di riferimento sulle API per la funzione PDOStatement::columnCount nel driver Microsoft PDO_SQLSRV per PHP per SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8d89a568-0c7c-40dd-9f54-db7313600df3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c1cfa12ea94a0ffd952473f13782e2bc49c4810
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645274"
---
# <a name="pdostatementcolumncount"></a>PDOStatement::columnCount
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Restituisce il numero di colonne in un set di risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int PDOStatement::columnCount ();  
```  
  
## <a name="return-value"></a>Valore restituito  
Restituisce il numero di colonne in un set di risultati. Restituisce zero se il set di risultati è vuoto.  
  
## <a name="remarks"></a>Osservazioni  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
print $stmt->columnCount();   // 0  
  
echo "\n";  
$stmt->execute();  
print $stmt->columnCount();  
  
echo "\n";  
$stmt = $conn->query("select * from HumanResources.Department");  
print $stmt->columnCount();  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
