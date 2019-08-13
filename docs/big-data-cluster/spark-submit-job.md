---
title: Inviare processi Spark nei cluster Big Data di SQL Server in Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Inviare processi Spark nei cluster Big Data di SQL Server in Azure Data Studio.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6731a753c643512cd05dbc9d7b7de2c9a064576f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470684"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-azure-data-studio"></a>Inviare processi Spark nei cluster Big Data di SQL Server in Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Uno degli scenari chiave per i cluster Big Data di SQL Server è la possibilità di inviare processi Spark per la versione di anteprima di SQL Server 2019. La funzionalità di invio di processi Spark consente di inviare file Jar o Py locali con riferimenti ai cluster Big Data di SQL Server 2019. Consente inoltre di eseguire file Jar o Py che si trovano già nel file system HDFS. 

## <a name="prerequisites"></a>Prerequisites

- [Strumenti per Big Data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **kubectl**

- [Connettere Azure Data Studio al gateway HDFS/Spark del cluster Big Data](connect-to-big-data-cluster.md).

## <a name="open-spark-job-submission-dialog"></a>Aprire la finestra di dialogo di invio dei processi Spark

Ci sono diversi modi per aprire la finestra di dialogo di invio dei processi Spark. A tale scopo è possibile usare il dashboard, il menu di scelta rapida in Esplora oggetti e il riquadro comandi.

- Per aprire la finestra di dialogo di invio dei processi Spark, fare clic su **New Spark Job** (Nuovo processo Spark) nel dashboard.

    ![Menu per l'invio facendo clic nel dashboard](./media/submit-spark-job/new-spark-job.png)

- In alternativa, fare clic con il pulsante destro del mouse sul cluster in Esplora oggetti e scegliere **Submit Spark Job** (Invia processo Spark) dal menu di scelta rapida.

    ![Menu per l'invio facendo clic con il pulsante destro del mouse sul file](./media/submit-spark-job/submit-spark-job-1.png)


- Per aprire la finestra di dialogo di invio dei processi Spark con i campi relativi a Jar/Py prepopolati, fare clic con il pulsante destro del mouse su un file Jar/Py in Esplora oggetti e scegliere **Submit Spark Job** (Invia processo Spark) dal menu di scelta rapida.  

    ![Menu per l'invio facendo clic con il pulsante destro del mouse sul cluster](./media/submit-spark-job/submit-spark-job.png)

- Usare il comando **Submit Spark Job** (Invia processo Spark) dal riquadro comandi premendo **CTRL+MAIUSC+P** (in Windows) e **CMD+MAIUSC+P** (in Mac).

    ![Menu per l'invio nel riquadro comandi in Windows](./media/submit-spark-job/submit-spark-job-3.png)

    ![Menu per l'invio nel riquadro comandi in mac](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>Inviare un processo Spark 

La finestra di dialogo di invio dei processi Spark viene visualizzata come illustrato di seguito. Immettere il nome del processo, il percorso del file JAR/Py, la classe principale e gli altri campi. L'origine del file Jar/Py può essere locale o in HDFS. Se il processo Spark contiene file Py, file Jar di riferimento o file aggiuntivi, fare clic sulla scheda **ADVANCED** (AVANZATE) e immettere i percorsi di file corrispondenti. Fare clic su **Submit** (Invia) per inviare il processo Spark.

![Finestra di dialogo relativa a un nuovo processo Spark](./media/submit-spark-job/submit-spark-job-section.png)

![Finestra di dialogo relativa alle impostazioni avanzate](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>Monitorare l'invio del processo Spark

Una volta inviato il processo Spark, le informazioni sullo stato di invio e di esecuzione del processo vengono visualizzate nella cronologia attività a sinistra. I dettagli sullo stato di avanzamento e i log vengono visualizzati anche nella finestra **OUTPUT** nella parte inferiore.

- Quando il processo Spark è in corso, il pannello **Task History** (Cronologia attività) e la finestra **OUTPUT** vengono aggiornati in base allo stato di avanzamento.

    ![Visualizzare il processo Spark in corso](./media/submit-spark-job/monitor-spark-job-submission.png)

- Al termine del processo Spark, i collegamenti dell'interfaccia utente Spark e dell'interfaccia utente Yarn vengono visualizzati nella finestra **OUTPUT**. Fare clic sui collegamenti per altre informazioni.

    ![Collegamento del processo Spark nell'output](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server e sugli scenari correlati, vedere [Che cosa sono i cluster Big Data di SQL Server?](big-data-cluster-overview.md)