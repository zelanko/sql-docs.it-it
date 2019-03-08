---
title: Modelli di Machine Learning Train/Create con Spark
titleSuffix: SQL Server 2019 big data clusters
description: Usare PySpark per eseguire il training e creare modelli di machine learning con Spark nei cluster di big data di SQL Server (anteprima).
author: lgongmsft
ms.author: shivprashant
ms.manager: craigg
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1ef8f66d220561407c0bcafedde8a402f871924a
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578111"
---
# <a name="train-and-create-machine-learning-models-with-spark"></a>Eseguire il training e creare modelli di machine learning con Spark

Spark in cluster di big data di SQL Server Abilita intelligenza artificiale e machine learning. L'esempio illustra la modalità di training di un modello di machine learning tramite Python in Spark (PySpark) usando i dati archiviati in HDFS. 

L'esempio è una Guida dettagliata con i frammenti di codice che può essere utilizzato da un Notebook di Studio dei dati di Azure e un unico passaggio eseguire ogni cella alla volta. Per altre informazioni su come connettersi con Spark dal notebook, vedere [qui](notebooks-guidance.md)

Nell'esempio:

1. Iniziare con **comprendere i dati e stima desiderato**
2. **Caricare dati in HDFS e preparare i dati** per la creazione del modello
3. **Selezionare le funzionalità da usare**
4. **Divisione dei dati come set di training e test**
5. Raccolto un **pipeline ml e compilare un modello**
6. Usare il modello creato per **fare delle stime**
7. Come passaggio finale **rendere persistente il modello creato in un secondo momento usare**.

Apprendimento E2E prevede diversi passaggi aggiuntivi, ad esempio, esplorazione dei dati, analisi in componenti funzionalità selezione e un'entità, selezione del modello. Molti di questi passaggi vengono ignorati in questo caso per motivi di brevità.

## <a name="step-1---understanding-the-data-and-prediction-desired"></a>Passaggio 1: comprendere i dati e stima desiderato

Questo esempio Usa dati adult census income [qui]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv ). In `AdultCensusIncome.csv`, ogni riga rappresenta una fascia di reddito e altre caratteristiche, ad esempio l'età, ore-alla-settimana, education, occupazione e così via per un determinato contenuto per adulti. Compilare un modello che è possibile prevedere se l'intervallo di reddito. Il modello accetta età e ore-alla-settimana come funzioni e stimare se il reddito è > 50 K o < 50 K. 

## <a name="step-2---upload-the-data-to-hdfs-and-basic-explorations-on-data"></a>Passaggio 2: caricare i dati in HDFS ed esplorazioni di base sui dati
Da Azure Data Studio connettersi al gateway HDFS/Spark e creare una directory denominata `spark_ml` in HDFS. Scaricare [AdultCensusIncome.csv]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv ) al computer locale e il caricamento in HDFS. Caricare `AdultCensusIncome.csv` nella cartella creata.


A questo punto, scrivere codice. È possibile copiare il codice seguente e incollarlo in singole celle del notebook in Azure Data Studio. 

Il codice seguente legge il file CSV del dataframe di Spark. In seguito che conta il numero di righe e colonne e visualizzare i dati caricati.

```python
datafile = "/spark_ml/AdultCensusIncome.csv"

#Read the data to a spark data frame.
data_all = spark.read.format('csv').options(header='true', inferSchema='true', ignoreLeadingWhiteSpace='true', ignoreTrailingWhiteSpace='true').load(datafile)
print("Number of rows: {},  Number of coulumns : {}".format(data_all.count(), len(data_all.columns)))

#Replace "-" with "_" in column names
columns_new = [col.replace("-", "_") for col in data_all.columns]
data_all = data_all.toDF(*columns_new)

#Print Schema and show top 5 row
data_all.printSchema() 
data_all.show(5)
```

## <a name="step-3---select-features-to-use"></a>Passaggio 3: selezionare le funzionalità da usare

In questo passaggio, usare il comando seguente due termini
1. `Label`    -Fa riferimento al valore da stimare. Ciò viene rappresentato come una colonna nei dati.  
2. `Features` -Fa riferimento alle caratteristiche di dati per la stima. Noto anche come una certa `predictors` 

In questo esempio `Label`, è il **reddito** colonna. Per semplicità, scegliere **età** e **hours_per_week** come `Features`. In realtà le funzionalità vengono scelti applicando alcune tecniche di correlazione per comprendere ciò che caratterizzano meglio l'etichetta di stima.

```python
# Choose feature columns and the label column.
label = "income"
xvars = ["age", "hours_per_week"] #all numeric

print("label = {}".format(label))
print("features = {}".format(xvars))

select_cols = xvars
select_cols.append(label)
data = data_all.select(select_cols)

```

