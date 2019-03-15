---
title: Creare flussi di lavoro SSIS e SSRS con R - servizi di SQL Server Machine Learning
description: Scenari di integrazione di combinazione di servizi di SQL Server Machine Learning e R Services, Reporting Services (SSRS) e SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 76ddf3e3fdb43fea6bb8fd224f8199cda4134b64
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976301"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Creare flussi di lavoro SSIS e SSRS con R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come usare stored procedure in due importanti caratteristiche di SQL Server, SQL Server Integration Services (SSIS) e SQL Server Reporting Services SSRS, in modo che combina i dati relazionali, le funzioni di analisi scientifica dei dati dalle librerie di Microsoft R, e funzionalità di Business Intelligence per le trasformazioni di dati coordinato e la visualizzazione. Informazioni su quali funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] si prestano a una soluzione di analisi scientifica dei dati. Questo articolo inoltre ricorda che il codice e i dati in SQL Server, ad esempio il codice R incorporato nelle stored procedure, viene utilizzata con facilità in visualizzazioni disponibili in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

## <a name="bring-compute-power-to-the-data"></a>Potenza di calcolo ai dati

È stato un obiettivo chiave nella progettazione dell'integrazione di R e Python con SQL Server per portare analitica vicino ai dati. Ciò offre diversi vantaggi:

+ Sicurezza dei dati. Offrendo l'avvicinamento di R per l'origine dei dati consente di evitare lo spostamento dei dati inutili e non sicuri.
+ Velocità. I database sono ottimizzati per le operazioni basate su set. Le innovazioni recenti per i database, ad esempio le tabelle in memoria rendono i riepiloghi e aggregazioni fulmine e sono la soluzione ideale per l'analisi scientifica dei dati.
+ Facilità di integrazione e distribuzione. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è il punto centrale di operazioni per molte altre attività di gestione dati e applicazioni. Utilizzando i dati che si trovano nel database o warehouse per reporting, assicurarsi che i dati usati da soluzioni di machine learning siano coerenti e aggiornati. 
+ Efficienza tra cloud e locali. Invece di elaborare i dati in R, è possibile usare le pipeline di dati aziendali, inclusi [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e Azure Data Factory. La creazione di report con i risultati o l'analisi è semplice con Power BI o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

Con la giusta combinazione di SQL e R per le diverse attività di elaborazione e analisi di dati, sia i data scientist che gli sviluppatori possono essere più produttivi.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-data-transformation-and-automation"></a>Usare SSIS per l'automazione e la trasformazione dei dati

I flussi di lavoro per l'analisi scientifica dei dati sono altamente iterativi e implicano molte trasformazioni dei dati, tra cui ridimensionamento, aggregazioni, calcolo delle probabilità, ridenominazione e unione degli attributi. I data scientist sono abituati a eseguire molte di queste attività in R, Python o con un altro linguaggio, ma, per eseguire tali flussi di lavoro su dati aziendali, è necessaria la perfetta integrazione con strumenti e processi ETL.

Poiché [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consente di eseguire operazioni complesse in R tramite Transact-SQL e stored procedure, è possibile integrare attività specifiche di R con i processi ETL esistenti senza dover intervenire per adattare lo sviluppo. Anziché eseguire una serie di attività a elevato utilizzo di memoria in R, la preparazione dei dati può essere ottimizzata usando gli strumenti più efficienti, tra cui [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Di seguito sono riportate alcune idee per come è possibile automatizzare l'elaborazione dei dati e pipeline di modellazione in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Usare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] attività per creare le funzionalità di dati necessari nel database SQL
+ Usare la diramazione condizionale per cambiare il contesto di calcolo per i processi R
+ Eseguire processi R che generano i propri dati nel database e condividere dati con le applicazioni
+ Quando si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], caricare lo script R salvato in una variabile di testo ed eseguirlo in SQL Server

## <a name="ssis-example"></a>Esempio SSIS

Nell'esempio seguente proviene da un post di blog MSDN ora dal ritirati creato da Jimmy Wong a questo URL: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`.

In questo esempio illustra come automatizzare le attività mediante SSIS. Si creano stored procedure con R incorporato usando SQL Server Management Studio e quindi eseguire le stored procedure dal [attività Esegui T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) in un pacchetto SSIS.

Per eseguire questo esempio, è necessario avere familiarità con Management Studio, SSIS, Progettazione SSIS, progettazione del pacchetto e T-SQL. Il pacchetto SSIS Usa tre [attività Esegui T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) che inserire i dati di training in una tabella, i dati del modello e valutare i dati per ottenere l'output delle stime.

### <a name="create-tables"></a>Creare tabelle

Eseguire lo script seguente in SQL Server Management Studio per creare alcune tabelle: uno per archiviare i dati e l'altro per archiviare un modello. Il ruolo della tabella ssis_iris è come dati di training in uno scenario di operazionalizzazione. 

```T-SQL
Use irissql
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

### <a name="create-a-stored-procedure-that-loads-training-data"></a>Creare una stored procedure che carica i dati di training

Questo script crea una stored procedure che carica Iris in un frame di dati usando il set di dati R predefinito.

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

### <a name="define-an-execute-sql-task-that-refreshes-the-model"></a>Definire un'attività Esegui SQL che viene aggiornato il modello

In Progettazione SSIS, creare un [attività Esegui SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task).

![Inserimento di dati](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "inserire i dati")

Lo script per SQLStatement è come indicato di seguito. Lo script rimuove i dati esistenti e quindi ricaricato nuovi dati usando il **load_iris** stored procedure creata nel passaggio precedente.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

### <a name="create-a-stored-procedure-that-generates-a-model"></a>Creare una stored procedure che genera un modello

Questa stored procedure è codice che crea un modello lineare utilizzando [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod). Le librerie RevoScaleR e revoscalepy vengono caricate automaticamente nelle sessioni di R e Python in SQL Server.

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

### <a name="define-an-execute-sql-task-that-runs-the-model-generation-stored-procedure"></a>Definire un'attività Esegui SQL che esegue la stored procedure generazione del modello

In questo passaggio [attività Esegui SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) esegue il **generate_iris_rx_model** stored procedure, la creazione del modello e averlo inserito nella tabella ssis_iris_models.

![Genera un modello lineare](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "genera un modello lineare")

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

Dopo aver completato questa attività, è possibile eseguire una query il ssis_iris_models che contiene un modello binario.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Stimare i risultati (punteggio) utilizzando il modello di "Training"

In questo semplice esempio, il presupposto è che ssis_iris_model è un modello con training. Poiché lo scopo di un modello con training per generare stime, siamo pronti per eseguire una stima utilizzando lo. 

A tale scopo, inserire lo script R nella query SQL per attivare i [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) funzione predefinita di R in ssis_iris_model. Chiamare una stored procedure in SQL Server **predict_species_length** esegue questa operazione.

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

### <a name="define-an-execute-sql-task-that-predicts-outcomes"></a>Definire un'attività Esegui SQL che consente di stimare i risultati

Usando [attività Esegui SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task), eseguire il **predict_species_length** stored procedure per generare lunghezza del petalo stimato.

![Generare stime](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "generare stime")

```T-SQL
exec predict_species_length 'rxLinMod';
```

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