---
title: PDOStatement::errorCode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4161abec-c12b-444e-9de5-f1dac7b3e0e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1092f1736c4d217a3e875a7df8060b0f722fd080
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80907912"
---
# <a name="pdostatementerrorcode"></a>PDOStatement::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera il valore SQLSTATE dell'operazione più recente per l'oggetto istruzione del database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
string PDOStatement::errorCode();  
```  
  
## <a name="return-value"></a>Valore restituito  
Restituisce un valore SQLSTATE di cinque caratteri sotto forma di stringa oppure NULL se non esiste alcuna operazione nell'handle di istruzione.  
  
## <a name="remarks"></a>Osservazioni  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
In questo esempio viene illustrata una query SQL che contiene un errore.  Viene quindi visualizzato il codice di errore.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print $stmt->errorCode();  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
