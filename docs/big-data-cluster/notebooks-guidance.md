---
title: Esegui i notebook in Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Questo articolo illustra come eseguire i notebook di Jupyter in Azure Data Studio connesso a un cluster di big data di SQL Server 2019.
author: achatter
ms.author: jroth
manager: craigg
ms.date: 05/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 6cc491ee2592ad68ff334e0c1b7287b5754220dc
ms.sourcegitcommit: c1cc44c3b5ad030d8726be8819594341fc3d9f91
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65462054"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Come usare i notebook in fase di anteprima di SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come avviare l'esperienza Notebook nella versione più recente di [**Studio di Azure Data**](../azure-data-studio/download.md) e su come iniziare a creare i tuoi notebook. Viene inoltre illustrato come scrivere i notebook con kernel diversi.

## <a name="connect-to-sql-server"></a>Connessione a SQL Server

È possibile connettersi al tipo di connessione di Microsoft SQL Server in Azure Data Studio.
In Azure Data Studio, è possibile anche premere F1 e fare clic su **nuova connessione** e connettersi a SQL Server.

![Informazioni di connessione](media/notebooks-guidance/connection-info.png)

## <a name="launch-notebooks"></a>Avviare i notebook

Esistono diversi modi per avviare un nuovo notebook.

- Andare alla **dal Menu File** in Azure Data Studio e quindi fare clic su **nuovo Notebook**.

    ![Nuovo notebook](media/notebooks-guidance/file-new-notebook.png)

- Fare clic con il pulsante destro sul **SQL Server** connessione e quindi avviare **nuovo Notebook**.

    ![Nuovo notebook](media/notebooks-guidance/server-new-notebook.png)

- Aprire il riquadro comandi (**Ctrl + MAIUSC + P**)) e quindi digitare **nuovo Notebook**. Un nuovo file denominato `Notebook-1.ipynb` apre.

## <a name="supported-kernels-and-attach-to-context"></a>Supportati i kernel e associare al contesto

L'installazione di Notebook in Azure Data Studio supporta in modo nativo SQL Kernel. Se si sono uno sviluppatore SQL e si desidera usare i notebook e quindi il risultato sarà la prescelta Kernel. 

Il Kernel SQL è anche utilizzabile per connettersi alle istanze del server PostgreSQL. Se si è uno sviluppatore di PostgreSQL e si vuole connettere il notebook per il PostgreSQL Server, quindi scaricare il [ **estensioni di PostgreSQL** ](../azure-data-studio/postgres-extension.md) nel marketplace delle estensioni di Studio dei dati di Azure e quindi avvio veloce **nuovo Notebook** per aprire un'istanza di notebook per la connessione al server PostgreSQL.

