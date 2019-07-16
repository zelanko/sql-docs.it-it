---
title: Punteggio nativo tramite l'istruzione T-SQL stimare - servizi di SQL Server Machine Learning
description: Generare stime utilizzando la funzione di stima T-SQL, valutazione degli input dta rispetto a un modello con training preliminare scritte in R o Python in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 65a7954aa18f9e8dbdfd814a6b0d189683e4606f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962317"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Punteggio nativo usando la funzione di stima T-SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Utilizzi di assegnazione dei punteggi nativa [funzione T-SQL stimare](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) e le funzionalità native di C++ estensione in SQL Server 2017 per generare i valori di stima o *punteggi* per nuovi input di dati in tempo quasi reale. Questa metodologia offre la velocità di elaborazione possibili più veloce di previsione e stima dei carichi di lavoro, ma viene fornito con requisiti di piattaforma e della libreria: solo funzioni RevoScaleR e revoscalepy dispongono di implementazioni di C++.

Assegnazione dei punteggi nativa richiede la presenza di un modello già sottoposto a training. In SQL Server 2017 Windows o Linux o in Database SQL di Azure, è possibile chiamare la funzione PREDICT in Transact-SQL per richiamare sui nuovi dati forniti come parametro di input di assegnazione dei punteggi nativa. La funzione PREDICT restituisce i punteggi su dati di input che è fornire.

## <a name="how-native-scoring-works"></a>Funzionamento del punteggio nativo

Librerie native di assegnazione dei punteggi Usa native C++ da Microsoft in grado di leggere un modello già sottoposto a training, in precedenza archiviato in un particolare formato binario o salvato su disco come flusso di byte non elaborati e generare punteggi per nuovi input di dati fornito. Poiché il training del modello, pubblicati e archiviati, può essere utilizzato per la valutazione senza la necessità di chiamare l'interprete R o Python. Di conseguenza, viene ridotto l'overhead di più le interazioni di processo, molto più veloce stima delle prestazioni negli scenari di produzione dell'organizzazione.

Per usare l'assegnazione dei punteggi nativa, chiamare la funzione di stima T-SQL e passare gli input necessari seguenti:

+ Un modello compatibile basato su un algoritmo supportato.
+ Dati di input, in genere definiti come una query SQL.

La funzione restituisce stime per i dati di input, insieme a tutte le colonne di dati di origine che si desidera pass-through.

## <a name="prerequisites"></a>Prerequisiti

STIMA è disponibile in tutte le edizioni del motore di database di SQL Server 2017 e abilitato per impostazione predefinita, tra cui SQL Server 2017 Machine Learning Services in Windows, SQL Server 2017 (Windows), SQL Server 2017 (Linux) o Database SQL di Azure. È necessario non installare R, Python, o abilitare le funzionalità aggiuntive.

+ Il modello deve essere sottoposto a training in anticipo usando uno degli **rx** algoritmi elencati di seguito.

+ Serializzare il modello usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) per R, e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) per Python. Queste funzioni di serializzazione sono state ottimizzate per supportare l'assegnazione dei punteggi veloce.

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>Algoritmi supportati

+ modelli revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ Modelli di RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Se è necessario usare i modelli da MicrosoftML o microsoftml, usare [attribuzione dei punteggi in tempo reale con sp_rxPredict](real-time-scoring.md).

Tipi di modelli non supportati includono i tipi seguenti:

+ Modelli contenenti altre trasformazioni
+ I modelli usando la `rxGlm` o `rxNaiveBayes` algoritmi in RevoScaleR o revoscalepy equivalenti
+ Modelli di linguaggio PMML
+ Modelli creati con altre librerie open source o di terze parti

## <a name="example-predict-t-sql"></a>Esempio: PREDICT (T-SQL)

In questo esempio, si crea un modello e quindi chiama la funzione di stima in tempo reale da T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Passaggio 1. Preparare e salvare il modello

Eseguire il codice seguente per creare il database di esempio e le tabelle necessarie.

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

Usare l'istruzione seguente per popolare la tabella di dati con i dati di **iris** set di dati.

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

Il codice seguente crea un modello basato sul **iris** set di dati e lo salva nella tabella denominata **modelli**.

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
> Assicurarsi di usare la [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) funzione RevoScaleR per salvare il modello. R standard `serialize` funzione non è possibile generare il formato richiesto.

È possibile eseguire un'istruzione, ad esempio il comando seguente per visualizzare il modello archiviato in formato binario:

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Passaggio 2. Esecuzione di stima sul modello

L'istruzione di stima semplice seguente ottiene una classificazione dal modello di albero delle decisioni usando il **assegnazione dei punteggi nativa** (funzione). Consente di prevedere la specie di iris in base agli attributi forniti, lunghezza del petalo e larghezza.

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

Se viene visualizzato l'errore, "Errore durante l'esecuzione della funzione PREDICT. Modello è danneggiato o non valido", in genere significa che la query non ha restituito un modello. Controllare se il nome del modello aver digitato correttamente o se la tabella di modelli è vuota.

> [!NOTE]
> Poiché le colonne e valori restituiti da **PREDICT** possono variare in base al tipo di modello, è necessario definire lo schema dei dati restituiti tramite un **WITH** clausola.

## <a name="next-steps"></a>Passaggi successivi

Per una soluzione completa che include l'assegnazione dei punteggi nativa, vedere questi esempi dal team di sviluppo di SQL Server:

+ Distribuire lo script di Machine Learning: [Usando un modello Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Distribuire lo script di Machine Learning: [Usando un modello R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)