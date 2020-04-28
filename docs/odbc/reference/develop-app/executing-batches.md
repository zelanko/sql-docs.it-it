---
title: Esecuzione di batch | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305732"
---
# <a name="executing-batches"></a>Esecuzione di batch
Prima di eseguire un batch di istruzioni, un'applicazione deve prima controllare se sono supportate. A tale scopo, l'applicazione chiama **SQLGetInfo** con le opzioni SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. La prima opzione restituisce un valore che indica se le istruzioni di generazione del conteggio delle righe e dei set di risultati sono supportate in batch e procedure esplicite, mentre le ultime due opzioni restituiscono informazioni sulla disponibilità dei conteggi delle righe e dei set di risultati nell'esecuzione con parametri.  
  
 I batch di istruzioni vengono eseguiti tramite **SQLExecute** o **SQLExecDirect**. La chiamata seguente, ad esempio, esegue un batch esplicito di istruzioni per aprire un nuovo ordine di vendita.  
  
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
  
 Quando viene eseguito un batch di istruzioni che generano risultati, vengono restituiti uno o più conteggi di righe o set di risultati. Per informazioni su come recuperare questi risultati, vedere [più risultati](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se un batch di istruzioni include marcatori di parametro, questi vengono numerati in ordine crescente di parametri così come in qualsiasi altra istruzione. Il batch di istruzioni seguente, ad esempio, include parametri numerati da 1 a 21; quelli nella prima istruzione **Insert** sono numerati da 1 a 5 e quelli nell'ultima istruzione **Insert** sono numerati da 18 a 21.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 Per ulteriori informazioni sui parametri, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.
