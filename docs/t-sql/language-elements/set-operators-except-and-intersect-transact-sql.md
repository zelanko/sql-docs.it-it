---
title: EXCEPT e INTERSECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- INTERSECT_TSQL
- EXCEPT_TSQL
- INTERSECT
- EXCEPT
dev_langs:
- TSQL
helpviewer_keywords:
- EXCEPT operator [Transact-SQL]
- queries [SQL Server], comparing
- comparing queries
- INTERSECT operator
ms.assetid: b1019300-171a-4a1a-854f-e1e751de3565
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e3b60a01a114ab24be3dc76237134b3cbf34363
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396385"
---
# <a name="set-operators---except-and-intersect-transact-sql"></a>Operatori sui set - EXCEPT e INTERSECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituiscono righe distinte eseguendo un confronto dei risultati di due query.  
  
 EXCEPT restituisce righe distinte dalla query di input sinistra non generate dalla query di input destra.  
  
 INTERSECT restituisce righe distinte generate dall'operatore query di input sinistro e destro.  
  
 Le regole di base per la combinazione dei set di risultati di due query che utilizzano EXCEPT o INTERSECT sono le seguenti:  
  
-   Tutte le query devono includere lo stesso numero di colonne nello stesso ordine.  
  
-   I tipi di dati devono essere compatibili.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
{ <query_specification> | ( <query_expression> ) }   
{ EXCEPT | INTERSECT }  
{ <query_specification> | ( <query_expression> ) }  
```  
  
## <a name="arguments"></a>Argomenti  
 \<*query_specification*> | ( \<*query_expression*> )  
 Specifica di query o espressione di query che restituisce dati da confrontare con i dati di un'altra specifica o espressione di query. Le definizioni delle colonne coinvolte in un'operazione EXCEPT o INTERSECT non devono essere necessariamente identiche, ma devono essere confrontabili tramite una conversione implicita. Se i tipi di dati sono diversi, il tipo usato per eseguire il confronto e restituire i risultati viene determinato in base alle regole di [precedenza dei tipi di dati](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
 Se i tipi sono gli stessi ma la precisione, la scala o la lunghezza è diversa, il risultato viene determinato in base alle stesse regole previste per la combinazione di espressioni. Per altre informazioni, vedere [Precisione, scala e lunghezza &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 La specifica o l'espressione di query non può restituire colonne **xml**, **text**, **ntext**, **image** o con un tipo di dati CLR non binario definito dall'utente, perché questi tipi di dati non sono confrontabili.  
  
 EXCEPT  
 Restituisce tutti i valori distinti della query a sinistra dell'operatore EXCEPT che non vengono restituiti dalla query a destra.  
  
 INTERSECT  
 Restituisce tutti i valori distinti restituiti da entrambe le query sul lato sinistro e destro dell'operatore INTERSECT.  
  
## <a name="remarks"></a>Remarks  
 Quando le colonne confrontabili restituite dalle query a sinistra e a destra dell'operatore EXCEPT o INTERSECT usano tipi di dati character con regole di confronto diverse, il confronto viene eseguito in base alla [precedenza delle regole di confronto](../../t-sql/statements/collation-precedence-transact-sql.md). Se non è possibile eseguire questa conversione, in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] viene visualizzato un messaggio di errore.  
  
 Durante il confronto dei valori di colonna per la determinazione delle righe DISTINCT, due valori NULL vengono considerati uguali.  
  
 I nomi di colonna del set di risultati restituiti da EXCEPT o INTERSECT corrispondono a quelli restituiti dalla query a sinistra dell'operatore.  
  
 I nomi o gli alias di colonna in clausole ORDER BY devono fare riferimento a nomi di colonna restituiti dalla query a sinistra dell'operatore.  
  
 Il supporto di valori Null in qualsiasi colonna del set di risultati restituiti da EXCEPT o INTERSECT equivale a quello della colonna corrispondente restituita dalla query a sinistra dell'operatore.  
  
 Se EXCEPT o INTERSECT viene utilizzato insieme ad altri operatori all'interno di un'espressione, viene valutato in base all'ordine di precedenza seguente:  
  
1.  Espressioni racchiuse tra parentesi  
  
2.  Operatore INTERSECT  
  
3.  EXCEPT e UNION, valutati da sinistra verso destra in base alla relativa posizione nell'espressione  
  
 Se EXCEPT o INTERSECT viene utilizzato per confrontare più di due set di query, la conversione dei tipi di dati viene determinata tramite il confronto di due query alla volta e in base alle regole sopra indicate per la valutazione delle espressioni.  
  
 EXCEPT e INTERSECT non possono essere utilizzati in definizioni di viste partizionate distribuite e in notifiche di query.  
  
 EXCEPT e INTERSECT possono essere utilizzati in query distribuite, ma vengono eseguiti solo nel server locale e non è possibile eseguirne il push nel server collegato. Pertanto, l'utilizzo di EXCEPT e INTERSECT in query distribuite può influire sulle prestazioni.  
  
 I cursori fast forward-only e statici utilizzati con un'operazione EXCEPT o INTERSECT sono pienamente supportati nel set di risultati. Se con un'operazione EXCEPT o INTERSECT viene utilizzato un cursore gestito da keyset o dinamico, il cursore del set di risultati dell'operazione viene convertito in un cursore statico.  
  
 Quando un'operazione EXCEPT viene visualizzata tramite la funzionalità Showplan grafico di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], viene indicata come [left anti semi join](../../relational-databases/showplan-logical-and-physical-operators-reference.md), mentre un'operazione INTERSECT viene indicata come [left semi join](../../relational-databases/showplan-logical-and-physical-operators-reference.md).  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato l'uso degli operatori `INTERSECT` e `EXCEPT`. La prima query restituisce tutti i valori della tabella `Production.Product` per il confronto con i risultati ottenuti con `INTERSECT` e `EXCEPT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product ;  
--Result: 504 Rows  
```  
  
 La query seguente restituisce tutti i valori distinti restituiti da entrambe le query a sinistra e a destra dell'operatore `INTERSECT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
INTERSECT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 238 Rows (products that have work orders)  
```  
  
 La query seguente restituisce tutti i valori distinti della query a sinistra dell'operatore `EXCEPT` non presenti nella query a destra.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
EXCEPT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 266 Rows (products without work orders)  
```  
  
 La query seguente restituisce tutti i valori distinti della query a sinistra dell'operatore `EXCEPT` non presenti nella query a destra. Vengono utilizzate tabelle invertite rispetto a quelle dell'esempio precedente.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.WorkOrder  
EXCEPT  
SELECT ProductID   
FROM Production.Product ;  
--Result: 0 Rows (work orders without products)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Gli esempi seguenti mostrano come usare gli operatori `INTERSECT` e `EXCEPT`. La prima query restituisce tutti i valori della tabella `FactInternetSales` per il confronto con i risultati ottenuti con `INTERSECT` e `EXCEPT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales;  
--Result: 60398 Rows  
```  
  
 La query seguente restituisce tutti i valori distinti restituiti da entrambe le query a sinistra e a destra dell'operatore `INTERSECT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
INTERSECT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9133 Rows (Sales to customers that are female.)  
```  
  
 La query seguente restituisce tutti i valori distinti della query a sinistra dell'operatore `EXCEPT` non presenti nella query a destra.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
EXCEPT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9351 Rows (Sales to customers that are not female.)  
```  
  
  

