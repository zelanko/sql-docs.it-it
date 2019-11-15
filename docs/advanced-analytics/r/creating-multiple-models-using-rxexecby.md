---
title: Creare più modelli con rxExecBy
description: Usare la funzione rxExecBy della libreria RevoScaleR per compilare più minimodelli sui dati del computer archiviati in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dbba63ae69997c9c5dbdccf49ec590b3f4eba652
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727489"
---
# <a name="creating-multiple-models-using-rxexecby"></a>Creazione di più modelli con rxExecBy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La funzione **rxExecBy** in RevoScaleR supporta l'elaborazione parallela di più modelli correlati. Invece di eseguire il training di un modello di grandi dimensioni basato sui dati di più entità simili, un data scientist può creare rapidamente più modelli correlati, ognuno dei quali usa i dati specifici di una singola entità. 

Si supponga, ad esempio, di monitorare i guasti dei dispositivi e di acquisire i dati per più tipi diversi di apparecchiature. Usando rxExecBy, è possibile fornire un singolo set di dati di grandi dimensioni come input, specificare una colonna in cui stratificare il set di dati, ad esempio il tipo di dispositivo, e quindi creare più modelli per i singoli dispositivi.

Questo caso d'uso è stato definito ["perfettamente parallelo"](https://en.wikipedia.org/wiki/Embarrassingly_parallel) perché suddivide un problema complesso in più parti che vengono elaborate simultaneamente.

Le applicazioni tipiche di questo approccio includono la previsione per singoli contatori domestici intelligenti, la creazione di proiezioni di ricavi per linee di prodotti separate o la creazione di modelli per le approvazioni di prestiti personalizzate per le singole filiali bancarie.

## <a name="how-rxexec-works"></a>Come funziona rxExec

La funzione rxExecBy in RevoScaleR è progettata per l'elaborazione parallela di volumi elevati su un gran numero di set di dati di piccole dimensioni.

1. Si chiama la funzione rxExecBy come parte del codice R e si passa un set di dati non ordinati.
2. Specificare la partizione in base alla quale i dati devono essere raggruppati e ordinati.
3. Definire una funzione di trasformazione o modellazione da applicare a ogni partizione di dati
4. Quando la funzione viene eseguita, le query di dati vengono elaborate in parallelo se l'ambiente lo consente. Inoltre, le attività di modellazione o trasformazione vengono distribuite tra i singoli core ed eseguite in parallelo. I contesti di calcolo supportati per le operazioni includono RxSpark e RxInSQLServer.
5. Vengono restituiti più risultati.

## <a name="rxexecby-syntax-and-examples"></a>Sintassi ed esempi di rxExecBy

**rxExecBy** accetta quattro input, uno dei quali è un oggetto set di dati o origine dati che può essere partizionato su una colonna **chiave** specificata. La funzione restituisce un output per ogni partizione. Il formato dell'output dipende dalla funzione passata come argomento. Se ad esempio si passa una funzione di modellazione come rxLinMod, è possibile restituire un modello con training separato per ogni partizione del set di dati.

### <a name="supported-functions"></a>Funzioni supportate

Modellazione: `rxLinMod`, `rxLogit`, `rxGlm`, `rxDtree`

Assegnazione dei punteggi: `rxPredict`

Trasformazione o analisi: `rxCovCor`

## <a name="example"></a>Esempio

L'esempio seguente illustra come creare più modelli usando il set di dati Airline, partizionato sulla colonna [DayOfWeek]. La funzione definita dall'utente, `delayFunc`, viene applicata a ogni partizione chiamando rxExecBy. La funzione crea modelli distinti per il lunedì, il martedì e così via.

```sql
EXEC sp_execute_external_script
@language = N'R'
, @script = N'
delayFunc <- function(key, data, params) { 
    df <- rxImport(inData = airlineData) 
    rxLinMod(ArrDelay ~ CRSDepTime, data = df) 
} 
OutputDataSet <- rxExecBy(airlineData, c("DayOfWeek"), delayFunc)
'
, @input_data_1 = N'select ArrDelay, DayOfWeek, CRSDepTime from AirlineDemoSmall]'
, @input_data_1_name = N'airlineData'

```

Se viene visualizzato l'errore `varsToPartition is invalid`, controllare se il nome di una o più colonne chiave è stato digitato correttamente. Il linguaggio R distingue tra maiuscole e minuscole.

Questo particolare esempio non è ottimizzato per SQL Server e in molti casi è possibile ottenere prestazioni migliori usando SQL per raggruppare i dati. Usando rxExecBy, è tuttavia possibile creare processi in parallelo da R.

L'esempio seguente illustra il processo in R, usando SQL Server come contesto di calcolo:

```R
sqlServerConnString <- "SERVER=hostname;DATABASE=TestDB;UID=DBUser;PWD=Password;"
inTable <- paste("airlinedemosmall")
sqlServerDataDS <- RxSqlServerData(table = inTable, connectionString = sqlServerConnString)

# user function
".Count" <- function(keys, data, params)
{
  myDF <- rxImport(inData = data)
  return (nrow(myDF))
}

# Set SQL Server compute context with level of parallelism = 2
sqlServerCC <- RxInSqlServer(connectionString = sqlServerConnString, numTasks = 4)
rxSetComputeContext(sqlServerCC)

# Execute rxExecBy in SQL Server compute context
sqlServerCCResults <- rxExecBy(inData = sqlServerDataDS, keys = c("DayOfWeek"), func = .Count)
```


