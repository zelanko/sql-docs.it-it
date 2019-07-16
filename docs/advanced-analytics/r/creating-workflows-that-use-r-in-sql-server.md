---
title: Creare flussi di lavoro SSIS e SSRS con R - servizi di SQL Server Machine Learning
description: Scenari di integrazione di combinazione di servizi di SQL Server Machine Learning e R Services, Reporting Services (SSRS) e SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a9f3a76ac1829f529e0f3e5459ab842dcafa7c80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962690"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Creare flussi di lavoro SSIS e SSRS con R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come usare script R e Python incorporato usando le funzionalità di analisi scientifica dei dati e di lingua di SQL Server Machine Learning Services con due importanti caratteristiche di SQL Server: SQL Server Integration Services (SSIS) e SQL Server Reporting Services SSRS. Librerie di R e Python in SQL Server forniscono funzioni statistiche e predittive. SSIS e SSRS forniscono coordinato trasformazione ETL e le visualizzazioni, rispettivamente. Questo articolo illustra come creare tutte queste funzionalità in questo modello di flusso di lavoro:

> [!div class="checklist"]
> * Creare una stored procedure contenente eseguibile R o Python
> * Eseguire la stored procedure da SSIS o SSRS

Gli esempi in questo articolo sono principalmente sul SSIS e R, ma i concetti e passaggi si applicano ugualmente a Python. La seconda sezione fornisce indicazioni e i collegamenti per le visualizzazioni di SSRS.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>Usare SSIS per l'automazione

I flussi di lavoro per l'analisi scientifica dei dati sono altamente iterativi e implicano molte trasformazioni dei dati, tra cui ridimensionamento, aggregazioni, calcolo delle probabilità, ridenominazione e unione degli attributi. I data scientist sono abituati a eseguire molte di queste attività in R, Python o con un altro linguaggio, ma, per eseguire tali flussi di lavoro su dati aziendali, è necessaria la perfetta integrazione con strumenti e processi ETL.

