---
title: Installare modelli con training preliminare
description: Aggiungere modelli con training preliminare per l'analisi del sentiment e la definizione delle caratteristiche di un'immagine a Machine Learning Services per SQL Server (R o Python) o R Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 97da2ed795d002fa47900eb21ead90b48b525387
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727554"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Installare modelli di Machine Learning con training preliminare in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo illustra come usare PowerShell per aggiungere modelli di Machine Learning con training preliminare per l'*analisi del sentiment* e la *definizione delle caratteristiche di un'immagine* a un'istanza di SQL Server con l'integrazione di R o Python. I modelli con training preliminare creati da Microsoft sono pronti all'uso e vengono aggiunti a un'istanza come attività di post-installazione. Per altre informazioni su questi modelli, vedere la sezione [Risorse](#bkmk_resources) di questo articolo.

Dopo l'installazione, i modelli con training preliminare sono considerati un dettaglio di implementazione che alimenta funzioni specifiche nelle librerie MicrosoftML (R) e microsoftml (Python). Non è consigliabile (né possibile) visualizzare, personalizzare o ripetere il training dei modelli e nemmeno trattarli come risorsa indipendente in codice personalizzato o altre funzioni associate. 

Per usare i modelli con training preliminare, chiamare le funzioni elencate nella tabella seguente.

| Funzione R (MicrosoftML) | Funzione Python (microsoftml) | Uso |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | Genera un punteggio di sentiment positivo-negativo rispetto a input di testo. |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Estrae informazioni in formato testo da input di file di immagine. |

## <a name="prerequisites"></a>Prerequisiti

Gli algoritmi di Machine Learning comportano un utilizzo elevato delle risorse di calcolo. Per un carico di lavoro da basso a moderato sono consigliati 16 GB di RAM, incluso il completamento delle procedure dettagliate delle esercitazioni con tutti i dati di esempio.

Per aggiungere modelli con training preliminare è necessario disporre dei diritti di amministratore sul computer e su SQL Server.

Gli script esterni devono essere abilitati e il servizio Launchpad di SQL Server deve essere in esecuzione. Nelle istruzioni di installazione sono descritti i passaggi per abilitare e verificare queste funzionalità. 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
I modelli con training preliminare sono inclusi nel [pacchetto MicrosoftML per R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) o nel [pacchetto microsoftml per Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package).

[Machine Learning Services per SQL Server](sql-machine-learning-services-windows-install.md) include le versioni della libreria di Machine Learning per i due linguaggi e pertanto questo prerequisito viene soddisfatto senza che siano necessarie altre azioni da parte dell'utente. Poiché le librerie sono presenti, è possibile usare lo script di PowerShell descritto in questo articolo per aggiungere i modelli con training preliminare a queste librerie.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
I modelli con training preliminare sono inclusi nel [pacchetto MicrosoftML per R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package).

In [R Services per SQL Server](sql-r-services-windows-install.md), che include solo il supporto per R, non è integrato il [pacchetto MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package). Per aggiungere MicrosoftML, è necessario eseguire un [aggiornamento del componente](../install/upgrade-r-and-python.md). Questo aggiornamento offre il vantaggio di poter aggiungere contemporaneamente i modelli con training preliminare, evitando così di dover eseguire lo script di PowerShell. Se tuttavia l'aggiornamento è già stato eseguito, ma non sono stati subito aggiunti i modelli con training preliminare, è possibile eseguire lo script di PowerShell come descritto in questo articolo. Lo script funziona per entrambe le versioni di SQL Server. Prima di procedere, verificare che la libreria di MicrosoftML sia presente in `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`.
::: moniker-end

<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>Controllare se i modelli con training preliminare sono installati

I percorsi di installazione dei modelli per R e Python sono i seguenti:

+ Per R: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Per Python: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

I nomi dei file di modello sono elencati di seguito:

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

