---
title: 'Python + T-SQL: Esplorare i dati'
description: Esercitazione che illustra come incorporare il codice Python in stored procedure di SQL Server e funzioni T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2aef2ed82803af2a6ca1966cde5f5bf6675ca016
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "74901843"
---
# <a name="explore-and-visualize-the-data"></a>Esplorare e visualizzare i dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fa parte dell'esercitazione [Analisi Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md). 

In questo passaggio si esplorano i dati di esempio e si generano alcuni tracciati. Più avanti si apprenderà come serializzare gli oggetti grafici in Python e quindi deserializzare tali oggetti e creare tracciati.

## <a name="review-the-data"></a>Esaminare i dati

Dedicare prima di tutto un po' di tempo all'esame dello schema dei dati in quanto sono state apportate alcune modifiche per semplificare l'uso dei dati di NYC Taxi

+ Nel set di dati originale i file relativi a identificatori di taxi e record delle corse sono separati. I due set di dati originali sono stati uniti nelle colonne _medallion_, _hack_license_ e _pickup_datetime_.  
+ Il set di dati originale si estende su più file ed è piuttosto grande. È stato eseguito un sottocampionamento per ottenere solo l'1% del numero di record originale. La tabella dati corrente contiene 1.703.957 righe e 23 colonne.

**Identificatori di taxi**

La colonna _medallion_ rappresenta l'ID univoco del taxi.

La colonna _hack_license_ contiene il numero di patente del tassista (in forma anonima).

**Record delle corse e delle tariffe**

Il record di ogni corsa include il luogo e l'ora di inizio e fine della corsa e la distanza percorsa.

Il record di ogni tariffa include i dati del pagamento, ad esempio il tipo di pagamento, l'importo totale e l'importo della mancia.

Le ultime tre colonne possono essere usate per diverse attività di apprendimento automatico.  La colonna _tip_amount_ contiene valori numerici continui e può essere usata come colonna **label** per l'analisi della regressione. La colonna _tipped_ include solo valori sì/no e viene usata per la classificazione binaria. La colonna _tip_class_ include più **etichette di classe** e può essere quindi usata come etichetta per le attività di classificazione multiclasse.

I valori usati per le colonne etichetta sono tutti basati sulla colonna `tip_amount` usando le regole business seguenti:

+ I valori possibili per la colonna etichetta `tipped` sono 0 e 1

    Se `tip_amount` > 0, `tipped` = 1; in caso contrario `tipped` = 0

+ I valori di classe possibili per la colonna etichetta `tip_class` vanno da 0 a 4

    Classe 0: `tip_amount` = $ 0

    Classe 1: `tip_amount` > $ 0 e `tip_amount` <= $ 5
    
    Classe 2: `tip_amount` > $ 5 e `tip_amount` <= $ 10
    
    Classe 3: `tip_amount` > $ 10 e `tip_amount` <= $ 20
    
    Classe 4: `tip_amount` > $ 20

## <a name="create-plots-using-python-in-t-sql"></a>Creare tracciati usando Python in T-SQL

Lo sviluppo di una soluzione di analisi scientifica dei dati prevede in genere frequenti esplorazioni e visualizzazioni dei dati. Poiché la visualizzazione è uno strumento efficace per comprendere la distribuzione di dati e outlier, Python offre numerosi pacchetti per la visualizzazione dei dati. Il modulo **matplotlib** è tra le più diffuse librerie per la visualizzazione e include numerose funzioni per la creazione di istogrammi, grafici a dispersione, box plot e altri grafici per l'esplorazione dei dati.

In questa sezione viene illustrato come lavorare con i tracciati usando stored procedure. Invece che aprire l'immagine nel server, archiviare l'oggetto Python `plot` come dati di tipo **varbinary** e quindi scriverlo in un file che può essere condiviso o visualizzato altrove.

### <a name="create-a-plot-as-varbinary-data"></a>Creare un tracciato come dati varbinary

La stored procedure restituisce un oggetto Python `figure` serializzato come flusso di dati **varbinary**. Non è possibile visualizzare direttamente i dati binari, ma è possibile usare il codice Python nel client per deserializzare e visualizzare le cifre, quindi salvare il file di immagine in un computer client.

1. Creare la stored procedure **PyPlotMatplotlib**, se non è già stata creata dallo script di PowerShell.

    - La variabile `@query` definisce il testo della query (`SELECT tipped FROM nyctaxi_sample`) che viene passato al blocco di codice Python come argomento della variabile di input dello script `@input_data_1`.
    - Lo script Python è piuttosto semplice: gli oggetti `figure` di **matplotlib** vengono usati per creare l'istogramma e il grafico a dispersione e quindi vengono serializzati usando la libreria `pickle`.
    - L'oggetto grafico Python viene serializzato in un frame di dati **pandas** per l'output.
  
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

2. A questo punto, eseguire la stored procedure senza argomenti per generare un tracciato dai dati hardcoded come query di input.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. I risultati saranno simili ai seguenti:
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Da un [client Python](../python/setup-python-client-tools-sql.md) è ora possibile connettersi all'istanza di SQL Server che ha generato gli oggetti tracciato di tipo binario e visualizzare i tracciati. 

    A tale scopo, eseguire il codice Python seguente, sostituendo nome server, nome database e credenziali come appropriato. Verificare che la versione di Python sia la stessa nel client e nel server. Assicurarsi inoltre che la versione delle librerie Python nel client (ad esempio matplotlib) sia uguale o superiore a quella delle librerie installate nel server.
  
    **Con l'autenticazione di SQL Server:**
    
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

    **Con l'autenticazione di Windows:**

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

5.  Se la connessione viene stabilita correttamente, verrà visualizzato un messaggio simile al seguente:
  
    *The plots are saved in directory: xxxx*
  
6.  Il file di output viene creato nella directory di lavoro di Python. Per visualizzare il tracciato, individuare la directory di lavoro di Python e aprire il file. L'immagine seguente mostra un tracciato salvato nel computer client.
  
    ![Importo della mancia rispetto alla tariffa](media/sqldev-python-sample-plot.png "Importo della mancia rispetto alla tariffa") 

## <a name="next-step"></a>Passaggio successivo

[Creare funzionalità di dati mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Passaggio precedente

[Scaricare il set di dati NYC Taxi](demo-data-nyctaxi-in-sql.md)

