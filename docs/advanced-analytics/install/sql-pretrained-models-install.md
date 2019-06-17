---
title: Installare con training preliminare modelli di machine learning - SQL Server Machine Learning
description: Aggiungere modelli con training preliminare per la definizione delle funzionalità a sentiment analysis e l'immagine di SQL Server 2017 Machine Learning Services (R o Python) o SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 002713c8c3eb92a33cbb1461eaacb8a0d63a5c3f
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140749"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Installare con training preliminare modelli di machine learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come usare Powershell per aggiungere gratuito con training preliminare modelli di machine learning per *analisi del sentiment* e *definizione delle funzionalità immagine* a un'istanza di SQL Server con l'integrazione di R o Python. I modelli con training preliminare vengono creati da Microsoft e pronti da usare, aggiungere a un'istanza come un'attività di post-installazione. Per altre informazioni su questi modelli, vedere la [risorse](#bkmk_resources) sezione di questo articolo.

Una volta installato, i modelli con training preliminare vengono considerati un dettaglio di implementazione che power funzioni specifiche nel MicrosoftML (R) e librerie di microsoftml (Python). È non deve (e possibile) consente di visualizzare, personalizzare o ripetere il training dei modelli, né può è considerarli come risorsa indipendente nel codice personalizzato o abbinate altre funzioni. 

Per usare i modelli con training preliminare, chiamare le funzioni elencate nella tabella seguente.

| Funzione R (MicrosoftML) | Funzione Python (microsoftml) | Uso |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | Genera il punteggio del sentiment positivo, negativo tramite input di testo. |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Estrae le informazioni di testo di input di file di immagine. |

## <a name="prerequisites"></a>Prerequisiti

Algoritmi di Machine learning sono notevoli. Si consiglia di 16 GB di RAM per carichi di lavoro basso a moderato, incluso il completamento delle procedure dettagliate dell'esercitazione con tutti i dati di esempio.

È necessario disporre dei diritti di amministratore nel computer e SQL Server per aggiungere modelli con training preliminare.

È necessario abilitare gli script esterni e deve essere in esecuzione il servizio LaunchPad di SQL Server. Le istruzioni di installazione illustrano i passaggi per l'abilitazione e la verifica di queste funzionalità. 

[Pacchetto R MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) oppure [pacchetto Python microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) contengono i modelli con training preliminare.

+ [SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md) include entrambe le versioni in lingue della libreria di machine learning, in modo che questo prerequisito viene soddisfatta con senza alcun intervento da parte dell'utente. Poiché le librerie sono presenti, è possibile usare lo script di PowerShell descritto in questo articolo per aggiungere i modelli con training preliminare per queste librerie.

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md), ovvero solo R non include [pacchetto MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) predefiniti. Per aggiungere MicrosoftML, è necessario effettuare una [aggiornamento del componente](../install/upgrade-r-and-python.md). Uno dei vantaggi dell'aggiornamento del componente è che è possibile contemporaneamente aggiungere i modelli con training preliminare, che rende l'esecuzione dello script di PowerShell non necessario. Tuttavia, se già aggiornato ma hai perso l'aggiunta di modelli con training preliminare fin dall'inizio, è possibile eseguire lo script di PowerShell come descritto in questo articolo. Funziona per entrambe le versioni di SQL Server. Prima di procedere, verificare che la libreria di MicrosoftML esista in C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library.


<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>Verificare che siano installati i modelli con training preliminare

I percorsi di installazione per i modelli R e Python sono i seguenti:

+ Per r: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Per Python: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

I nomi di file di modello sono elencati di seguito:

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

Se i modelli sono già installati, ignorare il [passaggio di convalida](#verify) per confermare la disponibilità.

## <a name="download-the-installation-script"></a>Scaricare lo script di installazione

Fare clic su [ https://aka.ms/mlm4sql ](https://aka.ms/mlm4sql) per scaricare il file **Install-MLModels.ps1**.

## <a name="execute-with-elevated-privileges"></a>Esegui con privilegi elevati

1. Avviare PowerShell. Sulla barra dei comandi, fare doppio clic sull'icona di PowerShell e selezionare **Esegui come amministratore**.
2. Immettere un percorso completo del file di script di installazione e includere il nome dell'istanza. Supponendo che la cartella di download e un'istanza predefinita, il comando potrebbe essere simile al seguente:

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**Output**

In un connesso a internet in Machine Learning di SQL Server 2017 istanza predefinita con R e Python, si dovrebbe essere messaggi simili al seguente.

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

In primo luogo, verificare la presenza di nuovi file nei [mxlibs cartella](#file-location). Successivamente, eseguire il codice di esempio per verificare che i modelli sono installati e funzionanti. 

### <a name="r-verification-steps"></a>Passaggi di verifica di R

1. Avviare **RGUI. File EXE** in C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\bin\x64.

2. Incollare lo script R seguente al prompt dei comandi.

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

3. Premere INVIO per visualizzare i punteggi del sentiment. Output dovrebbe essere come segue:

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

### <a name="python-verification-steps"></a>Passaggi di verifica di Python

1. Avviare **Python.exe** in C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES.

2. Incollare lo script Python seguente al prompt dei comandi

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

3. Premere INVIO per stampare i punteggi. Output dovrebbe essere come segue:

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> Se gli script di demo esito negativo, controllare prima di tutto il percorso del file. In sistemi con più istanze di SQL Server o per istanze di tale esecuzione side-by-side con versioni autonome, è possibile che lo script di installazione leggere correttamente l'ambiente e posizionare i file in una posizione non valida. In genere, manualmente copia dei file nella cartella corretta mxlib corregge il problema.

## <a name="examples-using-pre-trained-models"></a>Esempi di utilizzo di modelli con training preliminare

Il collegamento seguente includono codice di esempio richiama i modelli con training preliminare.

+ [Esempio di codice: Analisi del sentiment con testo Featurizer](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>Ricerca e le risorse

Attualmente i modelli disponibili sono i modelli di reti neurali profonde (DNN) per la classificazione del sentiment analysis e l'immagine. Sono stati sottoposti a training di tutti i modelli con training preliminare usando Microsoft [calcolo Network Toolkit](https://cntk.ai/Features/Index.html), o **CNTK**.

La configurazione di ogni rete basa le implementazioni di riferimento seguenti:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Per altre informazioni sugli algoritmi usati in questi modelli di deep learning e come vengono implementate e sottoposto a training con CNTK, vedere gli articoli seguenti:

+ [Algoritmo i ricercatori Microsoft consente di impostare un'attività cardine ImageNet sfida](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft Computational Network Toolkit offre più efficiente di prestazioni di calcolo di apprendimento avanzato distribuito](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>Vedere anche

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md)
+ [Aggiornare i componenti di R e Python in istanze di SQL Server](../install/upgrade-r-and-python.md)
+ [Pacchetto MicrosoftML per R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [pacchetto microsoftml per Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
