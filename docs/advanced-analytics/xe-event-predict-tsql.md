---
title: Eventi estesi per il monitoraggio di istruzioni PREDICT - servizi di SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e680da7485069e6838edff260a505461a22c472b
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432244"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>Eventi estesi per il monitoraggio di istruzioni PREDICT

Questo articolo descrive gli eventi estesi fornito in SQL Server che è possibile usare per monitorare e analizzare i processi che utilizzano [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) per eseguire l'assegnazione dei punteggi in tempo reale in SQL Server.

Assegnazione dei punteggi in tempo reale genera i punteggi da un modello di machine learning che è archiviato in SQL Server. La funzione PREDICT non richiede un runtime esterni, ad esempio R o Python, solo un modello che è stato creato usando un formato binario specifico. Per altre informazioni, vedere [assegnazione dei punteggi in tempo reale](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="prerequisites"></a>Prerequisiti

Per informazioni generali su eventi estesi (operazione talvolta denominati XEvents) e su come tenere traccia degli eventi in una sessione, vedere questi articoli:

+ [Architettura e concetti degli eventi estesi](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [Configurare l'acquisizione di eventi in SQL Server Management Studio](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [Gestire sessioni di eventi in Esplora oggetti](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>Tabella degli eventi estesi

Gli eventi estesi seguenti sono disponibili in tutte le versioni di SQL Server che supportano il [prevedere di T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) istruzione, tra cui SQL Server in Linux e Database SQL di Azure. 

L'istruzione T-SQL stimare è stato introdotto in SQL Server 2017. 

|NAME |object_type|description| 
|----|----|----|
|predict_function_completed |evento  |Suddivisione tempo di esecuzione Builtin|
|predict_model_cache_hit |evento|Si verifica quando un modello viene recuperato dalla cache del modello di funzione PREDICT. Utilizzare questo evento insieme agli altri eventi predict_model_cache _ * per risolvere i problemi causati dalla cache dei modelli di funzione PREDICT.|
|predict_model_cache_insert |evento  |   Si verifica quando un modello viene inserito nella cache dei modelli di funzione PREDICT. Utilizzare questo evento insieme agli altri eventi predict_model_cache _ * per risolvere i problemi causati dalla cache dei modelli di funzione PREDICT.    |
|predict_model_cache_miss   |evento|Si verifica quando un modello non viene trovato nella cache dei modelli di funzione PREDICT. Le occorrenze di frequente di questo evento può indicare che è necessaria più memoria di SQL Server. Utilizzare questo evento insieme agli altri eventi predict_model_cache _ * per risolvere i problemi causati dalla cache dei modelli di funzione PREDICT.|
|predict_model_cache_remove |evento| Si verifica quando un modello viene rimosso dalla cache dei modelli per la funzione PREDICT. Utilizzare questo evento insieme agli altri eventi predict_model_cache _ * per risolvere i problemi causati dalla cache dei modelli di funzione PREDICT.|

## <a name="query-for-related-events"></a>Eseguire una query per eventi correlati

Per visualizzare un elenco di tutte le colonne restituite per questi eventi, eseguire la query seguente in SQL Server Management Studio:

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>Esempi

Per acquisire informazioni sulle prestazioni di una sessione di assegnazione dei punteggi usando PREDICT:

1. Creare un nuovo oggetto esteso sessione eventi, usando Management Studio o un altro supportata [strumento](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).
2. Aggiungere gli eventi `predict_function_completed` e `predict_model_cache_hit` alla sessione.
3. Avviare la sessione eventi estesi.
4. Eseguire la query che utilizza la stima.

Nei risultati esaminare queste colonne:

+ Il valore per `predict_function_completed` Mostra il tempo impiegato per il caricamento del modello e di assegnazione dei punteggi query.
+ Il valore booleano per `predict_model_cache_hit` indica se la query usato un modello memorizzato nella cache o meno. 

### <a name="native-scoring-model-cache"></a>Cache dei modelli per assegnazione dei punteggi nativa

Oltre agli eventi specifici da stimare, è possibile usare le query seguenti per ottenere altre informazioni relative al modello memorizzato nella cache e l'utilizzo della cache:

Visualizza cache dei modelli di assegnazione dei punteggi nativa:

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

