---
title: Assegnazione di punteggi nativi usando l'istruzione T-SQL PREDICT
description: Generare stime usando la funzione T-SQL PREDICT, assegnando un punteggio agli input DTA rispetto a un modello con training preliminare scritto in R o Python su SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: b148bd1ca51a7121ae043e2b616100e295c008aa
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344764"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Assegnazione di punteggi nativi mediante la funzione PREDICT T-SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Il Punteggio nativo usa la [funzione Predict T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) e C++ le funzionalità di estensione native di SQL Server 2017 per generare valori di stima o *punteggi* per i nuovi input di dati in tempo quasi reale. Questa metodologia offre la velocità di elaborazione più rapida possibile per i carichi di lavoro di previsione e di stima, ma include i requisiti della piattaforma e della libreria: solo C++ le funzioni di RevoScaleR e revoscalepy hanno implementazioni.

Per il Punteggio nativo è necessario disporre di un modello già sottoposto a training. In SQL Server 2017 Windows o Linux o nel database SQL di Azure è possibile chiamare la funzione PREDICT in Transact-SQL per richiamare il Punteggio nativo sui nuovi dati forniti come parametro di input. La funzione PREDICT restituisce i punteggi sugli input dei dati forniti.

## <a name="how-native-scoring-works"></a>Funzionamento del Punteggio nativo

Il Punteggio nativo USA C++ le librerie native di Microsoft in grado di leggere un modello già sottoposto a training, archiviato in precedenza in un formato binario speciale o salvato su disco come flusso di byte non elaborati e genera punteggi per i nuovi input di dati forniti. Poiché il modello viene sottoposto a training, pubblicato e archiviato, può essere usato per l'assegnazione dei punteggi senza dover chiamare l'interprete R o Python. Di conseguenza, l'overhead di più interazioni di processo viene ridotto, ottenendo prestazioni di stima molto più veloci negli scenari di produzione aziendali.

Per usare il Punteggio nativo, chiamare la funzione PREDICT T-SQL e passare gli input obbligatori seguenti:

+ Modello compatibile basato su un algoritmo supportato.
+ Dati di input, in genere definiti come query SQL.

La funzione restituisce le stime per i dati di input, insieme alle colonne di dati di origine che si desidera passare.

## <a name="prerequisites"></a>Prerequisiti

PREDICT è disponibile in tutte le edizioni del motore di database SQL Server 2017 e abilitato per impostazione predefinita, incluso SQL Server 2017 Machine Learning Services in Windows, SQL Server 2017 (Windows), SQL Server 2017 (Linux) o il database SQL di Azure. Non è necessario installare R, Python o abilitare funzionalità aggiuntive.

+ Il training del modello deve essere eseguito in anticipo utilizzando uno degli algoritmi **RX** supportati elencati di seguito.

+ Serializzare il modello usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) per R e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) per Python. Queste funzioni di serializzazione sono state ottimizzate per supportare il Punteggio rapido.

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>Algoritmi supportati

+ modelli revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ Modelli RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Se è necessario usare modelli di MicrosoftML o MicrosoftML, usare il [punteggio in tempo reale con sp_rxPredict](real-time-scoring.md).

I tipi di modello non supportati includono i tipi seguenti:

+ Modelli contenenti altre trasformazioni
+ Modelli che usano `rxGlm` gli `rxNaiveBayes` algoritmi o negli equivalenti RevoScaleR o revoscalepy
+ Modelli PMML
+ Modelli creati con altre librerie open source o di terze parti

## <a name="example-predict-t-sql"></a>Esempio: PREDICT (T-SQL)

In questo esempio viene creato un modello e quindi viene chiamata la funzione di stima in tempo reale da T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Passaggio 1. Preparare e salvare il modello

Eseguire il codice seguente per creare il database di esempio e le tabelle obbligatorie.

```sql
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

Usare l'istruzione seguente per popolare la tabella dati con i dati del set di dati **Iris** .

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

A questo punto, creare una tabella per archiviare i modelli.

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

Il codice seguente crea un modello basato sul set di dati **Iris** e lo salva nella tabella denominata **Models**.

```sql
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> Assicurarsi di usare la funzione [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) di RevoScaleR per salvare il modello. La funzione R `serialize` standard non è in grado di generare il formato richiesto.

Per visualizzare il modello archiviato in formato binario, è possibile eseguire un'istruzione come la seguente:

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Passaggio 2. Eseguire PREDICT sul modello

Tramite la semplice istruzione PREDICT seguente viene ottenuta una classificazione dal modello di albero delle decisioni utilizzando la funzione di assegnazione dei **punteggi nativa** . Consente di stimare le specie Iris in base agli attributi forniti, alla lunghezza e alla larghezza dei petali.

```sql
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

Se viene generato l'errore, "si è verificato un errore durante l'esecuzione della funzione PREDICT. Il modello è danneggiato o non è valido ", in genere significa che la query non ha restituito un modello. Controllare se il nome del modello è stato digitato correttamente o se la tabella Models è vuota.

> [!NOTE]
> Poiché le colonne e i valori restituiti da **Predict** possono variare in base al tipo di modello, è necessario definire lo schema dei dati restituiti utilizzando una clausola **with** .

## <a name="next-steps"></a>Passaggi successivi

Per una soluzione completa che includa il Punteggio nativo, vedere questi esempi del team di sviluppo di SQL Server:

+ Distribuire lo script ML: [Uso di un modello Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Distribuire lo script ML: [Uso di un modello R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)