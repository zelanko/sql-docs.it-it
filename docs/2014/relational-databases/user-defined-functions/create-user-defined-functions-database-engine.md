---
title: Creare funzioni definite dall'utente (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SCHEMABINDING clause
- schema-bound functions [SQL Server]
- user-defined functions [SQL Server], creating
- CREATE FUNCTION statement
- valid statements [SQL Server]
ms.assetid: f0d5dd10-73fd-4e05-9177-07f56552bdf7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 37a6846d8c185549bd6c54f32cb5ab02eb564d1d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211718"
---
# <a name="create-user-defined-functions-database-engine"></a>Creazione di funzioni definite dall'utente (Motore di database)
  In questo argomento viene descritto come creare una funzione definita dall'utente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare una funzione definita dall'utente:**  
  
     [Creare una funzione scalare](#Scalar)  
  
     [Creare una funzione con valori di tabella](#TVF)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Non è possibile utilizzare funzioni definite dall'utente per eseguire azioni che modificano lo stato del database.  
  
-   Le funzioni definite dall'utente non possono contenere una clausola OUTPUT INTO che ha una tabella come destinazione.  
  
-   Tramite le funzioni definite dall'utente non possono essere restituiti più set di risultati. Utilizzare una stored procedure se è necessario restituire più set di risultati.  
  
-   In una funzione definita dall'utente la gestione degli errori è limitata. Una funzione definita dall'utente non supporta TRY... CATCH, @ERROR o RAISERROR.  
  
-   Tramite le funzioni definite dall'utente non è possibile chiamare una stored procedure normale, bensì una estesa.  
  
-   Nelle funzioni definite dall'utente non è possibile utilizzare tabelle temporanee o SQL dinamiche. Sono consentite le variabili di tabella.  
  
-   In una funzione definita dall'utente non sono consentite istruzioni SET.  
  
-   La clausola FOR XML non è consentita  
  
-   È possibile nidificare le funzioni definite dall'utente, ovvero una funzione definita dall'utente ne può richiamare un'altra. Il livello di nidificazione aumenta all'avvio della funzione richiamata e diminuisce al termine dell'esecuzione della funzione. Le funzioni definite dall'utente possono essere nidificate fino a un massimo di 32 livelli. Se viene superato il livello massimo di nidificazioni, l'intera sequenza di funzioni chiamanti ha esito negativo. Qualsiasi riferimento al codice gestito presente in una funzione definita dall'utente Transact-SQL viene considerato come un livello nel contesto del limite di 32 livelli di nidificazione. I metodi richiamati da codice gestito non vengono inclusi nel conteggio per questo limite.  
  
-   Nella definizione di una funzione definita dall'utente Transact-SQL non è possibile includere le istruzioni di Service Broker seguenti:  
  
    -   BEGIN DIALOG CONVERSATION  
  
    -   END CONVERSATION  
  
    -   GET CONVERSATION GROUP  
  
    -   MOVE CONVERSATION  
  
    -   RECEIVE  
  
    -   SEND  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione CREATE FUNCTION nel database e dell'autorizzazione ALTER per lo schema in cui la funzione è in fase di creazione. Se per la funzione viene specificato un tipo definito dall'utente, è necessario disporre dell'autorizzazione EXECUTE per tale tipo.  
  
##  <a name="scalar-functions"></a><a name="Scalar"></a>Funzioni scalari  
 Negli esempi seguenti viene creata una funzione scalare a più istruzioni nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . La funzione accetta un valore di input, un valore `ProductID`e restituisce un singolo valore di dati, la quantità aggregata del prodotto specificato nelle scorte.  
  
```  
IF OBJECT_ID (N'dbo.ufnGetInventoryStock', N'FN') IS NOT NULL  
    DROP FUNCTION ufnGetInventoryStock;  
GO  
CREATE FUNCTION dbo.ufnGetInventoryStock(@ProductID int)  
RETURNS int   
AS   
-- Returns the stock level for the product.  
BEGIN  
    DECLARE @ret int;  
    SELECT @ret = SUM(p.Quantity)   
    FROM Production.ProductInventory p   
    WHERE p.ProductID = @ProductID   
        AND p.LocationID = '6';  
     IF (@ret IS NULL)   
        SET @ret = 0;  
    RETURN @ret;  
END;  
GO  
  
```  
  
 Nell'esempio seguente viene utilizzata la funzione `ufnGetInventoryStock` per conoscere la quantità di scorte corrente dei prodotti il cui valore `ProductModelID` è compreso tra 75 e 80.  
  
```  
SELECT ProductModelID, Name, dbo.ufnGetInventoryStock(ProductID)AS CurrentSupply  
FROM Production.Product  
WHERE ProductModelID BETWEEN 75 and 80;  
  
```  
  
##  <a name="table-valued-functions"></a><a name="TVF"></a>Funzioni con valori di tabella  
 Nell'esempio seguente viene creata una funzione inline con valori di tabella nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . La funzione accetta un parametro di input, un ID (punto vendita) cliente e restituisce le colonne `ProductID`, `Name`e l'aggregazione delle vendite per l'anno in corso come valore `YTD Total` per ogni prodotto venduto al punto vendita.  
  
```  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
  
```  
  
 Nell'esempio seguente viene richiamata la funzione e viene specificato l'ID cliente 602.  
  
```  
SELECT * FROM Sales.ufn_SalesByStore (602);  
  
```  
  
 Nell'esempio seguente viene creata una funzione con valori di tabella nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . Nella funzione viene accettato un solo parametro di input, un valore `EmployeeID` , e tramite essa viene restituito un elenco di tutti i dipendenti che fanno riferimento direttamente o indirettamente al dipendente specificato. La funzione viene quindi richiamata specificando l'ID dipendente 109.  
  
```  
IF OBJECT_ID (N'dbo.ufn_FindReports', N'TF') IS NOT NULL  
    DROP FUNCTION dbo.ufn_FindReports;  
GO  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0 -- Get the initial list of Employees for Manager n  
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1 -- Join recursive member to anchor  
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);  
  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Funzioni definite dall'utente](user-defined-functions.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)  
  
  
