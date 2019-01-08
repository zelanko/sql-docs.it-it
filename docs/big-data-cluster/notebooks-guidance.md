---
title: Esegui i notebook in Azure Data Studio
titleSuffix: SQL Server 2019 big data clusters
description: Questo articolo illustra come eseguire i notebook di Jupyter in Azure Data Studio conneected a un cluster di big data di SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: af1393b38b297e451903d5a39942a3e878c88ee6
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246610"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>Come usare i notebook in fase di anteprima di SQL Server 2019

Questo articolo descrive come avviare i notebook di Jupyter in un cluster di big data e su come iniziare a creare i tuoi notebook. Viene inoltre illustrato come inviare processi rispetto al cluster.

## <a name="prerequisites"></a>Prerequisiti

Per usare i notebook, è necessario installare i prerequisiti seguenti:

- [Un cluster di big data di SQL Server 2019](deployment-guidance.md)
- [Strumenti di big data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **Kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-hadoop-gateway-knox-end-point"></a>Connettersi al punto di fine Hadoop Gateway Knox

È possibile connettersi a endpoint diversi del cluster. È possibile connettersi al tipo di connessione di Microsoft SQL Server o per il punto finale di gateway HDFS/Spark.
In Azure Data Studio (anteprima), premere F1 e fare clic su **nuova connessione** ed è possibile connettersi al punto finale di gateway di HDFS/Spark.

![immagine1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>Sfoglia HDFS

Dopo essersi connessi, sarà in grado di individuare la cartella HDFS. WebHDFS viene avviato quando viene completata la distribuzione, e sarà in grado **Refresh**, aggiungere **nuova Directory**, **caricare** file, e **eliminare**.

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

  Specificare un nome del Notebook, ad esempio, `Test.ipynb`. Fare clic su **Salva**.

![image6](media/notebooks-guidance/image6.png)

## <a name="supported-kernels-and-attach-to-context"></a>Supportati i kernel e associare al contesto

L'installazione di Notebook supporta kernel PySpark e Spark, Magic Spark, che consentono di scrivere il codice Python e Scala con Spark. Facoltativamente, è possibile scegliere Python per scopi di sviluppo locale.

![image7](media/notebooks-guidance/image7.png)

Quando si seleziona uno di questi kernel, verrà installato tale kernel nell'ambiente virtuale e iniziare a scrivere codice nel linguaggio supportato.

|Kernel|Descrizione
|:-----|:-----
|Kernel PySpark|Per la scrittura di codice Python con Spark compute dal cluster.
|Kernel Spark|Per la scrittura di codice Scala con Spark compute dal cluster.
|Kernel Python|Per la scrittura di codice Python per lo sviluppo locale.

Il `Attach to` fornisce il contesto per il Kernel da collegare. Quando si è connessi alla fine HDFS/Spark gateway (Knox) scegliere l'impostazione predefinita `Attach to` tale punto di fine del cluster.

![image8](media/notebooks-guidance/image8.png)

## <a name="hello-world-in-different-contexts"></a>HelloWorld in contesti diversi

### <a name="pyspark-kernel"></a>Kernel Pyspark

Scegliere il PySpark Kernel e nel tipo di cella nel codice seguente:

![image9](media/notebooks-guidance/image9.png)

Fare clic su Esegui e si dovrebbe vedere l'applicazione Spark in corso l'avvio e si verrà visualizzato l'output seguente:

![Image10](media/notebooks-guidance/image10.png)

L'output dovrebbe essere simile all'immagine seguente.

![Image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel"></a>Kernel Spark
Aggiungere una nuova cella di codice facendo il **+ Code** comando sulla barra degli strumenti.

![Image12](media/notebooks-guidance/image12.png)

È anche possibile visualizzare le opzioni"cella" quando si fa clic sull'icona di opzioni seguente:

![Image13](media/notebooks-guidance/image13.png)

Ecco le opzioni per tutte le celle:

![Image14](media/notebooks-guidance/image14.png)-

A questo punto, scegliere il Kernel Spark nell'elenco a discesa per i kernel e nella cella digita/Incolla-

![Image15](media/notebooks-guidance/image15.png)

Fare clic su **eseguiti** e viene visualizzata l'applicazione Spark in corso l'avvio e verrà creata la sessione di Spark come **spark** e verranno definite il **HelloWorld** oggetto.

Il blocco appunti dovrebbe essere simile all'immagine seguente.

![Image16](media/notebooks-guidance/image16.png)

Dopo aver definito l'oggetto quindi nella prossima cella Notebook, digitare il codice seguente:

![Image17](media/notebooks-guidance/image17.png)

Fare clic su **eseguire** nel Notebook di menu e verrà visualizzato "Hello, world!" Nell'output.

![Image18](media/notebooks-guidance/image18.png)

### <a name="local-python-kernel"></a>Kernel python in locale
Scegliere il Kernel Python in locale e nel tipo di cella in:

![Image19](media/notebooks-guidance/image19.png)

È consigliabile vedere l'output seguente:

![Image20](media/notebooks-guidance/image20.png)

### <a name="markdown-text"></a>Testo di markdown
Aggiungere una nuova cella di testo facendo il **+ testo** comando sulla barra degli strumenti.

![Image21](media/notebooks-guidance/image21.png)

Fare clic sull'icona di anteprima per aggiungere il codice markdown

![Image22](media/notebooks-guidance/image22.png)

Fare clic sull'icona di anteprima per attivare/disattivare per visualizzare solo il markdown

![Image23](media/notebooks-guidance/image23.png)

## <a name="manage-packages"></a>Gestire i pacchetti
Uno degli aspetti che è stato ottimizzato per lo sviluppo Python locale era includono la possibilità di installare i pacchetti che i clienti sono necessario per i loro scenari. Per impostazione predefinita, si includono i pacchetti più comuni, ad esempio pandas, numpy e così via, ma se ci si aspetta un pacchetto che non è incluso quindi scrivere il codice seguente nella cella Notebook: 

```python
import <package-name>
```

Quando si esegue questo comando, si otterrà un `Module not found` errore. Se il pacchetto esiste, non si verrà visualizzato l'errore.

Se si trova un `Module not Found` errori, quindi fare clic su **Gestisci pacchetti** per avviare il terminale con il percorso per il Virtualenv identificato. È ora possibile installare i pacchetti in locale. Usare i comandi seguenti per installare i pacchetti:

```bash
./pip install <package-name>
```

Dopo aver installato il pacchetto, sarà possibile tornare nella cella Notebook e digitare il comando seguente:

```python
import <package-name>
```

A questo punto quando si esegue la cella, non si dovrebbe accedere non è più il `Module not found` errore.

Per disinstallare un pacchetto, usare il comando seguente dal terminale:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come usare un notebook esistente, vedere [come gestire i notebook in Azure Data Studio](notebooks-how-to-manage.md).