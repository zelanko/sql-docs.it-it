---
title: 'Lezione 1: esplorare e visualizzare i dati tramite Python e T-SQL'
description: Esercitazione che illustra come incorporare Python in SQL Server stored procedure e funzioni T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6ee82de1431a6bc21596505dc4b008b817b35830
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714701"
---
# <a name="explore-and-visualize-the-data"></a>Esplorare e visualizzare i dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fa parte di un'esercitazione [relativa all'analisi Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md). 

In questo passaggio si esplorano i dati di esempio e si generano alcuni tracciati. In seguito si apprenderà come serializzare oggetti grafici in Python, quindi deserializzare tali oggetti e creare tracciati.

## <a name="review-the-data"></a>Esaminare i dati

Prima di tutto, è necessario esaminare lo schema dei dati, in quanto sono state apportate alcune modifiche per semplificare l'uso dei dati dei taxi di NYC

+ Il set di dati originale usava file distinti per gli identificatori di taxi e i record di viaggio. Sono stati aggiunti i due set di impostazioni originali per lecolonne medaglier, _hack_license_e _pickup_datetime_.  
+ Il set di dati originale estendeva molti file ed era piuttosto grande. È downsampling ottenere solo l'1% del numero di record originale. La tabella dati corrente contiene 1.703.957 righe e 23 colonne.

**Identificatori di taxi**

La colonna medaglione rappresenta il numero di ID univoco del taxi.

La colonna _hack_license_ contiene il numero di licenza del tassista (resi anonimi).

**Record delle corse e delle tariffe**

Il record di ogni corsa include il luogo e l'ora di inizio e fine della corsa e la distanza percorsa.

Il record di ogni tariffa include i dati del pagamento, ad esempio il tipo di pagamento, l'importo totale e l'importo della mancia.

Le ultime tre colonne possono essere usate per diverse attività di apprendimento automatico.  La colonna _tip_amount_ contiene valori numerici continui e può essere usata come colonna **label** per l'analisi della regressione. La colonna _tipped_ include solo valori sì/no e viene usata per la classificazione binaria. La colonna _tip_class_ include più **etichette di classe** e può essere quindi usata come etichetta per le attività di classificazione multiclasse.

I valori utilizzati per le colonne di etichette sono tutti basati sulla `tip_amount` colonna, utilizzando le regole di business seguenti:

+ Per la `tipped` colonna Label sono possibili valori 0 e 1

    Se `tip_amount` > 0, `tipped` = 1; in `tipped` caso contrario = 0

+ La colonna `tip_class` label presenta i valori di classe possibili 0-4

    Classe 0: `tip_amount` = $0

    Classe 1: `tip_amount` > $0 e `tip_amount` < = $5
    
    Classe 2: `tip_amount` > $5 e `tip_amount` < = $10
    
    Classe 3: `tip_amount` > $10 e `tip_amount` < = $20
    
    Classe 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>Creare tracciati con Python in T-SQL

Lo sviluppo di una soluzione di analisi scientifica dei dati prevede in genere frequenti esplorazioni e visualizzazioni dei dati. Poiché la visualizzazione è uno strumento potente per comprendere la distribuzione dei dati e degli outlier, Python fornisce molti pacchetti per la visualizzazione dei dati. Il modulo **matplotlib** è una delle librerie più diffuse per la visualizzazione e include molte funzioni per la creazione di istogrammi, grafici a dispersione, tracciati di box e altri grafici di esplorazione dei dati.

In questa sezione viene illustrato come utilizzare i tracciati utilizzando le stored procedure. Anziché aprire l'immagine nel server, archiviare l'oggetto `plot` Python come dati **varbinary** e quindi scriverlo in un file che può essere condiviso o visualizzato altrove.

### <a name="create-a-plot-as-varbinary-data"></a>Creazione di un tracciato come dati varbinary

Il stored procedure restituisce un oggetto Python `figure` serializzato come flusso di dati **varbinary** . Non è possibile visualizzare direttamente i dati binari, ma è possibile usare il codice Python sul client per deserializzare e visualizzare le cifre, quindi salvare il file di immagine in un computer client.

1. Creare il stored procedure **PyPlotMatplotlib**, se lo script di PowerShell non è già stato fatto.

    - La variabile `@query` definisce il testo `SELECT tipped FROM nyctaxi_sample`della query, che viene passato al blocco di codice Python come argomento della variabile `@input_data_1`di input dello script.
    - Lo script Python è piuttosto semplice: gli oggetti **matplotlib** `figure` vengono usati per creare l'istogramma e il grafico a dispersione e questi oggetti vengono `pickle` quindi serializzati usando la libreria.
    - L'oggetto grafico Python viene serializzato in un dataframe di Pandas per l'output.
  
    ```sql
    DROP PROCEDURE IF EXISTS PyPlotMatplotlib;
    GO

    CREATE PROCEDURE [dbo].[PyPlotMatplotlib]
    AS
    BEGIN
        SET NOCOUNT ON;
        DECLARE @query nvarchar(max) =
        N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'
        EXECUTE sp_execute_external_script
        @language = N'Python',
        @script = N'
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import pandas as pd
    import pickle

    fig_handle = plt.figure()
    plt.hist(InputDataSet.tipped)
    plt.xlabel("Tipped")
    plt.ylabel("Counts")
    plt.title("Histogram, Tipped")
    plot0 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.tip_amount)
    plt.xlabel("Tip amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Tip amount")
    plot1 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.fare_amount)
    plt.xlabel("Fare amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Fare amount")
    plot2 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.scatter( InputDataSet.fare_amount, InputDataSet.tip_amount)
    plt.xlabel("Fare Amount ($)")
    plt.ylabel("Tip Amount ($)")
    plt.title("Tip amount by Fare amount")
    plot3 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    OutputDataSet = plot0.append(plot1, ignore_index=True).append(plot2, ignore_index=True).append(plot3, ignore_index=True)
    ',
    @input_data_1 = @query
    WITH RESULT SETS ((plot varbinary(max)))
    END
    GO
    ```

2. A questo punto, eseguire il stored procedure senza argomenti per generare un tracciato dai dati hardcoded come query di input.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. I risultati dovrebbero essere simili ai seguenti:
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Da un [client Python](../python/setup-python-client-tools-sql.md)è ora possibile connettersi all'istanza SQL Server che ha generato gli oggetti tracciato binario e visualizzare i tracciati. 

    A tale scopo, eseguire il codice Python seguente, sostituendo il nome del server, il nome del database e le credenziali in base alle esigenze. Verificare che la versione di Python sia la stessa nel client e nel server. Assicurarsi inoltre che le librerie Python nel client (ad esempio matplotlib) siano della versione uguale o superiore rispetto alle librerie installate nel server.
  
    **Uso dell'autenticazione SQL Server:**
    
    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **Utilizzando l'autenticazione di Windows:**

    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=True;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  Se la connessione ha esito positivo, verrà visualizzato un messaggio simile al seguente:
  
    *I tracciati vengono salvati nella directory: xxxx*
  
6.  Il file di output viene creato nella directory di lavoro di Python. Per visualizzare il tracciato, individuare la directory di lavoro Python e aprire il file. Nell'immagine seguente viene illustrato un tracciato salvato nel computer client.
  
    Importo della ![mancia rispetto alla tariffa] Importo della (media/sqldev-python-sample-plot.png "mancia rispetto alla tariffa") 

## <a name="next-step"></a>Passaggio successivo

[Creare funzionalità di dati mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Passaggio precedente

[Scaricare il set di dati di NYC Taxi](demo-data-nyctaxi-in-sql.md)

