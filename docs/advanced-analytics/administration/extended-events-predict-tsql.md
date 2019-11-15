---
title: Monitorare T-SQL con eventi estesi
description: Informazioni su come usare eventi estesi per monitorare le istruzioni T-SQL PREDICT e risolverne i problemi in Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9e891ee16ce664e12f12b16c9deda957d0fa2263
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727730"
---
# <a name="monitor-predict-t-sql-statements-with-extended-events-in-sql-server-machine-learning-services"></a>Monitorare le istruzioni T-SQL PREDICT con eventi estesi in Machine Learning Services per SQL Server

Informazioni su come usare eventi estesi per monitorare le istruzioni T-SQL [PREDICT](../../t-sql/queries/predict-transact-sql.md) e risolverne i problemi in Machine Learning Services per SQL Server.

## <a name="table-of-extended-events"></a>Tabella degli eventi estesi

Gli eventi estesi seguenti sono disponibili in tutte le versioni di SQL Server che supportano l'istruzione T-SQL [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql). 

|NAME |object_type|description| 
|----|----|----|
|predict_function_completed |evento  |Scomposizione del tempo di esecuzione predefinita|
|predict_model_cache_hit |evento|Si verifica quando un modello viene recuperato dalla cache dei modelli per la funzione PREDICT. Usare questo evento insieme agli altri eventi predict_model_cache_* per risolvere i problemi causati dalla cache dei modelli per la funzione PREDICT.|
|predict_model_cache_insert |evento  |   Si verifica quando un modello viene inserito nella cache dei modelli per la funzione PREDICT. Usare questo evento insieme agli altri eventi predict_model_cache_* per risolvere i problemi causati dalla cache dei modelli per la funzione PREDICT.    |
|predict_model_cache_miss   |evento|Si verifica quando un modello non viene trovato all'interno della cache dei modelli per la funzione PREDICT. Se questo evento si verifica spesso, può essere necessaria una maggiore quantità di memoria per SQL Server. Usare questo evento insieme agli altri eventi predict_model_cache_* per risolvere i problemi causati dalla cache dei modelli per la funzione PREDICT.|
|predict_model_cache_remove |evento| Si verifica quando un modello viene rimosso dalla cache dei modelli per la funzione PREDICT. Usare questo evento insieme agli altri eventi predict_model_cache_* per risolvere i problemi causati dalla cache dei modelli per la funzione PREDICT.|

## <a name="query-for-related-events"></a>Query per eventi correlati

Per visualizzare un elenco di tutte le colonne restituite per questi eventi, eseguire la query seguente in SQL Server Management Studio:

```sql
SELECT * 
FROM sys.dm_xe_object_columns 
WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Esempi

Per acquisire informazioni sulle prestazioni di una sessione di assegnazione dei punteggi tramite PREDICT:

1. Creare una nuova sessione di eventi estesi usando Management Studio o un altro [strumento](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools) supportato.
2. Aggiungere gli eventi `predict_function_completed` e `predict_model_cache_hit` alla sessione.
3. Avviare la sessione di eventi estesi.
4. Eseguire la query che usa PREDICT.

Nei risultati esaminare queste colonne:

+ Il valore di `predict_function_completed` indica il tempo impiegato dalla query per caricare il modello e assegnare i punteggi.
+ Il valore booleano di `predict_model_cache_hit` indica se la query ha usato o meno un modello memorizzato nella cache. 

### <a name="native-scoring-model-cache"></a>Cache dei modelli di assegnazione dei punteggi nativa

Oltre agli eventi specifici di PREDICT, è possibile usare le query seguenti per ottenere altre informazioni sul modello memorizzato nella cache e sull'uso della cache:

Visualizzare la cache dei modelli di assegnazione dei punteggi nativa:

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

Per altre informazioni sugli eventi estesi (talvolta denominati XEvent) e su come tenere traccia degli eventi in una sessione, vedere questi articoli:

+ [Monitorare gli script Python e R con eventi estesi in Machine Learning Services per SQL Server](extended-events.md)
+ [Concetti e architettura degli eventi estesi](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurare l'acquisizione di eventi in SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Gestire sessioni di eventi in Esplora oggetti](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)
