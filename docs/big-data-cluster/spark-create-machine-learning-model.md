---
title: Creazione ed esportazione di modelli di Machine Learning Spark con MLeap
titleSuffix: SQL Server big data clusters
description: Usare PySpark per eseguire il training e creare modelli di Machine Learning con Spark in SQL Server cluster di Big Data (anteprima). Esportare con MLeap e quindi assegnare un punteggio al modello con Java in SQL Server.
author: lgongmsft
ms.author: lgong
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aa4c31eca725e8e662937259f078cf00a3441915
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2019
ms.locfileid: "67727382"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>Creare, esportare e assegnare punteggi ai modelli di Machine Learning Spark nei cluster SQL Server Big Data

Nell'esempio seguente viene illustrato come compilare un modello con [Spark ml](https://spark.apache.org/docs/latest/ml-guide.html), esportare il modello in [MLeap](http://mleap-docs.combust.ml/)e assegnare un punteggio al modello in SQL Server con l' [estensione del linguaggio Java](../language-extensions/language-extensions-overview.md). Questa operazione viene eseguita nel contesto di un cluster SQL Server 2019 Big Data.

Il diagramma seguente illustra le operazioni eseguite in questo esempio:

![Eseguire il training del Punteggio Export con Spark](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>Prerequisiti

Tutti i file per questo esempio si trovano [https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml)in.

Per eseguire l'esempio, è necessario disporre anche dei seguenti prerequisiti:

- Un [cluster SQL Server Big Data](deploy-get-started.md)

- [Strumenti per Big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Training del modello con Spark ML

Per questo esempio, il Census Data (**AdultCensusIncome. csv**) viene usato per compilare un modello di pipeline di Spark ml.

1. Usare il file [mleap_sql_test/Setup. sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh) per scaricare il set di dati da Internet e inserirlo in HDFS nel cluster SQL Server Big Data. Questo consente l'accesso a Spark.

1. Scaricare quindi il notebook di esempio [train_score_export_ml_models_with_spark. ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb). Da una riga di comando di PowerShell o bash, eseguire il comando seguente per scaricare il notebook:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   Questo notebook contiene le celle con i comandi necessari per questa sezione dell'esempio.

1. Aprire il notebook in Azure Data Studio ed eseguire ogni blocco di codice. Per ulteriori informazioni sull'utilizzo dei notebook, vedere la pagina relativa [alla modalità di utilizzo dei notebook in SQL Server 2019 Preview](notebooks-guidance.md).

I dati vengono prima letti in Spark e suddivisi in set di dati di training e di testing. Il codice addestra quindi un modello di pipeline con i dati di training. Infine, esporta il modello in un bundle MLeap.

> [!TIP]
> È anche possibile esaminare o eseguire il codice Python associato a questi passaggi all'esterno del notebook nel file [mleap_sql_test/mleap_pyspark. py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py) .

## <a name="model-scoring-with-sql-server"></a>Assegnazione di punteggi al modello con SQL Server

Ora che il modello di pipeline di Spark ML si trova in un formato [MLeap bundle](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) di serializzazione comune, è possibile assegnare un punteggio al modello in Java senza la presenza di Spark. 

In questo esempio viene utilizzata l' [estensione del linguaggio Java](../language-extensions/language-extensions-overview.md) in SQL Server. Per assegnare un punteggio al modello in SQL Server, è prima di tutto necessario compilare un'applicazione Java in grado di caricare il modello in Java e assegnargli un punteggio. È possibile trovare il codice di esempio per questa applicazione Java nella [cartella MSSQL-mleap-app](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app).

Dopo aver compilato l'esempio, è possibile usare Transact-SQL per chiamare l'applicazione Java e assegnare un punteggio al modello con una tabella di database. Questo può essere visualizzato nel file di origine [mleap_sql_test/mleap_sql_tests. py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py) .

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster di Big Data, vedere [How to deploy SQL Server Big Data Clusters on Kubernetes](deployment-guidance.md)
