---
title: 'Lezione 1: esplorare e visualizzare i dati con R e T-SQL'
description: Esercitazione che illustra come esplorare e visualizzare i dati SQL Server usando le funzioni R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2c204e06edd830d8036b6d0119ce1aff1a9c6833
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715376"
---
# <a name="lesson-1-explore-and-visualize-the-data"></a>Lezione 1: Esplorare e visualizzare i dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fa parte di un'esercitazione per sviluppatori SQL sull'uso di R in SQL Server.

In questo passaggio verranno esaminati i dati di esempio e quindi verranno generati alcuni tracciati usando [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) da [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e la funzione [cron](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist) generica in base R. Queste funzioni R sono già incluse in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

Uno degli obiettivi principali di questa lezione è illustrare come chiamare le funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] R da nelle stored procedure e salvare i risultati nei formati di file dell'applicazione:

+ Creare una stored procedure usando **RxHistogram** per generare un tracciato R come dati varbinary. Usare **bcp** per esportare il flusso binario in un file di immagine.
+ Creare un stored procedure usando il **cron** per generare un tracciato, salvando i risultati come output jpg e PDF.

> [!NOTE]
> Poiché la visualizzazione è uno strumento potente per comprendere la forma e la distribuzione dei dati, R offre una gamma di funzioni e pacchetti per la generazione di istogrammi, grafici a dispersione, tracciati di box e altri grafici di esplorazione dei dati. R in genere crea immagini usando un dispositivo R per l'output grafico, che è possibile acquisire e archiviare come tipo di dati **varbinary** per il rendering nell'applicazione. È anche possibile salvare le immagini in uno dei formati di file di supporto (. JPG,. PDF e così via).

## <a name="review-the-data"></a>Esaminare i dati

Lo sviluppo di una soluzione di analisi scientifica dei dati prevede in genere frequenti esplorazioni e visualizzazioni dei dati. Per prima cosa è necessario esaminare i dati di esempio, se non è già stato fatto.

Nel set di dati pubblico originale, gli identificatori di taxi e i record di viaggio sono stati forniti in file distinti. Tuttavia, per semplificare l'utilizzo dei dati di esempio, i due set di dati originali sono Stati Uniti in joinalle colonne medaglione, _hack\_license_e _pickup\_DateTime_.  È stato eseguito anche un campionamento dei record in modo da ottenere solo l'1% del numero di record originale. Il set di dati ridotto risultante include 1.703.957 righe e 23 colonne.

**Identificatori di taxi**
  
-   La colonna medaglione rappresenta il numero di ID univoco del taxi.
  
-   La _colonna\_License hack_ contiene il numero di licenza del tassista (resi anonimi).
  
**Record delle corse e delle tariffe**
  
-   Il record di ogni corsa include il luogo e l'ora di inizio e fine della corsa e la distanza percorsa.
  
-   Il record di ogni tariffa include i dati del pagamento, ad esempio il tipo di pagamento, l'importo totale e l'importo della mancia.
  
-   Le ultime tre colonne possono essere usate per diverse attività di apprendimento automatico. La _colonna\_importo Tip_ contiene valori numerici continui e può essere utilizzata come colonna **Label** per l'analisi di regressione. La colonna _tipped_ include solo valori sì/no e viene usata per la classificazione binaria. La colonna della _classe\_Tip_ ha più **etichette di classe** e pertanto può essere usata come etichetta per le attività di classificazione multiclasse.
  
    In questa procedura dettagliata è descritta soltanto l'attività di classificazione binaria. Si consiglia di provare a creare modelli per le altre due attività di apprendimento automatico, la regressione e la classificazione multiclasse.
  
-   I valori utilizzati per le colonne di etichette sono tutti basati sulla _colonna\_importo Tip_ , usando le regole di business seguenti:
  
    |Nome colonna derivata|Regola|
    |-|-|
     |tipped|Se tip_amount > 0, tipped = 1, altrimenti tipped = 0|
    |tip_class|Classe 0: tip_amount = $0<br /><br />Classe 1: tip_amount > $0 e tip_amount <= $5<br /><br />Classe 2: tip_amount > $5 e tip_amount <= $10<br /><br />Classe 3: tip_amount > $10 e tip_amount <= $20<br /><br />Classe 4: tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>Creare una stored procedure usando rxHistogram per tracciare i dati

Per creare il tracciato, usare [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram), una delle funzioni R avanzate disponibili in [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). Questo passaggio traccia un istogramma in base ai dati di [!INCLUDE[tsql](../../includes/tsql-md.md)] una query. È possibile eseguire il wrapping di questa funzione in un stored procedure, **PlotRxHistogram**.

1. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Esplora oggetti fare clic con il pulsante destro del mouse sul database **NYCTaxi_Sample** e selezionare **nuova query**.

