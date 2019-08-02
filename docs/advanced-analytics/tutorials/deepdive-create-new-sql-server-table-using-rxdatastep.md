---
title: Creare una nuova tabella SQL Server usando RevoScaleR rxDataStep
description: Esercitazione dettagliata su come creare una tabella SQL Server usando il linguaggio R SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b18f2bd42070746551d21ff7508e7fce58b49037
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714916"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Creare una nuova tabella SQL Server usando rxDataStep (esercitazione SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa lezione fa parte dell' [esercitazione su RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare le [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa lezione si apprenderà come spostare i dati tra i frame di dati in memoria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il contesto e i file locali.

> [!NOTE]
> In questa lezione viene utilizzato un set di dati diverso. Il set di dati dei ritardi delle compagnie aeree è un set di dati pubblico ampiamente usato per gli esperimenti di machine learning. I file di dati usati in questo esempio sono disponibili nella stessa directory degli altri esempi del prodotto.

## <a name="load-data-from-a-local-xdf-file"></a>Caricare i dati da un file XDF locale

Nella prima metà di questa esercitazione è stata usata la funzione **RxTextData** per importare i dati in R da un file di testo e quindi è stata usata la funzione **RxDataStep** per spostare i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dati in.

Questa lezione richiede un approccio diverso e usa i dati di un file salvato nel [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). Dopo aver eseguito alcune trasformazioni leggere sui dati utilizzando il file XDF, è possibile salvare i dati trasformati in una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nuova tabella.

**Che cos'è XDF?**

Il formato XDF è uno standard XML sviluppato per i dati ad alta dimensionalità ed è il formato di file nativo usato da [Machine Learning server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Si tratta di un formato di file binario con un'interfaccia R che ottimizza l'elaborazione e l'analisi di righe e colonne.  È possibile usarlo per spostare i dati e archiviare subset di dati utili per l'analisi.

1. Impostare il contesto di calcolo sulla workstation locale. **Per questo passaggio sono necessarie le autorizzazioni DDL.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. Definire un nuovo oggetto origine dati usando la funzione **RxXdfData** . Per definire un'origine dati XDF, specificare il percorso del file di dati.  

    È possibile specificare il percorso del file usando una variabile di testo. Tuttavia, in questo caso, è disponibile un comodo collegamento, che consiste nell'usare la funzione **rxGetOption** e ottenere il file (AirlineDemoSmall. XDF) dalla directory dei dati di esempio.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Chiamare [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) nei dati in memoria per visualizzare un riepilogo del set di dati.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Risultati**

```R
Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)
Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)
Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday
```

> [!NOTE]
> 
> Si noti che non è stato necessario chiamare altre funzioni per caricare i dati nel file XDF e che è stato possibile chiamare immediatamente **rxGetVarInfo** nei dati. Questo perché XDF è il metodo di archiviazione provvisorio predefinito per **RevoScaleR**. Oltre ai file XDF, la funzione **rxGetVarInfo** ora supporta più tipi di origine.

## <a name="move-contents-to-sql-server"></a>Spostare il contenuto in SQL Server

Con l'origine dati XDF creata nella sessione di R locale, è ora possibile spostare i dati in una tabella di database, archiviando *DayOfWeek* come integer con valori compresi tra 1 e 7.

1. Definire un oggetto origine dati SQL Server, specificando una tabella che contenga i dati e la connessione al server remoto.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. Per precauzione, includere un passaggio per verificare se esiste già una tabella con lo stesso nome ed eliminare la tabella se esiste. Una tabella esistente con lo stesso nome impedisce la creazione di un nuovo.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. Caricare i dati nella tabella utilizzando **rxDataStep**. Questa funzione sposta i dati tra due origini dati già definite e può facoltativamente trasformare i dati in Route.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    Si tratta di una tabella di dimensioni piuttosto grandi, quindi è necessario attendere che venga visualizzato un messaggio di stato finale simile al seguente: *Righe lette: 200000, totale righe elaborate: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>Caricare dati da una tabella SQL

Una volta che i dati sono presenti nella tabella, è possibile caricarli usando una semplice query SQL. 

1. Creare una nuova origine dati SQL Server. L'input è una query sulla nuova tabella appena creata e caricata con i dati. Questa definizione aggiunge livelli di fattore per la colonna *DayOfWeek* , usando l'argomento *colInfo* per **RxSqlServerData**.
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. Chiamare **rxSummary** ancora una volta per esaminare un riepilogo dei dati nella query.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Eseguire un'analisi in blocchi tramite rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)