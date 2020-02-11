---
title: Specificare i parametri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- stored procedures [SQL Server], parameters
- output parameters [SQL Server]
- input parameters [SQL Server]
ms.assetid: 902314fe-5f9c-4d0d-a0b7-27e67c9c70ec
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f936853c284196b05b6da6369f4410bed2297d4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62736364"
---
# <a name="specify-parameters"></a>Specificare i parametri
  Se si specificano parametri di procedura, i programmi chiamanti sono in grado di passare i valori nel corpo della procedura. Tali valori possono essere utilizzati per diversi scopi durante l'esecuzione della procedura. Inoltre, i parametri di procedura possono restituire valori al programma chiamante se il parametro è contrassegnato come parametro OUTPUT.  
  
 Una procedura può disporre al massimo di 2100 parametri, a ciascuno dei quali vengono assegnati un nome, un tipo di dati e una direzione. Facoltativamente, ai parametri possono essere assegnati i valori predefiniti.  
  
 Nella sezione seguente vengono fornite informazioni sul passaggio dei valori nei parametri e sulla modalità di utilizzo di ognuno degli attributi di parametro durante una chiamata alla procedura.  
  
## <a name="passing-values-into-parameters"></a>Passaggio dei valori nei parametri  
 I valori dei parametri forniti con una chiamata alla procedura devono essere costanti o una variabile. Non è possibile utilizzare un nome di funzione come valore di parametro. Le variabili possono essere definite dall'utente oppure di sistema, ad esempio \@\@spid.  
  
 Negli esempi seguenti viene illustrato il passaggio dei valori dei parametri alla procedura `uspGetWhereUsedProductID`. Viene illustrato come passare i parametri come costanti e variabili e utilizzare una variabile per passare il valore di una funzione.  
  