Poiché [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consente di eseguire operazioni complesse in R tramite Transact-SQL e stored procedure, è possibile integrare le attività di analisi scientifica dei dati con i processi ETL esistenti. Anziché eseguire una serie di attività a elevato utilizzo di memoria, la preparazione dei dati può essere ottimizzata usando gli strumenti più efficienti, tra cui [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Di seguito sono riportate alcune idee per come è possibile automatizzare l'elaborazione dei dati e pipeline di modellazione in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Estrarre i dati in locale o cloud origini per creare dati di training 
+ Compilare ed eseguire i modelli R o Python come parte di un flusso di lavoro di integrazione di dati
+ Ripetere il training dei modelli a intervalli regolari (pianificata)
+ Caricare i risultati dallo script R o Python ad altre destinazioni, ad esempio Excel, Power BI, Oracle e Teradata, per citarne alcuni
+ Usare le attività SSIS per creare funzionalità di dati nel database SQL
+ Usare la diramazione condizionale per cambiare contesto di calcolo per i processi R e Python

## <a name="ssis-example"></a>Esempio SSIS

Nell'esempio seguente proviene da un post di blog MSDN ora dal ritirati creato da Jimmy Wong a questo URL: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

In questo esempio illustra come automatizzare le attività mediante SSIS. Si creano stored procedure con R incorporato usando SQL Server Management Studio e quindi eseguire le stored procedure dal [attività Esegui T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) in un pacchetto SSIS.

Per eseguire questo esempio, è necessario avere familiarità con Management Studio, SSIS, Progettazione SSIS, progettazione del pacchetto e T-SQL. Il pacchetto SSIS Usa tre [attività Esegui T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) che inserire i dati di training in una tabella, i dati del modello e valutare i dati per ottenere l'output delle stime.

### <a name="load-training-data"></a>Caricare i dati di training

Eseguire lo script seguente in SQL Server Management Studio per creare una tabella per archiviare i dati. È necessario creare e usare un database di prova per questo esercizio. 

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

Creare una stored procedure che carica i dati di training in frame di dati. Questo esempio Usa il set di dati Iris incorporato. 

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

In Progettazione SSIS, creare un [attività Esegui SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) che esegue la stored procedure è definita. Lo script per **SQLStatement** rimuove i dati esistenti, specifica i dati da inserire e quindi chiama la stored procedure per fornire i dati.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![Inserimento di dati](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "inserire i dati")

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

Creare una stored procedure che genera un modello lineare utilizzando [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod). Le librerie RevoScaleR e revoscalepy sono automaticamente disponibili nelle sessioni di R e Python in SQL Server in modo che non è necessario importare la libreria.

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

In Progettazione SSIS, creare un [attività Esegui SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) per eseguire il **generate_iris_rx_model** stored procedure. Il modello viene serializzato e salvato nella tabella ssis_iris_models. Lo script per **SQLStatement** è come segue:

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![Genera un modello lineare](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "genera un modello lineare")

Come un checkpoint, dopo aver completato questa attività, è possibile eseguire una query il ssis_iris_models che contiene un modello binario.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Stimare i risultati (punteggio) utilizzando il modello di "Training"

Ora che avete il codice che carica i dati di training e genera un modello, l'unico passaggio verso sinistra utilizza il modello per generare stime. 

A tale scopo, inserire lo script R nella query SQL per attivare i [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) funzione predefinita di R in ssis_iris_model. Chiamare una stored procedure **predict_species_length** esegue questa operazione.

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

In Progettazione SSIS, creare un [attività Esegui SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) che esegue il **predict_species_length** stored procedure per generare lunghezza del petalo stimato.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![Generare stime](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "generare stime")

### <a name="run-the-solution"></a>Eseguire la soluzione

In Progettazione SSIS, premere F5 per eseguire il pacchetto. Verrà visualizzato un risultato simile allo screenshot seguente.

![F5 per eseguire in modalità di debug](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 per eseguire in modalità di debug")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>Utilizzo di SSRS per le visualizzazioni

Anche se R è possibile creare grafici e visualizzazioni interessanti, non è ben integrata con origini dati esterne, vale a dire che ogni grafico deve essere prodotto singolarmente. Anche la condivisione può essere difficile.

Usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], è possibile eseguire operazioni complesse in R tramite [!INCLUDE[tsql](../../includes/tsql-md.md)] stored procedure, che possono essere facilmente usate da un'ampia gamma di strumenti, tra cui creazione di report aziendali [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e Power BI.

### <a name="ssrs-example"></a>Esempio SSRS

[R Graphics Device for Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/) (R Graphics Device per Microsoft Reporting Services - SSRS)

Questo progetto CodePlex fornisce il codice per la creazione di un elemento del report personalizzato che esegue il rendering dell'output grafico di R come un'immagine che può essere usata in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] i report.  Usando l'elemento del report personalizzato, è possibile:

+ Pubblicare i grafici e i tracciati creati usando R Graphics Device nei dashboard di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

+ Passare i parametri di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ai tracciati R

> [!NOTE]
> Per questo esempio, il codice che supporta R Graphics Device per Reporting Services deve essere installato nel server di Reporting Services, nonché in Visual Studio. Sono anche necessarie la compilazione e la configurazione manuali.

## <a name="next-steps"></a>Passaggi successivi

Gli esempi SSRS e SSIS in questo articolo illustrano due casi di esecuzione di stored procedure che contengono script R o Python incorporato. Il punto chiave è che è possibile rendere lo script R o Python disponibili per qualsiasi applicazione o lo strumento che può inviare una richiesta di esecuzione per una stored procedure. Un vantaggio aggiuntivo per SSIS è che è possibile creare pacchetti per automatizzano e pianificare l'ampia gamma di operazioni, ad esempio l'acquisizione dei dati, di pulizia, modifica e così via, R o Python funzionalità di analisi scientifica dei dati incluso nella catena di operazioni. Per altre informazioni e suggerimenti, vedere [codice rendere operativo R tramite stored procedure in SQL Server Machine Learning Services](operationalizing-your-r-code.md).