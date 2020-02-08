---
title: Come usare i notebook SQL
titleSuffix: Azure Data Studio
description: Informazioni su come usare i notebook SQL in Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; maghan; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.custom: seodec18
ms.date: 06/28/2019
ms.openlocfilehash: df1e49af0378b6af4a3d82b5a5ec2a4293be5e35
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74957085"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>Come usare i notebook in Azure Data Studio

Questo articolo descrive come avviare l'esperienza dei notebook in Azure Data Studio e come iniziare a creare notebook personalizzati. Viene inoltre illustrato come scrivere notebook usando kernel diversi.


## <a name="connect-to-sql-server"></a>Connessione a SQL Server

È possibile connettersi al tipo di connessione Microsoft SQL Server in Azure Data Studio.
In Azure Data Studio è anche possibile premere F1, quindi fare clic su **Nuova connessione**  e connettersi a SQL Server.

![immagine1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>Avviare i notebook

Ci sono diversi modi per avviare un nuovo notebook.

1. Passare al **menu File**in Azure Data Studio e quindi fare clic su **New Notebook** (Nuovo notebook).

    ![immagine3](media/sql-notebooks/file-new-notebook.png)

3. Fare clic con il pulsante destro del mouse sulla connessione a **SQL Server** e quindi avviare **New Notebook** (Nuovo notebook). 
    ![immagine3](media/sql-notebooks/server-new-notebook.png)

4. Aprire il riquadro comandi (**CTRL+MAIUSC+P**) e quindi digitare **New Notebook** (Nuovo notebook). Verrà aperto un nuovo file denominato `Notebook-1.ipynb`.

## <a name="supported-kernels-and-attach-to-context"></a>Contesto di collegamento e kernel supportati

L'installazione del notebook in Azure Data Studio supporta in modo nativo il kernel SQL. Se si è uno sviluppatore SQL e si vogliono usare i notebook, si sceglierà questo kernel. 

Il kernel SQL può essere usato anche per la connessione alle istanze del server PostgreSQL. Se si è uno sviluppatore PostgreSQL e si vuole eseguire la connessione al server PostgreSQL, scaricare l'[**estensione PostgreSQL**](postgres-extension.md) nel marketplace delle estensioni di Azure Data Studio.

![immagine7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Kernel SQL

Nelle celle di codice all'interno del notebook, in modo analogo all'editor di query, è supportata l'esperienza di codifica SQL moderna, che semplifica le attività quotidiane con funzionalità predefinite come un editor SQL avanzato, IntelliSense e frammenti di codice predefiniti. I frammenti di codice consentono di generare la sintassi SQL appropriata per creare database, tabelle, viste, stored procedure e così via, nonché aggiornare gli oggetti di database esistenti. Usare i frammenti di codice per creare rapidamente copie del database a scopo di sviluppo o test e per generare ed eseguire script.

Fare clic su **Esegui** per eseguire ogni cella.

Kernel SQL per la connessione a un'istanza di SQL Server

![immagine7](media/sql-notebooks/intellisense-code-cell.png)

Risultati delle query

![immagine19](media/sql-notebooks/sql-cell-results.png)

Kernel SQL per la connessione a un'istanza del server PostgreSQL 

![immagine18](media/sql-notebooks/pgsql-code-cell.png)

Risultati delle query

![immagine20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Configurare Python per i notebook

Quando si seleziona uno degli altri kernel oltre a SQL nell'elenco a discesa di kernel, viene visualizzata la finestra **Configure Python for Notebooks** (Configurare Python per i notebook). Le dipendenze dei notebook vengono installate in una posizione specifica, ma è possibile scegliere se impostare la posizione di installazione. L'installazione può richiedere del tempo ed è consigliabile non chiudere l'applicazione fino al completamento dell'installazione. Al termine dell'installazione, è possibile iniziare a scrivere il codice nel linguaggio supportato.

![immagine21](media/sql-notebooks/configure-python.png)

Una volta completata l'installazione, verrà visualizzata una notifica nella cronologia attività, insieme alla posizione del server back-end Jupyter in esecuzione nel terminale di output.

![immagine22](media/sql-notebooks/jupyter-backend.png)

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

![immagine8](media/sql-notebooks/notebook-toolbar.png)

La cella passa alla modalità di modifica e sarà quindi possibile digitare la sintassi markdown e, nello stesso tempo, visualizzare l'anteprima

![immagine9](media/sql-notebooks/notebook-markdown-cell.png)

Se si fa clic all'esterno della cella di testo, viene visualizzato il testo markdown.

![immagine10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>Notebook attendibili e non attendibili

I notebook aperti in Azure Data Studio sono **attendibili** per impostazione predefinita.

Se si apre un notebook da un'altra origine, verrà aperto in modalità **non attendibile** e sarà quindi possibile impostarlo come **attendibile**.

### <a name="save"></a>Salvare 

È possibile salvare il notebook premendo **CTRL+S**, facendo clic sui comandi **Salva**, **Salva con nome** e **Salva tutto** del menu File e tramite i comandi **File: Salva** immessi nel riquadro comandi.

### <a name="pyspark3pyspark-kernel"></a>Kernel Pyspark3/PySpark

Scegliere `PySpark Kernel` e nella cella digitare il codice seguente.

Fare clic su **Esegui**.

L'applicazione Spark viene avviata e restituisce l'output seguente:

![immagine12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Kernel Spark | Linguaggio Scala

Scegliere `Spark|Scala Kernel` e nella cella digitare il codice seguente.

![immagine13](media/sql-notebooks/spark-scala.png)

È anche possibile visualizzare le opzioni della cella facendo clic sull'icona delle opzioni visualizzata sotto.

![immagine14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Kernel Spark | Linguaggio R

Scegliere Spark | R nell'elenco a discesa per i kernel. Nella cella digitare o incollare il codice. Fare clic su **Esegui** per visualizzare l'output seguente.

![immagine15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>Kernel Python locale

Scegliere il kernel Python locale e nella cella digitare il codice seguente.

![immagine16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>Gestire i pacchetti
Uno degli aspetti ottimizzati per lo sviluppo Python locale è la possibilità di installare i pacchetti che potrebbero essere necessari ai clienti per i loro scenari. Per impostazione predefinita, vengono inclusi pacchetti comuni come `pandas`, `numpy` e così via, ma se si prevede che un pacchetto non sia incluso, è possibile scrivere il codice seguente nella cella del notebook: 

```python
import <package-name>
```

Quando si esegue questo comando, viene restituito `Module not found`. Se il pacchetto esiste, l'errore non verrà visualizzato.

Se viene restituito un errore `Module not Found`, fare clic su **Gestisci pacchetti** per avviare la procedura guidata. 

![immagine17](media/sql-notebooks/manage-packages.png)

In questa procedura guidata sarà possibile visualizzare i pacchetti **installati**. È possibile eseguire ricerche nell'elenco e trovare la versione associata di ognuno di questi pacchetti. Se è necessario **disinstallare** uno di questi pacchetti, si può fare clic su di esso e quindi sull'opzione **Uninstall selected packages** (Disinstalla pacchetti selezionati).

È anche possibile **aggiungere nuovi** pacchetti, **cercare** un pacchetto specifico, scegliere la versione correlata e **installarlo**. Per impostazione predefinita, viene selezionata la versione più recente del pacchetto cercato. 

Una volta installato il pacchetto, dovrebbe essere possibile passare alla cella del notebook e digitare il comando seguente:

```python
import <package-name>
```

Se è necessario **disinstallare** uno di questi pacchetti, è possibile fare clic su uno o più pacchetti e quindi sull'opzione **Uninstall selected packages** (Disinstalla pacchetti selezionati).

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come usare un notebook esistente, vedere [Come gestire i notebook in Azure Data Studio](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions).