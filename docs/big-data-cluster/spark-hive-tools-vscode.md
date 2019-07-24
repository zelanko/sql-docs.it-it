---
title: Eseguire processi Spark con Spark & gli strumenti hive per VS Code nel cluster Big Data SQL Server
titleSuffix: SQL Server big data clusters
description: Inviare un processo Spark con Spark & hive Tools for Visual Studio Code in SQL Server cluster Big Data.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4458666792d7f4629b4e1820e98e2dbb9901c2b6
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425981"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>Inviare processi Spark in SQL Server cluster Big Data in Visual Studio Code

Informazioni su come usare Spark & hive Tools per Visual Studio Code per creare e inviare script di PySpark per Apache Spark. verrà prima di tutto descritto come installare gli strumenti di Spark & hive in Visual Studio Code e quindi verrà illustrato come inviare i processi a Spark.  

Spark & gli strumenti hive possono essere installati su piattaforme supportate da Visual Studio Code, tra cui Windows, Linux e macOS. Di seguito sono elencati i prerequisiti specifici per le diverse piattaforme.


## <a name="prerequisites"></a>Prerequisiti

Per completare le procedure descritte in questo articolo, sono necessari gli elementi seguenti:

- Un cluster SQL Server Big Data. Vedere [SQL Server Big Data cluster](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions).
- [Visual Studio Code](https://code.visualstudio.com/).
- [Mono](https://www.mono-project.com/docs/getting-started/install/). Mono è necessario solo per Linux e macOS.
- [Configurare l'ambiente PySpark Interactive per Visual Studio Code](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment).
- Una directory locale denominata **HDexample**.  Questo articolo usa **C:\HD\HDexample**.

## <a name="install-spark--hive-tools"></a>Installare Spark & gli strumenti hive

Dopo aver completato i prerequisiti, è possibile installare Spark & hive Tools for Visual Studio Code.  Completare i passaggi seguenti per installare Spark & hive Tools:

1. Aprire Visual Studio Code.

2. Dalla barra dei menu passare a **Visualizza** > **Estensioni**.

3. Nella casella di ricerca immettere **Spark & hive**.

4. Selezionare **Spark & hive Tools** nei risultati della ricerca e quindi selezionare **Install (installa**).  

   ![Installare l'estensione](./media/spark-hive-tools-vscode/extension.png)

5. Ricarica quando necessario.

## <a name="open-work-folder"></a>Apri cartella di lavoro

Completare i passaggi seguenti per aprire una cartella di lavoro e creare un file in Visual Studio Code:

1. Dalla barra dei menu passare a **File** > **Apri cartella** > **C:\HD\HDexample** e quindi selezionare il pulsante **Seleziona cartella**. La cartella viene visualizzata nella vista di **Explorer** a sinistra.

2. Dalla vista di **Explorer** selezionare la cartella, **HDexample**, e quindi l'icona **Nuovo file** accanto alla cartella di lavoro.

   ![Nuovo file](./media/spark-hive-tools-vscode/new-file.png)

3. Denominare il nuovo file `.py` con l'estensione di file (script Spark).  Questo esempio usa **HelloWorld.py**.
4. Copiare e incollare il codice seguente nel file di script:
   ```python
    import sys
    from operator import add
    from pyspark.sql import SparkSession, Row
    
    spark = SparkSession\
        .builder\
        .appName("PythonWordCount")\
        .getOrCreate()
    
    data = [Row(col1='pyspark and spark', col2=1), Row(col1='pyspark', col2=2), Row(col1='spark vs hadoop', col2=2), Row(col1='spark', col2=2), Row(col1='hadoop', col2=2)]
    df = spark.createDataFrame(data)
    lines = df.rdd.map(lambda r: r[0])

    counters = lines.flatMap(lambda x: x.split(' ')) \
        .map(lambda x: (x, 1)) \
        .reduceByKey(add)
    
    output = counters.collect()
    sortedCollection = sorted(output, key = lambda r: r[1], reverse = True)
    
    for (word, count) in sortedCollection:
        print("%s: %i" % (word, count))
   ```

## <a name="link-a-sql-server-big-data-cluster"></a>Collegare un cluster SQL Server Big Data

Prima di poter inviare script ai cluster da Visual Studio Code, è necessario collegare un cluster Big Data SQL Server.

1. Dalla barra dei menu passare a **Visualizza** > **riquadro comandi**e immettere **Spark/hive: Link a Cluster**.

   ![comando di collegamento di un cluster](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. Selezionare il tipo di cluster collegato **SQL Server Big Data**.

3. Immettere SQL Server endpoint Big Data.

4. Immettere SQL Server nome utente del cluster di Big Data.

5. Immettere la password per l'amministratore utente.

6. Impostare il nome visualizzato del cluster (facoltativo).

7. Elencare i cluster, rivedere la visualizzazione dell' **output** per la verifica.

## <a name="list-clusters"></a>Elencare cluster

1. Dalla barra dei menu passare a **Visualizza** > **riquadro comandi**e immettere **Spark/hive: List Cluster**.

2. Esaminare la vista **OUTPUT**.  La vista mostrerà i cluster collegati.

    ![Impostare una configurazione del cluster predefinito](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>Impostare il cluster predefinito

1. Riaprire la cartella **HDexample** creata [in precedenza](#open-work-folder), se è stata chiusa.  

2. Selezionare il file **HelloWorld.py** creato in [precedenza](#open-work-folder) e verrà aperto nell'editor di script.

3. Collegare un cluster se non è ancora stato fatto.

4. Fare clic con il pulsante destro del mouse sull' **editor di script e selezionare Spark/hive: Set Default Cluster**.   

5. Selezionare un cluster come predefinito per il file di script corrente. Gli strumenti aggiornano automaticamente il file di configurazione **.VSCode\settings.json**. 

   ![Impostare la configurazione del cluster predefinito](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>Inviare query PySpark interattive

È possibile inviare query PySpark interattive attenendosi alla procedura seguente:

1. Riaprire la cartella **HDexample** creata [in precedenza](#open-work-folder), se è stata chiusa.  

2. Selezionare il file **HelloWorld.py** creato in [precedenza](#open-work-folder) e verrà aperto nell'editor di script.

3. Collegare un cluster se non è ancora stato fatto.

4. Scegliere tutto il codice e fare clic con il pulsante destro del mouse **sull'editor di script e selezionare Spark: PySpark Interactive** per inviare la query oppure usare la combinazione di tasti **CTRL+ALT+I**.

   ![menu di scelta rapida interattivo pyspark](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. Se non è stato specificato un cluster predefinito, selezionare il cluster. Dopo alcuni istanti, i risultati di **Python Interactive** vengono visualizzati in una nuova scheda. Gli strumenti consentono anche di inviare un blocco di codice, anziché l'intero file di script, usando il menu di scelta rapida. 

   ![finestra interattiva di Python interattiva di pyspark](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. Immettere **"%% info"** , quindi premere **MAIUSC + INVIO** per visualizzare le informazioni sul processo. (Facoltativo)

   ![Visualizza informazioni sui processi](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > Quando l' **estensione Python abilitata** è deselezionata nelle impostazioni (l'impostazione predefinita è selezionata), i risultati dell'interazione pyspark inviati utilizzeranno la finestra precedente.
   >
   > ![estensione Python interattiva di pyspark disabilitata](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>Inviare un processo batch PySpark

1. Riaprire la cartella **HDexample** creata [in precedenza](#open-work-folder), se è stata chiusa.  

2. Selezionare il file **HelloWorld.py** creato in [precedenza](#open-work-folder) e verrà aperto nell'editor di script.

3. Collegare un cluster se non è ancora stato fatto.

4. Fare clic con il pulsante destro del mouse sull'editor **di script e quindi selezionare Spark: PySpark Batch**, oppure usare la combinazione di tasti **Ctrl + Alt + H**. 

5. Se non è stato specificato un cluster predefinito, selezionare il cluster. Dopo aver inviato un processo Python, i log di invio vengono visualizzati nella finestra **OUTPUT** in Visual Studio Code. Vengono visualizzati anche l'**URL dell'interfaccia utente di Spark** e l'**URL dell'interfaccia utente di Yarn**. È possibile aprire l'URL in un Web browser per tenere traccia dello stato del processo.

   ![Risultato dell'invio del processo Python](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Configurazione di Apache Livy

La configurazione di [Apache Livy](https://livy.incubator.apache.org/) è supportata ed è possibile impostarla in **.VSCode\settings.json** nella cartella dell'area di lavoro. Attualmente, la configurazione di Livio supporta solo script Python. Per altre informazioni, vedere [Livy LEGGIMI](https://github.com/cloudera/livy/blob/master/README.rst ).

### <a id="triggerlivyconf"></a>**Come attivare la configurazione di Livio**

#### <a name="method-1"></a>Metodo 1

1. Dalla barra dei menu passare a **File** > **Preferenze** > **Impostazioni**.  
2. Nella casella di testo **Impostazioni ricerca** immettere **HDInsight Job Sumission: Livy Conf** (Invio processo HDInsight: Conf. Livy).  
3. Selezionare **Edit in settings.json** (Modifica in settings.json) per il risultato della ricerca pertinente.

#### <a name="method-2"></a>Metodo 2

Inviare un file. si noti `.vscode` che la cartella viene aggiunta automaticamente alla cartella di lavoro. È possibile trovare la configurazione di Livio facendo `.vscode\settings.json`clic su.

+ Impostazioni di progetto:

    ![Configurazione di Livy](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>Per le impostazioni **driverMomory** e **executorMomry**, impostare il valore unità, ad esempio 1 g o 1024 m. 

### <a name="supported-livy-configurations"></a>Configurazioni di Livio supportate

#### <a name="post-batches"></a>POST/Batches

**Corpo della richiesta**

| name | description | type |
| :- | :- | :- |
| file | File contenente l'applicazione da eseguire | percorso (obbligatorio) |
| proxyUser | Utente da rappresentare durante l'esecuzione del processo | string |
| className | Classe principale Java/Spark dell'applicazione | string |
| args | Argomenti della riga di comando per l'applicazione | elenco di stringhe |
| jars | file JAR da usare in questa sessione | Elenco di stringhe |
| pyFiles | File di Python da usare in questa sessione | Elenco di stringhe |
| files | file da usare in questa sessione | Elenco di stringhe |
| driverMemory | Quantità di memoria da usare per il processo del driver | string |
| driverCores | Numero di core da usare per il processo del driver | int |
| executorMemory | Quantità di memoria da usare per ogni processo executor | string |
| executorCores | Numero di core da usare per ogni executor | int |
| numExecutors | Numero di executor da avviare per questa sessione | int |
| archives | Archivi da usare in questa sessione | Elenco di stringhe |
| queue | Nome della coda a cui YARN viene effettuato l'invio | string |
| name | Nome della sessione | string |
| conf | Proprietà di configurazione di Spark | Mapping della chiave = val |

#### <a name="response-body"></a>Contenuto risposta

Oggetto batch creato.

| name | description | type |
| :- | :- | :- |
| id | ID sessione | int |
| appId | ID applicazione della sessione | string |
| appInfo | Informazioni dettagliate sull'applicazione | Mapping della chiave = val |
| log | Righe di log | elenco di stringhe |
| state | Stato batch | string |

>[!NOTE]
>La configurazione di Livio assegnata viene visualizzata nel riquadro di output quando si invia lo script.

## <a name="additional-features"></a>Funzionalità aggiuntive

Spark & hive per Visual Studio Code supporta le funzionalità seguenti:

- **Completamento automatico di IntelliSense**. Vengono visualizzati suggerimenti per parole chiave, metodi, variabili e così via. Icone diverse rappresentano vari tipi di oggetti.

    ![Spark & gli strumenti hive per Visual Studio Code tipi di oggetti IntelliSense](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **Indicatore di errore di IntelliSense**. Il servizio di linguaggio sottolinea gli errori di modifica nello script Hive.     
- **Evidenziazioni della sintassi**. Il servizio di linguaggio usa colori diversi per differenziare variabili, parole chiave, tipi di dati, funzioni e così via. 

    ![Highlights Spark & hive Tools for Visual Studio Code Syntax](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>Scollegare il cluster

1. Dalla barra dei menu passare a **Visualizza** > **riquadro comandi...** , quindi immettere **Spark/hive: Unlink a Cluster**.  

2. Selezionare il cluster da scollegare.  

3. Esaminare la vista **OUTPUT** per verificare i dati.  

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sul cluster SQL Server Big Data e sugli scenari correlati, vedere [SQL Server Big Data Clusters](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions).
