---
title: Restituire dati da una stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], returning data
- returning data from stored procedure
ms.assetid: 7a428ffe-cd87-4f42-b3f1-d26aa8312bf7
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4f9ee8851ce00c429ba277dd6e0be3286284f548
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74307987"
---
# <a name="return-data-from-a-stored-procedure"></a>Restituire dati da una stored procedure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Sono disponibili tre modalità per la restituzione di dati da una procedura a un programma chiamante: i set di risultati, i parametri di output e i codici restituiti. Questo argomento offre informazioni sui tre approcci.  
  
## <a name="returning-data-using-result-sets"></a>Restituzione di dati tramite i set di risultati
Se si include nel corpo di una stored procedure un'istruzione SELECT (ma non un'istruzione SELECT... INTO o INSERT... SELECT), le righe specificate dall'istruzione SELECT vengono inviate direttamente al client.  Per set di risultati di grandi dimensioni, l'esecuzione della stored procedure non passa all'istruzione successiva fino a quando l'intero set di risultati non è stato inviato al client.  Per set di risultati di piccole dimensioni, i risultati vengono sottoposti a spooling per la restituzione al client e nel frattempo l'esecuzione continua.  Se durante l'esecuzione della stored procedure vengono eseguite più istruzioni SELECT di questo tipo, vengono inviati al client più set di risultati.  Questo comportamento si applica anche ai batch TSQL nidificati, alle stored procedure nidificate e ai batch TSQL di primo livello.
 
 
 ### <a name="examples-of-returning-data-using-a-result-set"></a>Esempi di restituzione di dati tramite un set di risultati 
  L'esempio seguente visualizza una stored procedure che restituisce i valori LastName e SalesYTD per tutte le righe SalesPerson che appaiono anche nella vista vEmployee.
  
 ```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetEmployeeSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetEmployeeSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetEmployeeSalesYTD  
AS    
  
    SET NOCOUNT ON;  
    SELECT LastName, SalesYTD  
    FROM Sales.SalesPerson AS sp  
    JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
    
RETURN  
GO  
  
```  

  
## <a name="returning-data-using-an-output-parameter"></a>Restituzione di dati tramite un parametro di output  
 Se si specifica la parola chiave OUTPUT per un parametro nella definizione della procedura, il valore corrente del parametro può essere restituito al programma chiamante dalla procedura, se quest'ultima è disponibile. Per salvare il valore del parametro in una variabile che può essere utilizzata nel programma chiamante, in tale programma deve essere utilizzata la parola chiave OUTPUT durante l'esecuzione della procedura. Per altre informazioni sui tipi di dati che possono essere usati come parametri di output, vedere [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
### <a name="examples-of-output-parameter"></a>Esempi di parametri di output  
 Nell'esempio seguente viene illustrata una procedura con un parametro di input e uno di output. Il parametro `@SalesPerson` riceve un valore di input specificato dal programma chiamante. L'istruzione SELECT usa il valore passato nel parametro di input per ottenere il valore `SalesYTD` corretto. Assegna anche il valore al parametro di output `@SalesYTD` che restituisce il valore al programma chiamante al termine della procedura.  
  
```sql
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
  
```sql
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
 [!INCLUDE[tsql](../../includes/tsql-md.md)] consente di usare nelle procedure il tipo di dati **cursor** solo per i parametri OUTPUT. Se per un parametro viene specificato il tipo di dati **cursor** , nella definizione della procedura devono essere specificate per tale parametro entrambe le parole chiave VARYING e OUTPUT. Un parametro può essere specificato solo come OUTPUT, ma se nella dichiarazione del parametro è specificata la parola chiave VARYING, il tipo di dati deve essere **cursor** e deve essere specificata anche la parola chiave OUTPUT.  
  
> [!NOTE]  
>  Il tipo di dati **cursor** non può essere associato a variabili di applicazione tramite API di database come OLE DB, ODBC, ADO e DB-Library. Poiché in un'applicazione è possibile eseguire una procedura solo in seguito all'associazione dei parametri OUTPUT, le procedure con parametri OUTPUT di tipo **cursor** non possono essere chiamate dalle API di database. È possibile chiamare queste procedure da trigger, procedure o batch [!INCLUDE[tsql](../../includes/tsql-md.md)] solo quando la variabile OUTPUT di tipo **cursor** è assegnata a una variabile locale [!INCLUDE[tsql](../../includes/tsql-md.md)] di tipo **cursor** .  
  
### <a name="rules-for-cursor-output-parameters"></a>Regole per parametri di output di tipo cursor  
 Quando si esegue la procedura, ai parametri di output di tipo **cursor** si applicano le regole seguenti:  
  
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
 Nell'esempio seguente viene creata una procedura in cui è specificato un parametro di output `@currency_cursor` usando il tipo di dati **cursor**. La procedura viene quindi chiamata in un batch.  
 
 Creare innanzitutto la procedura per la dichiarazione e l'apertura di un cursore per la tabella Currency.  
  
```sql
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
  
```sql
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
 Una procedura può restituire un valore intero, denominato codice restituito, per indicare lo stato di esecuzione di una procedura. Per specificare il codice restituito per una procedura, utilizzare l'istruzione RETURN. Come per i parametri OUTPUT, è necessario salvare il codice restituito in una variabile quando la procedura viene eseguita per utilizzare il valore del codice restituito nel programma chiamante. La variabile di assegnazione `@result` del tipo di dati **int** viene ad esempio usata per archiviare il codice restituito dalla procedura `my_proc`:  
  
```sql
DECLARE @result int;  
EXECUTE @result = my_proc;  
```  
  
 I codici restituiti vengono in genere utilizzati nei blocchi per il controllo di flusso all'interno delle procedure per impostare il valore del codice restituito per ogni possibile situazione di errore. È possibile usare la funzione @@ERROR dopo un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] per rilevare se si è verificato un errore durante l'esecuzione dell'istruzione.  Prima dell'introduzione della gestione degli errori TRY/CATCH/THROW in TSQL, in certi casi i codici restituiti erano necessari per determinare l'esito positivo o negativo delle stored procedure.  Le stored procedure devono sempre indicare un esito negativo con un errore (se necessario, generato mediante THROW o RAISERROR) e non basarsi su un codice restituito per la segnalazione dell'errore.  È consigliabile evitare l'uso del codice restituito anche per la restituzione di dati dell'applicazione.
  
### <a name="examples-of-return-codes"></a>Esempi di codici restituiti  
 Nell'esempio seguente viene illustrata la procedura `usp_GetSalesYTD` con una modalità di gestione degli errori che consente di impostare valori speciali del codice restituito per errori diversi. Nella tabella seguente sono inclusi i valori interi assegnati dalla procedura a ogni possibile errore e viene indicato il significato di ogni valore.  
  
|Valore del codice restituito|Significato|  
|-----------------------|-------------|  
|0|L'esecuzione è stata completata.|  
|1|Non è stato specificato un valore obbligatorio per un parametro.|  
|2|Il valore specificato per il parametro non è valido.|  
|3|Si è verificato un errore durante il recupero del valore delle vendite.|  
|4|È stato trovato un valore delle vendite NULL per il venditore.|  
  
```sql
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
  
```sql
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
   PRINT 'ERROR: You must enter a valid last name for the sales person.'  
ELSE IF @ret_code = 3  
   PRINT 'ERROR: An error occurred getting sales value.'  
ELSE IF @ret_code = 4  
   PRINT 'ERROR: No sales recorded for this employee.'     
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [Cursori](../../relational-databases/cursors.md)   
 [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
