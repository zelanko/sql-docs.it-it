---
title: $PARTITION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- $partition_TSQL
- $partition
dev_langs:
- TSQL
helpviewer_keywords:
- $PARTITION function
- partitions [SQL Server], numbers
ms.assetid: abc865d0-57a8-49da-8821-29457c808d2a
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: c8795fddb719debb147a0733cc5cfb831662058e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832971"
---
# <a name="partition-transact-sql"></a>$PARTITION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il numero della partizione a cui verrebbe eseguito il mapping di un set di valori di una colonna di partizionamento per una funzione di partizione specificata in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
[ database_name. ] $PARTITION.partition_function_name(expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *database_name*  
 Nome del database contenente la funzione di partizione.  
  
 *partition_function_name*  
 Nome di una funzione di partizione esistente in base alla quale viene applicato un set di valori di una colonna di partizionamento.  
  
 *expression*  
 [Espressione](../../t-sql/language-elements/expressions-transact-sql.md) il cui tipo di dati deve corrispondere al tipo di dati della colonna di partizionamento corrispondente o deve poter essere convertito in modo implicito in tale tipo di dati. *expression* può essere anche il nome di una colonna di partizionamento che partecipa a *partition_function_name*.  
  
## <a name="return-types"></a>Tipi restituiti  
 **int**  
  
## <a name="remarks"></a>Osservazioni  
 $PARTITION restituisce un valore **int** compreso tra 1 e il numero di partizioni della funzione di partizione.  
  
 $PARTITION restituisce il numero di partizione per qualsiasi valore valido, indipendentemente dal fatto che il valore esista in una tabella o in un dice partizionato che utilizza la funzione di partizione.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-getting-the-partition-number-for-a-set-of-partitioning-column-values"></a>R. Recupero del numero di partizione per un set di valori di colonne di partizionamento  
 Nell'esempio seguente viene creata una funzione di partizione `RangePF1` che esegue il partizionamento di una tabella o di un indice in quattro partizioni. $PARTITION consente di stabilire che il valore `10`, che rappresenta la colonna di partizionamento di `RangePF1`, verrebbe inserito nella partizione 1 della tabella.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE PARTITION FUNCTION RangePF1 ( int )  
AS RANGE FOR VALUES (10, 100, 1000) ;  
GO  
SELECT $PARTITION.RangePF1 (10) ;  
GO  
```  
  
### <a name="b-getting-the-number-of-rows-in-each-nonempty-partition-of-a-partitioned-table-or-index"></a>B. Recupero del numero di righe di ogni partizione non vuota di una tabella o di un indice partizionato  
 Nell'esempio seguente viene restituito il numero di righe di ogni partizione della tabella `TransactionHistory` contenente dati. La tabella `TransactionHistory` utilizza la funzione di partizione `TransactionRangePF1` ed è partizionata in base alla colonna `TransactionDate`.  
  
 Per eseguire l'esempio è necessario innanzitutto eseguire lo script PartitionAW.sql nel database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Per altre informazioni, vedere [PartitioningScript](https://go.microsoft.com/fwlink/?LinkId=201015).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT $PARTITION.TransactionRangePF1(TransactionDate) AS Partition,   
COUNT(*) AS [COUNT] FROM Production.TransactionHistory   
GROUP BY $PARTITION.TransactionRangePF1(TransactionDate)  
ORDER BY Partition ;  
GO  
```  
  
### <a name="c-returning-all-rows-from-one-partition-of-a-partitioned-table-or-index"></a>C. Restituzione di tutte le righe di una partizione di una tabella o di un indice partizionato  
 Nell'esempio seguente vengono restituite tutte le righe incluse nella partizione `5` della tabella `TransactionHistory`.  
  
> [!NOTE]  
>  Per eseguire l'esempio è necessario innanzitutto eseguire lo script PartitionAW.sql nel database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Per altre informazioni, vedere [PartitioningScript](https://go.microsoft.com/fwlink/?LinkId=201015).  
  
```  
SELECT * FROM Production.TransactionHistory  
WHERE $PARTITION.TransactionRangePF1(TransactionDate) = 5 ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)  
  
  
