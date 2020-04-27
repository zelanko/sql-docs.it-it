---
title: Restituire dati da una stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], returning data
- returning data from stored procedure
ms.assetid: 7a428ffe-cd87-4f42-b3f1-d26aa8312bf7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b11f924ce5692378896f1fd7d50186861abf223
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63140437"
---
# <a name="return-data-from-a-stored-procedure"></a>Restituire dati da una stored procedure
  Sono disponibili due modalità di restituzione di set di risultati o di dati da una procedura a un programma chiamante, cioè i parametri di output e i codici restituiti. In questo argomento vengono fornite informazioni su entrambi gli approcci.  
  
## <a name="returning-data-using-an-output-parameter"></a>Restituzione di dati tramite un parametro di output  
 Se si specifica la parola chiave OUTPUT per un parametro nella definizione della procedura, il valore corrente del parametro può essere restituito al programma chiamante dalla procedura, se quest'ultima è disponibile. Per salvare il valore del parametro in una variabile che può essere utilizzata nel programma chiamante, in tale programma deve essere utilizzata la parola chiave OUTPUT durante l'esecuzione della procedura. Per altre informazioni sui tipi di dati che possono essere usati come parametri di output, vedere [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql).  
  
### <a name="examples-of-output-parameter"></a>Esempi di parametri di output  
 Nell'esempio seguente viene illustrata una procedura con un parametro di input e uno di output. Il parametro `@SalesPerson` riceve un valore di input specificato dal programma chiamante. L'istruzione SELECT usa il valore passato nel parametro di input per ottenere il valore `SalesYTD` corretto. Assegna anche il valore al parametro di output `@SalesYTD` che restituisce il valore al programma chiamante al termine della procedura.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
@SalesPerson nvarchar(50),  
@SalesYTD money OUTPUT  
AS    
  
    SET NOCOUNT ON;  
    SELECT @SalesYTD = SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 Nell'esempio seguente viene chiamata la procedura creata nel primo esempio e viene salvato il valore di output restituito dalla procedura chiamata nella variabile `@SalesYTD` , che è locale nel programma chiamante.  
  
```  
-- Declare the variable to receive the output value of the procedure.  
DECLARE @SalesYTDBySalesPerson money;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTDBySalesPerson  
EXECUTE Sales.uspGetEmployeeSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDBySalesPerson OUTPUT;  
-- Display the value returned by the procedure.  
PRINT 'Year-to-date sales for this employee is ' +   
    convert(varchar(10),@SalesYTDBySalesPerson);  
GO  
  
```  
  
 Inoltre, è possibile specificare valori di input per i parametri OUTPUT quando la procedura viene eseguita. Questa operazione consente alla procedura di ricevere un valore dal programma chiamante, modificare o eseguire operazioni con il valore, quindi restituire il nuovo valore al programma chiamante. Nell'esempio precedente, è possibile assegnare un valore alla variabile `@SalesYTDBySalesPerson` prima che il programma chiami la procedura `Sales.uspGetEmployeeSalesYTD` . L'istruzione di esecuzione passa il valore della variabile `@SalesYTDBySalesPerson` nel parametro OUTPUT `@SalesYTD` . Nel corpo della procedura il valore può quindi essere utilizzato per calcoli che consentono di generare un nuovo valore. Il nuovo valore viene passato di nuovo alla procedura tramite il parametro OUTPUT, aggiornando il valore nella variabile `@SalesYTDBySalesPerson` al termine della procedura. Questa funzionalità viene in genere denominata "funzionalità di passaggio per riferimento".  
  
 Se si specifica OUTPUT per un parametro quando si chiama una procedura e tale parametro non è stato definito utilizzando OUTPUT nella definizione della procedura, viene restituito un messaggio di errore. Tuttavia, è possibile eseguire una procedura con i parametri di output e non specificare OUTPUT in fase di esecuzione della procedura. Non viene restituito alcun errore, ma non è possibile utilizzare il valore di output nel programma chiamante.  
  
### <a name="using-the-cursor-data-type-in-output-parameters"></a>Utilizzo del tipo di dati cursor nei parametri OUTPUT  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)]le routine possono utilizzare `cursor` il tipo di dati solo per i parametri di output. Se per `cursor` un parametro viene specificato il tipo di dati, è necessario specificare entrambe le parole chiave VARYING e output per tale parametro nella definizione della procedura. Un parametro può essere specificato solo come OUTPUT, ma se nella dichiarazione del parametro è specificata la parola chiave VARYing, il tipo di `cursor` dati deve essere e deve essere specificata anche la parola chiave output.  
  