2. Incollare lo script seguente per creare un stored procedure che traccia l'istogramma. Questo esempio è denominato **RPlotRxHistogram*.

    ```sql
    CREATE PROCEDURE [dbo].[RxPlotHistogram]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM nyctaxi_sample'  
      EXECUTE sp_execute_external_script @language = N'R',  
                                         @script = N'  
       image_file = tempfile();  
       jpeg(filename = image_file);  
       #Plot histogram  
       rxHistogram(~tipped, data=InputDataSet, col=''lightgreen'',   
       title = ''Tip Histogram'', xlab =''Tipped or not'', ylab =''Counts'');  
       dev.off();  
       OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
       ',  
       @input_data_1 = @query  
       WITH RESULT SETS ((plot varbinary(max)));  
    END
    GO
    ```

Gli elementi chiave da comprendere in questo script sono i seguenti: 
  
+ La variabile `@query` definisce il testo della query (`'SELECT tipped FROM nyctaxi_sample'`) che viene passato allo script R come argomento alla variabile di input dello script `@input_data_1`. Per gli script R che vengono eseguiti come processi esterni, è necessario avere un mapping uno-a-uno tra input e script e gli input per il sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure che avvia la sessione di r SQL Server.
  
+ All'interno dello script R, viene definita`image_file`una variabile () per archiviare l'immagine. 

+ Per generare il tracciato viene chiamata la funzione **rxHistogram** della libreria RevoScaleR.
  
+ Il dispositivo R è impostato su **off** perché si sta eseguendo questo comando come script esterno in SQL Server. In genere in R, quando si esegue un comando di traccia di alto livello, R apre una finestra grafica, denominata *dispositivo*. È possibile disattivare il dispositivo se si scrive in un file o si gestisce l'output in un altro modo.
  
+ L'oggetto grafico R viene serializzato in un data.frame R per l'output.

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>Eseguire l'stored procedure e usare bcp per esportare i dati binari in un file di immagine

La stored procedure restituisce l'immagine come un flusso di dati varbinary, che ovviamente non è possibile visualizzare direttamente. Tuttavia, è possibile usare l'utilità **bcp** utilità per ottenere i dati varbinary e salvarli come file di immagine in un computer client.
  
1. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eseguire l'istruzione seguente:
  
    ```sql
    EXEC [dbo].[RxPlotHistogram]
    ```
  
    **Risultati**
    
    *traccia* *0xFFD8FFE000104A4649...*
  
2. Aprire un prompt dei comandi di PowerShell ed eseguire il comando seguente, specificando il nome dell'istanza, il nome del database, il nome utente e le credenziali appropriati come argomenti. Per coloro che usano le identità di Windows, è possibile sostituire **-U** e **-P** con **-T**.
  
    ```powershell
    bcp "exec RxPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
    ```

    > [!NOTE]
    > Le opzioni di comando per BCP fanno distinzione tra maiuscole e minuscole.
  
3. Se la connessione viene stabilita, verrà richiesto di immettere altre informazioni sul formato di file grafico. 

   Premere INVIO a ogni richiesta per accettare le impostazioni predefinite, ad eccezione di quanto segue:
    
   + Per **prefix-length of field plot**digitare 0
  
   + Digitare **Y** per salvare i parametri di output e riutilizzarli in seguito.
  
    ```powershell
    Enter the file storage type of field plot [varbinary(max)]: 
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **Risultati**
    
    ```powershell
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > Se si salvano le informazioni di formato su file (bcp.fmt), l'utilità **bcp** genera una definizione di formato che è possibile applicare a comandi simili in futuro senza specificare le opzioni di formato di file grafico. Per usare il file di formato, aggiungere `-f bcp.fmt` alla fine di qualsiasi riga di comando, dopo l'argomento password.
  
4.  Il file di output verrà creato nella stessa directory in cui è stato eseguito il comando di PowerShell. Per visualizzare il grafico, è sufficiente aprire il file plot.jpg.
  
    ![Corse di taxi con e senza mancia](media/rsql-devtut-tippedornot.jpg "Corse di taxi con e senza mancia")  
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>Creare una stored procedure usando il cron e più formati di output

In genere, i data scientist generano più visualizzazioni di dati per ottenere informazioni dettagliate sui dati da prospettive diverse. In questo esempio verrà creato un stored procedure denominato **RPlotHist** per scrivere istogrammi, scatterplot e altri elementi grafici R in. JPG e. Formato PDF.

Questo stored procedure usa la funzione **cron** per creare l'istogramma, esportando i dati binari nei formati più diffusi, ad esempio. JPG,. PDF, e. PNG. 

1. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Esplora oggetti fare clic con il pulsante destro del mouse sul database **NYCTaxi_Sample** e selezionare **nuova query**.