![Connessione di PostgreSQL](media/notebooks-guidance/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Kernel SQL

Nelle celle di codice del blocco appunti, simile all'editor di query, Supportiamo SQL moderna esperienza che agevola le attività quotidiane con funzionalità incorporate, ad esempio un editor SQL avanzato, IntelliSense e frammenti di codice incorporato di codifica. Frammenti di codice consentono di generare la sintassi SQL appropriata per creare database, tabelle, viste, stored procedure e così via e per aggiornare gli oggetti di database esistenti. Usare frammenti di codice per creare rapidamente copie del database per lo sviluppo o a scopo di test e di generare ed eseguire gli script.

Fare clic su **eseguire** da eseguire ogni cella.

Kernel di SQL per connettersi all'istanza di SQL Server

![Kernel SQL](media/notebooks-guidance/intellisense-code-cell.png)

Risultati delle query

![Risultati query](media/notebooks-guidance/sql-cell-results.png)

Kernel di SQL per connettersi all'istanza del PostgreSQL Server 

![Connessione di PostgreSQL](media/notebooks-guidance/pgsql-code-cell.png)

Risultati delle query

![Risultati query](media/notebooks-guidance/pgsql-cell-results.png)

Se si desidera aggiungere celle testo a quella esistente Notebook collegati al Kernel di SQL, fare clic sui **+ testo** comando sulla barra degli strumenti.

![Barra degli strumenti del blocco appunti](media/notebooks-guidance/notebook-toolbar.png)

Le modifiche di cella per la modalità di modifica e a questo punto digitare markdown e si vedrà l'anteprima allo stesso tempo

![Cella di markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Facendo clic all'esterno della cella di testo visualizzerà il testo di markdown.

![Testo di markdown](media/notebooks-guidance/notebook-markdown-preview.png)


### <a name="configure-python-for-notebooks"></a>Configurare Python per i notebook

Quando si seleziona una delle altre kernel oltre a SQL dall'elenco a discesa kernel, viene richiesto di **configurare Python per notebook**. Le dipendenze di Notebook installate in un percorso specificato, ma è possibile decidere se si desidera impostare il percorso di installazione. Questa installazione può richiedere molto tempo e si consiglia di non chiudere l'applicazione fino al completamento dell'installazione. Una volta completata l'installazione, è possibile iniziare a scrivere codice nel linguaggio supportato.

![Configurare python](media/notebooks-guidance/configure-python.png)

Dopo l'installazione viene completata, si noterà una notifica nella cronologia di attività con il percorso del server back-end Jupyter in esecuzione nel terminale di Output.

![Back-end di Jupyter](media/notebooks-guidance/jupyter-backend.png)

|Kernel|Descrizione
|:-----|:-----
| Kernel SQL | Scrivere codice SQL destinate ai database relazionale.
|PySpark3 e il Kernel PySpark| Scrivere il codice Python con Spark compute dal cluster.
|Kernel Spark|Scrivere il codice R e Scala con Spark compute dal cluster.
|Kernel Python|Scrivere il codice Python per lo sviluppo locale.

`Attach to` fornisce il contesto per il Kernel da collegare. Se si usa SQL Kernel, è quindi possibile `Attach to` qualsiasi delle istanze di SQL Server.

Se si usa il Kernel Python3 il `Attach to` è `localhost`. È possibile usare questo kernel per lo sviluppo Python locale.

Quando si è connessi al cluster di big data 2019 di SQL Server, il valore predefinito `Attach to` tale punto di fine del cluster e consente di inviare il codice Python, Scala e R usando le risorse di calcolo di Spark del cluster.

### <a name="code-cells-and-markdown-cells"></a>Le celle di codice e le celle di Markdown

Aggiungere una nuova cella di codice facendo il **+ Code** comando sulla barra degli strumenti.

Aggiungere una nuova cella di testo facendo il **+ testo** comando sulla barra degli strumenti.

![Barra degli strumenti del blocco appunti](media/notebooks-guidance/notebook-toolbar.png)

Le modifiche di cella per la modalità di modifica e a questo punto digitare markdown e si vedrà l'anteprima allo stesso tempo

![Cella di markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Facendo clic all'esterno della cella di testo visualizzerà il testo di markdown.

![Testo di markdown](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>O Non attendibile

Apri in Studio di Azure Data i notebook sono predefiniti **attendibile**.

Se si apre un Notebook da un'altra origine, verrà aperta **Non Trusted** modalità e quindi è possibile renderlo **attendibile**.

### <a name="run-cells"></a>Eseguire le celle
Se si desidera eseguire tutte le celle del blocco appunti, quindi fare clic sui **eseguire le celle** pulsante sulla barra degli strumenti.

![Testo di markdown](media/notebooks-guidance/run-cell.png)


### <a name="clear-results"></a>Cancella risultati

Se si desidera cancellare i risultati di tutte le celle eseguite nel blocco appunti, quindi è possibile fare clic sui **Clear Results** pulsante sulla barra degli strumenti.

![Testo di markdown](media/notebooks-guidance/clear-results.png)

### <a name="save"></a>Salvare

Per salvare il notebook di effettuare una delle operazioni seguenti.

- Selezionare Ctrl + S
- Fare clic su **File** > **Salva**
- Fare clic su **File** > **Salva con nome...**
- Fare clic su **File** > **Salva tutto** 
- Nel riquadro comandi, immettere **File: Salvare** 

### <a name="pyspark3pyspark-kernel"></a>Kernel di Pyspark3/PySpark

Scegliere il `PySpark Kernel` e nel tipo di cella nel codice seguente.

Fare clic su **Esegui**.

L'applicazione Spark viene avviato e restituisce l'output seguente:

![Applicazione Spark](media/notebooks-guidance/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel Spark | Linguaggio di scala

Scegliere il `Spark|Scala Kernel` e nel tipo di cella nel codice seguente.

![Spark in Scala](media/notebooks-guidance/spark-scala.png)

È anche possibile visualizzare le opzioni"cella" quando si fa clic sull'icona di opzioni seguente:

![Opzioni di cella](media/notebooks-guidance/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel Spark | Linguaggio R

Scegliere Spark | R nella casella di riepilogo per i kernel. Nella cella, digitare o incollare il codice. Fare clic su **eseguiti** per visualizzare l'output seguente.

![Spark, R](media/notebooks-guidance/spark-r.png)

### <a name="local-python-kernel"></a>Kernel Python in locale

Scegliere il Kernel Python in locale e nel tipo di cella in:

![Python in locale](media/notebooks-guidance/local-python.png)

## <a name="manage-packages"></a>Gestire i pacchetti

Uno degli aspetti che è stato ottimizzato per lo sviluppo Python locale era includono la possibilità di installare i pacchetti che i clienti sono necessario per i loro scenari. Per impostazione predefinita, si includono i pacchetti più comuni, ad esempio `pandas`, `numpy` e così via, ma se si prevede un pacchetto che non è incluso, quindi scrivere il codice seguente nella cella notebook: 

```python
import <package-name>
```

Quando si esegue questo comando, `Module not found` viene restituito. Se il pacchetto esiste, non si verrà visualizzato l'errore.

Se viene restituito un `Module not Found` errori, quindi fare clic su **Gestisci pacchetti** per avviare il terminale. È ora possibile installare i pacchetti in locale. Usare i comandi seguenti per installare i pacchetti:

```bash
./pip install <package-name>
```

   > [!Tip]
   > In Mac, seguire le istruzioni nella finestra del terminale per installare i pacchetti. 

Dopo aver installato il pacchetto, sarà possibile tornare nella cella Notebook e digitare il comando seguente:

```python
import <package-name>
```

Per disinstallare un pacchetto, usare il comando seguente dal terminale:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come usare un notebook esistente, vedere [come gestire i notebook in Azure Data Studio](notebooks-how-to-manage.md).