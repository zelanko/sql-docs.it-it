---
title: PDOStatement::fetchObject
description: Informazioni di riferimento sulle API per la funzione PDOStatement::fetchObject nel driver Microsoft PDO_SQLSRV per PHP per SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 71ad1932-cab3-4c29-8950-f5e82547d3b5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 459505e3c00a85b6e879e89a3a3b21fb8b3fcf9c
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645871"
---
# <a name="pdostatementfetchobject"></a>PDOStatement::fetchObject
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera la riga seguente sotto forma di oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
mixed PDOStatement::fetchObject([ $class_name[,$ctor_args ]] )  
```  
  
#### <a name="parameters"></a>Parametri  
$*class_name*: stringa facoltativa che specifica il nome della classe da creare. Il valore predefinito è stdClass.  
  
$*ctor_args*: matrice facoltativa con argomenti per un costruttore di classe personalizzata.  
  
## <a name="return-value"></a>Valore restituito  
In caso di esito positivo, restituisce un oggetto con un'istanza della classe. Le proprietà sono mappate sulle colonne. Restituisce false in caso di errore.  
  
## <a name="remarks"></a>Osservazioni  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchObject();  
   print $result->Name;  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
