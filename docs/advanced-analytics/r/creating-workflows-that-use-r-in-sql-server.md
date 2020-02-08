---
title: Creare flussi di lavoro SSIS e SSRS con R
description: Scenari di integrazione che combinano Machine Learning Services per SQL Server e R Services, Reporting Services (SSRS) e SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2b8d55e95991437e4d76911fd26afb5b1bc9c550
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68715177"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Creare flussi di lavoro SSIS e SSRS con R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo illustra come usare lo script R e Python incorporato usando il linguaggio e le caratteristiche di data science di Machine Learning Services per SQL Server con due importanti funzionalità di SQL Server: SQL Server Integration Services (SSIS) e SQL Server Reporting Services (SSRS). Le librerie R e Python in SQL Server forniscono funzioni statistiche e predittive. SSIS e SSRS forniscono rispettivamente la trasformazione ETL coordinata e le visualizzazioni. Questo articolo illustra come inserire tutte queste caratteristiche in questo modello di flusso di lavoro:

> [!div class="checklist"]
> * Creare una stored procedure contenente R o Python eseguibile
> * Eseguire la stored procedure da SSIS o SSRS

Gli esempi in questo articolo riguardano principalmente R e SSIS, ma gli stessi concetti e passaggi si applicano anche a Python. La seconda sezione fornisce linee guida e collegamenti per le visualizzazioni SSRS.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>Usare SSIS per l'automazione

I flussi di lavoro per l'analisi scientifica dei dati sono altamente iterativi e implicano molte trasformazioni dei dati, tra cui ridimensionamento, aggregazioni, calcolo delle probabilità, ridenominazione e unione degli attributi. I data scientist sono abituati a eseguire molte di queste attività in R, Python o con un altro linguaggio, ma, per eseguire tali flussi di lavoro su dati aziendali, è necessaria la perfetta integrazione con strumenti e processi ETL.

