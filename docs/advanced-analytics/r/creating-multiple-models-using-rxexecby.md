---
title: Creazione di più modelli usando rxExecBy - servizi di SQL Server Machine Learning
description: Utilizzare la funzione rxExecBy dalla libreria RevoScaleR compilare più modelli di formattazione rapida sui dati archiviati in SQL Server in macchine.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 246f786243a95598f899034b3e0c67481d4082e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641835"
---
# <a name="creating-multiple-models-using-rxexecby"></a>Creazione di più modelli con rxExecBy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Il **rxExecBy** funzione in RevoScaleR supporta l'elaborazione parallela di più modelli correlati. Anziché train uno modelli di grandi dimensioni basati sui dati da più entità simile, un data scientist può creare rapidamente molti modelli correlati, ognuna con i dati specifici di una singola entità. 

Si supponga, ad esempio, che si esegue il monitoraggio errori del dispositivo, acquisizione dei dati per molti tipi diversi di apparecchiature. Usando rxExecBy, è possibile fornire un singolo set di dati di grandi dimensioni come input, specificare una colonna in cui clinico il set di dati, ad esempio tipo di dispositivo e quindi creare più modelli per i singoli dispositivi.

È stato definito in questo caso d'uso ["piacevolmente parallele"](https://en.wikipedia.org/wiki/Embarrassingly_parallel) quanto rispetta un problema complesso grandi dimensioni in parti di componente per l'elaborazione simultanea.

Le applicazioni tipiche di questo approccio includono previsione per singoli contatori intelligenti componenti del nucleo familiare, la creazione di proiezioni dei ricavi per le linee di prodotti separata o creazione di modelli per le approvazioni del prestito personalizzate in base ai rami singoli bank.

## <a name="how-rxexec-works"></a>Come funziona rxExec

La funzione rxExecBy in RevoScaleR è progettata per l'elaborazione su un numero elevato di piccoli set di dati parallela con volumi elevati.

1. Chiamare la funzione rxExecBy come parte del codice R e passare un set di dati non ordinati.
2. Specificare la partizione mediante il quale i dati devono essere raggruppati e ordinati.
3. Definisce una trasformazione o una funzione che deve essere applicato a ogni partizione di dati di modellazione
4. Quando viene eseguita la funzione, le query di dati vengono elaborate in parallelo se l'ambiente lo supporta. Inoltre, le attività di modellazione o trasformazione vengono distribuite tra core singoli ed eseguite in parallelo. Contesto di calcolo supportati per tre operazioni includono RxSpark e RxInSQLServer.
5. Vengono restituiti più risultati.

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy sintassi ed esempi

**rxExecBy** accetta quattro specifica di input, uno degli input da un oggetto origine dati o set di dati che può essere partizionato in uno specifico **chiave** colonna. La funzione restituisce un output per ogni partizione. Il formato dell'output dipende dalla funzione che viene passata come argomento. Ad esempio, se si passa una funzione di modellazione, ad esempio rxLinMod, è possibile restituire un modello con training separato per ogni partizione del set di dati.

### <a name="supported-functions"></a>Funzioni supportate

Modellazione delle minacce: `rxLinMod`, `rxLogit`, `rxGlm`, `rxDtree`

Assegnazione di punteggi: `rxPredict`,

Trasformazione o l'analisi: `rxCovCor`

## <a name="example"></a>Esempio

Nell'esempio seguente viene illustrato come creare più modelli utilizzando il set di dati relativi alle compagnie aeree, che viene partizionata sulla colonna [DayOfWeek]. La funzione definita dall'utente, `delayFunc`, viene applicata a ognuna delle partizioni da rxExecBy chiamante. La funzione Crea modelli separati per lunedì, martedì, e così via.

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

Se viene visualizzato l'errore, `varsToPartition is invalid`, controllare se il nome della colonna chiave o colonne sia stato digitato correttamente. Il linguaggio R è tra maiuscole e minuscole.

Questo esempio specifico non è ottimizzato per SQL Server, ed è impossibile in molti casi ottenere prestazioni migliori utilizzando SQL per raggruppare i dati. Tuttavia, usando rxExecBy, è possibile creare processi paralleli da R.

Nell'esempio seguente illustra il processo in R usando SQL Server come contesto di calcolo:

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


