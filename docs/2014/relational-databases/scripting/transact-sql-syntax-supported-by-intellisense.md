---
title: Sintassi Transact-SQL supportata da IntelliSense | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL IntelliSense
- IntelliSense [SQL Server], Transact-SQL syntax
ms.assetid: 194e8f4f-fd7e-4f32-a169-f23531128004
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6db4de99458ced7471414540bc46704cfab928fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063324"
---
# <a name="transact-sql-syntax-supported-by-intellisense"></a>Sintassi Transact-SQL supportata da IntelliSense
  In questo argomento vengono descritti le istruzioni e gli elementi di sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] supportati da IntelliSense in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="statements-supported-by-intellisense"></a>Istruzioni supportate da IntelliSense  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], IntelliSense supporta solo le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] di uso più frequente. Alcune condizioni generali dell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] potrebbero impedire il funzionamento di IntelliSense. Per altre informazioni, vedere [Risoluzione dei problemi di IntelliSense &#40;SQL Server Management Studio&#41;](troubleshooting-intellisense.md).  
  
> [!NOTE]  
>  IntelliSense non è disponibile per gli oggetti di database crittografati, ad esempio stored procedure o funzioni definite dall'utente crittografate. Le funzionalità Guida relativa ai parametri e Informazioni rapide non sono disponibili per i parametri di stored procedure estese e per i tipi definiti dall'utente di Integrazione con CLR.  
  
### <a name="select-statement"></a>Istruzione SELECT  
 L'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] offre supporto IntelliSense per gli elementi della sintassi seguenti nell'istruzione SELECT:  
  
|||  
|-|-|  
|SELECT|WHERE|  
|FROM|ORDER BY|  
|HAVING|UNION|  
|FOR|GROUP BY|  
|Torna all'inizio|OPTION (hint)|  
  
### <a name="additional-transact-sql-statements-that-are-supported"></a>Istruzioni Transact-SQL aggiuntive supportate  
 L'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] offre inoltre supporto IntelliSense per le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] elencate nella tabella seguente.  
  
|Istruzione Transact-SQL|Sintassi supportata|  
|-----------------------------|----------------------|  
|[INSERT](/sql/t-sql/statements/insert-transact-sql)|Tutta la sintassi, eccetto la clausola *execute_statement* .|  
|[UPDATE](/sql/t-sql/queries/update-transact-sql)|Tutta la sintassi.|  
|[DELETE](/sql/t-sql/statements/delete-transact-sql)|Tutta la sintassi.|  
|[DECLARE @local_variable](/sql/t-sql/language-elements/declare-local-variable-transact-sql)|Tutta la sintassi.|  
|[SET @local_variable](/sql/t-sql/language-elements/set-local-variable-transact-sql)|Tutta la sintassi.|  
|[EXECUTE](/sql/t-sql/language-elements/execute-transact-sql)|Esecuzione di stored procedure e di funzioni definite dall'utente e di sistema.|  
|[CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql)|Tutta la sintassi.|  
|[CREATE VIEW](/sql/t-sql/statements/create-view-transact-sql)|Tutta la sintassi.|  
|[CREATE PROCEDURE](/sql/t-sql/statements/create-procedure-transact-sql)|Tutta la sintassi, con le eccezioni seguenti:<br /><br /> Non è disponibile supporto IntelliSense per la clausola EXTERNAL NAME.<br /><br /> Nella clausola AS IntelliSense supporta solo le istruzioni e la sintassi elencate in questo argomento.|  
|[ALTER PROCEDURE](/sql/t-sql/statements/alter-procedure-transact-sql)|Tutta la sintassi, con le eccezioni seguenti:<br /><br /> Non è disponibile supporto IntelliSense per la clausola EXTERNAL NAME.<br /><br /> Nella clausola AS IntelliSense supporta solo le istruzioni e la sintassi elencate in questo argomento.|  
|[USE](/sql/t-sql/language-elements/use-transact-sql)|Tutta la sintassi.|  
  
## <a name="intellisense-in-supported-statements"></a>IntelliSense in istruzioni supportate  
 Nell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] IntelliSense supporta i seguenti elementi della sintassi quando vengono utilizzati in una delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] supportate:  
  
