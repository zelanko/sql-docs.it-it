---
title: PDOStatement::getColumnMeta | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 57bc8d1e6112a64f99864ce08f7adb81db6df781
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799115"
---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera i metadati per una colonna.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>Parametri  
*$conn*: (intero) numero in base zero della colonna di cui si vuole recuperare i metadati.  
  
## <a name="return-value"></a>Valore restituito  
Una matrice associativa (chiave e valore) che contiene i metadati per la colonna. Vedere la sezione Osservazioni per una descrizione dei campi nella matrice.  
  
## <a name="remarks"></a>Remarks  
Nella tabella seguente sono descritti i campi della matrice restituita da getColumnMeta.  
  
|NAME|VALUES|  
|--------|----------|  
|native_type|Specifica il tipo PHP per la colonna. Sempre stringa.|  
|driver:decl_type|Specifica il tipo SQL usato per rappresentare il valore della colonna nel database. Se la colonna nel set di risultati è il risultato di una funzione, questo valore non viene restituito da PDOStatement::getColumnMeta.|  
|flags|Specifica i flag impostati per la colonna. Sempre 0.|  
|NAME|Specifica il nome della colonna nel database.|  
|table|Specifica il nome della tabella contenente la colonna nel database. Sempre vuoto.|  
|len|Specifica la lunghezza della colonna.|  
|precisione|Specifica la precisione numerica della colonna.|  
|pdo_type|Specifica il tipo della colonna come rappresentato dalle costanti PDO::PARAM_*. Sempre PDO::PARAM_STR (2).|  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$stmt = $conn->query("select * from Person.ContactType");  
$metadata = $stmt->getColumnMeta(2);  
var_dump($metadata);  
  
print $metadata['sqlsrv:decl_type'] . "\n";  
print $metadata['native_type'] . "\n";  
print $metadata['name'];  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
