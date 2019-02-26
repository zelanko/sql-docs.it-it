---
title: Diretta - istruzione preparata Driver PDO_SQLSRV esecuzione istruzione | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 005a2c4b34c9aae2cfdfe4663cbfcbe06a68b81a
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676109"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>Esecuzione di istruzioni diretta e preparata nel driver PDO_SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Questo argomento illustra come usare l'attributo PDO::SQLSRV_ATTR_DIRECT_QUERY per specificare l'esecuzione diretta delle istruzioni anziché l'impostazione predefinita, che corrisponde all'esecuzione di istruzioni preparate. Utilizzo di un'istruzione preparata può comportare prestazioni migliori se l'istruzione viene eseguita più volte utilizzando l'associazione di parametro.  
  
## <a name="remarks"></a>Remarks  
Se si desidera inviare una [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione direttamente al server senza preparazione dell'istruzione dal driver, è possibile impostare l'attributo PDO:: sqlsrv_attr_direct_query [PDO:: SetAttribute](../../connect/php/pdo-setattribute.md) (o come un'opzione driver passato a [PDO::__construct](../../connect/php/pdo-construct.md)) o quando si chiama [PDO:: Prepare](../../connect/php/pdo-prepare.md). Per impostazione predefinita, il valore di PDO:: sqlsrv_attr_direct_query è False (usare l'esecuzione dell'istruzione preparata).  
  
Se si usa [PDO:: query](../../connect/php/pdo-query.md), è possibile l'esecuzione diretta. Prima di chiamare [PDO:: query](../../connect/php/pdo-query.md), chiamare [PDO:: SetAttribute](../../connect/php/pdo-setattribute.md) e PDO:: sqlsrv_attr_direct_query su True.  Ogni chiamata a [PDO:: query](../../connect/php/pdo-query.md) possono essere eseguite con un'impostazione diversa per PDO:: sqlsrv_attr_direct_query.  
  
Se si usa [PDO:: Prepare](../../connect/php/pdo-prepare.md) e [pdostatement:: Execute](../../connect/php/pdostatement-execute.md) per eseguire una query più volte con parametri associati, l'esecuzione dell'istruzione preparata consente di ottimizzare l'esecuzione della query ripetute.  In questo caso, chiamare [PDO:: Prepare](../../connect/php/pdo-prepare.md) con PDO:: sqlsrv_attr_direct_query impostato su False nel parametro di matrice opzioni driver. Se necessario, è possibile eseguire le istruzioni preparate con PDO:: sqlsrv_attr_direct_query impostato su False.  
  
Dopo aver chiamato [PDO:: Prepare](../../connect/php/pdo-prepare.md), non è possibile modificare il valore di PDO:: sqlsrv_attr_direct_query durante l'esecuzione di query preparata.  
  
Se una query richiede il contesto che è stato impostato in una query precedente, eseguire le query con PDO:: sqlsrv_attr_direct_query impostato su True. Ad esempio, se si usano le tabelle temporanee nelle query, PDO:: sqlsrv_attr_direct_query deve essere impostato su True.  
  
L'esempio seguente illustra che quando è necessario contesto da un'istruzione precedente, è necessario impostare PDO:: sqlsrv_attr_direct_query su True. Questo esempio Usa le tabelle temporanee, sono disponibili solo per le istruzioni successive nel programma quando le query vengono eseguite direttamente.  
  
> [!NOTE]
> Se la query consiste nel richiamare una stored procedure e tabelle temporanee vengono usate in questa stored procedure, utilizzare [PDO:: Exec](../../connect/php/pdo-exec.md) invece.

```  
<?php  
   $conn = new PDO('sqlsrv:Server=(local)', '', '');  
   $conn->setAttribute(constant('PDO::SQLSRV_ATTR_DIRECT_QUERY'), true);  
  
   $stmt1 = $conn->query("DROP TABLE #php_test_table");  
  
   $stmt2 = $conn->query("CREATE TABLE #php_test_table ([c1_int] int, [c2_int] int)");  
  
   $v1 = 1;  
   $v2 = 2;  
  
   $stmt3 = $conn->prepare("INSERT INTO #php_test_table (c1_int, c2_int) VALUES (:var1, :var2)");  
  
   if ($stmt3) {  
      $stmt3->bindValue(1, $v1);  
      $stmt3->bindValue(2, $v2);  
  
      if ($stmt3->execute())  
         echo "Execution succeeded\n";       
      else  
         echo "Execution failed\n";  
   }  
   else  
      var_dump($conn->errorInfo());  
  
   $stmt4 = $conn->query("DROP TABLE #php_test_table");  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Guida di programmazione per i driver Microsoft per PHP per SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