## <a name="step-4---split-as-training-and-test-set"></a>Passaggio 4: suddividere come set di training e test

Usare il 75% delle righe per addestrare il modello e il resto del 25% per valutare il modello. Inoltre, rendere persistente il training e set di dati in un archivio HDFS di test. Il passaggio non è necessaria, ma visualizzati per illustrare il salvataggio e il caricamento con formato ORC. Altri formati, ad esempio, `Parquet` può anche essere usato.

Registrare questo passaggio che dovrebbe essere creata con il nome AdultCensusIncomeTrain e AdultCensusIncomeTest due directory

```python

# Split data into train and test.
train, test = data.randomSplit([0.75, 0.25], seed=123)

print("train ({}, {})".format(train.count(), len(train.columns)))
print("test ({}, {})".format(test.count(), len(test.columns)))

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train.write.mode('overwrite').orc(train_data_path)
test.write.mode('overwrite').orc(test_data_path)
print("train and test datasets saved to {} and {}".format(train_data_path, test_data_path))

```

## <a name="step-5---put-together-a-pipeline-and-build-a-model"></a>Passaggio 5: mettere insieme una pipeline e compilare un modello
[Pipeline di Spark ML](https://spark.apache.org/docs/2.3.1/ml-pipeline.html) Consenti a tutti i passaggi di sequenza come un flusso di lavoro e rendono più semplice provare diversi algoritmi e i relativi parametri. Il codice seguente crea prima di tutto le fasi e quindi inserisce insieme queste fasi in pipeline di Machine Learning.  LogisticRegression viene utilizzato per creare il modello.

```python
from pyspark.ml import Pipeline, PipelineModel
from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler
from pyspark.ml.classification import LogisticRegression

reg = 0.1
print("Using LogisticRegression model with Regularization Rate of {}.".format(reg))

# create a new Logistic Regression model.
lr = LogisticRegression(regParam=reg)

dtypes = dict(train.dtypes)
dtypes.pop(label)

si_xvars = []
ohe_xvars = []
featureCols = []
for idx,key in enumerate(dtypes):
    if dtypes[key] == "string":
        featureCol = "-".join([key, "encoded"])
        featureCols.append(featureCol)
        
        tmpCol = "-".join([key, "tmp"])
        si_xvars.append(StringIndexer(inputCol=key, outputCol=tmpCol, handleInvalid="skip")) #, handleInvalid="keep"
        ohe_xvars.append(OneHotEncoder(inputCol=tmpCol, outputCol=featureCol))
    else:
        featureCols.append(key)

# string-index the label column into a column named "label"
si_label = StringIndexer(inputCol=label, outputCol='label')

# assemble the encoded feature columns in to a column named "features"
assembler = VectorAssembler(inputCols=featureCols, outputCol="features")

```

A questo punto, raccolto la pipeline. 

```python
# put together the pipeline
stages = []
stages.extend(si_xvars)
stages.extend(ohe_xvars)
stages.append(si_label)
stages.append(assembler)
stages.append(lr)
pipe = Pipeline(stages=stages)
print("Pipeline Created")

```

Ora che la pipeline viene creata, usarlo per il training del modello.

```python
# train the model
model = pipe.fit(train)
print("Model Trained")
print("Model is ", model)
print("Model Stages", model.stages)

```

## <a name="step-6---predict-using-the-model-and-evaluate-the-model-accuracy"></a>Passaggio 6: eseguire la stima utilizzando il modello e valutare l'accuratezza del modello
Il codice seguente usa il set di dati di test per stimare il risultato tramite il modello creato nel passaggio precedente. Misura di accuratezza del modello con il `areaUnderROC` e `areaUnderPR` metrica.

```python
from pyspark.ml.evaluation import BinaryClassificationEvaluator
# make prediction
pred = model.transform(test)

# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```


## <a name="step-7---persist-the-models-to-hdfs"></a>Passaggio 7: salvare in modo permanente i modelli in HDFS
Infine, salvare in modo permanente il modello in HDFS per un uso successivo. Post di questo passaggio il modello creato vengono salvati come /spark_ml/AdultCensus.mml

```python
##NOTE: by default the model is saved to and loaded from path

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

model.write().overwrite().save(model_fs)
print("saved model to {}".format(model_fs))

# load the model file (from dbfs)
model2 = PipelineModel.load(model_fs)
assert str(model2) == str(model)
print("loaded model from {}".format(model_fs))
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come iniziare a usare i notebook di PySpark, vedere [come usare i notebook](notebooks-guidance.md).