-   Tutti i tipi di join, ad esempio APPLY  
  
-   PIVOT e UNPIVOT  
  
-   Riferimenti agli oggetti di database seguenti:  
  
    -   Database e schemi  
  
    -   Tabelle, viste, funzioni con valori di tabella ed espressioni di tabella  
  
    -   Colonne  
  
    -   Procedure e parametri di procedura  
  
    -   Funzioni ed espressioni scalari  
  
    -   Variabili locali  
  
    -   Espressioni di tabella comuni (CTE)  
  
-   Oggetti di database cui viene fatto riferimento solo in istruzioni CREATE o ALTER nello script o nel batch, ma che non esistono nel database perché lo script o il batch non è ancora stato eseguito. Questi oggetti sono i seguenti:  
  
    -   Tabelle e procedure specificate in un'istruzione CREATE TABLE o CREATE PROCEDURE nello script o nel batch.  
  
    -   Modifiche a tabelle e procedure specificate in un'istruzione ALTER TABLE o ALTER PROCEDURE nello script o nel batch.  
  
    > [!NOTE]  
    >  IntelliSense non è disponibile per le colonne di un'istruzione CREATE VIEW fino a che non è stata eseguita l'istruzione CREATE VIEW.  
  
 IntelliSense non è disponibile per gli elementi elencati sopra quando vengono usati in altre istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] . Il supporto IntelliSense è ad esempio disponibile per i nomi di colonna utilizzati in un'istruzione SELECT, ma non per le colonne utilizzate nell'istruzione CREATE FUNCTION.  
  
## <a name="examples"></a>Esempi  
 All'interno di uno script o di un batch [!INCLUDE[tsql](../../includes/tsql-md.md)] , nell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] IntelliSense supporta solo le istruzioni e la sintassi elencate in questo argomento. Negli esempi di codice [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti sono mostrati le istruzioni e gli elementi della sintassi che IntelliSense supporta. Ad esempio, nel batch seguente, IntelliSense è disponibile per l'istruzione `SELECT` quando è codificata da sola, ma non quando `SELECT` è contenuta in un'istruzione `CREATE FUNCTION` .  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE Name LIKE N'Road-250%' and Color = N'Red';  
GO  
CREATE FUNCTION Production.ufn_Red250 ()  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT Name  
    FROM AdventureWorks2012.Production.Product  
    WHERE Name LIKE N'Road-250%'  
      AND Color = N'Red'  
);GO  
```  
  
 Questa funzionalità si applica anche ai set di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] nella clausola AS di un'istruzione CREATE PROCEDURE o ALTER PROCEDURE.  
  
 All'interno di uno script o un batch [!INCLUDE[tsql](../../includes/tsql-md.md)] , IntelliSense supporta gli oggetti che sono stati specificati in un'istruzione CREATE o ALTER, ma questi oggetti non esistono nel database perché le istruzioni non sono state eseguite. È possibile ad esempio immettere nell'editor di query il codice seguente:  
  
```  
USE MyTestDB;  
GO  
CREATE TABLE MyTable  
    (PrimaryKeyCol   INT PRIMARY KEY,  
    FirstNameCol      NVARCHAR(50),  
   LastNameCol       NVARCHAR(50));  
GO  
SELECT   
```  
  
 Quando si digita `SELECT`, IntelliSense elenca **PrimaryKeyCol**, **FirstNameCol**e **LastNameCol** come possibili elementi dell'elenco di selezione, anche se lo script non è stato eseguito e `MyTable` non esiste ancora in `MyTestDB`.  
  
  
