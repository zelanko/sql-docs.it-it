---
title: PDOStatement::getAttribute | Microsoft Docs
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 014f679480caaabd42863d2551cfa4c25bbe94d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992984"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera il valore di un attributo PDOStatement predefinito o di un attributo personalizzato del driver.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>Parametri  
$*attribute*: numero intero, una delle costanti PDO::ATTR_* o PDO::SQLSRV_ATTR_\*. Gli attributi supportati sono gli attributi che è possibile impostare con [PDOStatement:: SetAttribute](../../connect/php/pdostatement-setattribute.md), DOP:: SQLSRV_ATTR_DIRECT_QUERY (per altre informazioni, vedere [esecuzione di istruzioni dirette ed esecuzione di istruzioni preparate nel driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)), DOP: : ATTR_CURSOR e DOP:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE. per ulteriori informazioni, vedere [tipi di cursore (driver PDO_SQLSRV)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).  
  
## <a name="return-value"></a>Valore restituito  
In caso di esito positivo, restituisce un valore misto per un attributo predefinito del PDO o per un attributo personalizzato del driver. In caso di errore, restituisce Null.  
  
## <a name="remarks"></a>Remarks  
Per un esempio, vedere [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) .  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