```  
USE AdventureWorks2012;  
GO  
-- Passing values as constants.  
EXEC dbo.uspGetWhereUsedProductID 819, '20050225';  
GO  
-- Passing values as variables.  
DECLARE @ProductID int, @CheckDate datetime;  
SET @ProductID = 819;  
SET @CheckDate = '20050225';  
EXEC dbo.uspGetWhereUsedProductID @ProductID, @CheckDate;  
GO  
-- Try to use a function as a parameter value.  
-- This produces an error message.  
EXEC dbo.uspGetWhereUsedProductID 819, GETDATE();  
GO  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
## <a name="specifying-parameter-names"></a>Specifica dei nomi di parametri  
 Quando si crea una procedura e si dichiara un nome di parametro, tale nome deve iniziare con un singolo carattere \@ e deve essere univoco nell'ambito della procedura.  
  
 La denominazione dei parametri e l'assegnazione dei valori appropriati in modo esplicito a ogni parametro in una chiamata alla procedura consentono ai parametri di essere forniti in qualsiasi ordine. Se ad esempio per la procedura **my_proc** sono previsti tre parametri denominati **\@first**, **\@second** e **\@third**, i valori passati alla procedura possono essere assegnati ai nomi dei parametri, ad esempio: `EXECUTE my_proc @second = 2, @first = 1, @third = 3;`  
  
> [!NOTE]
>  Se un valore di parametro viene specificato nel formato ** \@parametro =**_valore_, tutti i parametri successivi devono essere specificati in questo modo. Se i valori dei parametri non vengono passati nel formato ** \@Parameter =**_value_, i valori devono essere specificati nello stesso ordine, da sinistra a destra, dei parametri elencati nell'istruzione create procedure.  
> 
> [!WARNING]
>  Qualsiasi parametro passato nel formato ** \@Parameter =**_value_ con il parametro errato, causerà la generazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di un errore e impedirà l'esecuzione della procedura.  
  
## <a name="specifying-parameter-data-types"></a>Specifica dei tipi di dati per i parametri  
 I parametri devono essere definiti con un tipo di dati quando vengono dichiarati in un'istruzione CREATE PROCEDURE. Il tipo di dati di un parametro consente di determinare il tipo e l'intervallo di valori accettati per il parametro quando viene chiamata la procedura. Se, ad esempio, si definisce un parametro con un tipo di dati `tinyint`, verranno accettati soltanto i valori numerici nell'intervallo compreso tra 0 e 255 quando passati in tale parametro. Se una procedura viene eseguita con un valore incompatibile con il tipo di dati, verrà restituito un errore.  
  
## <a name="specifying-parameter-default-values"></a>Specifica dei valori predefiniti per i parametri  
 Un parametro è considerato facoltativo se dispone di un valore predefinito specificato al momento della relativa dichiarazione. Non è necessario fornire un valore per un parametro facoltativo in una chiamata alla procedura.  
  
 Il valore predefinito di un parametro viene utilizzato quando:  
  
-   Non viene specificato alcun valore nella chiamata alla procedura.  
  
-   Viene specificata la parola chiave DEFAULT come valore nella chiamata alla procedura.  
  
> [!NOTE]  
>  Se il valore predefinito è una stringa di caratteri contenente spazi vuoti o punteggiatura o se inizia con un numero, ad esempio 6xxx, è necessario racchiuderlo tra virgolette singole.  
  
 Se per il parametro non può essere specificato in modo appropriato alcun valore come predefinito, specificare come tale NULL. È consigliabile la restituzione di un messaggio personalizzato da parte della procedura se quest'ultima viene eseguita senza un valore per il parametro.  
  
 Nell'esempio seguente viene creata la procedura `usp_GetSalesYTD` con un parametro di input, `@SalesPerson`. NULL viene assegnato come valore predefinito per il parametro e utilizzato nelle istruzioni di gestione degli errori per restituire un messaggio di errore personalizzato nei casi in cui la procedura venga eseguita senza un valore per il parametro `@SalesPerson` .  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetSalesYTD  
@SalesPerson nvarchar(50) = NULL  -- NULL default value  
AS   
    SET NOCOUNT ON;   
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
BEGIN  
   PRINT 'ERROR: You must specify the last name of the sales person.'  
   RETURN  
END  
-- Get the sales for the specified sales person and   
-- assign it to the output parameter.  
SELECT SalesYTD  
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 Di seguito è riportato un esempio di esecuzione della procedura. Tramite la prima istruzione la procedura viene eseguita senza specificare un valore di input. Tale operazione determina la restituzione del messaggio di errore personalizzato da parte delle istruzioni di gestione degli errori nella procedura. Tramite la seconda istruzione viene fornito un valore di input e viene restituito il set di risultati previsto.  
  
```  
-- Run the procedure without specifying an input value.  
EXEC Sales.usp_GetSalesYTD;  
GO  
-- Run the procedure with an input value.  
EXEC Sales.usp_GetSalesYTD N'Blythe';  
GO  
```  
  
 Sebbene sia possibile omettere i parametri per cui sono stati forniti valori predefiniti, è possibile troncare soltanto l'elenco di parametri. Ad esempio, se una procedura dispone di cinque parametri, è possibile omettere sia il quarto sia il quinto parametro. Tuttavia, il quarto parametro non può essere ignorato finché il quinto parametro è incluso, a meno che i parametri non vengano specificati nel formato ** \@Parameter =**_value_.  
  
## <a name="specifying-parameter-direction"></a>Specifica della direzione di un parametro  
 La direzione di un parametro può essere input, cioè un valore viene passato nel corpo della procedura, o output, vale a dire che tramite la procedura viene restituito un valore al programma chiamante. Il parametro di input è l'impostazione predefinita.  
  
 Per specificare un parametro di output, è necessario includere la parola chiave OUTPUT nella definizione del parametro nell'istruzione CREATE PROCEDURE. Tramite la procedura, al programma chiamante viene restituito il valore corrente del parametro di output quando la procedura è disponibile. Nel programma chiamante deve inoltre essere utilizzata la parola chiave OUTPUT quando si esegue la procedura per salvare il valore del parametro in una variabile utilizzabile nel programma chiamante.  
  
 Nell'esempio seguente viene creata la procedura `Production.usp`_`GetList` , mediante la quale viene restituito un elenco di prodotti i cui prezzi non superano un determinato importo. Nell'esempio viene illustrato l'utilizzo di più istruzioni SELECT e di più parametri OUTPUT. I parametri OUTPUT consentono a una procedura esterna, a un batch o a più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] di accedere a un valore impostato durante l'esecuzione della procedura.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
  
```  
  
 Eseguire `usp_GetList` per restituire un elenco dei prodotti di [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] (biciclette) con un prezzo inferiore a 700 dollari. I parametri ** \@** di output cost e ** \@ComparePrices** vengono utilizzati con il linguaggio per il controllo di flusso per restituire un messaggio nella finestra **messaggi** .  
  
> [!NOTE]  
>  La variabile OUTPUT deve essere definita durante la creazione della procedura e durante l'utilizzo della variabile. Il nome di parametro e quello della variabile non devono corrispondere. Il tipo di dati e la posizione del parametro devono tuttavia corrispondere, a meno che non __ ** \@venga utilizzato ListPrice =** variable.  
  
```  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
  
```  
  
 Di seguito è riportato il set di risultati parziale:  
  
```  
Product                                            List Price  
-------------------------------------------------- ------------------  
Road-750 Black, 58                                 539.99  
Mountain-500 Silver, 40                            564.99  
Mountain-500 Silver, 42                            564.99  
...  
Road-750 Black, 48                                 539.99  
Road-750 Black, 52                                 539.99  
  
(14 row(s) affected)  
  
These items can be purchased for less than $700.00.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
