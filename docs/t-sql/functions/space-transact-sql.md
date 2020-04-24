---
title: SPACE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SPACE_TSQL
- SPACE
dev_langs:
- TSQL
helpviewer_keywords:
- strings [SQL Server], repeated spaces
- repeated spaces
- SPACE function
ms.assetid: b4fac3b8-2d47-4c11-a6a6-009e5a538f40
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cca2bded1868bfb8d57cc8d68c50ec80afeeb28c
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635644"
---
# <a name="space-transact-sql"></a>SPACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una stringa di spazi ripetuti.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
SPACE ( integer_expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *integer_expression*  
 Valore intero positivo che indica il numero di spazi. Se l'argomento *integer_expression* è negativo, viene restituita una stringa Null.  
  
 Per altre informazioni, vedere [Espressioni &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Tipi restituiti  
 **varchar**  
  
## <a name="remarks"></a>Osservazioni  
 Per includere spazi in dati Unicode oppure per restituire più di 8000 spazi, utilizzare l'istruzione REPLICATE anziché SPACE.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono rimossi gli spazi dei cognomi e quindi vengono concatenati una virgola, due spazi e i nomi delle persone elencate nella tabella `Person` di `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT RTRIM(LastName) + ',' + SPACE(2) +  LTRIM(FirstName)  
FROM Person.Person  
ORDER BY LastName, FirstName;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente vengono rimossi gli spazi dei cognomi e quindi vengono concatenati una virgola, due spazi e i nomi delle persone elencate nella tabella `DimCustomer` di `AdventureWorksPDW2012`.  
  
```  
-- Uses AdventureWorks  
  
SELECT RTRIM(LastName) + ',' + SPACE(2) +  LTRIM(FirstName)  
FROM dbo.DimCustomer  
ORDER BY LastName, FirstName;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [REPLICATE &#40;Transact-SQL&#41;](../../t-sql/functions/replicate-transact-sql.md)   
 [Funzioni stringa &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Funzioni predefinite &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  


