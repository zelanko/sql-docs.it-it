---
title: Precedenza degli operatori (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], precedence
- operator precedence [Transact-SQL]
- order of operator execution [Transact-SQL]
- precedence [SQL Server], operators
ms.assetid: f04d2439-6fff-4e4c-801f-cc62faef510a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 933212da81784d7d186fc6ef7c0cdfaa4edab24b
ms.sourcegitcommit: 7ead3a042d369315fc83a9ccc3d74f62e7b05bc0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2019
ms.locfileid: "54012317"
---
# <a name="operator-precedence-transact-sql"></a>Precedenza degli operatori (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Quando in un'espressione complessa vengono utilizzati più operatori, la sequenza di esecuzione delle operazioni è determinata dalla precedenza degli operatori. L'ordine di esecuzione può modificare in modo significativo il valore restituito.  
  
 Nella tabella seguente sono indicati i livelli di precedenza degli operatori. Un operatore con livelli di precedenza più elevati viene valutato prima di un operatore con un livello di precedenza inferiore (nella tabella seguente 1 è il livello più elevato e 8 è il livello più basso).
  
|Level|Operatori|  
|-----------|---------------|  
|1|~ (NOT bit per bit)|  
|2|* (moltiplicazione), / (divisione), % (modulo)|  
|3|+ (positivo), - (negativo), + (addizione), + (concatenazione), - (sottrazione), & (AND bit per bit), ^ (OR esclusivo bit per bit), &#124; (OR bit per bit)|  
|4|=, >, \<, >=, <=, <>, !=, !>, !< (operatori di confronto)|  
|5|NOT|  
|6|AND|  
|7|ALL, ANY, BETWEEN, IN, LIKE, OR, SOME|  
|8|= (assegnazione)|  
  
 Se due operatori di un'espressione hanno lo stesso livello di precedenza, vengono valutati da sinistra verso destra in base alla posizione nell'espressione. Nell'espressione utilizzata nell'istruzione `SET` seguente, ad esempio, l'operatore di sottrazione viene valutato prima dell'operatore di addizione.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 4 - 2 + 27;  
-- Evaluates to 2 + 27 which yields an expression result of 29.  
SELECT @MyNumber;  
```  
  
 Per ignorare l'ordine di precedenza predefinito degli operatori in un'espressione, è possibile utilizzare le parentesi. Tutti gli operatori racchiusi tra parentesi vengono valutati per primi in modo da ottenere un singolo valore, che verrà quindi utilizzato dagli operatori all'esterno delle parentesi.  
  
 Nell'espressione utilizzata nell'istruzione `SET` seguente, ad esempio, l'operatore di moltiplicazione ha un livello di precedenza più alto rispetto all'operatore di addizione e viene pertanto valutato per primo. Il risultato dell'espressione è `13`.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * 4 + 5;  
-- Evaluates to 8 + 5 which yields an expression result of 13.  
SELECT @MyNumber;  
```  
  
 Nell'espressione utilizzata nell'istruzione `SET` seguente le parentesi fanno sì che venga eseguita per prima l'addizione. Il risultato dell'espressione è `18`.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + 5);  
-- Evaluates to 2 * 9 which yields an expression result of 18.  
SELECT @MyNumber;  
```  
  
 Se in un'espressione vengono utilizzate parentesi nidificate, viene valutata per prima l'espressione più interna. Nell'esempio seguente con parentesi nidificate, l'espressione `5 - 3` corrisponde al set di parentesi più interno della struttura nidificata. Questa espressione restituisce il valore `2`. L'operatore di addizione (`+`) somma quindi questo risultato a `4`. Il valore restituito da questa operazione è `6`. Infine, il valore `6` viene moltiplicato per `2` e il risultato dell'espressione `12`.  
  
```sql  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + (5 - 3) );  
-- Evaluates to 2 * (4 + 2) which then evaluates to 2 * 6, and   
-- yields an expression result of 12.  
SELECT @MyNumber;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Operatori logici &#40;Transact-SQL&#41;](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [Operatori &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Funzioni predefinite &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
