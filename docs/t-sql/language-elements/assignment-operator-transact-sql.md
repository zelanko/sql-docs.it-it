---
description: = (operatore di assegnazione) (Transact-SQL)
title: = (operatore di assegnazione) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], assignment
- assignment operators [Transact-SQL]
- headings [SQL Server columns]
- relationships [SQL Server], assignment operators
- column headings [SQL Server]
ms.assetid: c3040db6-21d6-40ac-a783-82c98ec006cc
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86e9675dd5a11869c73f8f7dc77c12589cd38e1f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468042"
---
# <a name="-assignment-operator-transact-sql"></a>= (operatore di assegnazione) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Il segno di uguale (=) è l'unico operatore di assegnazione supportato in [!INCLUDE[tsql](../../includes/tsql-md.md)]. Nell'esempio seguente viene creata la variabile `@MyCounter` e quindi viene utilizzato l'operatore di assegnazione per impostare `@MyCounter` su un valore restituito da un'espressione.  
  
```sql  
DECLARE @MyCounter INT;  
SET @MyCounter = 1;  
```  
  
 È inoltre possibile utilizzare l'operatore di assegnazione per stabilire una relazione tra l'intestazione di una colonna e l'espressione che definisce i valori di tale colonna. Nell'esempio seguente vengono visualizzate le intestazioni di colonna `FirstColumnHeading` e `SecondColumnHeading`. Nell'intestazione di colonna `xyz` viene visualizzata la stringa `FirstColumnHeading` per tutte le righe e nell'intestazione di colonna `Product` vengono elencati gli ID di tutti i prodotti della tabella `SecondColumnHeading`.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT FirstColumnHeading = 'xyz',  
       SecondColumnHeading = ProductID  
FROM Production.Product;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Operatori &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operatori composti &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Espressioni &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
