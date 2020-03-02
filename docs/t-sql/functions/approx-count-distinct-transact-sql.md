---
title: APPROX_COUNT_DISTINCT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPROX_COUNT_DISTINCT
dev_langs:
- TSQL
author: joesackmsft
ms.author: josack
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 56485f088d375ceffaadb923999f27f794acb5c5
ms.sourcegitcommit: d876425e5c465ee659dd54e7359cda0d993cbe86
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/24/2020
ms.locfileid: "77568114"
---
# <a name="approx_count_distinct-transact-sql"></a>APPROX_COUNT_DISTINCT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Questa funzione restituisce il numero approssimativo di valori univoci non Null in un gruppo. 
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse and Parallel Data Warehouse  

APPROX_COUNT_DISTINCT ( expression )   
```  
  
## <a name="arguments"></a>Argomenti  
*expression*  
[Espressione](../../t-sql/language-elements/expressions-transact-sql.md) di qualsiasi tipo, a eccezione di **image**, **sql_variant**, **ntext** o **text**. 

## <a name="return-types"></a>Tipi restituiti
 **bigint**  
  
## <a name="remarks"></a>Osservazioni  
`APPROX_COUNT_DISTINCT( expression )` valuta un'espressione per ogni riga in un gruppo e restituisce il numero approssimativo di valori univoci non Null in un gruppo. Questa funzione è progettata per fornire aggregazioni su set di dati di grandi dimensioni in cui la velocità di risposta è più importante della precisione assoluta.  

`APPROX_COUNT_DISTINCT` è progettata per l'uso in scenari Big Data ed è ottimizzata per le condizioni seguenti:
- Accesso a set di dati con più di milioni di righe *e*
- Aggregazione di una colonna o di più colonne con molti valori distinti

L'implementazione della funzione garantisce un tasso di errore fino al 2% con una probabilità del 97%. 

`APPROX_COUNT_DISTINCT` richiede meno memoria rispetto a un'operazione COUNT DISTINCT completa.  Dato il footprint di memoria più piccolo, è meno probabile che `APPROX_COUNT_DISTINCT` causi lo spill della memoria su disco rispetto a un'operazione COUNT DISTINCT precisa. Per altre informazioni sull'algoritmo usato per ottenere questo risultato, vedere [HyperLogLog](https://en.wikipedia.org/wiki/HyperLogLog).

> [!NOTE]
> Con le stringhe sensibili alle regole di confronto, APPROX_COUNT_DISTINCT usa una corrispondenza binaria e fornisce i risultati che verrebbero generati in presenza di regole di confronto BIN e non BIN2. 
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-approx_count_distinct"></a>R. Uso di APPROX_COUNT_DISTINCT 
Questo esempio restituisce il numero approssimativo di chiavi di ordine diverse dalla tabella orders.
  
```sql
SELECT APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders;
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Approx_Distinct_OrderKey
------------------------
15164704
```
  
### <a name="b-using-approx_count_distinct-with-group-by"></a>B. Uso di APPROX_COUNT_DISTINCT con GROUP BY 
Questo esempio restituisce il numero approssimativo di chiavi di ordine diverse in base allo stato dell'ordine dalla tabella orders. 
  
```sql
SELECT O_OrderStatus, APPROX_COUNT_DISTINCT(O_OrderKey) AS Approx_Distinct_OrderKey
FROM dbo.Orders
GROUP BY O_OrderStatus
ORDER BY O_OrderStatus; 
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
O_OrderStatus                                                    Approx_Distinct_OrderKey
---------------------------------------------------------------- ------------------------
F                                                                7397838
O                                                                7387803
P                                                                388036
```
    
## <a name="see-also"></a>Vedere anche
[Funzioni di aggregazione &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md) 
