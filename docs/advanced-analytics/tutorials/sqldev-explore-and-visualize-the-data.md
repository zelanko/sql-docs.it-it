---
title: 'Lezione 1 esplorare e visualizzare i dati usando R e T-SQL: SQL Server Machine Learning'
description: Esercitazione che illustra come esplorare e visualizzare i dati di SQL Server usando funzioni R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b6822892547b8fa4ff3ad4dced02908d10cd39ec
ms.sourcegitcommit: 299b63e04498eba22659970cd077f247c1657931
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898996"
---
# <a name="lesson-1-explore-and-visualize-the-data"></a>Lezione 1: Esplorare e visualizzare i dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fa parte di un'esercitazione per sviluppatori SQL su come usare R in SQL Server.

In questo passaggio verrà esaminare i dati di esempio e quindi generati alcuni tracciati usando [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) dalla [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e il tipo generico [Hist](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist) funzione in r di base. Queste funzioni R sono già inclusi [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

Degli obiettivi principali di questa lezione è che mostra come chiamare funzioni R [!INCLUDE[tsql](../../includes/tsql-md.md)] nelle stored procedure e salvare i risultati in formati di file dell'applicazione:

+ Creare una stored procedure usando **RxHistogram** per generare un tracciato R sotto forma di dati varbinary. Uso **bcp** per esportare il flusso binario in un file di immagine.
+ Creare una stored procedure usando **Hist** per generare un tracciato, salvataggio dei risultati come output JPG e PDF.

> [!NOTE]
> Poiché la visualizzazione è uno strumento efficace per comprendere la forma dei dati e la distribuzione, R fornisce una gamma di funzioni e i pacchetti per la generazione di istogrammi, grafici a dispersione, box plot e altri grafici di esplorazione dei dati. R crea in genere le immagini usando un dispositivo R per l'output grafico, che è possibile acquisire e archiviare come un **varbinary** tipo di dati per il rendering nell'applicazione. È inoltre possibile salvare le immagini per tutti i formati di file di supporto (. JPG. PDF e così via).

## <a name="review-the-data"></a>Esaminare i dati

Lo sviluppo di una soluzione di analisi scientifica dei dati prevede in genere frequenti esplorazioni e visualizzazioni dei dati. Quindi, innanzitutto è opportuno esaminare i dati di esempio, se non è già presente.

Nel set di dati pubblico originale, sono stati forniti gli identificatori di taxi e i record delle corse in file separati. Tuttavia, per rendere più facile da usare i dati di esempio, due set di dati originale sono stati uniti nelle colonne _medallion_, _hack\_licenza_, e _pickup\_ Data/ora_.  È stato eseguito anche un campionamento dei record in modo da ottenere solo l'1% del numero di record originale. Il set di dati ridotto risultante include 1.703.957 righe e 23 colonne.

**Identificatori di taxi**
  
-   Il _medallion_ colonna rappresenta il numero di id univoco del taxi.
  
-   Il _hack\_licenza_ colonna contiene i taxi numero di patente (resi anonimizzato).
  
**Record delle corse e delle tariffe**
  
-   Il record di ogni corsa include il luogo e l'ora di inizio e fine della corsa e la distanza percorsa.
  
-   Il record di ogni tariffa include i dati del pagamento, ad esempio il tipo di pagamento, l'importo totale e l'importo della mancia.
  
-   Le ultime tre colonne possono essere usate per diverse attività di apprendimento automatico. Il _suggerimento\_quantità_ colonna contiene valori numerici continui e può essere utilizzato come il **etichetta** colonna per l'analisi di regressione. La colonna _tipped_ include solo valori sì/no e viene usata per la classificazione binaria. Il _suggerimento\_classe_ colonna ha più **etichette di classe** e pertanto può essere utilizzato come etichetta per le attività di classificazione multiclasse.
  
    In questa procedura dettagliata è descritta soltanto l'attività di classificazione binaria. Si consiglia di provare a creare modelli per le altre due attività di apprendimento automatico, la regressione e la classificazione multiclasse.
  
-   I valori utilizzati per le colonne etichetta sono tutti basati sul _suggerimento\_quantità_ colonna utilizzando le regole di business:
  
    |Nome colonna derivata|Regola|
    |-|-|
     |tipped|Se tip_amount > 0, tipped = 1, altrimenti tipped = 0|
    |tip_class|Classe 0: tip_amount = $0<br /><br />Classe 1: tip_amount > $0 e tip_amount <= $5<br /><br />Classe 2: tip_amount > $5 e tip_amount <= $10<br /><br />Classe 3: tip_amount > $10 e tip_amount <= $20<br /><br />Classe 4: tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>Creare una stored procedure, l'uso di rxHistogram per tracciare i dati

Per creare il tracciato, utilizzare [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram), una delle funzioni R avanzate disponibili nel [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). Questo passaggio viene tracciata un istogramma basato sui dati da un [!INCLUDE[tsql](../../includes/tsql-md.md)] query. È possibile eseguire il wrapping di questa funzione in una stored procedure **PlotRxHistogram**.

1. Nelle [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], in Esplora oggetti, fare doppio clic il **NYCTaxi_Sample** del database e selezionare **nuova Query**.

2. Incollare lo script seguente per creare una stored procedure che viene tracciata l'istogramma. Questo esempio è denominato **RPlotRxHistogram*.

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

Punti chiave per comprendere in questo script includono quanto segue: 
  
+ La variabile `@query` definisce il testo della query (`'SELECT tipped FROM nyctaxi_sample'`) che viene passato allo script R come argomento alla variabile di input dello script `@input_data_1`. Per gli script R eseguiti come processi esterni, è necessario avere un mapping uno a uno tra gli input allo script e gli input per il [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure che avvia la sessione di R in SQL Server di sistema.
  
+ In questo script R, una variabile (`image_file`) è definito per archiviare l'immagine. 

+ Il **rxHistogram** funzione della libreria RevoScaleR viene chiamata per generare il tracciato.
  
+ Il dispositivo R viene impostato su **disattivata** perché si esegue questo comando come uno script esterno in SQL Server. In genere in R, quando si esegue un comando di tracciamento ad alto livello, R consente di aprire una finestra grafica, denominata un *dispositivo*. È possibile disattivare il dispositivo se si esegue la scrittura in un file o la gestione di un altro modo l'output.
  
+ L'oggetto grafico R viene serializzato in un data.frame R per l'output.

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>Eseguire la stored procedure e uso di bcp per esportare i dati binari in un file di immagine

La stored procedure restituisce l'immagine come un flusso di dati varbinary, che ovviamente non è possibile visualizzare direttamente. Tuttavia, è possibile usare l'utilità **bcp** utilità per ottenere i dati varbinary e salvarli come file di immagine in un computer client.
  
1. In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eseguire l'istruzione seguente:
  
    ```sql
    EXEC [dbo].[RxPlotHistogram]
    ```
  
    **Risultati**
    
    *plot* *0xFFD8FFE000104A4649...*
  
2. Aprire un prompt dei comandi di PowerShell ed eseguire il comando seguente, fornendo il nome dell'istanza appropriata, nome del database, nome utente e le credenziali come argomenti. Per chi usa le identità di Windows, è possibile sostituire **- U** e **-P** con **-T**.
  
    ```powershell
    bcp "exec RxPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
    ```

    > [!NOTE]
    > Opzioni di comando per bcp sono tra maiuscole e minuscole.
  
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
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>Creare una stored procedure con più formati di output e Hist

In genere, i data Scientist possono generano più visualizzazioni dei dati per ottenere informazioni dettagliate sui dati da prospettive diverse. In questo esempio, si creerà una stored procedure denominata **RPlotHist** scrivere istogrammi, grafici e altri elementi grafici R per. JPG e. Formato PDF.

Questa stored procedure viene utilizzata la **Hist** funzione per creare l'istogramma, esportando i dati binari in formati comuni, ad esempio. JPG. PDF, e. PNG. 

1. Nelle [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], in Esplora oggetti, fare doppio clic il **NYCTaxi_Sample** del database e selezionare **nuova Query**.

2. Incollare lo script seguente per creare una stored procedure che viene tracciata l'istogramma. Questo esempio è denominato **RPlotHist** .
  
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

Eseguire l'istruzione seguente per esportare i dati binari tracciato in formati di file JPEG e PDF.

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

I numeri nei nomi dei file vengono generati in modo casuale per garantire che non si ottiene un errore durante il tentativo di scrivere in un file esistente.

### <a name="view-output"></a>Visualizzare l'output 

Per visualizzare il grafico, aprire la cartella di destinazione ed esaminare i file che sono stati creati dal codice R nella stored procedure.

1. Andare nella cartella indicata nel messaggio di STDOUT (nell'esempio, si tratta C:\temp\plots\)

2. Apri `rHistogram_Tipped.jpg` per mostrare il numero di corse è stata ricevuta una Mancia e è stata ricevuta alcuna descrizione. (Questa istogramma è simile a quello generato nel passaggio precedente).

3. Apri `rHistograms_Tip_and_Fare_Amount.pdf` per visualizzare la distribuzione dell'importo delle mance, eseguirne la tracciatura rispetto gli importi delle tariffe.
    
  ![istogramma che mostra tip_amount e fare_amount](media/rsql-devtut-tipamtfareamt.PNG "istogramma che mostra tip_amount e fare_amount")

4. Apri `rXYPlots_Tip_vs_Fare_Amount.pdf` per visualizzare un grafico a dispersione con l'importo della tariffa per l'asse x e l'importo della Mancia sull'asse y.

   ![importo della Mancia tracciate nel importo della tariffa](media/rsql-devtut-tipamtbyfareamt.PNG "importo della Mancia tracciate nel importo della tariffa in")

## <a name="next-lesson"></a>Lezione successiva

[Lezione 2: Creare funzionalità di dati mediante T-SQL](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>Lezione precedente

[Imposta i dati demo dei Taxi di NYC](demo-data-nyctaxi-in-sql.md)
