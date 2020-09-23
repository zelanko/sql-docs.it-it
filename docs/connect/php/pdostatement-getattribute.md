---
title: PDOStatement::getAttribute
description: Informazioni di riferimento sulle API per la funzione PDOStatement::getAttribute nel driver Microsoft PDO_SQLSRV per PHP per SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07cc46717dafe973dee05647f1d08134d858c58e
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646751"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera il valore di un attributo PDOStatement predefinito o di un attributo personalizzato del driver.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>Parametri  
$*attribute*: un Integer, una delle costanti PDO::ATTR_* o PDO::SQLSRV_ATTR_\*. Sono supportati gli attributi che è possibile impostare con [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), PDO::SQLSRV_ATTR_DIRECT_QUERY (per altre informazioni, vedere [Esecuzione di istruzioni diretta e preparata nel driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)), PDO::ATTR_CURSOR e PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE (per altre informazioni, vedere [Tipi di cursore (driver PDO_SQLSRV)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)).  
  
## <a name="return-value"></a>Valore restituito  
In caso di esito positivo, restituisce un valore misto per un attributo predefinito del PDO o per un attributo personalizzato del driver. In caso di errore, restituisce Null.  
  
## <a name="remarks"></a>Osservazioni  
Per un esempio, vedere [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) .  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="see-also"></a>Vedere anche  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