> [!NOTE]  
>  Il tipo di dati `cursor` non può essere associato a variabili di applicazione tramite le API di database, quali OLE DB, ODBC, ADO e DB-Library. Poiché in un'applicazione è possibile eseguire una procedura solo in seguito all'associazione dei parametri OUTPUT, le procedure con parametri OUTPUT di tipo `cursor` non possono essere chiamate dalle API di database. È possibile chiamare queste procedure da trigger, procedure o batch [!INCLUDE[tsql](../../../includes/tsql-md.md)] solo quando la variabile OUTPUT di tipo `cursor` è assegnata a una variabile locale [!INCLUDE[tsql](../../../includes/tsql-md.md)] di tipo `cursor`.  
  
### <a name="rules-for-cursor-output-parameters"></a>Regole per parametri di output di tipo cursor  
 Quando si esegue la procedura, per i parametri di output di tipo `cursor` vengono applicate le regole seguenti:  
  
-   Con cursori forward-only, nel set di risultati del cursore sono incluse solo le righe che al completamento della procedura si trovano oltre la posizione del cursore, ad esempio:  
  
    -   Un cursore non scorrevole viene aperto in una procedura in un set di risultati di 100 righe denominato RS.  
  
    -   La procedura recupera le prime 5 righe del set di risultati RS.  
  
    -   La procedura restituisce il set di risultati al chiamante.  
  
    -   Il set di risultati RS restituito al chiamante include le righe comprese tra la riga 6 e la riga 100 di RS e la posizione del cursore nel chiamante precede la prima riga di RS.  
  
-   Con cursori forward-only, se il cursore precede la prima riga quando la procedura è disponibile, l'intero set di risultati viene restituito al trigger, alla procedura o al batch chiamante. Quando viene restituito, il cursore è posizionato prima della prima riga.  
  
-   Con cursori forward-only, se il cursore è posizionato oltre l'ultima riga quando la procedura è disponibile, viene restituito un set di risultati vuoto al trigger, alla procedura o al batch chiamante.  
  
    > [!NOTE]  
    >  Un set di risultati vuoto non equivale a un valore Null.  
  
-   Con cursori scorrevoli, quando è disponibile la procedura, tutte le righe del set di risultati vengono restituite al trigger, alla procedura o al batch chiamante. Quando viene restituito, il cursore è nella stessa posizione in cui si trovava durante l'ultima operazione di recupero eseguita dalla procedura.  
  
-   Con qualsiasi tipo di cursore, se il cursore è chiuso, viene restituito un valore Null al trigger, alla procedura o al batch chiamante. Questa situazione si verifica anche quando un cursore viene assegnato a un parametro, ma non viene mai aperto.  
  
    > [!NOTE]  
    >  Lo stato chiuso di un cursore è rilevante solo in fase di restituzione. È possibile, ad esempio, chiudere un cursore nel corso di una procedura, riaprirlo in una fase successiva e restituire il set di risultati di tale cursore al trigger, alla procedura o al batch chiamante.  
  
### <a name="examples-of-cursor-output-parameters"></a>Esempi di parametri di output di tipo cursor  
 Nell'esempio seguente viene creata una stored procedure che specifica un parametro di output `@currency`_`cursor` utilizzando il `cursor` tipo di dati. La procedura viene quindi chiamata in un batch.  
  
 Creare innanzitutto la procedura per la dichiarazione e l'apertura di un cursore per la tabella Currency.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspCurrencyCursor', 'P' ) IS NOT NULL  
    DROP PROCEDURE dbo.uspCurrencyCursor;  
GO  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
  
```  
  
 Eseguire quindi un batch che consenta di dichiarare una variabile locale di cursore, eseguire la procedura per assegnare il cursore alla variabile locale e recuperare le righe dal cursore.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
  
```  
  
## <a name="returning-data-using-a-return-code"></a>Restituzione di dati tramite un codice restituito  
 Una procedura può restituire un valore intero, denominato codice restituito, per indicare lo stato di esecuzione di una procedura. Per specificare il codice restituito per una procedura, utilizzare l'istruzione RETURN. Come per i parametri OUTPUT, è necessario salvare il codice restituito in una variabile quando la procedura viene eseguita per utilizzare il valore del codice restituito nel programma chiamante. La variabile `@result` di assegnazione del tipo `int` di dati, ad esempio, viene utilizzata per archiviare il codice restituito `my_proc`dalla procedura, ad esempio:  
  
