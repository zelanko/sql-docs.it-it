---
title: "Istruzione diretta: esecuzione di istruzioni preparate per l'esecuzione di istruzioni PDO_SQLSRV | Microsoft Docs"
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
ms.openlocfilehash: fa9e544fb7b79009d86a5742946a722d5adc18f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993625"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>Esecuzione di istruzioni diretta e preparata nel driver PDO_SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Questo argomento illustra come usare l'attributo PDO::SQLSRV_ATTR_DIRECT_QUERY per specificare l'esecuzione diretta delle istruzioni anziché l'impostazione predefinita, che corrisponde all'esecuzione di istruzioni preparate. L'utilizzo di un'istruzione preparata può comportare prestazioni migliori se l'istruzione viene eseguita più volte utilizzando l'associazione di parametri.  
  
## <a name="remarks"></a>Remarks  
Se si desidera inviare un' [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione direttamente al server senza la preparazione dell'istruzione da parte del driver, è possibile impostare l'attributo DOP:: SQLSRV_ATTR_DIRECT_QUERY con [DOP:: SetAttribute](../../connect/php/pdo-setattribute.md) (o come opzione del driver passata a [DOP:: __construct ](../../connect/php/pdo-construct.md)) o quando si chiama [dop::p ripare](../../connect/php/pdo-prepare.md). Per impostazione predefinita, il valore di DOP:: SQLSRV_ATTR_DIRECT_QUERY è false (usare l'esecuzione dell'istruzione preparata).  
  
Se si usa il metodo [DOP:: query](../../connect/php/pdo-query.md), potrebbe essere necessario l'esecuzione diretta. Prima di chiamare il metodo [DOP:: query](../../connect/php/pdo-query.md), chiamare [DOP:: SETATTRIBUTE](../../connect/php/pdo-setattribute.md) e impostare DOP:: SQLSRV_ATTR_DIRECT_QUERY su true.  Ogni chiamata a [DOP:: query](../../connect/php/pdo-query.md) può essere eseguita con un'impostazione diversa per DOP:: SQLSRV_ATTR_DIRECT_QUERY.  
  
Se si usa [DOP::p repare](../../connect/php/pdo-prepare.md) e [PDOStatement:: Execute](../../connect/php/pdostatement-execute.md) per eseguire una query più volte usando parametri associati, l'esecuzione di istruzioni preparate ottimizza l'esecuzione della query ripetuta.  In questa situazione, chiamare [DOP::p repare](../../connect/php/pdo-prepare.md) con DOP:: SQLSRV_ATTR_DIRECT_QUERY impostato su false nel parametro di matrice delle opzioni del driver. Quando necessario, è possibile eseguire istruzioni preparate con DOP:: SQLSRV_ATTR_DIRECT_QUERY impostato su false.  
  
Dopo aver chiamato [DOP::p repare](../../connect/php/pdo-prepare.md), il valore di DOP:: SQLSRV_ATTR_DIRECT_QUERY non può essere modificato quando si esegue la query preparata.  
  
Se una query richiede il contesto impostato in una query precedente, eseguire le query con DOP:: SQLSRV_ATTR_DIRECT_QUERY impostato su true. Se ad esempio si usano tabelle temporanee nelle query, il valore di DOP:: SQLSRV_ATTR_DIRECT_QUERY deve essere impostato su true.  
  
L'esempio seguente mostra che quando il contesto di un'istruzione precedente è obbligatorio, è necessario impostare il valore di DOP:: SQLSRV_ATTR_DIRECT_QUERY su true. In questo esempio vengono utilizzate tabelle temporanee, che sono disponibili solo per le istruzioni successive del programma quando le query vengono eseguite direttamente.  
  
> [!NOTE]
> Se la query deve richiamare una stored procedure e le tabelle temporanee vengono usate in questa stored procedure, usare [DOP:: Exec](../../connect/php/pdo-exec.md) .

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
[Guida alla programmazione per i driver Microsoft per PHP per SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
