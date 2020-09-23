---
title: PDOStatement::errorInfo
description: Informazioni di riferimento sulle API per la funzione PDOStatement::errorInfo nel driver Microsoft PDO_SQLSRV per PHP per SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e45bebe8-ea4c-49b6-93db-cf1ae65f530c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e05d43caec418257bb107dcb40aa918e406538f
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645212"
---
# <a name="pdostatementerrorinfo"></a>PDOStatement::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera informazioni dettagliate sugli errori dell'ultima operazione dell'handle di istruzione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
array PDOStatement::errorInfo();  
```  
  
## <a name="return-value"></a>Valore restituito  
Una matrice di informazioni sugli errori dell'ultima operazione dell'handle di istruzione. La matrice include i campi seguenti:  
  
-   Codice di errore SQLSTATE  
  
-   Codice di errore specifico del driver.  
  
-   Messaggio di errore specifico del driver.  
  
Se non si verificano errori o se SQLSTATE non è impostata, i campi specifici del driver saranno NULL.  
  
## <a name="remarks"></a>Osservazioni  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
In questo esempio, l'istruzione SQL presenta un errore che verrà quindi restituito.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print_r ($stmt->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
