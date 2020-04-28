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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d68ea1c13655ca7c57ba076823f461a4b2e22055
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283511"
---
# <a name="batches-of-sql-statements"></a>Batch di istruzioni SQL
Un batch di istruzioni SQL è un gruppo di due o più istruzioni SQL o una singola istruzione SQL che ha lo stesso effetto di un gruppo di due o più istruzioni SQL. In alcune implementazioni, l'intera istruzione batch viene eseguita prima che tutti i risultati siano disponibili. Questa operazione è spesso più efficiente rispetto all'invio di istruzioni separatamente, perché il traffico di rete può spesso essere ridotto e l'origine dati può talvolta ottimizzare l'esecuzione di un batch di istruzioni SQL. In altre implementazioni, la chiamata di **SQLMoreResults** attiva l'esecuzione dell'istruzione successiva nel batch. ODBC supporta i tipi di batch seguenti:  
  
-   **Batch espliciti** Un *batch esplicito* è due o più istruzioni SQL separate da punti e virgola (;). Il batch di istruzioni SQL seguente, ad esempio, apre un nuovo ordine di vendita. A tale scopo, è necessario inserire righe in entrambe le tabelle Orders e Lines. Si noti che non è presente un punto e virgola dopo l'ultima istruzione.  
  
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
  
-   **Procedure** Se una stored procedure contiene più di un'istruzione SQL, viene considerata un batch di istruzioni SQL. Ad esempio, l'istruzione specifica SQL Server seguente crea una routine che restituisce un set di risultati contenente informazioni su un cliente e un set di risultati che elenca tutti gli ordini di vendita aperti per il cliente:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     L'istruzione **create procedure** non è un batch di istruzioni SQL. Tuttavia, la procedura creata è un batch di istruzioni SQL. Nessun punto e virgola separa le due istruzioni **Select** perché l'istruzione **create procedure** è specifica di SQL Server e SQL Server non richiede punti e virgola per separare più istruzioni in un'istruzione **create procedure** .  
  
-   **Matrici di parametri** Le matrici di parametri possono essere utilizzate con un'istruzione SQL con parametri come metodo efficace per eseguire operazioni bulk. È ad esempio possibile utilizzare matrici di parametri con l'istruzione **Insert** seguente per inserire più righe nella tabella Lines durante l'esecuzione di una sola istruzione SQL:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Se un'origine dati non supporta matrici di parametri, il driver potrà emularle eseguendo l'istruzione SQL una volta per ogni set di parametri. Per ulteriori informazioni, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md) e [matrici di valori di parametri](../../../odbc/reference/develop-app/arrays-of-parameter-values.md), più avanti in questa sezione.  
  
 I diversi tipi di batch non possono essere combinati in modo interoperativo. Ovvero il modo in cui un'applicazione determina il risultato dell'esecuzione di un batch esplicito che include le chiamate di routine, un batch esplicito che usa matrici di parametri e una chiamata di procedura che usa matrici di parametri è specifica del driver.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Istruzioni per la generazione di risultati e senza risultati](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Esecuzione di batch](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Errori e batch](../../../odbc/reference/develop-app/errors-and-batches.md)
