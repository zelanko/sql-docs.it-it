---
title: pacchetto Python microsoftml - servizi di SQL Server Machine Learning
description: Modelli per Python, in relazione ai carichi di lavoro di SQL Server machine learning e introduce il Microsoft algoritmi di machine learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8f4c0eb20b0e0cd64065c7db0687b1dc36b2dbe7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962753"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (modulo di Python in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**microsoftml** è un modulo Python35 compatibile di Microsoft che fornisce algoritmi di apprendimento automatico ad alte prestazioni. Include funzioni per il training e le trasformazioni, assegnazione dei punteggi, analisi del testo e immagine ed estrazione di funzioni per la derivazione di valori da dati esistenti.

Di machine learning le API sono state sviluppate da Microsoft per applicazioni interne di machine learning e sono state perfezionate nel corso degli anni per supportare prestazioni elevate sui big data, tramite l'elaborazione multicore e flusso rapido dei dati. Questo pacchetto ha avuto origine come equivalente di una versione di R, Python [MicrosoftML](../r/ref-r-microsoftml.md), che ha funzioni simili. 

## <a name="full-reference-documentation"></a>Documentazione di riferimento complete

Il **microsoftml** libreria distribuita in vari prodotti Microsoft, ma che utilizzo è lo stesso sia ottenere la libreria in SQL Server o un altro prodotto. Perché le funzioni sono uguali, [documentazione per le funzioni di microsoftml singoli](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) pubblicata in un'unica posizione sotto il [riferimento Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per Microsoft Machine Learning Server. Qualsiasi prodotto specifico deve comportamenti esistono, verranno indicate nella pagina della Guida funzione discrepanze.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

Il **microsoftml** modulo è basata su Python 3.5 e disponibile solo quando si installa uno dei seguenti prodotti Microsoft o download:

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Librerie client Python per un client di data science](setup-python-client-tools-sql.md)

> [!NOTE]
> Sono versioni di rilascio versione completa del prodotto Windows sola, a partire da SQL Server 2017. Il supporto per Linux **microsoftml** sono le novità [anteprima di SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dipendenze dei pacchetti

Gli algoritmi **microsoftml** dipendono [revoscalepy](ref-py-revoscalepy.md) per:

+ Oggetti origine dei dati. Dati utilizzati dalle **microsoftml** le funzioni vengono create utilizzando **revoscalepy** funzioni.
+ Remote computing (mutevoli l'esecuzione della funzione a un'istanza remota di SQL Server). Il **revoscalepy** libreria fornisce funzioni per la creazione e l'attivazione di un server remoto di calcolo scelta per SQL server.

Nella maggior parte dei casi, si caricherà i pacchetti insieme ogni volta che si usa **microsoftml**.

## <a name="functions-by-category"></a>Funzioni per categoria

In questa sezione elenca le funzioni in base alla categoria per farsi un'idea dell'utilizzo di ciascuna di esse. È anche possibile usare la [sommario](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per trovare le funzioni in ordine alfabetico.

## <a name="1-training-functions"></a>1-training di funzioni

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | Eseguire il training di un insieme di modelli. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | Foresta casuale. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | Modello lineare. con Stochastic Dual Ascent di Coordinate. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | Alberi con Boosting. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | Regressione logistica. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | Rete neurale. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | Rilevamento delle anomalie. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>Funzioni di 2-trasformazione

### <a name="categorical-variable-handling"></a>Gestione di variabili categorica

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | Converte una colonna di testo in categorie. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | Genera un hash e consente di convertire una colonna di testo in categorie. |

### <a name="schema-manipulation"></a>Modificare lo schema

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | Concatena più colonne in un singolo vettore. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | Elimina le colonne da un set di dati. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | Consente di mantenere le colonne di un set di dati. |


### <a name="variable-selection"></a>selezione di variabili

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |Selezione di funzionalità basato su conteggi. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | Selezione di funzionalità basato sull'informazione mutua in base. |


### <a name="text-analytics"></a>Analitica di testo

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | Converte le colonne di testo in funzioni numeriche. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | Analisi del sentiment. |


### <a name="image-analytics"></a>Analitica immagine 

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | Carica un'immagine. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | Ridimensiona un'immagine. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | Estrae pixel da un'immagine. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Converte un'immagine in funzionalità. |

### <a name="featurization-functions"></a>Funzioni di definizione delle funzionalità

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | Trasformazione dei dati per le origini dati |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>Funzioni di assegnazione dei punteggi di 3

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Punteggi tramite un modello di Microsoft machine learning |

## <a name="how-to-call-microsoftml"></a>Come chiamare microsoftml

Le funzioni nello **microsoftml** possono essere chiamati nel codice Python incapsulato nelle stored procedure. La maggior parte degli sviluppatori di compilare **microsoftml** soluzioni in locale, e quindi eseguire la migrazione di codice Python alle stored procedure come un esercizio di distribuzione.

Il **microsoftml** del pacchetto Python è installato per impostazione predefinita, ma a differenza **revoscalepy**, non è caricato per impostazione predefinita quando si avvia una sessione di Python tramite i file eseguibili di Python installati con SQL Server.

Innanzitutto, importare il **microsoftml** del pacchetto e importare **revoscalepy** se è necessario usare contesti di calcolo remoti o sugli oggetti origine dati o di connettività correlati. Quindi, fare riferimento a singole funzioni che è necessario.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di Python](../tutorials/sql-server-python-tutorials.md)
+ [Esercitazione: Incorporare il codice Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Riferimento di Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

