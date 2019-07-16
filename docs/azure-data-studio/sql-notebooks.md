---
title: Come usare i notebook di SQL Studio di dati di Azure
titleSuffix: Azure Data Studio
description: Informazioni su come usare i notebook di SQL Studio di dati di Azure
ms.custom: seodec18
ms.date: 06/28/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9af2e04a3973eddfcd714c7968c35e544302aba9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959269"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>Come usare i notebook in Azure Data Studio

Questo articolo descrive come avviare l'esperienza Notebook in Azure Data Studio e su come iniziare a creare i tuoi notebook. Viene inoltre illustrato come scrivere i notebook con kernel diversi.


## <a name="connect-to-sql-server"></a>Connessione a SQL Server

È possibile connettersi al tipo di connessione di Microsoft SQL Server in Azure Data Studio.
In Azure Data Studio, è possibile anche premere F1 e fare clic su **nuova connessione** e connettersi a SQL Server.

![immagine1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>Avviare i notebook

Esistono diversi modi per avviare un nuovo notebook.

1. Andare alla **dal Menu File** in Azure Data Studio e quindi fare clic su **nuovo Notebook**.

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. Fare clic con il pulsante destro sul **SQL Server** connessione e quindi avviare **nuovo Notebook**. 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. Aprire il riquadro comandi (**Ctrl + MAIUSC + P**)) e quindi digitare **nuovo Notebook**. Un nuovo file denominato `Notebook-1.ipynb` apre.

## <a name="supported-kernels-and-attach-to-context"></a>Supportati i kernel e associare al contesto

L'installazione di Notebook in Azure Data Studio supporta in modo nativo SQL Kernel. Se si sono uno sviluppatore SQL e si desidera usare i notebook e quindi il risultato sarà la prescelta Kernel. 

Il Kernel SQL è anche utilizzabile per connettersi alle istanze del server PostgreSQL. Se si è uno sviluppatore di PostgreSQL e si desidera connettersi al PostgreSQL Server, quindi scaricare il [ **estensioni di PostgreSQL** ](postgres-extension.md) nel marketplace delle estensioni di Studio dei dati di Azure.

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Kernel SQL

Nelle celle di codice del blocco appunti, simile all'editor di query, Supportiamo SQL moderna esperienza che agevola le attività quotidiane con funzionalità incorporate, ad esempio un editor SQL avanzato, IntelliSense e frammenti di codice incorporato di codifica. Frammenti di codice consentono di generare la sintassi SQL appropriata per creare database, tabelle, viste, stored procedure e così via e per aggiornare gli oggetti di database esistenti. Usare frammenti di codice per creare rapidamente copie del database per lo sviluppo o a scopo di test e di generare ed eseguire gli script.

Fare clic su **eseguire** da eseguire ogni cella.

Kernel di SQL per connettersi all'istanza di SQL Server

![image7](media/sql-notebooks/intellisense-code-cell.png)

Risultati delle query

![Image19](media/sql-notebooks/sql-cell-results.png)

Kernel di SQL per connettersi all'istanza del PostgreSQL Server 

![Image18](media/sql-notebooks/pgsql-code-cell.png)

Risultati delle query

![Image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Configurare Python per i notebook

Quando si seleziona una delle altre kernel oltre a SQL dall'elenco a discesa kernel, viene richiesto di **configurare Python per notebook**. Le dipendenze di Notebook installate in un percorso specificato, ma è possibile decidere se si desidera impostare il percorso di installazione. Questa installazione può richiedere molto tempo e si consiglia di non chiudere l'applicazione fino al completamento dell'installazione. Una volta completata l'installazione, è possibile iniziare a scrivere codice nel linguaggio supportato.

![Image21](media/sql-notebooks/configure-python.png)

Dopo l'installazione viene completata, si noterà una notifica nella cronologia di attività con il percorso del server back-end Jupyter in esecuzione nel terminale di Output.

![Image22](media/sql-notebooks/jupyter-backend.png)

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

![image8](media/sql-notebooks/notebook-toolbar.png)

Le modifiche di cella per la modalità di modifica e a questo punto digitare markdown e si vedrà l'anteprima allo stesso tempo

![image9](media/sql-notebooks/notebook-markdown-cell.png)

Facendo clic all'esterno della cella di testo visualizzerà il testo di markdown.

![Image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>O Non attendibile

Apri in Studio di Azure Data i notebook sono predefiniti **attendibile**.

Se si apre un Notebook da un'altra origine, verrà aperta **Non Trusted** modalità e quindi è possibile renderlo **attendibile**.

### <a name="save"></a>Salva 

È possibile salvare i Notebook dal **Ctrl + S** o facendo clic sui **salvataggio File**, **Salva con nome File...**  e **File Salva tutto** comandi dal menu File e **File: Salvare** comandi immessi nel riquadro comandi.

### <a name="pyspark3pyspark-kernel"></a>Kernel di Pyspark3/PySpark

Scegliere il `PySpark Kernel` e nel tipo di cella nel codice seguente.

Fai clic su **Esegui**.

L'applicazione Spark viene avviato e restituisce l'output seguente:

![Image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel Spark | Linguaggio di scala

Scegliere il `Spark|Scala Kernel` e nel tipo di cella nel codice seguente.

![Image13](media/sql-notebooks/spark-scala.png)

È anche possibile visualizzare le opzioni"cella" quando si fa clic sull'icona di opzioni seguente:

![Image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel Spark | Linguaggio R

Scegliere Spark | R nella casella di riepilogo per i kernel. Nella cella, digitare o incollare il codice. Fare clic su **eseguiti** per visualizzare l'output seguente.

![Image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>Kernel Python in locale

Scegliere il Kernel Python in locale e nel tipo di cella in:

![Image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>Gestire i pacchetti
Uno degli aspetti che è stato ottimizzato per lo sviluppo Python locale era includono la possibilità di installare i pacchetti che i clienti sono necessario per i loro scenari. Per impostazione predefinita, si includono i pacchetti più comuni, ad esempio `pandas`, `numpy` e così via, ma se si prevede un pacchetto che non è incluso, quindi scrivere il codice seguente nella cella notebook: 

```python
import <package-name>
```

Quando si esegue questo comando, `Module not found` viene restituito. Se il pacchetto esiste, non si verrà visualizzato l'errore.

Se viene restituito un `Module not Found` errori, quindi fare clic su **Gestisci pacchetti** per avviare l'esperienza guidata. 

![Image17](media/sql-notebooks/manage-packages.png)

In questa procedura guidata sarà in grado di vedere le **Installed** pacchetti. È possibile cercare l'elenco e la versione associata di ognuno di questi pacchetti. Se devi **disinstallare** uno di questi pacchetti, è possibile fare clic su uno dei pacchetti e quindi fare clic sui **disinstallare i pacchetti selezionati** opzione.

È inoltre possibile fare clic su **Aggiungi nuovo** di pacchetti **ricerca** per un particolare pacchetto, scegliere la versione correlata e fare clic su **installare**. Per impostazione predefinita, selezionare la versione più recente del pacchetto di ricerca. 

Dopo aver installato il pacchetto, sarà possibile tornare nella cella Notebook e digitare il comando seguente:

```python
import <package-name>
```

Se devi **disinstallare** uno di questi pacchetti, è possibile fare clic su uno o più pacchetti e quindi fare clic sui **disinstallare i pacchetti selezionati** opzione.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come usare un notebook esistente, vedere [come gestire i notebook in Azure Data Studio](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions).