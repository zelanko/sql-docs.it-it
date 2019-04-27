---
title: Libreria di funzioni di MicrosoftML R - servizi di SQL Server Machine Learning
description: Introduzione alla libreria di funzioni di MicrosoftML in SQL Server 2016 R Services e SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 73d9dcf56c0eb5e69704adf169946f6aa28a432c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641819"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (libreria R in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML** è una libreria di funzioni R da Microsoft che fornisce algoritmi di apprendimento automatico ad alte prestazioni. Include funzioni per il training e le trasformazioni, assegnazione dei punteggi, analisi del testo e immagine ed estrazione di funzioni per la derivazione di valori da dati esistenti.

Di machine learning le API sono state sviluppate da Microsoft per le applicazioni di apprendimento interne e sono state perfezionate nel corso degli anni per supportare prestazioni elevate sui big data, tramite l'elaborazione multicore e flusso rapido dei dati. MicrosoftML include anche numerose trasformazioni per l'elaborazione di immagini e testo.

## <a name="full-reference-documentation"></a>Documentazione di riferimento complete

Il **MicrosoftML** libreria distribuita in vari prodotti Microsoft, ma che utilizzo è lo stesso sia ottenere la libreria in SQL Server o un altro prodotto. Perché le funzioni sono uguali, [documentazione per le singole funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) pubblicata in un'unica posizione sotto il [riferimento R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per Microsoft Machine Learning Server. Qualsiasi prodotto specifico deve comportamenti esistono, verranno indicate nella pagina della Guida funzione discrepanze.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

