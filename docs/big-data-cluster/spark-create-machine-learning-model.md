---
title: Creare ed esportare modelli con MLeap di apprendimento automatico Spark
titleSuffix: SQL Server big data clusters
description: Usare PySpark per eseguire il training e creare modelli di machine learning con Spark nei cluster di big data di SQL Server (anteprima). Esportare con MLeap e quindi assegnare un punteggio del modello con Java in SQL Server.
author: lgongmsft
ms.author: lgong
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aa4c31eca725e8e662937259f078cf00a3441915
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727382"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>Creare, esportare e assegnare un punteggio modelli di machine learning Spark nei cluster di SQL Server i big Data

L'esempio seguente viene illustrato come creare un modello con [Spark ML](https://spark.apache.org/docs/latest/ml-guide.html), esportare il modello per [MLeap](http://mleap-docs.combust.ml/)e assegnare un punteggio in SQL Server con il modello relativo [estensione del linguaggio Java](../language-extensions/language-extensions-overview.md). Questa operazione viene eseguita nel contesto di un cluster di big data di SQL Server 2019.

Il diagramma seguente illustra le operazioni eseguite in questo esempio:

![Eseguire il training di esportazione di punteggio con spark](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>Prerequisiti

Tutti i file per questo esempio si trovano nel [ https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml ](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml).

Per eseguire l'esempio, è necessario disporre anche i prerequisiti seguenti:

- Oggetto [cluster di big data di SQL Server](deploy-get-started.md)

- [Strumenti dei big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Training del modello con Spark ML

Per questo esempio, dati di censimento (**AdultCensusIncome.csv**) consente di compilare un modello di pipeline di Spark ML.

1. Usare la [mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh) file da scaricare il set di dati da internet e inserirlo in HDFS nel cluster di big data di SQL Server. In questo modo è accessibile tramite Spark.

1. Scaricare quindi il notebook di esempio [train_score_export_ml_models_with_spark.ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb). Dalla riga di comando di PowerShell o bash, eseguire il comando seguente per scaricare il notebook:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   Questo notebook contiene celle con i comandi necessari per questa sezione dell'esempio.

1. Aprire il notebook in Azure Data Studio ed eseguire ogni blocco di codice. Per altre informazioni sull'uso di notebook, vedere [come usare i notebook in fase di anteprima di SQL Server 2019](notebooks-guidance.md).

I dati vengono innanzitutto leggere in Spark e suddiviso in set di training e set di dati di testing. Il codice quindi esegue il training di un modello di pipeline con i dati di training. Infine, viene esportato il modello in un bundle MLeap.

> [!TIP]
> È anche possibile esaminare o eseguire il codice Python associato a questi passaggi di fuori il notebook nel [mleap_sql_test/mleap_pyspark.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py) file.

## <a name="model-scoring-with-sql-server"></a>Modello di assegnazione dei punteggi con SQL Server

Ora che è il modello di pipeline di Spark ML in una serializzazione common [bundle MLeap](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) formato, è possibile assegnare un punteggio del modello in Java senza la presenza di Spark. 

Questo esempio Usa la [estensione del linguaggio Java](../language-extensions/language-extensions-overview.md) in SQL Server. Per assegnare un punteggio il modello in SQL Server, è necessario innanzitutto creare un'applicazione Java che è possibile caricare il modello in Java e assegnare un punteggio. È possibile trovare il codice di esempio per l'applicazione Java nel [cartella mssql-mleap-app](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app).

Dopo aver compilato il codice di esempio, è possibile utilizzare Transact-SQL per chiamare l'applicazione Java e assegnare un punteggio del modello con una tabella di database. Può essere visualizzato in tre [mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py) file di origine.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster di big data, vedere [come distribuire i dati di grandi dimensioni di SQL Server di cluster in Kubernetes](deployment-guidance.md)
