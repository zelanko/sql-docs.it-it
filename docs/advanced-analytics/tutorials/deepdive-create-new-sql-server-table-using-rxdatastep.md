---
title: Crea nuova tabella di SQL Server mediante rxDataStep RevoScaleR - SQL Server Machine Learning
description: Procedura dettagliata su come creare una tabella di SQL Server Usa il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1fb3f83cd3bbd39e3af4936ce8dfb8f16bad82d8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641465"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Crea nuova tabella di SQL Server mediante rxDataStep (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

In questa lezione si informazioni su come spostare dati tra frame di dati in memoria, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contesto e i file locali.

> [!NOTE]
> In questa lezione viene utilizzato un set di dati diverso. Il set di dati dei ritardi delle compagnie aeree è un set di dati pubblico ampiamente usato per esperimenti di machine learning. I file di dati usati in questo esempio sono disponibili nella stessa directory in altri esempi del prodotto.

## <a name="load-data-from-a-local-xdf-file"></a>Caricare dati da un file XDF locale

Nella prima metà di questa esercitazione, è stata utilizzata la **RxTextData** funzionare per importare dati in R da un file di testo e quindi utilizzato il **RxDataStep** funzione per spostare i dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

In questa lezione adotta un approccio diverso, e Usa i dati da un file salvato nel [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). Dopo avere eseguito alcune piccole trasformazioni sui dati usando il file XDF, salvare i dati trasformati in un nuovo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella.

**Che cos'è XDF?**

Il formato XDF è uno standard XML sviluppato per i dati a elevata dimensionalità ed è il formato di file nativo usato da [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Si tratta di un formato di file binario con un'interfaccia R che ottimizza l'elaborazione e l'analisi di righe e colonne.  È possibile usarlo per spostare i dati e archiviare subset di dati utili per l'analisi.

1. Impostare il contesto di calcolo sulla workstation locale. **Per questo passaggio sono necessarie autorizzazioni DDL.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. Definire un nuovo oggetto origine dati usando la funzione **RxXdfData** . Per definire un'origine dati XDF, specificare il percorso al file di dati.  

    È possibile specificare il percorso del file usando una variabile di testo. Tuttavia, in questo caso, vi è una comoda scorciatoia, che consiste nell'usare la **rxGetOption** funzionare e ottenere il file (airlinedemosmall. Xdf) dalla directory di dati di esempio.
  
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
> Si noti che non è stato necessario chiamare altre funzioni per caricare i dati nel file XDF e che è stato possibile chiamare immediatamente **rxGetVarInfo** nei dati. Ciò avviene perché XDF è il metodo di archiviazione provvisorio predefinito per **RevoScaleR**. Oltre ai file XDF, i **rxGetVarInfo** funzione ora supporta più tipi di origine.

## <a name="move-contents-to-sql-server"></a>Spostare i contenuti a SQL Server

Con l'origine dati XDF creata nella sessione R locale, è ora possibile passare i dati in una tabella di database, la memorizzazione *DayOfWeek* come integer con valori compresi tra 1 e 7.

1. Definire un oggetto di origine dati di SQL Server, specificare una tabella per contenere i dati e connessione al server remoto.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. Come precauzione, includere un passaggio che controlla se una tabella con lo stesso nome già esiste ed elimina la tabella se esistente. Una tabella esistente gli stessi nomi impedisce di creare uno nuovo.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. Caricare i dati nella tabella usando **rxDataStep**. Questa funzione consente di spostare i dati tra due già definito le origini dati e, facoltativamente, possono trasformare i dati in transito.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    Si tratta di una tabella piuttosto grande, pertanto, attendere fino a quando non viene visualizzato un messaggio di stato finale come questo: *Righe lette: 200000, totale righe elaborate: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>Caricare i dati da una tabella SQL

Una volta sono presenti dati nella tabella, è possibile caricarlo usando una semplice query SQL. 

1. Creare una nuova origine dati SQL Server. L'input è una query sulla nuova tabella appena creato e caricato con i dati. Questa definizione aggiunge livelli di fattore per il *DayOfWeek* colonna, utilizzando il *colInfo* argomento **RxSqlServerData**.
  
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