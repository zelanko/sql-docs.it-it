---
title: RIGHT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RIGHT_TSQL
- RIGHT
dev_langs:
- TSQL
helpviewer_keywords:
- rightmost character of expression
- RIGHT function
- character strings [SQL Server], RIGHT
ms.assetid: 43f1fe1f-aa18-47e3-ba20-e03e32254a6d
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6cb8be487b665e49a79a74d398ff2e3fbabd3a2e
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635685"
---
# <a name="right-transact-sql"></a>RIGHT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce la parte finale di una stringa di caratteri, di lunghezza pari al numero di caratteri specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
RIGHT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *character_expression*  
 [Espressione](../../t-sql/language-elements/expressions-transact-sql.md) di dati di tipo carattere o binario. *character_expression* può essere una costante, una variabile o una colonna. *character_expression* può essere di qualsiasi tipo di dati, eccetto **text** o **ntext**, implicitamente convertibile in **varchar** o **nvarchar**. In alternativa usare la funzione [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) per convertire in modo esplicito *character_expression*.  
  
 *integer_expression*  
 Valore Integer positivo che specifica quanti caratteri di *character_expression* verranno restituiti. Se l'argomento *integer_expression* è negativo, viene restituito un errore. Se *integer_expression* è di tipo **bigint** e contiene un valore elevato, *character_expression* deve essere di un tipo di dati di grandi dimensioni, ad esempio **varchar(max)** .  
  
## <a name="return-types"></a>Tipi restituiti  
 Restituisce **varchar** quando *character_expression* è un tipo di dati carattere non Unicode.  
  
 Restituisce **nvarchar** quando *character_expression* è un tipo di dati carattere Unicode.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caratteri supplementari (coppie di surrogati)  
 Quando si utilizzano le regole di confronto SC, la funzione RIGHT considera una coppia di surrogati UTF-16 come un singolo carattere. Per altre informazioni, vedere [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-right-with-a-column"></a>A. Uso di LEFT con una colonna  
 Nell'esempio seguente vengono restituiti gli ultimi cinque caratteri del nome di ciascuna persona nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT RIGHT(FirstName, 5) AS 'First Name'  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
First Name  
----------  
Ken  
Terri  
berto  
Rob  
  
(4 row(s) affected)  
  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-right-with-a-column"></a>B. Uso di RIGHT con una colonna  
 Nell'esempio seguente vengono restituiti gli ultimi cinque caratteri di ogni cognome nella tabella `DimEmployee`.  
  
```  
-- Uses AdventureWorks  
  
SELECT RIGHT(LastName, 5) AS Name  
FROM dbo.DimEmployee  
ORDER BY EmployeeKey;  
```  
  
 Set di risultati parziale:  
  
 ```
Name
-----
lbert
Brown
rello
lters
 ```  
  
### <a name="c-using-right-with-a-character-string"></a>C. Uso di LEFT con una stringa di caratteri  
 Nell'esempio seguente viene usata la funzione `RIGHT` per restituire gli ultimi due caratteri della stringa di caratteri `abcdefg`.  
  
```  
SELECT RIGHT('abcdefg', 2); 
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-------  
fg
```  
  
## <a name="see-also"></a>Vedere anche  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funzioni per i valori stringa &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

