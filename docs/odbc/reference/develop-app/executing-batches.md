---
title: Esecuzione di batch Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ce0c043fcfad41a624ad129a757a047d2c87fb6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305732"
---
# <a name="executing-batches"></a>Esecuzione di batch
Prima che un'applicazione esegua un batch di istruzioni, deve prima verificare se sono supportate. A tale scopo, l'applicazione chiama **SQLGetInfo** con le opzioni SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. La prima opzione restituisce se le istruzioni di generazione e generazione di set di risultati sono supportate in batch e procedure espliciti, mentre le ultime due opzioni restituiscono informazioni sulla disponibilità dei conteggi delle righe e dei set di risultati nell'esecuzione con parametri.  
  
 I batch di istruzioni vengono eseguiti tramite **SQLExecute** o **SQLExecDirect**. Ad esempio, la chiamata seguente esegue un batch esplicito di istruzioni per aprire un nuovo ordine cliente.  
  
```  
SQLCHAR *BatchStmt =  
   "INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)"  
      "VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 1, 1234, 10);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 2, 987, 8);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 3, 566, 17);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 4, 412, 500)";  
  
SQLExecDirect(hstmt, BatchStmt, SQL_NTS);  
```  
  
 Quando viene eseguito un batch di istruzioni che generano risultati, vengono restituiti uno o più conteggi di riga o set di risultati. Per informazioni su come recuperarli, vedere [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se un batch di istruzioni include marcatori di parametro, questi vengono numerati in ordine crescente di parametri come in qualsiasi altra istruzione. Ad esempio, il batch di istruzioni seguente ha parametri numerati da 1 a 21; quelli nella prima istruzione **INSERT** sono numerati da 1 a 5 e quelli nell'ultima istruzione **INSERT** sono numerati da 18 a 21.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 Per ulteriori informazioni sui parametri, vedere [Parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md)più avanti in questa sezione.
