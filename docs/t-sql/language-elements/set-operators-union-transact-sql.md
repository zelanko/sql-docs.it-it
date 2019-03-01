---
title: UNION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UNION
- UNION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UNION queries
- combining query results
- UNION operator [SQL Server]
ms.assetid: 607c296f-8a6a-49bc-975a-b8d0c0914df7
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b4fddc20d2ee9adbfb0f67f88fcb75661ebc828
ms.sourcegitcommit: c61c7b598aa61faa34cd802697adf3a224aa7dc4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56154796"
---
# <a name="set-operators---union-transact-sql"></a>Operatori sui set - UNION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Combina i risultati di due o più query in un unico set di risultati. Questo set include tutte le righe che appartengono a tutte le query nell'operazione di unione. L'operazione UNION è diversa dall'utilizzo di join che combinano le colonne di due tabelle.  
  
Di seguito sono riportate le regole di base per la combinazione dei set di risultati di due query tramite l'istruzione UNION:  
  
-   Tutte le query devono includere lo stesso numero di colonne nello stesso ordine.  
  
-   I tipi di dati devono essere compatibili.  
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
    { <query_specification> | ( <query_expression> ) }   
  UNION [ ALL ]   
  <query_specification | ( <query_expression> )   
 [ UNION [ ALL ] <query_specification> | ( <query_expression> )   
    [ ...n ] ]   
```  
  
## <a name="arguments"></a>Argomenti  
\<query_specification> | ( \<query_expression> ) Specifica o espressione di query che restituisce dati da combinare con i dati di un'altra specifica o espressione di query. Le definizioni delle colonne di un'operazione UNION non devono essere necessariamente identiche, ma devono essere compatibili tramite una conversione implicita. Se i tipi di dati sono diversi, il tipo di dati risultante viene definito in base alle regole valide per la [precedenza dei tipi di dati](../../t-sql/data-types/data-type-precedence-transact-sql.md). Quando i tipi sono gli stessi ma differiscono per precisione, scala o lunghezza, il risultato viene determinato in base alle stesse regole previste per la combinazione di espressioni. Per altre informazioni, vedere [Precisione, scala e lunghezza &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
Le colonne con tipo di dati **xml** devono essere equivalenti. Tutte le colonne devono essere tipizzate in un XML Schema oppure senza tipo. In caso di colonne tipizzate, esse devono essere tipizzate nella stessa raccolta di XML Schema.  
  
UNION  
Specifica che più set di risultati devono essere combinati e restituiti come singolo set di risultati.  
  
ALL  
Incorpora tutte le righe nei risultati, inclusi i duplicati. Se viene omesso, le righe duplicate vengono rimosse.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-a-simple-union"></a>A. Utilizzo di un semplice operatore UNION  
Nell'esempio seguente il set di risultati include il contenuto delle colonne `ProductModelID` e `Name` di entrambe le tabelle `ProductModel` e `Gloves`.  
 
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Here is the simple union.  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
```  
  
### <a name="b-using-select-into-with-union"></a>b. Utilizzo di SELECT INTO con UNION  
Nell'esempio seguente la clausola `INTO` nella seconda istruzione `SELECT` specifica che la tabella denominata `ProductResults` contiene il set di risultati finale ottenuto con l'unione delle colonne selezionate delle tabelle `ProductModel` e `Gloves`. La tabella `Gloves` viene creata nella prima istruzione `SELECT`.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.ProductResults', 'U') IS NOT NULL  
DROP TABLE dbo.ProductResults;  
GO  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
INTO dbo.ProductResults  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
SELECT ProductModelID, Name   
FROM dbo.ProductResults;  
  
```  
  
### <a name="c-using-union-of-two-select-statements-with-order-by"></a>C. Utilizzo dell'operatore UNION in due istruzioni SELECT con la clausola ORDER BY  
L'ordine di alcuni parametri utilizzati con la clausola UNION è importante. Nell'esempio seguente vengono illustrati l'utilizzo errato e quello corretto di `UNION` in due istruzioni `SELECT` in cui una colonna deve essere rinominata nell'output.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
/* INCORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
ORDER BY Name  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
/* CORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
  
```  
  
### <a name="d-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>D. Utilizzo dell'operatore UNION in tre istruzioni SELECT per illustrare gli effetti dell'opzione ALL e delle parentesi  
Negli esempi seguenti viene utilizzato l'operatore `UNION` per combinare i risultati di tre tabelle contenenti 5 righe di dati identiche. Nel primo esempio viene utilizzato `UNION ALL` per mostrare i record duplicati e vengono restituite tutte le 15 righe. Nel secondo esempio l'operatore `UNION` viene utilizzato senza l'opzione `ALL` per eliminare le righe duplicate dai risultati combinati delle tre istruzioni `SELECT` e vengono restituite 5 righe.  
  
