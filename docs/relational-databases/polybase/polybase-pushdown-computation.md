---
title: Calcoli con distribuzione in PolyBase | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 94e360c19c4f734b891701a4ec40c82cdb57927d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71710488"
---
# <a name="pushdown-computations-in-polybase"></a>Calcoli con distribuzione in PolyBase

## <a name="dmv"></a>Vista a gestione dinamica

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Il calcolo con distribuzione migliora le prestazioni delle query nel cluster Hadoop.

## <a name="enable-pushdown"></a>Abilitare la distribuzione

La procedura per l'abilitazione della distribuzione viene descritta nell'articolo seguente:

[Abilitare il calcolo con distribuzione in Hadoop](polybase-configure-hadoop.md#pushdown)

## <a name="select-a-subset-of-rows"></a>Selezionare un subset di righe

Usare la distribuzione del predicato per migliorare le prestazioni se la query seleziona un subset di righe da una tabella esterna.

In questo esempio, SQL Server 2016 avvia un processo MapReduce per recuperare le righe corrispondenti al predicato `customer.account_balance < 200000` in Hadoop. Dato che la query può essere completata correttamente senza eseguire la scansione di tutte le righe della tabella, vengono copiate in SQL Server solo le righe che soddisfano i criteri del predicato. In questo modo si risparmia molto tempo ed è necessario meno spazio per l'archiviazione temporanea quando il numero di saldi dei clienti inferiori a 200000 è ridotto rispetto al numero di clienti con saldi superiori o uguali a 200000.

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>Selezionare un subset di colonne

Usare la distribuzione del predicato per migliorare le prestazioni se la query seleziona un subset di colonne da una tabella esterna.

In questa query, SQL Server avvia un processo MapReduce per pre-elaborare il file di testo delimitato di Hadoop in modo tale che solo i dati per le due colonne, customer.name e customer.zip_code, verranno copiati in SQL Server PDW.

```sql
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>Distribuzione per operatori ed espressioni di base

SQL Server consente gli operatori e le espressioni di base seguenti per la distribuzione del predicato.

+ Operatori di confronto binari (\<, >, =, !=, <>, >=, <=) per valori numerici, di data e di ora.

+ Operatori aritmetici ( +, -, *, /, % ).

+ Operatori logici (AND, OR).

+ Operatori unari (NOT, IS NULL, IS NOT NULL).

Gli operatori BETWEEN, NOT, IN e LIKE possono essere propagati. Il comportamento effettivo dipende dal modo in cui Query Optimizer riscrive le espressioni degli operatori come serie di istruzioni che usano operatori relazionali di base.

La query in questo esempio include più predicati di cui è possibile eseguire il push in Hadoop. SQL Server è in grado di eseguire il push di processi MapReduce in Hadoop per eseguire il predicato `customer.account_balance <= 200000`. Anche l'espressione `BETWEEN 92656 and 92677` è costituita da operazioni binarie e logiche di cui è possibile eseguire il push in Hadoop. L'operatore **AND** logico in `customer.account_balance and customer.zipcode` è un'espressione finale.

Con questa combinazione di predicati, i processi MapReduce possono eseguire interamente la clausola WHERE. Solo i dati che soddisfano i criteri SELECT vengono copiati in SQL Server PDW.

```sql
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="force-pushdown"></a>Forzare la distribuzione

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

## <a name="disable-pushdown"></a>Disabilitare la distribuzione

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su PolyBase, vedere [Che cos'è PolyBase?](polybase-guide.md).
