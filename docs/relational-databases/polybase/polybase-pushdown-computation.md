---
description: Calcoli con distribuzione in PolyBase
title: Calcoli con distribuzione in PolyBase | Microsoft Docs
dexcription: Enable pushdown computation to improve performance of queries on your Hadoop cluster. You can select a subset of rows/columns in an external table for pushdown.
ms.date: 11/17/2020
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 59ff1e7807a8bdd8427e3b902bf53c111d52c7b7
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2020
ms.locfileid: "96127839"
---
# <a name="pushdown-computations-in-polybase"></a>Calcoli con distribuzione in PolyBase

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

Il calcolo con distribuzione migliora le prestazioni delle query su origini dati esterne. A partire da SQL Server 2016, sono disponibili calcoli con distribuzione per le origini dati esterne Hadoop. SQL Server 2019 introduce i calcoli con distribuzione per altri tipi di origini dati esterne.

## <a name="enable-pushdown-computation"></a> Abilitare il calcolo con distribuzione

Gli articoli seguenti includono informazioni sulla configurazione del calcolo con distribuzione per tipi specifici di origini dati esterne:

- [Abilitare il calcolo con distribuzione in Hadoop](polybase-configure-hadoop.md#pushdown)
- [Configurare PolyBase per l'accesso a dati esterni in Oracle](polybase-configure-oracle.md)
- [Configurare PolyBase per l'accesso a dati esterni in Teradata](polybase-configure-teradata.md)
- [Configurare PolyBase per l'accesso a dati esterni in MongoDB](polybase-configure-mongodb.md)
- [Configurare PolyBase per l'accesso a dati esterni con i tipi generici ODBC](polybase-configure-odbc-generic.md)
- [Configurare PolyBase per l'accesso a dati esterni in SQL Server](polybase-configure-sql-server.md)

## <a name="select-a-subset-of-rows"></a>Selezionare un subset di righe

Usare la distribuzione del predicato per migliorare le prestazioni se la query seleziona un subset di righe da una tabella esterna.

In questo esempio, SQL Server 2016 avvia un processo MapReduce per recuperare le righe corrispondenti al predicato `customer.account_balance < 200000` in Hadoop. Dato che la query può essere completata correttamente senza eseguire la scansione di tutte le righe della tabella, vengono copiate in SQL Server solo le righe che soddisfano i criteri del predicato. In questo modo si risparmia molto tempo ed è necessario meno spazio per l'archiviazione temporanea quando il numero di saldi dei clienti inferiori a 200000 è ridotto rispetto al numero di clienti con saldi superiori o uguali a 200000.

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>Selezionare un subset di colonne

Usare la distribuzione del predicato per migliorare le prestazioni se la query seleziona un subset di colonne da una tabella esterna.

In questa query, SQL Server avvia un processo MapReduce per pre-elaborare il file di testo delimitato di Hadoop in modo tale che solo i dati per le due colonne, customer.name e customer.zip_code, vengano copiati in SQL Server.

```sql
SELECT customer.name, customer.zip_code
FROM customer
WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>Distribuzione per operatori ed espressioni di base

SQL Server consente gli operatori e le espressioni di base seguenti per la distribuzione del predicato.

- Operatori di confronto binari (`<`, `>`, `=`, `!=`, `<>`, `>=`, `<=`) per valori numerici, di data e di ora.
- Operatori aritmetici (`+`, `-`, `*`, `/`, `%`).
- Operatori logici (`AND`, `OR`).
- Operatori unari (`NOT`, `IS NULL`, `IS NOT NULL`).

Gli operatori `BETWEEN`, `NOT`, `IN` e `LIKE` potrebbero essere distribuiti. Il comportamento effettivo dipende dal modo in cui Query Optimizer riscrive le espressioni degli operatori come serie di istruzioni che usano operatori relazionali di base.

La query in questo esempio include più predicati di cui è possibile eseguire il push in Hadoop. SQL Server è in grado di eseguire il push di processi MapReduce in Hadoop per eseguire il predicato `customer.account_balance <= 200000`. Anche l'espressione `BETWEEN 92656 AND 92677` è costituita da operazioni binarie e logiche di cui è possibile eseguire il push in Hadoop. L'operatore **AND** logico in `customer.account_balance AND customer.zipcode` è un'espressione finale.

Con questa combinazione di predicati, i processi MapReduce possono eseguire interamente la clausola WHERE. Solo i dati che soddisfano i criteri `SELECT` vengono copiati in SQL Server.

```sql
SELECT * FROM customer 
WHERE customer.account_balance <= 200000 
    AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="examples"></a>Esempio

### <a name="force-pushdown"></a>Forzare la distribuzione

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

### <a name="disable-pushdown"></a>Disabilitare la distribuzione

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su PolyBase, vedere [Che cos'è PolyBase?](polybase-guide.md).
