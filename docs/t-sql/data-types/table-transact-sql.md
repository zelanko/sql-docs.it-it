---
title: table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d4a36b287554332589f11a352233eaffe972ac06
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981736"
---
# <a name="table-transact-sql"></a>table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

È un tipo di dati speciale usato per archiviare un set di risultati per elaborazioni successive. Il tipo **table** viene principalmente usato per l'archiviazione temporanea di un set di righe restituito come set di risultati di una funzione con valori di tabella. È possibile dichiarare funzioni e variabili di tipo **table**. Le variabili di tipo **table** possono essere usate in funzioni, stored procedure e batch. Per dichiarare variabili di tipo **table**, usare [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  

**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
table_type_definition ::=   
    TABLE ( { <column_definition> | <table_constraint> } [ ,...n ] )   
  
<column_definition> ::=   
    column_name scalar_data_type   
    [ COLLATE <collation_definition> ]   
    [ [ DEFAULT constant_expression ] | IDENTITY [ ( seed , increment ) ] ]   
    [ ROWGUIDCOL ]   
    [ column_constraint ] [ ...n ]   
  
 <column_constraint> ::=   
    { [ NULL | NOT NULL ]   
    | [ PRIMARY KEY | UNIQUE ]   
    | CHECK ( logical_expression )   
    }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n ] )  
     | CHECK ( logical_expression )   
     }   
