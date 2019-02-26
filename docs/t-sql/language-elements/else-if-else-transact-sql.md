---
title: ELSE (IF...ELSE) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ELSE
- ELSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 6f2b4278-0dea-4603-bbd3-7cbad602a645
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3d6e241d73040a30fcca5de3114110089259ab8b
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/25/2019
ms.locfileid: "56801725"
---
# <a name="else-ifelse-transact-sql"></a>ELSE (IF...ELSE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Impone le condizioni per l'esecuzione di un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)]. L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] (*sql_statement*) che segue *Boolean_expression* viene eseguita se *Boolean_expression* restituisce TRUE. La parola chiave facoltativa ELSE rappresenta un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] alternativa che viene eseguita quando l'argomento *Boolean_expression* restituisce FALSE o NULL.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
## <a name="arguments"></a>Argomenti  
 *Boolean_expression*  
 Espressione che restituisce TRUE o FALSE. Se *Boolean_expression* contiene un'istruzione SELECT, tale istruzione deve essere racchiusa tra parentesi.  
  
 { *sql_statement* | *statement_block* }  
 Qualsiasi istruzione o gruppo di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] valido definito con un blocco di istruzioni. Per definire un blocco di istruzioni (batch), utilizzare le parole chiave del linguaggio per il controllo di flusso BEGIN ed END. Sebbene tutte le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] siano valide nell'ambito di un blocco BEGIN...END, alcune istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] non devono essere raggruppate nello stesso batch (blocco di istruzioni).  
  
## <a name="result-types"></a>Tipi restituiti  
 **Boolean**  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-a-simple-boolean-expression"></a>A. Esecuzione di un'espressione booleana  
 Nell'esempio seguente è presente un'espressione booleana semplice (`1=1`) con valore true e di conseguenza viene stampata la prima istruzione.  
  
```  
IF 1 = 1 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
```  
  
 Nell'esempio seguente è presente un'espressione booleana semplice (`1=2`) con valore false e di conseguenza viene stampata la seconda istruzione.  
  
```  
IF 1 = 2 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
GO  
```  
  
### <a name="b-using-a-query-as-part-of-a-boolean-expression"></a>b. Utilizzo di una query come parte di un'espressione booleana  
 Nell'esempio seguente viene eseguita una query come parte dell'espressione booleana. Poiché nella tabella `Product` sono presenti 10 biciclette che soddisfano la clausola `WHERE`, verrà eseguita la prima istruzione di stampa. Modificare `> 5` in `> 15` per ottenere il modo in cui potrebbe essere eseguita la seconda parte dell'istruzione.  
  
```  
USE AdventureWorks2012;  
GO  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
PRINT 'There are more than 5 Touring-3000 bicycles.'  
ELSE PRINT 'There are 5 or less Touring-3000 bicycles.' ;  
GO  
```  
  
### <a name="c-using-a-statement-block"></a>C. Utilizzo di un blocco di istruzioni  
 Nell'esempio seguente viene eseguita una query come parte dell'espressione booleana e successivamente vengono eseguiti blocchi di istruzioni leggermente diversi in base al risultato dell'espressione booleana. Ogni blocco di istruzioni inizia con `BEGIN` e termina con `END`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @AvgWeight decimal(8,2), @BikeCount int  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
BEGIN  
   SET @BikeCount =   
        (SELECT COUNT(*)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   SET @AvgWeight =   
        (SELECT AVG(Weight)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   PRINT 'There are ' + CAST(@BikeCount AS varchar(3)) + ' Touring-3000 bikes.'  
   PRINT 'The average weight of the top 5 Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.';  
END  
ELSE   
BEGIN  
SET @AvgWeight =   
        (SELECT AVG(Weight)  
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%' );  
   PRINT 'Average weight of the Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.' ;  
END ;  
GO  
```  
  
### <a name="d-using-nested-ifelse-statements"></a>D. Utilizzo di istruzioni IF...ELSE nidificate  
 L'esempio seguente mostra come è possibile annidare più istruzioni IF ... ELSE. Impostare la variabile `@Number` su `5`, `50` e `500` per eseguire il test di ogni istruzione.  
  
```  
DECLARE @Number int;  
SET @Number = 50;  
IF @Number > 100  
   PRINT 'The number is large.';  
ELSE   
   BEGIN  
      IF @Number < 10  
      PRINT 'The number is small.';  
   ELSE  
      PRINT 'The number is medium.';  
   END ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-query-as-part-of-a-boolean-expression"></a>E: Utilizzo di una query come parte di un'espressione booleana  
 L'esempio seguente usa `IF...ELSE` per determinare quale delle due risposte visualizzare all'utente, in base al peso di un elemento nella tabella `DimProduct`.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct WHERE ProductKey=@productKey)   
    (SELECT @productKey, EnglishDescription, Weight, 'This product is too heavy to ship and is only available for pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
ELSE  
    (SELECT @productKey, EnglishDescription, Weight, 'This product is available for shipping or pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Elementi del linguaggio per il controllo di flusso &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  


