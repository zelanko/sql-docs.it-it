---
title: Eseguire un notebook di esempio | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Questa esercitazione illustra come caricare l'esecuzione di un notebook Spark di esempio in un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4acb5c2306064da29d3537fc881dbfc3d312ad2f
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844235"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-big-data-cluster"></a>Esercitazione: Eseguire un notebook di esempio in un cluster Big Data di SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa esercitazione illustra come caricare ed eseguire un notebook di Azure Data Studio in un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Questa operazione consente infatti ai data scientist e ai data engineer di eseguire codice Python, R o Scala sul cluster.

> [!TIP]
> Se si preferisce, è possibile scaricare ed eseguire uno script per i comandi descritti in questa esercitazione. Per istruzioni, vedere gli [esempi di Spark](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark) in GitHub.

## <a id="prereqs"></a> Prerequisiti

- [Strumenti per Big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
- [Caricare dati di esempio nel cluster Big Data](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>Scaricare il file del notebook di esempio

Usare le istruzioni seguenti per caricare il file del notebook di esempio **spark-sql.ipynb** in Azure Data Studio.

1. Aprire un prompt dei comandi Bash (Linux) o Windows PowerShell.

1. Passare alla directory in cui si vuole scaricare il file del notebook di esempio.

1. Eseguire il comando **curl** seguente per scaricare il file del notebook da GitHub:

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-loading/transform-csv-files.ipynb' -o transform-csv-files.ipynb
   ```

## <a name="open-the-notebook"></a>Aprire il notebook

Questa procedura illustra come aprire il file del notebook in Azure Data Studio:

1. In Azure Data Studio connettersi all'istanza master del cluster Big Data. Per altre informazioni, vedere [Connettersi a un cluster Big Data](connect-to-big-data-cluster.md).

1. Fare doppio clic sulla connessione del gateway HDFS/Spark nella finestra **Server**. Selezionare quindi **Open Notebook** (Apri notebook).

   ![Apri notebook](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. Attendere che il **kernel** e il contesto di destinazione **(Connetti a**) siano popolati. Impostare il **kernel** su **PySpark3** e l'opzione **Connetti a** sull'indirizzo IP dell'endpoint del cluster Big Data.

   ![Imposta Kernel e Connetti a](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>Eseguire le celle del notebook

È possibile eseguire ogni cella del notebook premendo il pulsante di riproduzione a sinistra della cella. I risultati verranno visualizzati nel notebook al termine dell'esecuzione della cella.

![Eseguire la cella del notebook](media/tutorial-notebook-spark/run-notebook-cell.png)

Eseguire tutte le celle del notebook di esempio in successione. Per altre informazioni sull'uso dei notebook con [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere le risorse seguenti:

- [Come usare i notebook in SQL Server](notebooks-guidance.md)
- [Come gestire i notebook in Azure Data Studio](notebooks-how-to-manage.md)

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sui notebook:
> [!div class="nextstepaction"]
> [Altre informazioni sui notebook](notebooks-guidance.md)