```  
  
## <a name="arguments"></a>Argomenti  
*table_type_definition*  
Stesso subset di informazioni utilizzate per definire una tabella nell'istruzione CREATE TABLE. La dichiarazione di tabella include definizioni di colonna, nomi, tipi di dati e vincoli. Gli unici tipi di vincoli consentiti sono PRIMARY KEY, UNIQUE KEY e NULL.  
Per altre informazioni sulla sintassi, vedere [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md), [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) e [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  
*collation_definition*  
Regole di confronto della colonna costituite da impostazioni locali di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e stile di confronto, impostazioni locali di Windows e notazione binaria oppure regole di confronto di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non si specifica *collation_definition*, la colonna eredita le regole di confronto del database corrente. Se invece viene specificata come tipo CLR (Common Language Runtime) definito dall'utente, la colonna eredita le regole di confronto del tipo definito dall'utente.
  
## <a name="remarks"></a>Remarks  
Nella clausola FROM di un batch, alle variabili di tipo **table** viene fatto riferimento in base al nome, come illustrato nell'esempio seguente:
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
All'esterno di una clausola FROM, è necessario fare riferimento alle variabili di tipo **table** tramite un alias, come illustrato nell'esempio seguente:
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
Per query in scala ridotta con piani di query che non vengono modificati e quando la ricompilazione è una preoccupazione dominante, le variabili di tipo **table** offrono i vantaggi seguenti:
-   Le variabili di tipo **table** funzionano in modo analogo alle variabili locali. Queste variabili hanno un ambito ben definito, La variabile corrisponde alla funzione, alla stored procedure o al batch in cui è dichiarata.  
     All'interno del proprio ambito, le variabili **table** possono essere usate come normali tabelle. in tutti i casi in cui è possibile utilizzare una tabella o espressione di tabella in istruzioni SELECT, INSERT, UPDATE e DELETE. Non è tuttavia possibile usare **table** nell'istruzione seguente:  
  
```sql
SELECT select_list INTO table_variable;
```
  
La pulizia delle variabili di tipo **table** viene eseguita automaticamente alla fine della funzione, della stored procedure o del batch in cui sono definite.
  
-   Quando si usano variabili di tipo **table** nelle stored procedure, il numero di ricompilazioni delle stored procedure risulta minore rispetto a quando vengono usate tabelle temporanee, in assenza di scelte basate sui costi che influiscono sulle prestazioni.  
-   La durata delle transazioni che includono variabili di tipo **table** corrisponde solo alla durata dell'aggiornamento della variabile di tipo **table**. Le variabili di tipo **table** richiedono quindi una minore quantità di risorse di blocco e registrazione.  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni
Le variabili di tipo **table** non includono statistiche di distribuzione e non attivano ricompilazioni. In molti casi, l'utilità di ottimizzazione creerà un piano di query basandosi sul presupposto che la variabile di tabella non contenga righe. Per questo motivo, è necessario prestare attenzione in caso di utilizzo di una variabile di tabella se si prevede un numero elevato di righe (maggiore di 100). In tal caso, le tabelle temporanee potrebbero rappresentare una soluzione migliore. Per le query che uniscono in join la variabile di tabella con altre tabelle, usare l'hint RECOMPILE, con cui l'utilità di ottimizzazione userà la cardinalità corretta per la variabile di tabella.
  
Le variabili di tipo **table** non sono supportate nel modello di ragionamento basato sui costi dell'utilità di ottimizzazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È quindi consigliabile non usarle quando sono necessarie scelte basate sui costi per ottenere un piano di query efficiente. È preferibile utilizzare le tabelle temporanee quando sono necessarie scelte basate sui costi, Tale piano include in genere query con join, decisioni di parallelismo e scelte di selezione degli indici.
  
Per le query che modificano le variabili di tipo **table** non vengono generati piani di esecuzione di query parallele. La modifica di variabili di tipo **table** di grandi dimensioni o di variabili di tipo **table** in query complesse può influire sulle prestazioni. Nei casi in cui le variabili di tipo **table** vengono modificate, valutare la possibilità di usare invece tabelle temporanee. Per altre informazioni, vedere [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md). Le query che leggono le variabili di tipo **table** senza modificarle possono comunque essere eseguite in parallelo.
  
Non è possibile creare indici in modo esplicito su variabili di tipo **table** e per le variabili di tipo **table** non vengono mantenute statistiche. A partire da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], è stata introdotta una nuova sintassi che consente di creare determinati tipi di indice inline con la definizione della tabella.  Usando questa nuova sintassi, è possibile creare indici su variabili **tabella** come parte della definizione della tabella. In alcuni casi, è possibile ottenere un miglioramento delle prestazioni usando tabelle temporanee, che offrono statistiche e supporto completo per l'indice. Per altre informazioni sulle tabelle temporanee e la creazione di indici inline, vedere [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).

I vincoli CHECK, i valori DEFAULT e le colonne calcolate nella dichiarazione del tipo **table** non possono chiamare funzioni definite dall'utente.
  
L'operazione di assegnazione tra variabili di tipo **table** non è supportata.
  
Dato che hanno ambito limitato e non fanno parte del database permanente, le variabili di tipo **table** non sono interessate dalle operazioni di rollback di transazioni.
  
Le variabili di tabella non possono essere modificate dopo la creazione.

## <a name="table-variable-deferred-compilation"></a>Compilazione posticipata delle variabili di tabella
**La compilazione posticipata delle variabili di tabella** migliora la qualità del piano e le prestazioni generali per le query che fanno riferimento a variabili di tabella. Durante l'ottimizzazione e la compilazione iniziale del piano, questa funzionalità propagherà le stime della cardinalità basate sui conteggi effettivi delle righe di variabili di tabella. Queste informazioni esatte sui conteggi delle righe verranno quindi usate per ottimizzare le operazioni del piano a valle.

> [!NOTE]
> La compilazione posticipata delle variabili di tabella è una funzionalità di anteprima pubblica in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)].

Con la compilazione posticipata delle variabili di tabella, la compilazione di un'istruzione che fa riferimento a una variabile di tabella viene posticipata fino alla prima esecuzione effettiva dell'istruzione. Questo comportamento della compilazione posticipata è identico a quello delle tabelle temporanee. Questo cambiamento determina l'uso della cardinalità effettiva invece dell'ipotesi originale di una sola riga. 

Per abilitare l'anteprima pubblica della compilazione posticipata delle variabili di tabella, abilitare il livello di compatibilità del database 150 per il database a cui si è connessi quando si esegue la query.

La compilazione posticipata delle variabili di tabella **non** modifica altre caratteristiche delle variabili di tabella. Ad esempio, questa funzionalità non aggiunge statistiche di colonna alle variabili di tabella.

La compilazione posticipata delle variabili di tabella **non aumenta la frequenza di ricompilazione**. Piuttosto, sposta la posizione di esecuzione della compilazione iniziale. Il piano memorizzato nella cache risultante viene generato in base al conteggio delle righe delle variabili di tabella della compilazione posticipata iniziale. Il piano memorizzato nella cache viene riusato da query consecutive, fino a quando non viene rimosso o ricompilato. 

Il conteggio delle righe delle variabili di tabella usato per la compilazione del piano iniziale rappresenta un valore tipico e potrebbe essere diverso da un'ipotesi di conteggio di righe fisso. Se è diverso, è un vantaggio per le operazioni a valle. Se il conteggio delle righe delle variabili di tabella varia notevolmente tra le esecuzioni, questa funzionalità potrebbe non migliorare le prestazioni.

### <a name="disabling-table-variable-deferred-compilation-without-changing-the-compatibility-level"></a>Disabilitazione della compilazione posticipata delle variabili di tabella senza modificare il livello di compatibilità
Disabilitare la compilazione posticipata delle variabili di tabella nell'ambito del database o dell'istruzione mantenendo comunque un livello di compatibilità del database 150 o superiore. Per disabilitare la compilazione posticipata delle variabili di tabella per tutte le esecuzioni di query originate dal database, eseguire questo esempio nel contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = OFF;
```

