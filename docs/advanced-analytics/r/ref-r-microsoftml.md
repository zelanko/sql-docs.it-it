---
title: Libreria di funzioni MicrosoftML R
description: Introduzione alla libreria di funzioni MicrosoftML in SQL Server 2016 R Services e SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2cf89b26ffad2902223a84e19ccaf425aa6f8b2d
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344902"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (libreria R in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML** è una libreria di funzioni R offerta da Microsoft che fornisce algoritmi di apprendimento automatico a prestazioni elevate. Include funzioni per il training e le trasformazioni, l'assegnazione di punteggi, l'analisi di testo e immagini e l'estrazione delle funzionalità per la derivazione di valori da dati esistenti.

Le API di Machine Learning sono state sviluppate da Microsoft per le applicazioni di Machine Learning interne e sono state perfezionate nel corso degli anni per supportare prestazioni elevate in Big Data, usando l'elaborazione multicore e il flusso rapido dei dati. MicrosoftML include inoltre numerose trasformazioni per l'elaborazione di testo e immagini.

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

La libreria **MicrosoftML** viene distribuita in più prodotti Microsoft, ma l'utilizzo è lo stesso se si ottiene la libreria in SQL Server o in un altro prodotto. Poiché le funzioni sono uguali, la [documentazione per le singole funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) viene pubblicata in una sola posizione sotto il [riferimento R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per Microsoft Machine Learning server. Se sono presenti comportamenti specifici del prodotto, le discrepanze verranno indicate nella pagina della guida della funzione.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