Il **MicrosoftML** libreria è basata su R 3.4.3 e disponibile solo quando si installa uno dei seguenti prodotti Microsoft o download:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> Sono versioni di rilascio versione completa del prodotto Windows sola, a partire da SQL Server 2017. Il supporto per Linux **MicrosoftML** sono le novità [anteprima di SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dipendenze dei pacchetti

Gli algoritmi **MicrosoftML** dipendono [RevoScaleR](ref-r-revoscaler.md) per:

+ Oggetti origine dei dati. Dati utilizzati dalle **MicrosoftML** le funzioni vengono create utilizzando **RevoScaleR** funzioni.
+ Remote computing (mutevoli l'esecuzione della funzione a un'istanza remota di SQL Server). Il **RevoScaleR** libreria fornisce funzioni per la creazione e l'attivazione di un server remoto di calcolo scelta per SQL server.

Nella maggior parte dei casi, si caricherà i pacchetti insieme ogni volta che si usa **MicrosoftML**.

## <a name="functions-by-category"></a>Funzioni per categoria

In questa sezione elenca le funzioni in base alla categoria per farsi un'idea dell'utilizzo di ciascuna di esse. È anche possibile usare la [sommario](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per trovare le funzioni in ordine alfabetico.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>Algoritmi di apprendimento di 1

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | Un'implementazione di FastRank, un'implementazione efficiente dell'algoritmo di Boosting dei gradienti MART.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Una foresta casuale e implementazione di foresta regressione Quantile tramite [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees).  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Regressione logistica con L-BFGS.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | Macchine a vettori di supporto di una classe.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | Binaria e multiclasse regressione rete neurale.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | Ottimizzazione stochastic dual ascent di coordinate per lineare classificazione binaria e regressione. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | Esegue il training di un numero di modelli di vari tipi di ottenere migliore prestazioni predittive quanto è stato possibile ottenere da un singolo modello.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>Funzioni di 2-trasformazione

| Nome funzione | Descrizione |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | Trasformazione per creare una singola colonna con valori di vector da più colonne.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | Creare vettore indicatore usando trasformazione categorici con oggetto dictionary.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | Converte il valore categorico in una matrice indicatore eseguendo l'hashing. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | Produce un elenco di conteggi delle sequenze di parole consecutive, chiamate n-grammi, da un corpo di testo specificato. Offre il rilevamento della lingua, la suddivisione in token, la rimozione di parole non significative, normalizzazione del testo e generazione di funzionalità.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | Assegna un punteggio a testo in linguaggio naturale e consente di creare una colonna che contiene le probabilità che le valutazioni del testo sono positive.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | Consente di definire gli argomenti per l'estrazione di funzioni basata sui conteggi e basato su hash.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | Seleziona un set di colonne per ripetere il training, l'eliminazione di tutti gli altri. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | Seleziona le funzionalità tra le variabili specificate utilizzando una modalità specificata.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | Carica i dati dell'immagine.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | Ridimensiona un'immagine da una dimensione specificata usando un metodo di ridimensionamento specificato.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | Estrae i valori di pixel da un'immagine.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | Tutto un'immagine utilizzando un modello di rete neurale profonda con training preliminare.|


## <a name="3-scoring-and-training-functions"></a>Funzioni di training e assegnazione dei punteggi di 3

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | Esegue la libreria di assegnazione dei punteggi da SQL Server, tramite la stored procedure, o dal codice R, l'abilitazione di assegnazione dei punteggi in tempo reale offrire prestazioni molto più veloce di stima.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | Trasforma i dati da un set di dati di input a un set di dati di output.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Fornisce un riepilogo di un modello di Machine Learning di Microsoft R.|


## <a name="4-loss-functions-for-classification-and-regression"></a>4-perdita funzioni per la classificazione e regressione

| Nome funzione | Descrizione |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita di classificazione esponenziale. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita di classificazione di log.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita cardine classificazione. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita cardine smooth classificazione.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita di regressione di poisson. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Specifiche per la funzione di perdita al quadrato di regressione.   |   

## <a name="5-feature-selection-functions"></a>Funzioni di selezione delle caratteristiche di 5

| Nome funzione | Descrizione |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | Specifica per la selezione di funzionalità in modalità di conteggio. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | Specifica per la selezione di funzionalità in modalità basato sull'informazione mutua. |

## <a name="6-ensemble-modeling-functions"></a>Funzioni di modellazione dell'insieme-6

| Nome funzione | Descrizione |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | Crea un elenco che contiene il nome della funzione e gli argomenti per il training di un modello di albero rapida con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Crea un elenco che contiene il nome della funzione e gli argomenti per il training di un modello di foresta rapida con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | Crea un elenco che contiene il nome della funzione e gli argomenti per il training di un modello di apprendimento lineare rapido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Crea un elenco che contiene il nome della funzione e gli argomenti per il training di un modello di regressione logistica con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | Crea un elenco che contiene il nome della funzione e gli argomenti per il training di un modello OneClassSvm con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|

## <a name="7-neural-networking-functions"></a>Funzioni di rete neurale a 7

| Nome funzione | Descrizione |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | Specifica gli algoritmi di ottimizzazione per la [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) algoritmo di machine learning.|


## <a name="8-package-state-functions"></a>Funzioni dello stato di 8-package

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | Un oggetto ambiente usato per archiviare lo stato a livello di pacchetto. |


## <a name="how-to-use-microsoftml"></a>Come usare MicrosoftML

Le funzioni nello **MicrosoftML** possono essere chiamati nel codice R è incapsulato in stored procedure. La maggior parte degli sviluppatori di compilare **MicrosoftML** soluzioni in locale, e quindi eseguire la migrazione di codice R completato alle stored procedure come un esercizio di distribuzione.

Il **MicrosoftML** dal pacchetto per R è installato "out-of-the-box" in SQL Server 2017. È anche disponibile per l'uso con SQL Server 2016 se si aggiornano i componenti di R per l'istanza: [Aggiornare un'istanza di SQL Server utilizzando l'associazione](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

Il pacchetto non è caricato per impostazione predefinita. Come primo passaggio, caricare il **MicrosoftML** del pacchetto e quindi caricare **RevoScaleR** se è necessario usare contesti di calcolo remoti o sugli oggetti origine dati o di connettività correlati. Quindi, fare riferimento a singole funzioni che è necessario.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di R](../tutorials/sql-server-r-tutorials.md)
+ [Informazioni su come usare contesti di calcolo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R per sviluppatori SQL: Eseguire il training e come operazionalizzare un modello](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Esempi del prodotto Microsoft su GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Riferimento di R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 