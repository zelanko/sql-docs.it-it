---
title: DATETIME2FROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c74fae6a8f634170eaf11c9a63a3cf91a5b404d6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823175"
---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Questa funzione restituisce un valore di tipo **datetime2** per gli argomenti date e time. Il valore restituito ha una precisione specificata dall'argomento precision.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argomenti  
*year*  
Espressione Integer che specifica un anno.
  
*month*  
Espressione Integer che specifica un mese.
  
*day*  
Espressione Integer che specifica un giorno.
  
*hour*  
Espressione Integer che specifica le ore.
  
*minute*  
Espressione Integer che specifica i minuti.
  
*secondi*  
Espressione Integer che specifica i secondi.
  
*fractions*  
Espressione Integer che specifica un valore per i secondi frazionari.
  
*precisione*  
Espressione Integer che specifica la precisione del valore **datetime2** che verrà restituito da `DATETIME2FROMPARTS`.
  
## <a name="return-types"></a>Tipi restituiti
**datetime2(** *precision* **)**
  
## <a name="remarks"></a>Osservazioni  
`DATETIME2FROMPARTS` restituisce un valore di tipo **datetime2** completamente inizializzato. `DATETIME2FROMPARTS` genererà un errore se almeno un argomento obbligatorio ha un valore non valido. `DATETIME2FROMPARTS` restituisce null se almeno un argomento obbligatorio ha un valore null. Se tuttavia l'argomento *precision* ha un valore null, `DATETIME2FROMPARTS` genererà un errore.

L'argomento *fractions* dipende dall'argomento *precision*. Ad esempio, per un valore di *precision* pari a 7, ogni frazione rappresenta 100 nanosecondi, mentre per *precision* pari a 3, ogni frazione rappresenta un millisecondo. Per un valore di *precision* pari a zero, anche il valore di *fractions* deve essere zero. In caso contrario, `DATETIME2FROMPARTS` genererà un errore.
  
Questa funzione supporta la comunicazione remota con i server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e versioni successive. Non supporterà la comunicazione remota con i server con versioni precedenti a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Esempi  
  
### <a name="a-an-example-without-fractions-of-a-second"></a>R. Esempio senza frazioni di un secondo  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Esempio con frazioni di un secondo  
Questo esempio illustra l'uso dei parametri *fractions* e *precision*:
  
1.  Se *fractions* ha valore 5 e *precision* ha valore 1, il valore di *fractions* corrisponde a 5/10 di secondo.  
  
2.  Se *fractions* ha valore 50 e *precision* ha valore 2, il valore di *fractions* corrisponde a 50/100 di secondo.  
  
3.  Se *fractions* ha valore 500 e *precision* ha valore 3, il valore di *fractions* corrisponde a 500/1000 di secondo.  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vedere anche
[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)
  
  

