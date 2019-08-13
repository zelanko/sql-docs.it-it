---
title: Eseguire notebook in Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come eseguire notebook di Jupyter in Azure Data Studio con connessione a un cluster Big Data di SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 05/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 166964f97f5201d906ea2d1f6262b7a221eb2cba
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958293"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Come usare i notebook nella versione di anteprima di SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come avviare l'esperienza dei notebook nella versione più recente di [**Azure Data Studio** ](../azure-data-studio/download.md) e come iniziare a creare notebook personalizzati. Viene inoltre illustrato come scrivere notebook usando kernel diversi.

## <a name="connect-to-sql-server"></a>Connessione a SQL Server

È possibile connettersi al tipo di connessione Microsoft SQL Server in Azure Data Studio.
In Azure Data Studio è anche possibile premere F1, quindi fare clic su **Nuova connessione**  e connettersi a SQL Server.

![Informazioni di connessione](media/notebooks-guidance/connection-info.png)

## <a name="launch-notebooks"></a>Avviare i notebook

Ci sono diversi modi per avviare un nuovo notebook.

- Passare al **menu File**in Azure Data Studio e quindi fare clic su **New Notebook** (Nuovo notebook).

    ![Nuovo notebook](media/notebooks-guidance/file-new-notebook.png)

- Fare clic con il pulsante destro del mouse sulla connessione a **SQL Server** e quindi avviare **New Notebook** (Nuovo notebook).

    ![Nuovo notebook](media/notebooks-guidance/server-new-notebook.png)

- Aprire il riquadro comandi (**CTRL+MAIUSC+P**) e quindi digitare **New Notebook** (Nuovo notebook). Verrà aperto un nuovo file denominato `Notebook-1.ipynb`.

## <a name="supported-kernels-and-attach-to-context"></a>Contesto di collegamento e kernel supportati

L'installazione del notebook in Azure Data Studio supporta in modo nativo il kernel SQL. Se si è uno sviluppatore SQL e si vuole usare i notebook, si sceglierà questo kernel. 

Il kernel SQL può essere usato anche per la connessione alle istanze del server PostgreSQL. Se si è uno sviluppatore PostgreSQL e si vuole connettere i notebook al server PostgreSQL, scaricare l'[**estensione PostgreSQL**](../azure-data-studio/postgres-extension.md) nel marketplace delle estensioni di Azure Data Studio e quindi avviare **New Notebook** (Nuovo notebook) per aprire un'istanza di un notebook per la connessione al server PostgreSQL.