Il terzo esempio usa `ALL` con il primo operatore `UNION` e il secondo operatore `UNION`, che non usa `ALL`, viene racchiuso tra parentesi. Il secondo operatore `UNION` viene elaborato per primo in quanto è racchiuso tra parentesi e restituisce cinque righe perché l'opzione `ALL` non viene usata e i duplicati vengono rimossi. Queste 5 righe vengono combinate con i risultati della prima istruzione `SELECT` mediante le parole chiave `UNION ALL`. Questo esempio non rimuove i duplicati tra i due set di cinque righe. Il risultato finale include 10 righe.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.EmployeeOne', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeOne;  
GO  
IF OBJECT_ID ('dbo.EmployeeTwo', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeTwo;  
GO  
IF OBJECT_ID ('dbo.EmployeeThree', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeThree;  
GO  
  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeOne  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeTwo  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeThree  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
-- Union ALL  
SELECT LastName, FirstName, JobTitle  
FROM dbo.EmployeeOne  
UNION ALL  
SELECT LastName, FirstName ,JobTitle  
FROM dbo.EmployeeTwo  
UNION ALL  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle  
FROM dbo.EmployeeOne  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeOne  
UNION ALL  
(  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree  
);  
GO  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-simple-union"></a>E. Utilizzo di un semplice operatore UNION  
Nell'esempio seguente il set di risultati include il contenuto delle colonne `CustomerKey` di entrambe le tabelle `FactInternetSales` e `DimCustomer`. Poiché la parola chiave ALL non viene usata, i duplicati vengono esclusi dai risultati.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="f-using-union-of-two-select-statements-with-order-by"></a>F. Utilizzo dell'operatore UNION in due istruzioni SELECT con la clausola ORDER BY  
 Quando un'istruzione SELECT in un'istruzione UNION include una clausola ORDER BY, tale clausola deve essere inserita dopo tutte le istruzioni SELECT. Nell'esempio seguente vengono illustrati l'uso errato e quello corretto di `UNION` in due istruzioni `SELECT` in cui una colonna è ordinata con ORDER BY.  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT  
SELECT CustomerKey   
FROM FactInternetSales    
ORDER BY CustomerKey  
UNION   
SELECT CustomerKey   
FROM DimCustomer  
ORDER BY CustomerKey;  
  
-- CORRECT   
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="g-using-union-of-two-select-statements-with-where-and-order-by"></a>G. Uso dell'operatore UNION in due istruzioni SELECT con WHERE e ORDER BY  
Nell'esempio seguente vengono illustrati l'uso errato e quello corretto di `UNION` in due istruzioni `SELECT` in cui sono necessarie le clausole WHERE e ORDER BY.  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT   
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
ORDER BY CustomerKey   
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
  
-- CORRECT  
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="h-using-union-of-three-select-statements-to-show-effects-of-all-and-parentheses"></a>H. Uso dell'operatore UNION in tre istruzioni SELECT per illustrare gli effetti dell'opzione ALL e delle parentesi  
L'esempio seguente usa `UNION` per combinare i risultati della **stessa tabella** per illustrare gli effetti dell'opzione ALL e delle parentesi quando si usa `UNION`.  
  
Il primo esempio usa `UNION ALL` per visualizzare i record duplicati e restituisce ogni riga nella tabella di origine tre volte. Nel secondo esempio l'operatore `UNION` viene usato senza l'opzione `ALL` per eliminare le righe duplicate dai risultati combinati delle tre istruzioni `SELECT` e vengono restituite solo le righe non duplicate dalla tabella di origine.  
  
Il terzo esempio usa `ALL` con il primo operatore `UNION` e il secondo operatore `UNION`, che non usa`ALL`, viene racchiuso tra parentesi. Il secondo operatore `UNION` viene elaborato per primo perché è racchiuso tra parentesi. Restituisce solo le righe non duplicate della tabella perché l'opzione `ALL` non viene usata e i duplicati vengono rimossi. Queste righe vengono combinate con i risultati della prima istruzione `SELECT` mediante le parole chiave `UNION ALL`. Questo esempio non rimuove i duplicati tra i due set.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL  
(  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
);  
```  
  
## <a name="see-also"></a>Vedere anche  
[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
[Esempi di istruzioni SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md)  
  
  

