---
title: MSSQLSERVER_207 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 207 (Database Engine error)
ms.assetid: d1ab00c7-0331-437a-84fe-bae53b82feec
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5d39cfd6ca3eba8222dda09a83fdd809bb7d00e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915051"
---
# <a name="mssqlserver_207"></a>MSSQLSERVER_207
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|207|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQ_BADCOL|  
|Testo del messaggio|Il nome di colonna '%.*ls' non è valido.|  
  
## <a name="explanation"></a>Spiegazione  
 L'errore di query può essere causato da uno dei problemi seguenti:  
  
-   Il nome di colonna è errato oppure la colonna non esiste in alcuna delle tabelle specificate.  
  
-   Le regole di confronto del database rispettano la distinzione tra maiuscole e minuscole e la combinazione di maiuscole e minuscole del nome di colonna specificato nella query non corrisponde a quella della colonna definita nella tabella. Ad esempio, se una colonna viene definita in una tabella come **Cognome** e nel database vengono usate regole di confronto con distinzione tra maiuscole e minuscole, le query che fanno riferimento alla colonna con **COGNOME** o **cognome** restituiranno l'errore 207 poiché il nome di colonna non corrisponde.  
  
-   A un alias di colonna, definito nella clausola SELECT, viene fatto riferimento in un'altra clausola, ad esempio una clausola WHERE o GROUP BY. La query seguente, ad esempio, definisce l'alias di colonna `Year` nella clausola SELECT e fa riferimento all'alias nella clausola GROUP BY.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year, SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY Year;  
    ```  
  
     A causa dell'ordine in cui le clausole di query vengono elaborate logicamente, l'esempio restituisce l'errore 207. L'ordine di elaborazione è il seguente:  
  
    1.  FROM  
  
    2.  ATTIVA  
  
    3.  JOIN  
  
    4.  WHERE  
  
    5.  GROUP BY  
  
    6.  WITH CUBE o WITH ROLLUP  
  
    7.  HAVING  
  
    8.  SELECT  
  
    9. DISTINCT  
  
    10. ORDER BY  
  
    11. Torna all'inizio  
  
     Poiché un alias di colonna non viene definito fino a quando la clausola SELECT non viene elaborata, il nome di alias è sconosciuto al momento dell'elaborazione della clausola GROUP BY.  
  
-   L'istruzione MERGE genera questo errore quando la clausola *<merge_corrispondente>* fa riferimento alle colonne nella tabella di origine, ma quest'ultima non restituisce alcuna riga nella clausola WHEN NOT MATCHED BY SOURCE. L'errore si verifica poiché non è possibile accedere alle colonne della tabella di origine quando alla query non viene restituita alcuna riga. La clausola `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` può provocare ad esempio un errore nell'istruzione se non è possibile accedere a `Col1` nella tabella di origine.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare le informazioni seguenti e correggere l'istruzione in base alle esigenze.  
  
-   Presenza e ortografia corretta del nome di colonna nella tabella. Nell'esempio seguente viene eseguita una query sulla vista del catalogo **sys.columns** per restituire tutti i nomi di colonna per una tabella specifica.  
  
    ```  
    SELECT name FROM sys.columns WHERE object_id = OBJECT_ID('schema_name.table_name');  
    ```  
  
-   Distinzione tra maiuscole e minuscole delle regole di confronto del database. L'istruzione seguente restituisce le regole di confronto del database specificato.  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
     L'abbreviazione CS nel nome delle regole di confronto indica che le regole di confronto rispettano la distinzione tra maiuscole e minuscole. Latin1_General_CS_AS ad esempio è una regola di confronto con distinzione tra maiuscole e minuscole e distinzione tra caratteri accentati e non accentati. Modificare il nome di colonna in modo che corrisponda alla combinazione di maiuscole e minuscole del nome di colonna come definito nella tabella.  
  
-   Riferimento non corretto a un alias di colonna. Modificare l'istruzione ripetendo l'espressione che definisce l'alias nella clausola appropriata oppure utilizzando una tabella derivata. Nell'esempio seguente vengono ripetute le espressioni che definiscono l'alias `Year` nella clausola GROUP BY.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year ,SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY DATEPART(yyyy,OrderDate);  
    ```  
  
     Nell'esempio seguente viene utilizzata una tabella derivata per rendere disponibile il nome di alias ad altre clausole nella query. Si noti che l'alias `Year` viene definito nella clausola FROM, che viene elaborata per prima. In questo modo l'alias può essere utilizzato in altre clausole nella query.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT d.Year, SUM(TotalDue) AS Total  
    FROM (SELECT DATEPART(yyyy,OrderDate) AS Year, TotalDue  
          FROM Sales.SalesOrderHeader)AS d  
    GROUP BY Year;  
    ```  
  
-   La clausola WHEN NOT MATCHED BY SOURCE nell'istruzione MERGE fa riferimento a un valore cui è possibile accedere. Modificare l'istruzione MERGE in modo che venga restituita almeno una riga dalla tabella di origine nella clausola WHEN NOT MATCHED BY SOURCE. Può ad esempio essere necessario aggiungere o modificare la condizione di ricerca specificata per la clausola. In alternativa, è possibile modificare la clausola per specificare un valore che non fa riferimento alla tabella di origine, Ad esempio: `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = <expression, or other available value>`.  
  
## <a name="see-also"></a>Vedere anche  
 [MERGE &#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)   
 [DA &#40;&#41;Transact-SQL](/sql/t-sql/queries/from-transact-sql)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)  
  
  