2. Incollare lo script seguente per creare un stored procedure che traccia l'istogramma. Questo esempio è denominato **RPlotHist** .
  
    ```sql
    CREATE PROCEDURE [dbo].[RPlotHist]  
    AS  
    BEGIN  
      SET NOCOUNT ON;  
      DECLARE @query nvarchar(max) =  
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'  
      EXECUTE sp_execute_external_script @language = N'R',  
      @script = N'  
       # Set output directory for files and check for existing files with same names   
        mainDir <- ''C:\\temp\\plots''  
        dir.create(mainDir, recursive = TRUE, showWarnings = FALSE)  
        setwd(mainDir);  
        print("Creating output plot files:", quote=FALSE)
        
        # Open a jpeg file and output histogram of tipped variable in that file.  
        dest_filename = tempfile(pattern = ''rHistogram_Tipped_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.jpg'',sep="")  
        print(dest_filename, quote=FALSE);  
        jpeg(filename=dest_filename);  
        hist(InputDataSet$tipped, col = ''lightgreen'', xlab=''Tipped'',   
            ylab = ''Counts'', main = ''Histogram, Tipped'');  
         dev.off();  

        # Open a pdf file and output histograms of tip amount and fare amount.   
        # Outputs two plots in one row  
        dest_filename = tempfile(pattern = ''rHistograms_Tip_and_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=7);  
        par(mfrow=c(1,2));  
        hist(InputDataSet$tip_amount, col = ''lightgreen'',   
            xlab=''Tip amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram, Tip amount'', xlim = c(0,40), 100);  
        hist(InputDataSet$fare_amount, col = ''lightgreen'',   
            xlab=''Fare amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram,   
            Fare amount'',   
            xlim = c(0,100), 100);  
       dev.off();  
  
        # Open a pdf file and output an xyplot of tip amount vs. fare amount using lattice;  
        # Only 10,000 sampled observations are plotted here, otherwise file is large.  
        dest_filename = tempfile(pattern = ''rXYPlots_Tip_vs_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=4);  
        plot(tip_amount ~ fare_amount,   
            data = InputDataSet[sample(nrow(InputDataSet), 10000), ],   
            ylim = c(0,50),   
            xlim = c(0,150),   
            cex=.5,   
            pch=19,   
            col=''darkgreen'',    
            main = ''Tip amount by Fare amount'',   
            xlab=''Fare Amount ($)'',   
            ylab = ''Tip Amount ($)'');   
        dev.off();',  
     @input_data_1 = @query  
     END
    ```
  
+ L'output della query SELECT all'interno della stored procedure viene archiviato nel frame di dati R predefinito `InputDataSet`. Sarà quindi possibile chiamare diverse funzioni di creazione dei grafici R per generare i file grafici. La maggior parte degli script R incorporati rappresenta le opzioni di queste funzioni di grafici,  ad esempio `plot` o `hist`.
  
+ Tutti i file vengono salvati nella cartella locale C:\temp\Plots. La cartella di destinazione è definita dagli argomenti specificati nello script R come parte della stored procedure.  È possibile modificare la cartella di destinazione modificando il valore della variabile `mainDir`.

+ Per inviare i file in una cartella diversa, modificare il valore della variabile `mainDir` nello script R incorporato nella stored procedure. È anche possibile modificare lo script per produrre l'output in formati diversi, in più file e così via.

### <a name="execute-the-stored-procedure"></a>Eseguire la stored procedure

Eseguire l'istruzione seguente per esportare i dati del tracciato binario nei formati di file JPEG e PDF.

```sql
EXEC RPlotHist
```

**Risultati**
    
```sql
STDOUT message(s) from external script:
[1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 

C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]

C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
```

I numeri nei nomi file vengono generati in modo casuale per assicurarsi di non ricevere un errore durante il tentativo di scrittura in un file esistente.

### <a name="view-output"></a>Visualizza output 

Per visualizzare il tracciato, aprire la cartella di destinazione ed esaminare i file creati dal codice R nel stored procedure.

1. Passare alla cartella indicata nel messaggio STDOUT (nell'esempio, questo è C:\temp\plots\)

2. Apri `rHistogram_Tipped.jpg` per visualizzare il numero di corse che hanno ricevuto una mancia e i viaggi senza suggerimento. Questo istogramma è molto simile a quello generato nel passaggio precedente.

3. Apre `rHistograms_Tip_and_Fare_Amount.pdf` per visualizzare la distribuzione degli importi delle mance, tracciati in base agli importi delle tariffe.
    
  ![istogramma che mostra tip_amount e fare_amount](media/rsql-devtut-tipamtfareamt.PNG "istogramma che mostra tip_amount e fare_amount")

4. Aprire `rXYPlots_Tip_vs_Fare_Amount.pdf` per visualizzare un scatterplot con l'importo della tariffa sull'asse x e l'importo della Mancia sull'asse y.

   ![importo della Mancia tracciato sopra l'importo della tariffa](media/rsql-devtut-tipamtbyfareamt.PNG "importo della Mancia tracciato sopra l'importo della tariffa")

## <a name="next-lesson"></a>Lezione successiva

[Lezione 2: Creare funzionalità di dati con T-SQL](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>Lezione precedente

[Configurare i dati demo di NYC Taxi](demo-data-nyctaxi-in-sql.md)
