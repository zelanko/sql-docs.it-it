---
title: 'Lezione 1 esplorare e visualizzare i dati usando Python e T-SQL: SQL Server Machine Learning'
description: Esercitazione che illustra come incorporare Python in SQL Server funzioni e stored procedure T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 879b3e3d4a213c4b6f1ae1fd2c8e6f8f302a4eda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961873"
---
# <a name="explore-and-visualize-the-data"></a>Esplorare e visualizzare i dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fa parte di un'esercitazione [analitica di Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md). 

In questo passaggio è esplorare i dati di esempio e generati alcuni tracciati. Successivamente, è illustrato come serializzare oggetti grafici in Python, quindi deserializzare tali oggetti e creare tracciati.

## <a name="review-the-data"></a>Esaminare i dati

In primo luogo, è opportuno esplorare lo schema di dati, perché sono state apportate alcune modifiche per renderne più semplice usare i dati dei Taxi di NYC

+ Set di dati originale utilizzato file separati per gli identificatori di taxi e i record delle corse. È stato aggiunto due set di dati originale nelle colonne _medallion_, _hack_license_, e _pickup_datetime_.  
+ Set di dati originale con spanning molti file e molto grande. Abbiamo downsampling per ottenere solo l'1% del numero di record originale. La tabella di dati corrente include 1.703.957 righe e 23 colonne.

**Identificatori di taxi**

Il _medallion_ colonna rappresenta il numero di ID univoco del taxi.

Il _hack_license_ colonna contiene i taxi numero di patente (resi anonimizzato).

**Record delle corse e delle tariffe**

Il record di ogni corsa include il luogo e l'ora di inizio e fine della corsa e la distanza percorsa.

Il record di ogni tariffa include i dati del pagamento, ad esempio il tipo di pagamento, l'importo totale e l'importo della mancia.

Le ultime tre colonne possono essere usate per diverse attività di apprendimento automatico.  La colonna _tip_amount_ contiene valori numerici continui e può essere usata come colonna **label** per l'analisi della regressione. La colonna _tipped_ include solo valori sì/no e viene usata per la classificazione binaria. La colonna _tip_class_ include più **etichette di classe** e può essere quindi usata come etichetta per le attività di classificazione multiclasse.

I valori utilizzati per le colonne etichetta sono tutti basati sul `tip_amount` colonna utilizzando le regole di business:

+ Colonna di etichetta `tipped` dispone di valori 0 e 1

    Se `tip_amount` > 0, `tipped` = 1; in caso contrario `tipped` = 0

+ Colonna di etichetta `tip_class` dispone di valori possibili della classe 0 e 4

    Classe 0: `tip_amount` = $0

    Classe 1: `tip_amount` > $0 e `tip_amount` < = $5
    
    Classe 2: `tip_amount` > $5 e `tip_amount` < = $10
    
    Classe 3: `tip_amount` > $10 e `tip_amount` < = $20
    
    Classe 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>Creare grafici usando Python in T-SQL

Lo sviluppo di una soluzione di analisi scientifica dei dati prevede in genere frequenti esplorazioni e visualizzazioni dei dati. Poiché la visualizzazione è uno strumento efficace per comprendere distribuzione dei dati e outlier, Python offre numerosi pacchetti per la visualizzazione dei dati. Il **matplotlib** modulo è una delle librerie più diffuse per la visualizzazione e include molte funzioni per la creazione di istogrammi, grafici a dispersione, box plot e altri grafici di esplorazione dei dati.

In questa sezione descrive come usare i grafici di utilizzo delle stored procedure. Invece di aprire l'immagine nel server, archiviare l'oggetto di Python `plot` come **varbinary** dati e quindi scriverà che in un file che possono essere condivisi o visualizzati in un' posizione.

### <a name="create-a-plot-as-varbinary-data"></a>Creare un tracciato sotto forma di dati varbinary

La stored procedure restituisce un Python serializzato `figure` oggetto come flusso dei **varbinary** dei dati. Non è possibile visualizzare direttamente i dati binari, ma è possibile usare codice Python nel client per deserializzare e visualizzare le cifre e quindi salvare il file di immagine in un computer client.

1. Creare la stored procedure **PyPlotMatplotlib**, se lo script di PowerShell non è stato già fatto.

    - La variabile `@query` definisce il testo della query `SELECT tipped FROM nyctaxi_sample`, che viene passato al blocco di codice Python come argomento alla variabile di input di script, `@input_data_1`.
    - Lo script di Python è abbastanza semplice: **matplotlib** `figure` oggetti vengono utilizzati per eseguire il tracciato istogramma e a dispersione e questi oggetti vengono quindi serializzati utilizzando la `pickle` libreria.
    - L'oggetto graphics Python viene serializzato in un **pandas** frame di dati per l'output.
  
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

2. A questo punto è possibile eseguire la stored procedure senza argomenti per generare un grafico dai dati hardcoded come query di input.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. I risultati dovrebbero essere simile al seguente:
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Da un [client Python](../python/setup-python-client-tools-sql.md), è ora possibile connettersi all'istanza di SQL Server che ha generato gli oggetti tracciato binario e visualizzare i tracciati. 

    A tale scopo, eseguire il codice Python seguente, sostituendo il nome del server, nome del database e le credenziali come appropriato. Assicurarsi che la versione di Python è lo stesso per il client e server. Assicurarsi anche che le librerie di Python nel client (ad esempio matplotlib) siano la stessa versione o successiva rispetto alle librerie installate nel server.
  
    **Uso dell'autenticazione di SQL Server:**
    
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

    **Uso dell'autenticazione di Windows:**

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

5.  Se la connessione ha esito positivo, si dovrebbe vedere un messaggio simile al seguente:
  
    *I tracciati vengono salvati nella directory: xxxx*
  
6.  Il file di output viene creato nella directory di lavoro Python. Per visualizzare il tracciato, individuare la directory di lavoro di Python e aprire il file. L'immagine seguente mostra un tracciato salvato nel computer client.
  
    ![Quantità e delle tariffe importo della Mancia](media/sqldev-python-sample-plot.png "importo della Mancia quantità e delle tariffe") 

## <a name="next-step"></a>Passaggio successivo

[Creare funzionalità di dati mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Passaggio precedente

[Scaricare il set di dati dei Taxi di NYC](demo-data-nyctaxi-in-sql.md)

