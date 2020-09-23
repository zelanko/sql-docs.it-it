---
title: Confronto delle funzioni di esecuzione
description: Questo argomento elenca le diverse funzioni di esecuzione delle query quando si usano i driver Microsoft per PHP per SQL Server
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33d7ebe420dd59d4f659dbe2ce6c784b49b89d04
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680746"
---
# <a name="comparing-execution-functions"></a>Confronto delle funzioni di esecuzione
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

I [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] offrono diverse opzioni per l'esecuzione di funzioni.  

## <a name="sqlsrv-execution-functions"></a>Funzioni di esecuzione SQLSRV  
Se si usa il driver SQLSRV, usare [sqlsrv_query](../../connect/php/sqlsrv-query.md) per eseguire una query singola e [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) con [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) per eseguire un'istruzione preparata più volte con valori di parametro diversi per ogni esecuzione.  

## <a name="pdo_sqlsrv-execution-functions"></a>Funzioni di esecuzione PDO_SQLSRV 
Se si usa il driver PDO_SQLSRV, è possibile eseguire una query con una delle funzioni seguenti:  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) e [PDOStatement::execute](../../connect/php/pdostatement-execute.md).  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Guida di riferimento del driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Guida alla programmazione per i driver Microsoft per PHP per SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
