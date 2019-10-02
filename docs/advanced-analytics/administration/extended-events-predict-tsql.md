---
title: Monitorare la stima di T-SQL con gli eventi estesi
description: Informazioni su come usare gli eventi estesi per monitorare e risolvere i problemi relativi alle istruzioni T-SQL PREDICT in SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 958ac3e24a9deec231e7fd4d5da14477d693f4de
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714305"
---
# <a name="monitor-predict-t-sql-statements-with-extended-events-in-sql-server-machine-learning-services"></a>Monitorare le istruzioni T-SQL per la stima con eventi estesi in SQL Server Machine Learning Services

Informazioni su come usare gli eventi estesi per monitorare e risolvere i problemi relativi alle istruzioni T-SQL [Predict](../../t-sql/queries/predict-transact-sql.md) in SQL Server Machine Learning Services.

## <a name="table-of-extended-events"></a>Tabella degli eventi estesi

Gli eventi estesi seguenti sono disponibili in tutte le versioni di SQL Server che supportano l'istruzione T-SQL [Predict](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) . 

|NAME |object_type|description| 
|----|----|----|
|predict_function_completed |evento  |Suddivisione tempo di esecuzione predefinita|
|predict_model_cache_hit |evento|Si verifica quando un modello viene recuperato dalla cache del modello di funzione PREDICT. Usare questo evento insieme agli altri eventi predict_model_cache_ * per risolvere i problemi causati dalla cache del modello di funzione PREDICT.|
|predict_model_cache_insert |evento  |   Si verifica quando un modello viene inserito nella cache del modello di funzione PREDICT. Usare questo evento insieme agli altri eventi predict_model_cache_ * per risolvere i problemi causati dalla cache del modello di funzione PREDICT.    |
|predict_model_cache_miss   |evento|Si verifica quando un modello non viene trovato nella cache del modello di funzione PREDICT. Le occorrenze frequenti di questo evento potrebbero indicare che SQL Server necessita di più memoria. Usare questo evento insieme agli altri eventi predict_model_cache_ * per risolvere i problemi causati dalla cache del modello di funzione PREDICT.|
|predict_model_cache_remove |evento| Si verifica quando un modello viene rimosso dalla cache dei modelli per la funzione PREDICT. Usare questo evento insieme agli altri eventi predict_model_cache_ * per risolvere i problemi causati dalla cache del modello di funzione PREDICT.|

## <a name="query-for-related-events"></a>Query per eventi correlati

Per visualizzare un elenco di tutte le colonne restituite per questi eventi, eseguire la query seguente in SQL Server Management Studio:

```sql
SELECT * 
FROM sys.dm_xe_object_columns 
WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Esempi

Per acquisire informazioni sulle prestazioni di una sessione di assegnazione dei punteggi usando PREDICT:

1. Creare una nuova sessione eventi estesi usando Management Studio o un altro [strumento](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)supportato.
2. Aggiungere gli eventi `predict_function_completed` e `predict_model_cache_hit` alla sessione.
3. Avviare la sessione eventi estesi.
4. Eseguire la query che usa PREDICT.

Nei risultati esaminare le colonne seguenti:

+ Il valore di `predict_function_completed` indica la quantità di tempo impiegato dalla query per il caricamento del modello e l'assegnazione del punteggio.
+ Il valore booleano `predict_model_cache_hit` per indica se la query ha utilizzato o meno un modello memorizzato nella cache. 

### <a name="native-scoring-model-cache"></a>Cache dei modelli di assegnazione dei punteggi nativi

Oltre agli eventi specifici per la stima, è possibile utilizzare le query seguenti per ottenere ulteriori informazioni sul modello memorizzato nella cache e sull'utilizzo della cache:

Visualizzare la cache dei modelli di assegnazione dei punteggi nativi:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

Visualizzare gli oggetti nella cache dei modelli:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sugli eventi estesi (talvolta denominati XEvent) e su come tenere traccia degli eventi in una sessione, vedere i seguenti articoli:

+ [Monitorare gli script Python e R con gli eventi estesi in SQL Server Machine Learning Services](extended-events.md)
+ [Concetti e architettura degli eventi estesi](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurare l'acquisizione di eventi in SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Gestire sessioni di eventi nel Esplora oggetti](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)
