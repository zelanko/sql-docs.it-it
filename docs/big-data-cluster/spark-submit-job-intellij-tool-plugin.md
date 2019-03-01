---
title: Eseguire processi Spark in Azure Toolkit for IntelliJ nel Cluster di Big Data di SQL Server
titleSuffix: SQL Server Big Data Clusters
description: Inviare processi Spark nei cluster Big Data SQL Server in Azure Toolkit for IntelliJ.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.openlocfilehash: 06ce1d325caa0835381fd6f9ecd5428d2bbb6f66
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018477"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-intellij"></a>Inviare processi Spark nei cluster Big Data SQL Server in IntelliJ

Uno degli scenari chiave per i cluster di SQL Server Big Data è la possibilità di inviare processi Spark. La funzionalità di invio dei processi di Spark consente di inviare un file con estensione Jar o Py locali con i riferimenti a cluster di Big Data di SQL Server. Consente inoltre di eseguire un file con estensione Jar o Py, che sono già presenti nel file system HDFS. 

## <a name="prerequisites"></a>Prerequisiti

- Cluster di Big Data SQL Server.
- Oracle Java Development Kit. È possibile installarlo dal [sito Web Oracle](https://aka.ms/azure-jdks).
- IntelliJ IDEA. È possibile installarlo dal [sito Web di JetBrains](https://www.jetbrains.com/idea/download/).
- Azure Toolkit for IntelliJ estensione. Per istruzioni sull'installazione, vedere [installare Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation).

## <a name="link-sql-server-big-data-cluster"></a>Cluster di Big Data di collegamento SQL Server
1. Aprire lo strumento di IntelliJ IDEA.

2. Se si usa un certificato autofirmato, disabilitare la convalida dei certificati SSL dal **degli strumenti** dal menu **Azure**, **convalidare certificato SSL del Cluster Spark**, quindi **Disabilitare**.

    ![collegare i Cluster di Big Data di SQL Server - Disabilitare SSL](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-disableSSL.png)

3. Aprire Azure Explorer **View** dal menu **strumento Windows**e quindi selezionare **Azure Explorer**.
4. Fare clic con il pulsante destro sul **Cluster di Big Data di SQL Server**, selezionare **collegamento SQL Server Big Data Cluster**. Immettere il **Server**, **nome utente**, e **Password**, quindi fare clic su **OK**.

    ![collegare il cluster di Big Data - finestra di dialogo](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-dialog.png)

5. Quando viene visualizzata finestra di dialogo certificato del server non attendibile, fare clic su **Accept**. È possibile gestire il certificato in un secondo momento, vedere [certificati Server](https://www.jetbrains.com/help/idea/settings-tools-server-certificates.html).

6. Il cluster collegato sono elencati sotto **Cluster di Big Data di SQL Server**. È possibile monitorare il processo spark aprendo l'interfaccia utente di Yarn e l'interfaccia utente della cronologia di spark, si potrebbe anche Scollega, pulsante destro del mouse facendo clic sul cluster.

    ![collegare il cluster di Big Data - menu di scelta rapida](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-contextmenu.png)

## <a name="create-a-spark-scala-application-from-hdinsight-template"></a>Creare un'applicazione Spark Scala dal modello di HDInsight

1. Avviare IntelliJ IDEA e creare un progetto. Nel **nuovo progetto** finestra di dialogo, seguire i passaggi seguenti: 

   a. Selezionare **Spark di Azure o HDInsight** > **progetto con esempi (Scala) di Spark**.

   b. Nel **dello strumento di compilazione** selezionare uno dei modi seguenti, in base alle proprie esigenze:

      * **Maven**, per il supporto di procedura guidata di creazione del progetto Scala
      * **SBT**, per gestire le dipendenze e la compilazione per il progetto Scala

    ![La finestra di dialogo Nuovo progetto](./media/spark-submit-job-intellij-tool-plugin/create-hdi-scala-app.png)

2. Selezionare **Avanti**.

3. La procedura guidata di creazione del progetto Scala rileva automaticamente se è installato il plug-in Scala. Selezionare **Installa**.

   ![Controllo di plug-in scala](./media/spark-submit-job-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Per scaricare il plug-in Scala, selezionare **OK**. Seguire le istruzioni per riavviare IntelliJ. 

   ![Finestra di dialogo di installazione di plug-in Scala](./media/spark-submit-job-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. Nel **nuovo progetto** finestra, eseguire le operazioni seguenti:  

    ![Selezione di Spark SDK](./media/spark-submit-job-intellij-tool-plugin/hdi-new-project.png)

   a. Immettere un nome e percorso.

   b. Nel **SDK di progetto** elenco a discesa, seleziona **Java 1.8** per il cluster Spark 2.x oppure **Java 1.7** per il cluster Spark 1.x.

   c. Nel **versione di Spark** elenco a discesa, la creazione guidata progetto Scala integra la versione corretta per Spark SDK e Scala SDK. Se la versione del cluster Spark è precedente alla 2.0, selezionare **Spark 1.x**. In caso contrario, selezionare **Spark 2.x**. Questo esempio viene usato **Spark 2.0.2 (Scala 2.11.8)**.

6. Selezionare **Fine**.

7. Il progetto Spark crea automaticamente un elemento. Per visualizzare l'elemento, eseguire le operazioni seguenti:

   a. Nel **File** dal menu **struttura del progetto**.

   b. Nel **struttura del progetto** finestra di dialogo **artefatti** per visualizzare l'elemento predefinito creato. È anche possibile creare un elemento personalizzato selezionando il segno più (**+**).

      ![Informazioni sull'elemento nella finestra di dialogo](./media/spark-submit-job-intellij-tool-plugin/default-artifact.png)
      

## <a name="submit-application-to-sql-server-big-data-cluster"></a>Inviare l'applicazione al Cluster di Big Data di SQL Server
Dopo il collegamento di un Cluster di dati Big data di SQL Server, è possibile inviare l'applicazione al suo interno.

1. Impostare la configurazione nel **Run/Debug Configurations** finestra, fare clic su + ->**Apache Spark in SQL Server**, selezionare tab **eseguire in remoto in Cluster**, impostare i parametri come seguire, quindi fare clic su OK.

    ![Console interattiva Aggiungi voce di configurazione](./media/spark-submit-job-intellij-tool-plugin/interactive-console-add-config-entry.png)

    ![collegare il cluster di Big Data - config](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-config.png)

    * Per la **Spark cluster (solo Linux)**, selezionare il cluster in cui si desidera eseguire l'applicazione.

    * Selezionare un elemento nel progetto IntelliJ oppure selezionarne uno dal disco rigido.

    * **Nome della classe principale** campo: Il valore predefinito è la classe principale dal file selezionato. È possibile modificare la classe selezionando i puntini di sospensione (**...** ) e scegliendo un'altra classe.   

    * **Le configurazioni del processo** campo:  I valori predefiniti sono impostati come immagine illustrato in precedenza. È possibile modificare il valore o aggiungere una nuova chiave/valore per l'invio del processo. Per ulteriori informazioni: [Apache Livy, l'API REST](http://livy.incubator.apache.org./docs/latest/rest-api.html)

      ![Il significato di configurazione di Spark Submission dialogo finestra processo](./media/spark-submit-job-intellij-tool-plugin/submit-job-configurations.png)

    * **Argomenti della riga di comando** campo: È possibile immettere i valori di argomenti suddivisi per lo spazio per la classe principale, se necessario.

    * **Riferimento file con estensione jar** e **i file di cui viene fatto riferimento** campi: È possibile immettere i percorsi per i file e il file JAR di cui si fa riferimento se presente. Per ulteriori informazioni: [Configurazione di Apache Spark](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) 

      ![I file jar di Spark Submission della finestra di dialogo vale a dire](./media/spark-submit-job-intellij-tool-plugin/jar-files-meaning.png)

       > [!NOTE]  
       > Per caricare i file JAR di cui viene fatto riferimento e i file di cui viene fatto riferimento, vedere: [Come caricare risorse al cluster](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-storage-explorer)
                         
    * **Caricare percorso**: È possibile indicare la posizione di archiviazione per l'invio di risorse di progetto con estensione Jar o Scala. Esistono diversi tipi di archiviazione supportati: **Usare la sessione interattiva di Spark per caricare** e **WebHDFS Usa per caricare**
    
2. Fare clic su **SparkJobRun** per inviare il progetto per il cluster selezionato. Il **remoto processo Spark nel Cluster** scheda viene visualizzato lo stato di esecuzione del processo nella parte inferiore. È possibile arrestare l'applicazione facendo clic sul pulsante rosso.  

    ![cluster di Big Data Link - esecuzione](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-run.png)

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sul Cluster di Big Data di SQL Server e gli scenari correlati, vedere [quali sono i cluster di SQL Server 2019 dei big data](big-data-cluster-overview.md)?
