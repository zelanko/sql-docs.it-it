---
title: Esegui i notebook in Azure Data Studio
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo illustra come eseguire i notebook di Jupyter in Azure Data Studio conneected a un cluster di big data di SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/12/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 44ba203fcd7445add8fce00dd64913f85bcf4cc1
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161658"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Come usare i notebook in fase di anteprima di SQL Server 2019

Questo articolo descrive come avviare i notebook di Jupyter in un cluster di big data e su come iniziare a creare i tuoi notebook. Viene inoltre illustrato come inviare processi rispetto al cluster.

## <a name="prerequisites"></a>Prerequisiti

Per usare i notebook, è necessario installare i prerequisiti seguenti:

- [Un cluster di big data di SQL Server 2019](deployment-guidance.md)
- [Strumenti di big data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>Connettersi al punto finale del cluster di SQL Server i big Data

È possibile connettersi a endpoint diversi del cluster. È possibile connettersi al tipo di connessione di Microsoft SQL Server o per il punto finale del cluster di SQL Server i big Data.
In Azure Data Studio, premere F1 e fare clic su **nuova connessione** ed è possibile connettersi al punto di fine del cluster di SQL Server i big Data.

![immagine1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>Sfoglia HDFS

Dopo essersi connessi, sarà in grado di individuare la cartella HDFS. SQL Server inizia WebHDFS viene avviato quando viene completata la distribuzione. Con WebHDFS, è possibile **Refresh**, aggiungere **nuova Directory**, **caricare** file, e **Elimina**.

![immagine2](media/notebooks-guidance/image2.png)

Queste semplici operazioni consentono di inserire i propri dati in HDFS.

## <a name="launch-new-notebooks"></a>Avviare di nuovo notebook

>[!NOTE]
>Se si dispone di più processi Python in esecuzione nell'ambiente in uso, eliminare prima il `.scaleoutdata` cartella sotto la directory installata. Ciò deve attivare il `Reinstall Notebook dependencies` attività in Data Studio di Azure. Richiederà alcuni minuti per tutte le dipendenze da installare.

Se sono presenti problemi di installazione delle dipendenze di notebook, fare clic su Ctrl + MAIUSC + P o per Macintosh Cmd + MAIUSC + P e tipo `Reinstall Notebook dependencies` nel riquadro comandi.

![image3](media/notebooks-guidance/image3.png)

Esistono diversi modi per avviare un nuovo notebook.

1. Dal **Gestisci Dashboard**. Dopo aver apportato una nuova connessione, si verrà visualizzato un dashboard. Fare clic su **nuovo Notebook** attività dal dashboard.
  
    ![image4](media/notebooks-guidance/image4.png)

1. Fare doppio clic la connessione di Spark o HDFS e fare clic su **nuovo Notebook** nel menu di scelta rapida.

    ![image5](media/notebooks-guidance/image5.png)

    Un nuovo file denominato `Notebook-0.ipynb` apre.

    ![image6](media/notebooks-guidance/image6.png)

Quando si apre il notebook dal gruppo di comando, il notebook viene aperto come `Untitled-0.ipynb`.

## <a name="supported-kernels-and-attach-to-context"></a>Supportati i kernel e associare al contesto

L'installazione di Notebook supporta kernel PySpark e Spark, Magic Spark, che consentono di scrivere il codice Python e Scala con Spark. Facoltativamente, è possibile scegliere Python per scopi di sviluppo locale.

![image7](media/notebooks-guidance/image7.png)

Quando si seleziona uno di questi kernel, l'installazione consente di configurare tale kernel nell'ambiente virtuale e iniziare a scrivere codice nel linguaggio supportato.

|Kernel|Descrizione
|:-----|:-----
|PySpark3 e il Kernel PySpark| Scrivere il codice Python con Spark compute dal cluster.
|Kernel Spark|Scrivere il codice R e Scala con Spark compute dal cluster.
|Kernel Python|Scrivere il codice Python per lo sviluppo locale.

`Attach to` fornisce il contesto per il Kernel da collegare. Quando si è connessi a SQL Server i big data cluster punto finale, il valore predefinito `Attach to` tale punto di fine del cluster.

Quando non si è connessi al punto finale del cluster di SQL Server i big data, il valore predefinito del Kernel è Python e `Attach to` è `localhost`.

## <a name="hello-world-in-different-contexts"></a>HelloWorld in contesti diversi

### <a name="pyspark3pyspark-kernel"></a>Kernel di Pyspark3/PySpark

Scegliere il PySpark Kernel e nel tipo di cella nel codice seguente.

Fare clic su **Esegui**.

L'applicazione Spark viene avviato e restituisce l'output seguente:

![image8](media/notebooks-guidance/image8.png)

### <a name="spark-kernel--scala-language"></a>Kernel Spark | Linguaggio di scala

Scegliere Spark | Scala Kernel e nel tipo di cella nel codice seguente.

![image9](media/notebooks-guidance/image9.png)

Aggiungere una nuova cella di codice facendo il **+ Code** comando sulla barra degli strumenti.

A questo punto, scegliere Spark | Scala nell'elenco a discesa per i kernel e nella cella digita/Incolla in:

![Image10](media/notebooks-guidance/image10.png)

È anche possibile visualizzare le opzioni"cella" quando si fa clic sull'icona di opzioni seguente:

![Image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel--r-language"></a>Kernel Spark | Linguaggio R

Scegliere Spark | R nella casella di riepilogo per i kernel. Nella cella, digitare o incollare il codice. Fare clic su **eseguiti** per visualizzare l'output seguente.

![Image13](media/notebooks-guidance/image13.png)

### <a name="local-python-kernel"></a>Kernel Python in locale

Scegliere il Kernel Python in locale e nel tipo di cella in:

![Image14](media/notebooks-guidance/image14.png)

### <a name="markdown-text"></a>Testo di markdown

Aggiungere una nuova cella di testo facendo il **+ testo** comando sulla barra degli strumenti.

![Image15](media/notebooks-guidance/image15.png)

Fare doppio clic all'interno della cella di testo da modificare per Modifica vista 

![Image16](media/notebooks-guidance/image16.png)

Cella cambia la modalità di modifica

![Image17](media/notebooks-guidance/image17.png)

A questo punto markdown di tipo e verrà visualizzato l'anteprima allo stesso tempo

![Image18](media/notebooks-guidance/image18.png)

Fare clic su **Esegui**. Avvio dell'applicazione Spark crea la sessione di Spark come **spark** e definisce il **HelloWorld** oggetto.

Il blocco appunti dovrebbe essere simile all'immagine seguente.

Facendo clic all'esterno della cella di testo viene modificato in modalità di anteprima e nasconde il markdown.

![Image19](media/notebooks-guidance/image19.png)


## <a name="manage-packages"></a>Gestire i pacchetti
Uno degli aspetti che è stato ottimizzato per lo sviluppo Python locale era includono la possibilità di installare i pacchetti che i clienti sono necessario per i loro scenari. Per impostazione predefinita, si includono i pacchetti più comuni, ad esempio `pandas`, `numpy` e così via, ma se si prevede un pacchetto che non è incluso, quindi scrivere il codice seguente nella cella notebook: 

```python
import <package-name>
```

Quando si esegue questo comando, `Module not found` viene restituito. Se il pacchetto esiste, non si verrà visualizzato l'errore.

Se viene restituito un `Module not Found` errori, quindi fare clic su **Gestisci pacchetti** per avviare il terminale con il percorso per il Virtualenv identificato. È ora possibile installare i pacchetti in locale. Usare i comandi seguenti per installare i pacchetti:

```bash
./pip install <package-name>
```

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