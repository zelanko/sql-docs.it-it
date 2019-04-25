---
title: Batch di istruzioni SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09805ab73af76bc55890222fc1ffd0e1857d0f33
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62447389"
---
# <a name="batches-of-sql-statements"></a>Batch di istruzioni SQL
Un batch di istruzioni SQL è un gruppo di due o più istruzioni SQL o una singola istruzione SQL che ha lo stesso effetto di un gruppo di due o più istruzioni SQL. In alcune implementazioni, viene eseguita l'istruzione dell'intero batch prima che i risultati siano disponibili. Ciò è spesso più efficiente rispetto all'invio di istruzioni separatamente, perché il traffico di rete possa spesso essere ridotto e l'origine dati in alcuni casi può ottimizzare l'esecuzione di un batch di istruzioni SQL. Nelle altre implementazioni di chiamata **SQLMoreResults** attiva l'esecuzione dell'istruzione successiva nel batch. ODBC supporta i seguenti tipi di batch:  
  
-   **Batch espliciti** un' *esplicito batch* è due o più istruzioni SQL, separate da punti e virgola (;). Ad esempio, il batch di istruzioni SQL seguente apre un nuovo ordine di vendita. Questa operazione richiede l'inserimento di righe in tabelle di entrambi gli ordini e righe. Si noti che non vi sia alcun punto e virgola dopo l'ultima istruzione.  
  
    ```  
    INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
       VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 1, 1234, 10);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 2, 987, 8);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 3, 566, 17);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 4, 412, 500)  
    ```  
  
-   **Le procedure** se una procedura contiene più di un'istruzione SQL, è considerato un batch di istruzioni SQL. Ad esempio, l'istruzione specifici di SQL Server seguente crea una routine che restituisce un set di risultati contenente informazioni su un cliente e un elenco di tutti gli ordini di vendita open per quel cliente di set di risultati:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     Il **CREATE PROCEDURE** istruzione stessa non è un batch di istruzioni SQL. Tuttavia, la procedura che viene creato è un batch di istruzioni SQL. Punto e virgola non separazione le due **selezionate** istruzioni perché il **CREATE PROCEDURE** istruzione è specifica per SQL Server e SQL Server non richiede un punto e virgola per separare più istruzioni in un  **CREATE PROCEDURE** istruzione.  
  
-   **Matrici di parametri** matrici di parametri possono essere utilizzate con un'istruzione SQL con parametri come un metodo efficace per eseguire operazioni in blocco. Ad esempio, matrici di parametri sono utilizzabile con il codice seguente **Inserisci** istruzione per inserire più righe nella tabella di righe durante l'esecuzione di una sola istruzione SQL:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Se un'origine dati non supporta le matrici di parametri, il driver possibile emularli eseguendo l'istruzione SQL una volta per ogni set di parametri. Per altre informazioni, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md) e [matrici di valori di parametro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md), più avanti in questa sezione.  
  
 I diversi tipi di batch non possono essere combinati in modo interoperativo. Vale a dire, come un'applicazione determina il risultato dell'esecuzione di un batch esplicito che include procedure chiama, un batch esplicito che usa le matrici di parametri, e una chiamata di routine che usa matrici di parametri è specifico del driver.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Istruzioni per la generazione di risultati e senza risultati](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Esecuzione di batch](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Errori e batch](../../../odbc/reference/develop-app/errors-and-batches.md)