Per riabilitare la compilazione posticipata delle variabili di tabella per tutte le esecuzioni di query originate dal database, eseguire questo esempio nel contesto del database applicabile:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET DEFERRED_COMPILATION_TV = ON;
```

È anche possibile disabilitare la compilazione posticipata delle variabili di tabella per una query specifica assegnando DISABLE_DEFERRED_COMPILATION_TV come hint per la query USE HINT.  Esempio:

```sql
DECLARE @LINEITEMS TABLE 
    (L_OrderKey INT NOT NULL,
     L_Quantity INT NOT NULL
    );

INSERT @LINEITEMS
SELECT L_OrderKey, L_Quantity
FROM dbo.lineitem
WHERE L_Quantity = 5;

SELECT  O_OrderKey,
    O_CustKey,
    O_OrderStatus,
    L_QUANTITY
FROM    
    ORDERS,
    @LINEITEMS
WHERE   O_ORDERKEY  =   L_ORDERKEY
    AND O_OrderStatus = 'O'
OPTION (USE HINT('DISABLE_DEFERRED_COMPILATION_TV'));
```

  
## <a name="examples"></a>Esempi  
  
### <a name="a-declaring-a-variable-of-type-table"></a>A. Dichiarazione di una variabile di tipo table  
Nell'esempio seguente viene creata una variabile di tipo `table` in cui vengono archiviati i valori specificati nella clausola OUTPUT dell'istruzione UPDATE. Questa variabile è seguita da due istruzioni `SELECT` che restituiscono i valori in `@MyTableVar` e i risultati dell'operazione di aggiornamento nella tabella `Employee`. I risultati nella colonna `INSERTED.ModifiedDate` sono diversi rispetto ai valori nella colonna `ModifiedDate` della tabella `Employee`. Questa differenza è causata dalla definizione nella tabella `Employee` del trigger `AFTER UPDATE`, che aggiorna il valore di `ModifiedDate` alla data corrente. Le colonne restituite da `OUTPUT`, tuttavia, riflettono i dati prima dell'attivazione dei trigger. Per altre informazioni, vedere [Clausola OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).
  
```sql
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25   
OUTPUT INSERTED.BusinessEntityID,  
       DELETED.VacationHours,  
       INSERTED.VacationHours,  
       INSERTED.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
--Note that ModifiedDate reflects the value generated by an  
--AFTER UPDATE trigger.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. Creazione di una funzione inline con valori di tabella  
Nell'esempio seguente viene restituita una funzione inline con valori di tabella. L'esempio restituisce tre colonne `ProductID`, `Name` e l'aggregazione dei totali da inizio anno per negozio, come `YTD Total` per ogni prodotto venduto al negozio.
  
```sql
USE AdventureWorks2012;  
GO  
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
GO  
```  
  
Per richiamare la funzione, eseguire la query seguente.
  
```sql
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
## <a name="see-also"></a>Vedere anche
[COLLATE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[Funzioni definite dall'utente](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[Usare parametri con valori di tabella &#40;Motore di database&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[Hint di query &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)
