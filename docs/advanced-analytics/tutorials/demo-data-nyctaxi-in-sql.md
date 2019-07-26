---
title: Scaricare gli script e i dati demo di NYC taxi per Embedded R e Python
description: Istruzioni per il download dei dati di esempio relativi ai taxi di New York City e la creazione di un database. I dati vengono usati nelle esercitazioni SQL Server linguaggio Python e R che illustrano come incorporare gli script in SQL Server stored procedure e funzioni T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5d5d74090713666a2da6058d9eccee1e33e4d7cb
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469751"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>Dati demo di NYC taxi per SQL Server esercitazioni su Python e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo illustra come configurare un database di esempio costituito da dati pubblici di [New York City taxi e limousine Commission](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). Questi dati vengono usati in varie esercitazioni di R e Python per l'analisi nel database in SQL Server. Per velocizzare l'esecuzione del codice di esempio, è stato creato un campione rappresentativo dell'1% dei dati. Nel sistema, il file di backup del database è leggermente superiore a 90 MB, fornendo 1,7 milioni righe nella tabella dati primaria.

Per completare questo esercizio, è necessario disporre di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) o un altro strumento in grado di ripristinare un file di backup del database ed eseguire query T-SQL.

Le esercitazioni e le guide introduttive che usano questo set di dati includono quanto segue:

+ [Informazioni sulle analisi nel database con R in SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Informazioni sulle analisi nel database con Python in SQL Server](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>Download dei file

Il database di esempio è un file SQL Server 2016 BAK ospitato da Microsoft. È possibile ripristinarlo in SQL Server 2016 e versioni successive. Il download del file inizia immediatamente quando si fa clic sul collegamento. 

Dimensioni del file pari a circa 90 MB.

1. Fare clic su [NYCTaxi_Sample. bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) per scaricare il file di backup del database.

2. Copiare il file nella cartella C:\Programmi\Microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup

3. In Management Studio fare clic con il pulsante destro del mouse su **database** e scegliere **Ripristina file e gruppi di file**.

4. Immettere *NYCTaxi_Sample* come nome del database.

5. Fare clic su **da dispositivo** e quindi aprire la pagina Selezione file per selezionare il file di backup. Fare clic su **Aggiungi** per selezionare NYCTaxi_Sample. bak.

6. Selezionare la casella di controllo **Ripristina** e fare clic su **OK** per ripristinare il database.

## <a name="review-database-objects"></a>Esaminare gli oggetti di database
   
Verificare che gli oggetti di database esistano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nell' [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]istanza di utilizzando. Verranno visualizzati il database, le tabelle, le funzioni e le stored procedure.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>Oggetti nel database NYCTaxi_Sample

La tabella seguente riepiloga gli oggetti creati nel database demo di NYC taxi.

|**Nome oggetto**|**Tipo oggetto**|**Descrizione**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database | Crea un database e due tabelle:<br /><br />tabella dbo. nyctaxi_sample: Contiene il set di dati principale di NYC taxi. Alla tabella viene aggiunto un indice columnstore cluster per migliorare le prestazioni di archiviazione e query. Il campione dell'1% del set di dati NYC Taxi viene inserito in questa tabella.<br /><br />tabella _taxi_models dbo. NYC: Usato per salvare in modo permanente il modello di analisi avanzata con training.|
|**fnCalculateDistance** |funzione a valori scalari | Calcola la distanza diretta tra i percorsi di prelievo e di abbandono. Questa funzione viene usata nelle [funzionalità di creazione dei dati](sqldev-create-data-features-using-t-sql.md), [training e salvataggio di un modello](sqldev-train-and-save-a-model-using-t-sql.md) e [rendere operativo del modello R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |funzione con valori di tabella | Crea nuove funzionalità di dati per il training del modello. Questa funzione viene usata nelle [funzionalità create data](sqldev-create-data-features-using-t-sql.md) e [rendere operativo il modello R](sqldev-operationalize-the-model.md).|


Le stored procedure vengono create usando R e script Python disponibili in varie esercitazioni. Nella tabella seguente sono riepilogate le stored procedure che è possibile aggiungere facoltativamente al database demo di NYC taxi quando si esegue lo script da diverse lezioni.

|**Stored procedure**|**Lingua**|**Descrizione**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | Chiama la funzione RevoScaleR rxHistogram per tracciare l'istogramma di una variabile e quindi restituisce il tracciato come oggetto binario. Questa stored procedure viene utilizzata per [esplorare e visualizzare i dati](sqldev-explore-and-visualize-the-data.md).|
|**RPlotRHist** |R| Crea una rappresentazione grafica usando la funzione cron e salva l'output come file PDF locale. Questa stored procedure viene utilizzata per [esplorare e visualizzare i dati](sqldev-explore-and-visualize-the-data.md).|
|**RxTrainLogitModel**  |R| Effettua il training di un modello di regressione logistica chiamando un pacchetto R. Il modello consente di stimare il valore della colonna indicata. Viene eseguito un training usando il 70% dei dati selezionati casualmente. L'output della stored procedure corrisponde al modello con training, che viene salvato nella tabella nyc_taxi_models. Questa stored procedure viene utilizzata per [il training e il salvataggio di un modello](sqldev-train-and-save-a-model-using-t-sql.md).|
|**RxPredictBatchOutput**  |R | Chiama il modello sottoposto a training per creare stime utilizzando il modello. La stored procedure accetta una query come parametro di input e restituisce una colonna di valori numerici contenente i punteggi per le righe di input. Questa stored procedure viene utilizzata per [stimare i risultati potenziali](sqldev-operationalize-the-model.md).|
|**RxPredictSingleRow**  |R| Chiama il modello sottoposto a training per creare stime utilizzando il modello. Questa stored procedure accetta una nuova osservazione come input, con i singoli valori della funzionalità passati come parametri in linea, e restituisce un valore che stima il risultato in base alla nuova osservazione. Questa stored procedure viene utilizzata per [stimare i risultati potenziali](sqldev-operationalize-the-model.md).|

## <a name="query-the-data"></a>Eseguire query sui dati

Come passaggio di convalida, eseguire una query per confermare che i dati sono stati caricati.

1. In Esplora oggetti, in database, fare clic con il pulsante destro del mouse sul database **NYCTaxi_Sample** e avviare una nuova query.

2. Eseguire alcune query semplici:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
Il database contiene 1,7 milioni righe.

3. All'interno del database è presente una tabella **nyctaxi_sample** che contiene il set di dati. La tabella è stata ottimizzata per i calcoli basati su set con l'aggiunta di un [indice columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md). Eseguire questa istruzione per generare un riepilogo rapido della tabella.

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
I risultati dovrebbero essere simili a quelli mostrati nello screenshot seguente.

  ![Informazioni di riepilogo tabella](media/nyctaxidatatablesummary.png "Risultati query")

## <a name="next-steps"></a>Passaggi successivi

I dati di esempio di NYC taxi sono ora disponibili per l'apprendimento pratico.

+ [Informazioni sulle analisi nel database con R in SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Informazioni sulle analisi nel database con Python in SQL Server](sqldev-in-database-python-for-sql-developers.md)