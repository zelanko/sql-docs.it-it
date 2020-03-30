---
title: BINARY_CHECKSUM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BINARY_CHECKSUM
- BINARY_CHECKSUM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BINARY_CHECKSUM function
- binary [SQL Server], checksum values
ms.assetid: 07fece4d-58e3-446e-a3b5-92fe24d2d1fb
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 506f3f0e79501b16ea5455ab1ff4d4ee83a7abff
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68040216"
---
# <a name="binary_checksum--transact-sql"></a>BINARY_CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Restituisce il valore di checksum binario calcolato su una riga di una tabella o su un elenco di espressioni.
  
![Icona di collegamento a un articolo](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un articolo") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argomenti  
*\**  
Specifica che il calcolo viene eseguito su tutte le colonne della tabella. Nel calcolo eseguito da BINARY_CHECKSUM vengono ignorate le colonne con tipi di dati non confrontabili. I tipi di dati non confrontabili includono  
* **cursor**  
* **image**  
* **ntext**  
* **text**  
* **xml**  

e i tipi non confrontabili CLR (Common Language Runtime) definiti dall'utente.
  
*expression*  
[Espressione](../../t-sql/language-elements/expressions-transact-sql.md) di qualsiasi tipo. Durante il calcolo eseguito da BINARY_CHECKSUM le espressioni di tipi di dati non confrontabili vengono ignorate.

## <a name="return-types"></a>Tipi restituiti  
 **int**
  
## <a name="remarks"></a>Osservazioni  
Il calcolo di `BINARY_CHECKSUM(*)` su qualsiasi riga di una tabella restituisce sempre lo stesso valore, a meno che la riga non venga modificata in un secondo momento. `BINARY_CHECKSUM` soddisfa le proprietà di una funzione hash: quando viene applicata su due qualsiasi elenchi di espressioni restituisce lo stesso valore se gli elementi corrispondenti dei due elenchi sono dello stesso tipo di dati e risultano uguali quando vengono confrontati tramite l'operatore di uguaglianza (=). In questo contesto, si dice che i valori Null di un tipo specificato vengono considerati uguali ai fini del confronto. Se almeno uno dei valori nell'elenco di espressioni cambia, anche il valore di checksum dell'espressione può cambiare. Tale cambiamento non è tuttavia garantito. Per rilevare se i valori sono stati modificati, è quindi consigliabile usare `BINARY_CHECKSUM` solo se l'applicazione può tollerare l'occasionale mancanza di una modifica. In caso contrario, prendere in considerazione l'uso di `HASHBYTES`. Con un algoritmo hash MD5 specificato, le probabilità che `HASHBYTES` restituisca lo stesso risultato per due input diversi sono notevolmente inferiori rispetto a `BINARY_CHECKSUM`.
  
`BINARY_CHECKSUM` può essere eseguito su un elenco di espressioni e restituisce lo stesso valore per un elenco specificato. Se si applica `BINARY_CHECKSUM` a due elenchi di espressioni, viene restituito lo stesso valore se agli elementi corrispondenti dei due elenchi sono associati lo stesso tipo di dati e la stessa rappresentazione di byte. Per questa definizione, si presume che ai valori Null di un determinato tipo sia associata la stessa rappresentazione di byte.
  
`BINARY_CHECKSUM` e `CHECKSUM` sono funzioni simili. Consentono infatti di calcolare un valore di checksum in un elenco di espressioni, il cui ordine determina il valore restituito. L'ordine delle colonne usate per `BINARY_CHECKSUM(*)` corrisponde all'ordine delle colonne specificato nella definizione della tabella o della vista, incluse le colonne calcolate.
  
`BINARY_CHECKSUM` e `CHECKSUM` restituiscono valori diversi per i tipi di dati stringa, in cui a seconda delle impostazioni locali le stringhe con rappresentazione diversa possono risultare uguali. I tipi di dati stringa sono  

* **char**  
* **nchar**  
* **nvarchar**  
* **varchar**  

o  

* **sql_variant** (se il tipo di base di **sql_variant** è un tipo di dati stringa).  
  
Ad esempio, le stringhe "McCavity" e "Mccavity" hanno valori `BINARY_CHECKSUM` diversi. In un server in cui la distinzione tra maiuscole e minuscole è irrilevante, invece, `CHECKSUM` restituisce gli stessi valori di checksum per queste stringhe. È consigliabile evitare il confronto di valori `CHECKSUM` con valori `BINARY_CHECKSUM`.
 
`BINARY_CHECKSUM` supporta qualsiasi lunghezza di tipo **varbinary(max)** e fino a 255 caratteri di tipo **nvarchar(max)** .
  
## <a name="examples"></a>Esempi  
Nell'esempio seguente la funzione `BINARY_CHECKSUM` viene usata per rilevare le modifiche in una riga di tabella.
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable (column1 int, column2 varchar(256));  
GO  
INSERT INTO myTable VALUES (1, 'test');  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
UPDATE myTable set column2 = 'TEST';  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche
[Funzioni di aggregazione &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[HASHBYTES &#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
  
  
