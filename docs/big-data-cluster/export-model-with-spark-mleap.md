---
title: Esportare modelli di Machine Learning di Spark con MLeap
titleSuffix: SQL Server big data clusters
description: Informazioni su come esportare i modelli con MLeap di apprendimento automatico Spark.
author: lgongmsft
ms.author: lgong
ms.reviewer: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: e831345e82310b51e5802af70c91b0d397e66c90
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822451"
---
# <a name="export-spark-machine-learning-models-with-mleap"></a>Esportare i modelli con MLeap di apprendimento automatico Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Uno scenario di apprendimento automatico tipico prevede training del modello in Spark e assegnazione dei punteggi di fuori di Spark. Esporta modelli in un formato portabile in modo che può essere usato all'esterno di Spark. [MLeap](https://github.com/combust/mleap) è una tale formato del modello di scambio. La possibilità di Spark pipeline di machine learning e i modelli da esportare come formati di portatili e usato in qualsiasi sistema basati su JVM con il `Mleap` runtime.

Questa Guida dimostra come è possibile esportare i modelli spark usando Mleap. I passaggi sono riepilogati di seguito e dettagliati con il codice nella sezione seguente.

1. Iniziare creando un modello di Spark. Per questo utilizzo **del modello di Training e creazione di machine learning con Spark [qui.](train-and-create-machinelearning-models-with-spark.md)**
2. Come passaggio successivo verrà **importare i dati training\test e il modello**
3. **Esportare il modello come `Mleap` bundle**. Questo bundle esportato ora utilizzabile per assegnare un punteggio di fuori di spark.
4. Per convalidare, verrà importato il `Mleap` bundle back nuovamente e usarlo per assegnare un punteggio in Spark.

## <a name="step-1---start-by-creating-a-spark-model"></a>Passaggio 1: Start creando un modello di Spark
Eseguire [del modello di Training e creazione di machine learning con Spark](train-and-create-machinelearning-models-with-spark.md) per creare set di training/test e il modello e richiedere l'archiviazione HDFS. Il modello deve essere esportato come `AdultCensus.mml` sotto il `spark_ml` directory.

## <a name="step-2---import-the-trainingtest-data-and-the-model"></a>Passaggio 2: importare i dati training\test e il modello

Passaggio 1 creato il `AdultCensus.mml`, ovvero un modello di spark. 

In questo passaggio, importare il modello di spark.

```python
import mleap.pyspark
from mleap.pyspark.spark_support import SimpleSparkSerializer
from pyspark.ml import PipelineModel

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

print("load pyspark model from hbfs")
model = PipelineModel.load(model_fs)
print("Model is " , model)
print("Model stages", model.stages)
```

## <a name="step-3---export-the-model-as-mleap-bundle"></a>Passaggio 3: esportare il modello come `Mleap` bundle

Esportare il modello di Spark come un portatile `Mleap` modellare e archiviare i dati nell'archivio locale. Pubblicare un post in questo passaggio, il modello è disponibile in un formato portabile `Mleap` formattare e può essere usato all'esterno di Spark.

```python
import os

#Get the train and test datasets

# Write the train and test data sets to intermediate storage

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train = spark.read.orc(train_data_path)
test = spark.read.orc(test_data_path)

print("train: ({}, {})".format(train.count(), len(train.columns)))
train.printSchema()

print("test: ({}, {})".format(test.count(), len(test.columns)))
test.printSchema()

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# remove an old model file, if needed.
try:
    os.remove(model_file)
except OSError:
    pass

model_file_path = "jar:file:{}".format(model_file)
model.serializeToBundle(model_file_path, model.transform(train))

```

Rendere persistente il `Mleap` bundle da locale a hdfs

```python
print("persist the mleap bundle from local to hdfs")
from subprocess import Popen, PIPE
proc = Popen(["hadoop", "fs", "-put", "-f", model_file, os.path.join("/spark_ml", model_name_export)], stdout=PIPE, stderr=PIPE)
s_output, s_err = proc.communicate()
if(s_err):
    print("Error when storing to HDFS")
```

## <a name="step-3---validate-by-importing-the-mleap-bundle-and-scoring-in-spark"></a>Passaggio 3: convalidare l'importazione di `Mleap` bundle e Scoring in Spark
Nel passaggio 2, è stato già esportato il modello da un portatile `Mleap` formato che può essere usato all'esterno di Spark. In questo passaggio è stato possibile importare il `Mleap` serializzato in Spark e usarlo in Spark al punteggio nel set di test.
   
```python
model_deserialized = PipelineModel.deserializeFromBundle(model_file_path)
print("The deserialized model is ", model_deserialized)
print("The deserialized model stages are", model_deserialized.stages)

from pyspark.ml.evaluation import BinaryClassificationEvaluator

# make prediction
pred = model_deserialized.transform(test)


# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Results of using the model score test set")
print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```

## <a name="references"></a>Riferimenti

* [Introduzione a notebook di PySpark](notebooks-guidance.md)
* [Set di training e la creazione di modelli di machine learning con Spark](train-and-create-machinelearning-models-with-spark.md)