Se i modelli sono già installati, proseguire con il [passaggio di convalida](#verify) per verificare la disponibilità.

## <a name="download-the-installation-script"></a>Scaricare lo script di installazione

Fare clic su [https://aka.ms/mlm4sql](https://aka.ms/mlm4sql) per scaricare il file **Install-MLModels.ps1**.

## <a name="execute-with-elevated-privileges"></a>Eseguire con privilegi elevati

1. Avviare PowerShell. Sulla barra delle applicazioni fare clic con il pulsante destro del mouse sull'icona del programma PowerShell e scegliere **Esegui come amministratore**.
2. Immettere il percorso completo del file dello script di installazione e includere il nome dell'istanza. Supponendo che vengano usate la cartella Downloads e un'istanza predefinita, il comando potrebbe essere simile al seguente:

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**Output**

In un'istanza predefinita connessa a Internet di Machine Learning Services per SQL Server con R e Python, verranno visualizzati messaggi simili al seguente.

   ```powershell
   MSSQL14.MSSQLSERVER
        Verifying R models [9.2.0.24]
        Downloading R models [C:\Users\<user-name>\AppData\Local\Temp]
        Installing R models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\]
        Verifying Python models [9.2.0.24]
        Installing Python models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\]
   PS C:\WINDOWS\system32>
   ```

<a name="verify"> </a>

## <a name="verify-installation"></a>Verificare l'installazione

Per prima cosa, controllare che i nuovi file siano presenti nella [cartella mxlibs](#file-location). Eseguire quindi il codice demo per verificare che i modelli siano installati e funzionanti. 

### <a name="r-verification-steps"></a>Passaggi di verifica per R

1. Avviare **RGUI.EXE** in C:\Programmi\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64.

2. Incollare lo script R seguente nel prompt dei comandi.

    ```R
    # Create the data
    CustomerReviews <- data.frame(Review = c(
    "I really did not like the taste of it",
    "It was surprisingly quite good!",
    "I will never ever ever go to that place again!!"),
    stringsAsFactors = FALSE)

    # Get the sentiment scores
    sentimentScores <- rxFeaturize(data = CustomerReviews, 
                                    mlTransforms = getSentiment(vars = list(SentimentScore = "Review")))

    # Let's translate the score to something more meaningful
    sentimentScores$PredictedRating <- ifelse(sentimentScores$SentimentScore > 0.6, 
                                            "AWESOMENESS", "BLAH")

    # Let's look at the results
    sentimentScores
    ```

3. Premere INVIO per visualizzare i punteggi del sentiment. L'output sarà simile al seguente:

    ```R
    > sentimentScores
                                            Review SentimentScore
    1           I really did not like the taste of it      0.4617899
    2                 It was surprisingly quite good!      0.9601924
    3 I will never ever ever go to that place again!!      0.3103435
    PredictedRating
    1            BLAH
    2     AWESOMENESS
    3            BLAH
    ```

### <a name="python-verification-steps"></a>Passaggi di verifica per Python

1. Avviare **Python.exe** in C:\Programmi\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES.

2. Incollare lo script Python seguente nel prompt dei comandi.

    ```python
    import numpy
    import pandas
    from microsoftml import rx_logistic_regression, rx_featurize, rx_predict, get_sentiment

    # Create the data
    customer_reviews = pandas.DataFrame(data=dict(review=[
                "I really did not like the taste of it",
                "It was surprisingly quite good!",
                "I will never ever ever go to that place again!!"]))
                
    # Get the sentiment scores
    sentiment_scores = rx_featurize(
        data=customer_reviews,
        ml_transforms=[get_sentiment(cols=dict(scores="review"))])
        
    # Let's translate the score to something more meaningful
    sentiment_scores["eval"] = sentiment_scores.scores.apply(
                lambda score: "AWESOMENESS" if score > 0.6 else "BLAH")
    print(sentiment_scores)
    ```

3. Premere INVIO per visualizzare i punteggi. L'output sarà simile al seguente:

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> Se gli script demo hanno esito negativo, controllare prima il percorso del file. Nei sistemi con più istanze di SQL Server, o per istanze eseguite side-by-side con versioni autonome, è possibile che lo script di installazione non riesca a leggere l'ambiente in modo corretto e inserisca i file nel percorso sbagliato. È in genere possibile correggere il problema copiando manualmente i file nella cartella mxlib.

## <a name="examples-using-pre-trained-models"></a>Esempi d'uso dei modelli con training preliminare

Il collegamento seguente include codice di esempio che richiama i modelli con training preliminare.

+ [Codice di esempio: Analisi del sentiment tramite una funzione di definizione delle caratteristiche del testo](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>Ricerca e risorse

I modelli attualmente disponibili sono modelli di tipo DNN (Deep Neural Network) per l'analisi del sentiment e la classificazione delle immagini. Tutti i modelli sono stati sottoposti a training con il [Computation Network Toolkit](https://cntk.ai/Features/Index.html), o **CNTK**, di Microsoft.

La configurazione di ogni rete neurale è stata basata sulle seguenti implementazioni di riferimento:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Per altre informazioni sugli algoritmi usati in questi modelli di Deep Learning e sul modo in cui vengono implementati e sottoposti a training con CNTK, vedere questi articoli:

+ [Microsoft Researchers' Algorithm Sets ImageNet Challenge Milestone](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/) (L'algoritmo dei ricercatori Microsoft ottiene un importante risultato nella sfida di ImageNet)

+ [Microsoft Computational Network Toolkit offers most efficient distributed deep learning computational performance](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/) (Microsoft Computational Network Toolkit offre prestazioni di calcolo di massimo livello per il Deep Learning distribuito)

## <a name="see-also"></a>Vedere anche

+ [SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md)
+ [Aggiornare i componenti R e Python nelle istanze di SQL Server](../install/upgrade-r-and-python.md)
+ [Pacchetto MicrosoftML per R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [Pacchetto microsoftml per Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