La libreria **MicrosoftML** è basata su R 3.4.3 ed è disponibile solo quando si installa uno dei seguenti prodotti o download Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> Le versioni di rilascio complete del prodotto sono solo Windows, a partire da SQL Server 2017. Il supporto Linux per **MicrosoftML** è una novità di [SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dipendenze del pacchetto

Gli algoritmi in **MicrosoftML** dipendono da [RevoScaleR](ref-r-revoscaler.md) per:

+ Oggetti origine dati. I dati utilizzati dalle funzioni **MicrosoftML** vengono creati utilizzando le funzioni **RevoScaleR** .
+ Elaborazione remota (spostamento dell'esecuzione della funzione a un'istanza di SQL Server remota). La libreria **RevoScaleR** fornisce funzioni per la creazione e l'attivazione di un contesto di calcolo remoto per SQL Server.

Nella maggior parte dei casi, i pacchetti verranno caricati insieme quando si usa **MicrosoftML**.

## <a name="functions-by-category"></a>Funzioni per categoria

In questa sezione vengono elencate le funzioni per categoria per fornire un'idea del modo in cui vengono utilizzate. È anche possibile usare il [Sommario](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per trovare le funzioni in ordine alfabetico.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1-algoritmi di Machine Learning

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | Implementazione di FastRank, un'implementazione efficiente dell'algoritmo di boosting dei gradienti MART.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Implementazione di una foresta casuale e di una foresta di regressione quantile usando [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees).  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Regressione logistica con L-BFGS.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | Macchine a vettori di supporto di una classe.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | Rete neurale binaria, multiclasse e regressione.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | Ottimizzazione di scala doppia coordinata stocastica per la classificazione e la regressione binarie lineari. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | Consente di eseguire il training di un numero di modelli di vario tipo per ottenere prestazioni predittive migliori rispetto a quelle ottenute da un singolo modello.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2-funzioni di trasformazione

| Nome funzione | Descrizione |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | Trasformazione per creare una singola colonna con valori di vettore da più colonne.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | Crea Vector indicatore usando la trasformazione categorica con Dictionary.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | Converte il valore categorico in una matrice di indicatori mediante hashing. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | Produce un contenitore di conteggi di sequenze di parole consecutive, denominate n-grammi, da un corpus di testo specificato. Offre funzionalità di rilevamento, suddivisione in token, rimozione parole non significative, normalizzazione del testo e generazione di funzionalità.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | Assegna un punteggio al testo in linguaggio naturale e crea una colonna contenente le probabilità che le opinioni nel testo siano positive.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | consente di definire argomenti per l'estrazione di funzioni basate su conteggi e hash.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | Seleziona un set di colonne di cui ripetere il training, eliminando tutti gli altri. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | Consente di selezionare le funzionalità delle variabili specificate utilizzando una modalità specificata.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | Carica i dati dell'immagine.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | Ridimensiona un'immagine in una dimensione specificata usando un metodo di ridimensionamento specificato.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | Estrae i valori dei pixel da un'immagine.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | Featurizes un'immagine usando un modello di rete neurale prolungata con training preliminare.|


## <a name="3-scoring-and-training-functions"></a>3-funzioni di assegnazione di punteggi e training

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | Esegue la libreria di assegnazione dei punteggi da SQL Server, usando il stored procedure o dal codice R che consente il punteggio in tempo reale per garantire prestazioni di stima molto più veloci.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | Trasforma i dati da un set di dati di input a un set di dati di output.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Fornisce un riepilogo di un modello Microsoft R Machine Learning.|


## <a name="4-loss-functions-for-classification-and-regression"></a>4-funzioni di perdita per la classificazione e la regressione

| Nome funzione | Descrizione |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita di classificazione esponenziale. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita della classificazione dei log.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita della classificazione cerniera. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita della classificazione Smooth cerniera.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita di regressione di Poisson. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita di regressione quadrata.   |   

## <a name="5-feature-selection-functions"></a>5-funzioni di selezione delle funzioni

| Nome funzione | Descrizione |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | Specifica per la selezione delle funzioni in modalità conteggio. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | Specifica per la selezione delle funzioni in modalità reciproca. |

## <a name="6-ensemble-modeling-functions"></a>6-funzioni di modellazione Ensemble

| Nome funzione | Descrizione |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | Crea un elenco contenente il nome della funzione e gli argomenti per eseguire il training di un modello di albero rapido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Crea un elenco contenente il nome della funzione e gli argomenti per eseguire il training di un modello di foresta veloce con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | Crea un elenco contenente il nome della funzione e gli argomenti per eseguire il training di un modello lineare veloce con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Crea un elenco contenente il nome della funzione e gli argomenti per eseguire il training di un modello di regressione logistica con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | Crea un elenco contenente il nome della funzione e gli argomenti per eseguire il training di un modello OneClassSvm con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|

## <a name="7-neural-networking-functions"></a>7-funzioni di rete neurale

| Nome funzione | Descrizione |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | Specifica gli algoritmi di ottimizzazione per l'algoritmo di Machine Learning [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) .|


## <a name="8-package-state-functions"></a>8-funzioni di stato del pacchetto

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | Oggetto ambiente utilizzato per archiviare lo stato a livello di pacchetto. |


## <a name="how-to-use-microsoftml"></a>Come usare MicrosoftML

Le funzioni in **MicrosoftML** possono essere richiamate nel codice R incapsulato nelle stored procedure. La maggior parte degli sviluppatori compila le soluzioni **MicrosoftML** localmente e quindi esegue la migrazione del codice R completato alle stored procedure come esercizio di distribuzione.

Il pacchetto **MicrosoftML** per R è installato "all'interno di SQL Server 2017. È anche disponibile per l'uso con SQL Server 2016 se si aggiornano i componenti R per l'istanza: [Aggiornare un'istanza di SQL Server usando binding](../install/upgrade-r-and-python.md)

Il pacchetto non è caricato per impostazione predefinita. Come primo passaggio, caricare il pacchetto **MicrosoftML** e quindi caricare **RevoScaleR** se è necessario usare contesti di calcolo remoti o oggetti di connettività o origine dati correlati. Quindi, fare riferimento alle singole funzioni necessarie.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di R](../tutorials/sql-server-r-tutorials.md)
+ [Informazioni su come usare i contesti di calcolo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R per sviluppatori SQL: Eseguire il training e il rendere operativo di un modello](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Esempi di prodotti Microsoft su GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Guida di riferimento a R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 