Poiché [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consente di eseguire operazioni complesse in R tramite Transact-SQL e stored procedure, è possibile integrare le attività di data science con i processi ETL esistenti. Invece di eseguire una serie di attività a elevato utilizzo di memoria, la preparazione dei dati può essere ottimizzata usando gli strumenti più efficienti, tra cui [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Ecco alcune idee su come automatizzare le pipeline di elaborazione e modellazione dati usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Estrarre i dati da origini locali o cloud per compilare dati di training 
+ Compilare ed eseguire modelli R o Python come parte di un flusso di lavoro di integrazione dei dati
+ Ripetere il training di modelli a intervalli regolari (pianificati)
+ Caricare i risultati dallo script R o Python ad altre destinazioni, ad esempio Excel, Power BI, Oracle e Teradata, per citarne alcune
+ Usare le attività SSIS per creare caratteristiche dati nel database SQL
+ Usare la diramazione condizionale per cambiare il contesto di calcolo per i processi R e Python

## <a name="ssis-example"></a>Esempio SSIS

L'esempio seguente ha origine da un post di blog MSDN ritirato, creato da Jimmy Wong a questo URL: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

Questo esempio illustra come automatizzare le attività usando SSIS. Se creano le stored procedure con R incorporato usando SQL Server Management Studio e quindi si eseguono tali stored procedure dalle [attività di esecuzione T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) in un pacchetto SSIS.

Per eseguire questo esempio, è consigliabile avere familiarità con Management Studio, SSIS, Progettazione SSIS, progettazione pacchetti e T-SQL. Il pacchetto SSIS usa tre [attività di esecuzione T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) che inseriscono i dati di training in una tabella, modellano i dati e assegnano un punteggiano ai dati per ottenere l'output della stima.

### <a name="load-training-data"></a>Caricare i dati di training

Eseguire lo script seguente in SQL Server Management Studio per creare una tabella per archiviare i dati. Per questo esercizio è consigliabile creare e usare un database di test. 

```T-SQL
Use test-db
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO
```

Creare una stored procedure che carichi i dati di training nel frame di dati. Questo esempio usa il set di dati Iris predefinito. 

```T-SQL
Create procedure load_iris
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'iris_df <- iris;'
        , @input_data_1 = N''
        , @output_data_1_name = N'iris_df'
    with result sets (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100)));
end;
```

In Progettazione SSIS creare un'[attività Esegui SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) che esegua la stored procedure appena definita. Lo script per **SQLStatement** rimuove i dati esistenti, specifica i dati da inserire e quindi chiama la stored procedure per fornire i dati.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![Inserire i dati](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "Inserire i dati")

### <a name="generate-a-model"></a>Generare un modello

Eseguire lo script seguente in SQL Server Management Studio per creare una tabella che archivia un modello. 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

Creare una stored procedure che genera un modello lineare usando [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod). Le librerie RevoScaleR e revoscalepy sono disponibili automaticamente nelle sessioni R e Python in SQL Server, quindi non è necessario importare la libreria.

```T-SQL
Create procedure generate_iris_rx_model
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'
          irisLinMod <- rxLinMod(Sepal.Length ~ Sepal.Width + Petal.Length + Petal.Width + Species, data = ssis_iris);
          trained_model <- data.frame(payload = as.raw(serialize(irisLinMod, connection=NULL)));'
        , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris'
        , @input_data_1_name = N'ssis_iris'
        , @output_data_1_name = N'trained_model'
    with result sets ((model varbinary(max)));
end;
GO
```

In Progettazione SSIS creare un'[attività Esegui SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) per eseguire la stored procedure **generate_iris_rx_model**. Il modello viene serializzato e salvato nella tabella ssis_iris_models. Lo script per **SQLStatement** è il seguente:

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![Genera un modello lineare](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "Genera un modello lineare")

Come checkpoint, al termine di questa attività, è possibile eseguire una query su ssis_iris_models per verificare che contenga un modello binario.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Prevedere (assegnare un punteggio) i risultati usando il modello "con training"

Dopo aver creato il codice che carica i dati di training e genera un modello, l'ultimo passaggio da eseguire consiste nell'usare il modello per generare le stime. 

A tale scopo, inserire lo script R nella query SQL per attivare la funzione R predefinita [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) in ssis_iris_model. Una stored procedure denominata **predict_species_length** esegue questa attività.

```T-SQL
Create procedure predict_species_length (@model varchar(100))
as
begin
    declare @rx_model varbinary(max) = (select model from ssis_iris_models where model_name = @model);
    -- Predict based on the specified model:
    exec sp_execute_external_script
        @language = N'R'
        , @script = N'
irismodel <-unserialize(rx_model);
irispred <- rxPredict(irismodel, ssis_iris[,2:6]);
OutputDataSet <- cbind(ssis_iris[1], irispred$Sepal.Length_Pred, ssis_iris[2]);
colnames(OutputDataSet) <- c("id", "Sepal.Length.Actual", "Sepal.Length.Expected");
#OutputDataSet <- subset(OutputDataSet, Species.Length.Actual != Species.Expected);
'
    , @input_data_1 = N'
    select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris
    '
    , @input_data_1_name = N'ssis_iris'
    , @params = N'@rx_model varbinary(max)'
    , @rx_model = @rx_model
    with result sets ( ("id" int, "Species.Length.Actual" float, "Species.Length.Expected" float)
        );
end;
```

In Progettazione SSIS creare un'[attività Esegui SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) che esegue la stored procedure **predict_species_length** per generare la lunghezza prevista del petalo.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![Generare le stime](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "Generare le stime")

### <a name="run-the-solution"></a>Eseguire la soluzione

In Progettazione SSIS premere F5 per eseguire il pacchetto. Il risultato dovrebbe essere simile allo screenshot seguente.

![F5 per l'esecuzione in modalità debug](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 per l'esecuzione in modalità debug")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>Usare SSRS per le visualizzazioni

Anche se R consente di creare grafici e visualizzazioni interessanti, non è ben integrato con le origini dati esterne e questo significa che ogni grafico deve essere prodotto singolarmente. Anche la condivisione può essere difficile.

Usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] è possibile eseguire operazioni complesse in R tramite stored procedure di [!INCLUDE[tsql](../../includes/tsql-md.md)], facilmente accessibili da un'ampia gamma di strumenti per la creazione di report aziendali, tra cui [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e Power BI.

### <a name="ssrs-example"></a>Esempio SSRS

[R Graphics Device for Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/) (R Graphics Device per Microsoft Reporting Services - SSRS)

Questo progetto CodePlex fornisce il codice che consente di creare un elemento del report personalizzato che esegue il rendering dell'output grafico di R come immagine utilizzabile nei report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  Usando l'elemento del report personalizzato, è possibile:

+ Pubblicare i grafici e i tracciati creati usando R Graphics Device nei dashboard di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

+ Passare i parametri di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ai tracciati R

> [!NOTE]
> Per questo esempio, il codice che supporta R Graphics Device per Reporting Services deve essere installato nel server Reporting Services, oltre che in Visual Studio. Sono anche necessarie la compilazione e la configurazione manuali.

## <a name="next-steps"></a>Passaggi successivi

Gli esempi SSIS e SSRS in questo articolo illustrano due casi di esecuzione di stored procedure che contengono uno script R o Python incorporato. Il concetto fondamentale è che è possibile rendere disponibile uno script R o Python per qualsiasi applicazione o strumento in grado di inviare una richiesta di esecuzione in una stored procedure. Un altro vantaggio di SSIS è la possibilità di creare pacchetti che automatizzano e pianificano una vasta gamma di operazioni, ad esempio l'acquisizione, la pulizia e la manipolazione dei dati e così via, con le caratteristiche di data science R o Python incluse nella catena di operazioni. Per altre informazioni e idee, vedere [Rendere operativo il codice R usando le stored procedure in Machine Learning Services per SQL Server ](operationalizing-your-r-code.md).