---
title: Installare modelli di apprendimento automatico con training preliminare
description: Aggiungere modelli con training preliminare per l'analisi dei sentimenti e l'immagine conteggi a SQL Server 2017 Machine Learning Services (R o Python) o 2016 SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2045d6611d5f418a9ed102a1d776080973c08659
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344965"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Installare modelli di apprendimento automatico pre-sottoposti a training in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come usare PowerShell per aggiungere modelli di apprendimento automatico pre-addestrati gratuiti per l' *analisi dei sentimenti* e l' *immagine conteggi* a un'istanza di SQL Server con integrazione di R o Python. I modelli con training preliminare sono compilati da Microsoft e pronti all'uso, aggiunti a un'istanza come attività post-installazione. Per ulteriori informazioni su questi modelli, vedere la sezione [risorse](#bkmk_resources) di questo articolo.

Dopo l'installazione, i modelli con training preliminare sono considerati un dettaglio di implementazione che alimenta funzioni specifiche nelle librerie MicrosoftML (R) e MicrosoftML (Python). Non è consigliabile, né è possibile, visualizzare, personalizzare o ripetere il training dei modelli, né considerarli come una risorsa indipendente nel codice personalizzato o altre funzioni associate. 

Per usare i modelli con training, chiamare le funzioni elencate nella tabella seguente.

| Funzione R (MicrosoftML) | Funzione Python (microsoftml) | Uso |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | Genera il punteggio positivo negativo del sentimento sugli input di testo. |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Estrae le informazioni di testo dagli input del file di immagine. |

## <a name="prerequisites"></a>Prerequisiti

Gli algoritmi di Machine Learning sono a elevato utilizzo di calcolo. Per i carichi di lavoro da basso a moderato sono consigliate 16 GB di RAM, incluso il completamento delle procedure dettagliate dell'esercitazione con tutti i dati di esempio.

È necessario disporre dei diritti di amministratore per il computer e SQL Server per aggiungere modelli con training preliminare.

Gli script esterni devono essere abilitati ed è necessario che SQL Server servizio LaunchPad sia in esecuzione. Le istruzioni di installazione forniscono i passaggi per l'abilitazione e la verifica di queste funzionalità. 

Il pacchetto [R MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) o il [pacchetto MicrosoftML Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) contiene i modelli pre-sottoposti a training.

+ [SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md) include entrambe le versioni del linguaggio della libreria di Machine Learning, quindi questo prerequisito viene soddisfatto senza ulteriori azioni da parte dell'utente. Poiché le librerie sono presenti, è possibile usare lo script di PowerShell descritto in questo articolo per aggiungere i modelli pre-sottoposti a training a queste librerie.

+ [SQL Server 2016 r Services](sql-r-services-windows-install.md), che è solo r, non include il [pacchetto MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) . Per aggiungere MicrosoftML, è necessario eseguire un [aggiornamento del componente](../install/upgrade-r-and-python.md). Un vantaggio dell'aggiornamento dei componenti è che è possibile aggiungere contemporaneamente i modelli pre-sottoposti a training, rendendo necessario l'esecuzione dello script di PowerShell. Tuttavia, se è già stato eseguito l'aggiornamento, ma non è stato possibile aggiungere i modelli con training preliminare per la prima volta, è possibile eseguire lo script di PowerShell come descritto in questo articolo. Funziona per entrambe le versioni di SQL Server. Prima di procedere, verificare che la libreria MicrosoftML esista in C:\Programmi\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library.


<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>Controllare se sono installati modelli con training preliminare

I percorsi di installazione per i modelli R e Python sono i seguenti:

+ Per R:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Per Python:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

I nomi dei file di modello sono elencati di seguito:

+ AlexNet\_aggiornato. modello
+ ImageNet1K\_mean.xml
+ modello sottoposto a training
+ Resnet\_101\_aggiornato. modello
+ Resnet\_18\_-aggiornato. modello
+ Resnet\_50\_aggiornato. modello

Se i modelli sono già installati, proseguire con il [passaggio di convalida](#verify) per confermare la disponibilità.

## <a name="download-the-installation-script"></a>Scaricare lo script di installazione

Fare [https://aka.ms/mlm4sql](https://aka.ms/mlm4sql) clic per scaricare il file **Install-MLModels. ps1**.

## <a name="execute-with-elevated-privileges"></a>Esegui con privilegi elevati

1. Avviare PowerShell. Sulla barra delle applicazioni fare clic con il pulsante destro del mouse sull'icona del programma PowerShell e scegliere **Esegui come amministratore**.
2. Immettere il percorso completo del file script di installazione e includere il nome dell'istanza. Supponendo che la cartella Downloads e un'istanza predefinita, il comando potrebbe essere simile al seguente:

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**Output**

In una SQL Server connessa a Internet 2017 Machine Learning istanza predefinita con R e Python, verranno visualizzati messaggi simili al seguente.

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

Per prima cosa, cercare i nuovi file nella [cartella mxlibs](#file-location). Eseguire quindi il codice demo per verificare che i modelli siano installati e funzionanti. 

### <a name="r-verification-steps"></a>Passaggi di verifica R

1. Avviare **RGUI. EXE** in C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\bin\x64.

2. Incollare il seguente script R al prompt dei comandi.

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

3. Premere INVIO per visualizzare i punteggi dei sentimenti. L'output dovrebbe essere il seguente:

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

### <a name="python-verification-steps"></a>Passaggi di verifica Python

1. Avviare **Python. exe** in C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES.

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

3. Premere INVIO per stampare i punteggi. L'output dovrebbe essere il seguente:

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> Se gli script demo hanno esito negativo, controllare prima il percorso del file. Nei sistemi con più istanze di SQL Server o per istanze che vengono eseguite side-by-side con versioni autonome, è possibile che lo script di installazione legga erroneamente l'ambiente e inserisca i file nel percorso errato. In genere, la copia manuale dei file nella cartella mxlib corretta corregge il problema.

## <a name="examples-using-pre-trained-models"></a>Esempi di utilizzo di modelli con training preliminare

Il collegamento seguente include il codice di esempio che richiama i modelli sottoposti a training.

+ [Esempio di codice: Analisi del sentiment tramite testo Featurizer](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>Ricerca e risorse

Attualmente i modelli disponibili sono modelli DNN (Deep Neural Network) per l'analisi dei sentimenti e la classificazione delle immagini. Tutti i modelli con training preliminare sono stati sottoposti a training tramite Microsoft [computing network Toolkit](https://cntk.ai/Features/Index.html), o **CNTK**.

La configurazione di ogni rete è basata sulle implementazioni di riferimento seguenti:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Per altre informazioni sugli algoritmi usati in questi modelli di apprendimento avanzato e sul modo in cui vengono implementati e sottoposti a training usando CNTK, vedere questi articoli:

+ [Il set di algoritmi di Microsoft ricercatori ' imposta l'attività cardine Challenge](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft computazionale Network Toolkit offre prestazioni di calcolo di apprendimento avanzato distribuite più efficienti](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>Vedere anche

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md)
+ [Aggiornare i componenti R e Python in istanze di SQL Server](../install/upgrade-r-and-python.md)
+ [Pacchetto MicrosoftML per R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [pacchetto microsoftml per Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
