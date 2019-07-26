---
title: Creazione di più modelli con rxExecBy
description: Usare la funzione rxExecBy della libreria RevoScaleR per compilare più modelli mini sui dati del computer archiviati in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5d3e03e718aea725267a2251768ef040905b020e
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470190"
---
# <a name="creating-multiple-models-using-rxexecby"></a>Creazione di più modelli con rxExecBy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La funzione **rxExecBy** in RevoScaleR supporta l'elaborazione parallela di più modelli correlati. Anziché eseguire il training di un modello di grandi dimensioni in base ai dati di più entità simili, un data scientist può creare rapidamente molti modelli correlati, ciascuno dei quali USA i dati specifici di una singola entità. 

Si supponga, ad esempio, di monitorare gli errori dei dispositivi e di acquisire i dati per molti tipi diversi di apparecchiature. Utilizzando rxExecBy, è possibile fornire un singolo set di dati di grandi dimensioni come input, specificare una colonna in cui stratificare il set di dati, ad esempio il tipo di dispositivo, quindi creare più modelli per i singoli dispositivi.

Questo caso d'uso è stato definito ["piacevolmente parallelo"](https://en.wikipedia.org/wiki/Embarrassingly_parallel) poiché suddivide un problema complicato nelle parti componenti per l'elaborazione simultanea.

Le applicazioni tipiche di questo approccio includono la previsione per i singoli contatori Smart domestici, la creazione di proiezioni dei ricavi per le linee di prodotti separate o la creazione di modelli per le approvazioni di prestito personalizzate per i singoli rami bancari.

## <a name="how-rxexec-works"></a>Funzionamento di rxExec

La funzione rxExecBy in RevoScaleR è progettata per l'elaborazione parallela di volumi elevati su un numero elevato di set di dati di piccole dimensioni.

1. Si chiama la funzione rxExecBy come parte del codice R e si passa un set di dati di dati non ordinati.
2. Specificare la partizione in base alla quale i dati devono essere raggruppati e ordinati.
3. Definire una funzione di trasformazione o di modellazione da applicare a ogni partizione di dati
4. Quando la funzione viene eseguita, le query sui dati vengono elaborate in parallelo se l'ambiente lo supporta. Inoltre, le attività di modellazione o trasformazione vengono distribuite tra i singoli core ed eseguite in parallelo. Il contesto di calcolo supportato per le operazioni thee è RxSpark e RxInSQLServer.
5. Vengono restituiti più risultati.

## <a name="rxexecby-syntax-and-examples"></a>Sintassi ed esempi di rxExecBy

**rxExecBy** accetta quattro input, uno degli input costituito da un set di dati o da un oggetto origine dati che può essere partizionato in una colonna **chiave** specificata. La funzione restituisce un output per ogni partizione. Il formato dell'output dipende dalla funzione passata come argomento. Se ad esempio si passa una funzione di modellazione come rxLinMod, è possibile restituire un modello con training separato per ogni partizione del set di dati.

### <a name="supported-functions"></a>Funzioni supportate

Modellazione `rxLinMod`: `rxLogit`, `rxGlm`,,`rxDtree`

Punteggio: `rxPredict`,

Trasformazione o analisi:`rxCovCor`

## <a name="example"></a>Esempio

Nell'esempio seguente viene illustrato come creare più modelli utilizzando il set di dati della compagnia aerea, partizionato nella colonna [DayOfWeek]. La funzione definita dall'utente, `delayFunc`, viene applicata a ogni partizione chiamando rxExecBy. La funzione crea modelli distinti per lunedì, martedì e così via.

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

Se viene ricevuto l'errore, `varsToPartition is invalid`controllare se il nome della colonna o delle colonne chiave è tipizzato correttamente. Il linguaggio R fa distinzione tra maiuscole e minuscole.

Questo particolare esempio non è ottimizzato per SQL Server e in molti casi è possibile ottenere prestazioni migliori usando SQL per raggruppare i dati. Tuttavia, usando rxExecBy, è possibile creare processi paralleli da R.

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