![Connessione a PostgreSQL](media/notebooks-guidance/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Kernel SQL

Nelle celle di codice all'interno del notebook, in modo analogo all'editor di query, è supportata l'esperienza di codifica SQL moderna, che semplifica le attività quotidiane con funzionalità predefinite come un editor SQL avanzato, IntelliSense e frammenti di codice predefiniti. I frammenti di codice consentono di generare la sintassi SQL appropriata per creare database, tabelle, viste, stored procedure e così via, nonché aggiornare gli oggetti di database esistenti. Usare i frammenti di codice per creare rapidamente copie del database a scopo di sviluppo o test e per generare ed eseguire script.

Fare clic su **Esegui** per eseguire ogni cella.

Kernel SQL per la connessione a un'istanza di SQL Server

![Kernel SQL](media/notebooks-guidance/intellisense-code-cell.png)

Risultati delle query

![Risultati query](media/notebooks-guidance/sql-cell-results.png)

Kernel SQL per la connessione a un'istanza del server PostgreSQL 

![Connessione a PostgreSQL](media/notebooks-guidance/pgsql-code-cell.png)

Risultati delle query

![Risultati query](media/notebooks-guidance/pgsql-cell-results.png)

Se si vuole aggiungere celle di testo al notebook esistente collegato al kernel SQL, fare clic sul comando **+Testo** sulla barra degli strumenti.

![Barra degli strumenti del notebook](media/notebooks-guidance/notebook-toolbar.png)

La cella passa alla modalità di modifica e sarà quindi possibile digitare la sintassi markdown e, nello stesso tempo, visualizzare l'anteprima

![Cella di markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Se si fa clic all'esterno della cella di testo, viene visualizzato il testo markdown.

![Testo markdown](media/notebooks-guidance/notebook-markdown-preview.png)


### <a name="configure-python-for-notebooks"></a>Configurare Python per i notebook

Quando si seleziona uno degli altri kernel oltre a SQL nell'elenco a discesa di kernel, viene visualizzata la finestra **Configure Python for Notebooks** (Configurare Python per i notebook). Le dipendenze dei notebook vengono installate in una posizione specifica, ma è possibile scegliere se impostare la posizione di installazione. L'installazione può richiedere del tempo ed è consigliabile non chiudere l'applicazione fino al completamento dell'installazione. Al termine dell'installazione, è possibile iniziare a scrivere il codice nel linguaggio supportato.

![Configurare Python](media/notebooks-guidance/configure-python.png)

Una volta completata l'installazione, verrà visualizzata una notifica nella cronologia attività, insieme alla posizione del server back-end Jupyter in esecuzione nel terminale di output.

![Back-end Jupyter](media/notebooks-guidance/jupyter-backend.png)

|Kernel|Descrizione
|:-----|:-----
| Kernel SQL | Scrivere codice SQL destinato al database relazionale.
|Kernel PySpark3 e PySpark| Scrivere codice Python usando il contesto di calcolo Spark del cluster.
|Kernel Spark|Scrivere codice Scala e R usando il contesto di calcolo Spark del cluster.
|Kernel Python|Scrivere codice Python per lo sviluppo locale.

`Attach to` fornisce il contesto per il collegamento del kernel. Se si usa il kernel SQL, è possibile scegliere come valore di `Attach to` qualsiasi istanza di SQL Server.

Se si usa il kernel Python3, il valore di `Attach to` è `localhost`. È possibile usare questo kernel per lo sviluppo Python locale.

Quando si è connessi a un cluster Big Data di SQL Server 2019, il valore predefinito di `Attach to` è l'endpoint del cluster e consente di inviare codice Python, Scala e R usando il contesto di calcolo Spark del cluster.

### <a name="code-cells-and-markdown-cells"></a>Celle di codice e celle di markdown

Aggiungere una nuova cella di codice facendo clic sul comando **+Codice** sulla barra degli strumenti.

Aggiungere una nuova cella di testo facendo clic sul comando **+Testo** sulla barra degli strumenti.

![Barra degli strumenti del notebook](media/notebooks-guidance/notebook-toolbar.png)

La cella passa alla modalità di modifica e sarà quindi possibile digitare la sintassi markdown e, nello stesso tempo, visualizzare l'anteprima

![Cella di markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Se si fa clic all'esterno della cella di testo, viene visualizzato il testo markdown.

![Testo markdown](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>Notebook attendibili e non attendibili

I notebook aperti in Azure Data Studio sono **attendibili** per impostazione predefinita.

Se si apre un notebook da un'altra origine, verrà aperto in modalità **non attendibile** e sarà quindi possibile impostarlo come **attendibile**.

### <a name="run-cells"></a>Eseguire le celle
Se si vuole eseguire tutte le celle nel notebook, fare clic sul pulsante **Run Cells** (Esegui celle) sulla barra degli strumenti.

![Testo markdown](media/notebooks-guidance/run-cell.png)


### <a name="clear-results"></a>Cancella risultati

Se si vuole cancellare i risultati di tutte le celle eseguite nel notebook, fare clic sul pulsante **Cancella risultati** sulla barra degli strumenti.

![Testo markdown](media/notebooks-guidance/clear-results.png)

### <a name="save"></a>Salvare

Per salvare il notebook, eseguire una delle operazioni seguenti.

- Premere CTRL+S
- Fare clic su **File** > **Salva**
- Fare clic su **File** > **Salva con nome**.
- Fare clic su **File** > **Salva tutto** 
- Nel riquadro comandi immettere **File: Save** (File: Salva) 

### <a name="pyspark3pyspark-kernel"></a>Kernel Pyspark3/PySpark

Scegliere `PySpark Kernel` e nella cella digitare il codice seguente.

Fare clic su **Esegui**.

L'applicazione Spark viene avviata e restituisce l'output seguente:

![Applicazione Spark](media/notebooks-guidance/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel Spark | Linguaggio Scala

Scegliere `Spark|Scala Kernel` e nella cella digitare il codice seguente.

![Spark in Scala](media/notebooks-guidance/spark-scala.png)

È anche possibile visualizzare le opzioni della cella facendo clic sull'icona delle opzioni visualizzata sotto.

![Opzioni della cella](media/notebooks-guidance/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel Spark | Linguaggio R

Scegliere Spark | R nell'elenco a discesa per i kernel. Nella cella digitare o incollare il codice. Fare clic su **Esegui** per visualizzare l'output seguente.

![Spark in R](media/notebooks-guidance/spark-r.png)

### <a name="local-python-kernel"></a>Kernel Python locale

Scegliere il kernel Python locale e nella cella digitare il codice seguente.

![Python locale](media/notebooks-guidance/local-python.png)

## <a name="manage-packages"></a>Gestire i pacchetti

Uno degli aspetti ottimizzati per lo sviluppo Python locale è la possibilità di installare i pacchetti che potrebbero essere necessari ai clienti per i loro scenari. Per impostazione predefinita, vengono inclusi pacchetti comuni come `pandas`, `numpy` e così via, ma se si prevede che un pacchetto non sia incluso, è possibile scrivere il codice seguente nella cella del notebook: 

```python
import <package-name>
```

Quando si esegue questo comando, viene restituito `Module not found`. Se il pacchetto esiste, l'errore non verrà visualizzato.

Se viene restituito un errore `Module not Found`, fare clic su **Gestisci pacchetti** per avviare il terminale. È ora possibile installare i pacchetti localmente. Usare i comandi seguenti per installare i pacchetti:

```bash
./pip install <package-name>
```

   > [!Tip]
   > In Mac seguire le istruzioni nella finestra del terminale per installare i pacchetti. 

Una volta installato il pacchetto, dovrebbe essere possibile passare alla cella del notebook e digitare il comando seguente:

```python
import <package-name>
```

Per disinstallare un pacchetto, usare il comando seguente nel terminale:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come usare un notebook esistente, vedere [Come gestire i notebook in Azure Data Studio](notebooks-how-to-manage.md).