```  
DECLARE @result int;  
EXECUTE @result = my_proc;  
```  
  
 I codici restituiti vengono in genere utilizzati nei blocchi per il controllo di flusso all'interno delle procedure per impostare il valore del codice restituito per ogni possibile situazione di errore. È possibile usare la funzione @@ERROR dopo un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] per rilevare se si è verificato un errore durante l'esecuzione dell'istruzione.  
  
### <a name="examples-of-return-codes"></a>Esempi di codici restituiti  
 Nell'esempio seguente viene illustrata la procedura `usp_GetSalesYTD` con una modalità di gestione degli errori che consente di impostare valori speciali del codice restituito per errori diversi. Nella tabella seguente sono inclusi i valori interi assegnati dalla procedura a ogni possibile errore e viene indicato il significato di ogni valore.  
  
|Valore del codice restituito|Significato|  
|-----------------------|-------------|  
|0|L'esecuzione è stata completata.|  
|1|Non è stato specificato un valore obbligatorio per un parametro.|  
|2|Il valore specificato per il parametro non è valido.|  
|3|Si è verificato un errore durante il recupero del valore delle vendite.|  
|4|È stato trovato un valore delle vendite NULL per il venditore.|  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.usp_GetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.usp_GetSalesYTD;  
GO  
CREATE PROCEDURE Sales.usp_GetSalesYTD  
@SalesPerson nvarchar(50) = NULL,  -- NULL default value  
@SalesYTD money = NULL OUTPUT  
AS    
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
   BEGIN  
       PRINT 'ERROR: You must specify a last name for the sales person.'  
       RETURN(1)  
   END  
ELSE  
   BEGIN  
   -- Make sure the value is valid.  
   IF (SELECT COUNT(*) FROM HumanResources.vEmployee  
          WHERE LastName = @SalesPerson) = 0  
      RETURN(2)  
   END  
-- Get the sales for the specified name and   
-- assign it to the output parameter.  
SELECT @SalesYTD = SalesYTD   
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
-- Check for SQL Server errors.  
IF @@ERROR <> 0   
   BEGIN  
      RETURN(3)  
   END  
ELSE  
   BEGIN  
   -- Check to see if the ytd_sales value is NULL.  
     IF @SalesYTD IS NULL  
       RETURN(4)   
     ELSE  
      -- SUCCESS!!  
        RETURN(0)  
   END  
-- Run the stored procedure without specifying an input value.  
EXEC Sales.usp_GetSalesYTD;  
GO  
-- Run the stored procedure with an input value.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
-- Execute the procedure specifying a last name for the input parameter  
-- and saving the output value in the variable @SalesYTD  
EXECUTE Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
PRINT N'Year-to-date sales for this employee is ' +  
    CONVERT(varchar(10), @SalesYTDForSalesPerson);  
  
```  
  
 Nell'esempio seguente viene creato un programma per la gestione dei codici restituiti dalla procedura `usp_GetSalesYTD` .  
  
```  
-- Declare the variables to receive the output value and return code   
-- of the procedure.  
DECLARE @SalesYTDForSalesPerson money, @ret_code int;  
  
-- Execute the procedure with a title_id value  
-- and save the output value and return code in variables.  
EXECUTE @ret_code = Sales.usp_GetSalesYTD  
    N'Blythe', @SalesYTD = @SalesYTDForSalesPerson OUTPUT;  
--  Check the return codes.  
IF @ret_code = 0  
BEGIN  
   PRINT 'Procedure executed successfully'  
   -- Display the value returned by the procedure.  
   PRINT 'Year-to-date sales for this employee is ' + CONVERT(varchar(10),@SalesYTDForSalesPerson)  
END  
ELSE IF @ret_code = 1  
   PRINT 'ERROR: You must specify a last name for the sales person.'  
ELSE IF @ret_code = 2   
   PRINT 'EERROR: You must enter a valid last name for the sales person.'  
ELSE IF @ret_code = 3  
   PRINT 'ERROR: An error occurred getting sales value.'  
ELSE IF @ret_code = 4  
   PRINT 'ERROR: No sales recorded for this employee.'     
GO  
  
```  
  
## <a name="see-also"></a>Vedi anche  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)   
 [PRINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/print-transact-sql)   
 [IMPOSTA @local_variable &#40;&#41;Transact-SQL](/sql/t-sql/language-elements/set-local-variable-transact-sql)   
 [Cursori](../cursors.md)   
 [RETURN &#40;&#41;Transact-SQL](/sql/t-sql/language-elements/return-transact-sql)   
 [@@ERROR &#40;Transact-SQL&#41;](/sql/t-sql/functions/error-transact-sql)  
  
  
