---
title: PDO::errorCode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9846867cfc6bd50568440c5c66711457754af50c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993280"
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode recupera il valore SQLSTATE dell'ultima operazione dell'handle di database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>Valore restituito  
PDO::errorCode restituisce un valore SQLSTATE di cinque caratteri sotto forma di stringa oppure NULL se non sono state eseguite operazioni nell'handle di database.  
  
## <a name="remarks"></a>Remarks  
PDO::errorCode nel driver PDO_SQLSRV restituisce avvisi relativi ad alcune operazioni riuscite. Ad esempio, per una connessione riuscita, PDO::errorCode restituisce "01000", che indica SQL_SUCCESS_WITH_INFO.  
  
PDO::errorCode recupera i codici di errore solo per le operazioni eseguite direttamente sul database. Se si crea un'istanza di PDOStatement tramite PDO::prepare o PDO::query e viene generato un errore per l'oggetto istruzione, PDO::errorCode non recupera tale errore. Sarà necessario chiamare PDOStatement::errorCode per recuperare il codice di errore relativo a un'operazione eseguita su un particolare oggetto istruzione.  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
In questo esempio il nome della colonna errato (`Cityx` anziché `City`) causa un errore, che viene quindi segnalato.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
