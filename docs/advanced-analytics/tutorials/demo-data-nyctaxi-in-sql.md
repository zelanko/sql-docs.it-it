---
title: Scaricare i dati demo dei Taxi di NYC e gli script per embedded R e Python, SQL Server Machine Learning
description: Istruzioni per scaricare i dati di esempio relativi ai taxi di New York City e creazione di un database. I dati viene usati nelle esercitazioni sul linguaggio di SQL Server Python e R che illustra come incorporare script nelle funzioni di T-SQL e stored procedure SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: d20c37f0f136ad3f0ddf1b5ce046306101aafa78
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962100"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>Dati demo dei Taxi di NYC per le esercitazioni di SQL Server Python e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come configurare un database di esempio costituito da dati pubblici dal [Taxi di New York City and Limousine Commission](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). Questi dati vengono utilizzati nelle esercitazioni diversi R e Python per analitica nel database in SQL Server. Per rendere più rapido eseguire il codice di esempio, è stato creato un campione rappresentativo di % 1 dei dati. Nel sistema, il file di backup di database è leggermente superiore a 90 MB, fornendo 1.7 milioni di righe nella tabella di dati primario.

Per completare questo esercizio, è necessario disporre [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) o un altro strumento che è possibile ripristinare un file di backup di database ed eseguire query T-SQL.

Esercitazioni e guide introduttive utilizzano questo set di dati seguenti:

+ [Informazioni su analitica nel database con R in SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Informazioni su analitica nel database usando Python in SQL Server](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>Download dei file

Il database di esempio è un file di SQL Server 2016 BAK ospitato da Microsoft. È possibile ripristinarlo in SQL Server 2016 e versioni successive. Download di file inizia immediatamente quando si fa clic sul collegamento. 

Dimensioni del file sono di circa 90 MB.

1. Fare clic su [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) per scaricare il file di backup di database.

2. Copiare il file C:\Program files\Microsoft SQL Server\MSSQL-istanza-name\MSSQL\Backup cartella.

3. In Management Studio, fare doppio clic **database** e selezionare **Ripristina file e filegroup**.

4. Immettere *NYCTaxi_Sample* come nome del database.

5. Fare clic su **dal dispositivo** e quindi aprire la pagina di selezione file per selezionare il file di backup. Fare clic su **Add** selezionare NYCTaxi_Sample.bak.

6. Selezionare il **ripristinare** casella di controllo e fare clic su **OK** per ripristinare il database.

## <a name="review-database-objects"></a>Esaminare gli oggetti di database
   
Verificare gli oggetti di database siano presenti nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si dovrebbe essere il database, tabelle, funzioni e stored procedure.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>Oggetti nel database NYCTaxi_Sample

La tabella seguente riepiloga gli oggetti creati nel database di esempio dei Taxi di NYC.

|**Nome oggetto**|**Tipo oggetto**|**Descrizione**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database | Crea un database e due tabelle:<br /><br />Nella tabella dbo. nyctaxi_sample: Contiene il set di dati principale NYC Taxi. Alla tabella viene aggiunto un indice columnstore cluster per migliorare le prestazioni di archiviazione e query. Il campione dell'1% del set di dati dei Taxi di NYC viene inserito in questa tabella.<br /><br />tabella dbo.nyc_taxi_models: Utilizzato per rendere permanente il modello con training analitica avanzata.|
|**fnCalculateDistance** |funzione a valori scalari | Calcola la distanza diretta tra posizioni di salita e. Questa funzione viene utilizzata [creare funzionalità di dati](sqldev-create-data-features-using-t-sql.md), [training e salvataggio di un modello](sqldev-train-and-save-a-model-using-t-sql.md) e [Operazionalizzare il modello R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |funzione con valori di tabella | Crea nuova funzionalità di dati per il training del modello. Questa funzione viene utilizzata [creare funzionalità di dati](sqldev-create-data-features-using-t-sql.md) e [Operazionalizzare il modello R](sqldev-operationalize-the-model.md).|


Le stored procedure vengono create utilizzando lo script R e Python disponibili nelle varie esercitazioni. La tabella seguente riepiloga le stored procedure che è possibile aggiungere al database di demo dei Taxi di NYC, facoltativamente, quando si esegue lo script delle varie lezioni.

|**stored procedure**|**Lingua**|**Descrizione**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | Chiama la funzione di RevoScaleR rxHistogram per tracciare l'istogramma di una variabile e quindi restituisce il tracciato come oggetto binario. Questa stored procedure viene utilizzata [esplorare e visualizzare dati](sqldev-explore-and-visualize-the-data.md).|
|**RPlotRHist** |R| Crea un elemento grafico tramite la funzione Hist e l'output viene salvato come file PDF locale. Questa stored procedure viene utilizzata [esplorare e visualizzare dati](sqldev-explore-and-visualize-the-data.md).|
|**RxTrainLogitModel**  |R| Esegue il training di un modello di regressione logistica mediante la chiamata di un pacchetto R. Il modello consente di stimare il valore della colonna indicata. Viene eseguito un training usando il 70% dei dati selezionati casualmente. L'output della stored procedure corrisponde al modello con training, che viene salvato nella tabella nyc_taxi_models. Questa stored procedure viene utilizzata [eseguire il training e salvataggio di un modello](sqldev-train-and-save-a-model-using-t-sql.md).|
|**RxPredictBatchOutput**  |R | Chiama il modello con training per creare stime tramite il modello. La stored procedure accetta una query come parametro di input e restituisce una colonna di valori numerici contenente i punteggi per le righe di input. Questa stored procedure viene utilizzata [stimare i possibili risultati](sqldev-operationalize-the-model.md).|
|**RxPredictSingleRow**  |R| Chiama il modello con training per creare stime tramite il modello. Questa stored procedure accetta una nuova osservazione come input, con i singoli valori della funzionalità passati come parametri in linea, e restituisce un valore che stima il risultato in base alla nuova osservazione. Questa stored procedure viene utilizzata [stimare i possibili risultati](sqldev-operationalize-the-model.md).|

## <a name="query-the-data"></a>Eseguire query sui dati

Come passaggio di convalida, eseguire una query per verificare che i dati è stati caricati.

1. In Esplora oggetti, nel database, fare doppio clic il **NYCTaxi_Sample** , del database e avviare una nuova query.

2. Eseguire alcune semplici query:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
Il database contiene 1.7 milioni di righe.

3. All'interno del database è un **nyctaxi_sample** tabella che contiene il set di dati. La tabella è stata ottimizzata per i calcoli basati su set con l'aggiunta di un [indice columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md). Eseguire questa istruzione per generare un breve riepilogo per la tabella.

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
Risultati dovrebbero essere simili a quelli che mostra nello screenshot seguente.

  ![Le informazioni di riepilogo di tabella](media/nyctaxidatatablesummary.png "risultati della Query")

## <a name="next-steps"></a>Passaggi successivi

I dati di esempio dei Taxi di NYC sono ora disponibili per la formazione pratica.

+ [Informazioni su analitica nel database con R in SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Informazioni su analitica nel database usando Python in SQL Server](sqldev-in-database-python-for-sql-developers.md)