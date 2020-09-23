---
title: PDO::errorInfo
description: Informazioni di riferimento sulle API per la funzione PDO::errorInfo nel driver Microsoft PDO_SQLSRV per PHP per SQL Server.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9d5481d5-13bc-4388-b3aa-78676c0fc709
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 579b516481c6349396a342e2c98200d70d731d25
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646171"
---
# <a name="pdoerrorinfo"></a>PDO::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera informazioni dettagliate sugli errori dell'ultima operazione dell'handle di database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
array PDO::errorInfo();  
```  
  
## <a name="return-value"></a>Valore restituito  
Una matrice di informazioni sugli errori dell'ultima operazione dell'handle di database. La matrice include i campi seguenti:  
  
-   Codice di errore SQLSTATE.  
  
-   Codice di errore specifico del driver.  
  
-   Messaggio di errore specifico del driver.  
  
Se non si verificano errori o se il valore di SQLSTATE non è impostato, i campi specifici del driver sono NULL.  
  
## <a name="remarks"></a>Osservazioni  
PDO::errorInfo recupera solo le informazioni sugli errori per le operazioni eseguite direttamente sul database. Usare PDOStatement::errorInfo quando viene creata un'istanza di PDOStatement mediante PDO::prepare o PDO::query.  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
In questo esempio il nome della colonna errato (`Cityx` anziché `City`) causa un errore, che viene quindi segnalato.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
echo "\n";  
print_r ($conn->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
