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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ca0c77ccf18d47f14c7f9eb286158bb8d4642ddf
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617761"
---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Restituisce il valore di checksum binario calcolato su una riga di una tabella o su un elenco di espressioni.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
  
## <a name="remarks"></a>Remarks  
L'esecuzione della funzione BINARY_CHECKSUM(*) su una riga di una tabella restituisce sempre lo stesso valore, a meno che la riga non venga successivamente modificata. La funzione BINARY_CHECKSUM soddisfa le proprietà di una funzione hash poiché quando viene applicata su due elenchi di espressioni qualsiasi restituisce lo stesso valore se gli elementi corrispondenti dei due elenchi sono dello stesso tipo di dati e risultano uguali quando vengono confrontati tramite l'operatore di uguaglianza (=). In questo contesto, si dice che i valori Null di un tipo specificato vengono considerati uguali ai fini del confronto. Se almeno uno dei valori nell'elenco di espressioni cambia, anche il valore di checksum dell'espressione può cambiare. Questo comportamento non è tuttavia garantito. Per rilevare se i valori sono stati modificati, è pertanto consigliabile usare BINARY_CHECKSUM solo se l'applicazione può tollerare una modifica mancata occasionale. In caso contrario, prendere in considerazione l'uso di HashBytes. In presenza di un algoritmo hash MD5 specificato, le probabilità che HashBytes restituisca lo stesso risultato per due diversi input sono notevolmente inferiori rispetto a BINARY_CHECKSUM.
  
BINARY_CHECKSUM può essere eseguito su un elenco di espressioni e restituisce lo stesso valore per un elenco specificato. Se la funzione viene eseguita su due elenchi di espressioni, viene restituito lo stesso valore se agli elementi corrispondenti dei due elenchi sono associati lo stesso tipo di dati e la stessa rappresentazione di byte. Per questa definizione, si presume che ai valori Null di un determinato tipo sia associata la stessa rappresentazione di byte.
  
BINARY_CHECKSUM e CHECKSUM sono funzioni simili. Consentono infatti di calcolare un valore di checksum in un elenco di espressioni, il cui ordine determina il valore restituito. L'ordine delle colonne utilizzato per BINARY_CHECKSUM(*) corrisponde all'ordine delle colonne specificato nella definizione di tabella o vista. incluse le colonne calcolate.
  
Le funzioni BINARY_CHECKSUM e CHECKSUM possono restituire valori diversi solo per i tipi di dati stringa, in cui a seconda delle impostazioni locali le stringhe con rappresentazione diversa possono risultare uguali. I tipi di dati stringa sono  

* **char**  
* **nchar**  
* **nvarchar**  
* **varchar**  

o Gestione configurazione  

* **sql_variant** (se il tipo di base di **sql_variant** è un tipo di dati stringa).  
  
Ad esempio, le stringhe "McCavity" e "Mccavity" hanno valori BINARY_CHECKSUM diversi. In un server in cui la distinzione tra maiuscole e minuscole è irrilevante, invece, la funzione CHECKSUM restituisce per queste stringhe gli stessi valori di checksum. È consigliabile evitare il confronto tra valori CHECKSUM e valori BINARY_CHECKSUM.
 
BINARY_CHECKSUM supporta qualsiasi lunghezza di tipo **varbinary(max)** e fino a 255 caratteri di tipo **nvarchar(max)**.
  
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
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  
