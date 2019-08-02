---
title: pacchetto python microsoftml
description: Introduce gli algoritmi e i modelli di Microsoft Machine Learning per Python, come correlati a SQL Server carichi di lavoro di machine learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c7e7a25749484ff0db4d133f10862438ae5f8ea1
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715145"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (modulo Python in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**microsoftml** è un modulo compatibile con Python35 di Microsoft che fornisce algoritmi di apprendimento automatico a prestazioni elevate. Include funzioni per il training e le trasformazioni, l'assegnazione di punteggi, l'analisi di testo e immagini e l'estrazione delle funzionalità per la derivazione di valori da dati esistenti.

Le API di Machine Learning sono state sviluppate da Microsoft per le applicazioni di Machine Learning interne e sono state perfezionate nel corso degli anni per supportare prestazioni elevate in Big Data, usando l'elaborazione multicore e il flusso di dati veloce. Questo pacchetto è stato originato come Python equivalente a una versione di R, [MicrosoftML](../r/ref-r-microsoftml.md), con funzioni simili. 

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

La libreria **microsoftml** viene distribuita in più prodotti Microsoft, ma l'utilizzo è lo stesso se si ottiene la libreria in SQL Server o in un altro prodotto. Poiché le funzioni sono uguali, la [documentazione per le singole funzioni microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) viene pubblicata in una sola posizione sotto il [riferimento Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per Microsoft Machine Learning server. Se sono presenti comportamenti specifici del prodotto, le discrepanze verranno indicate nella pagina della guida della funzione.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

Il modulo **microsoftml** è basato su Python 3,5 ed è disponibile solo quando si installa uno dei seguenti prodotti o download Microsoft:

+ [Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Librerie client Python per un client data science](setup-python-client-tools-sql.md)

> [!NOTE]
> Le versioni di rilascio complete del prodotto sono solo Windows, a partire da SQL Server 2017. Il supporto Linux per **microsoftml** è una novità di [SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dipendenze del pacchetto

Gli algoritmi in **microsoftml** dipendono da [revoscalepy](ref-py-revoscalepy.md) per:

+ Oggetti origine dati. I dati utilizzati dalle funzioni **microsoftml** vengono creati utilizzando le funzioni **revoscalepy** .
+ Elaborazione remota (spostamento dell'esecuzione della funzione a un'istanza di SQL Server remota). La libreria **revoscalepy** fornisce funzioni per la creazione e l'attivazione di un contesto di calcolo remoto per SQL Server.

Nella maggior parte dei casi, i pacchetti verranno caricati insieme quando si usa **microsoftml**.

## <a name="functions-by-category"></a>Funzioni per categoria

In questa sezione vengono elencate le funzioni per categoria per fornire un'idea del modo in cui vengono utilizzate. È anche possibile usare il [Sommario](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per trovare le funzioni in ordine alfabetico.

## <a name="1-training-functions"></a>1-funzioni di training

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | Eseguire il training di un insieme di modelli. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | Foresta casuale. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | Modello lineare. con l'ascesa a doppia coordinata stocastica. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | Alberi con boosting. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | Regressione logistica. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | Rete neurale. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | Rilevamento delle anomalie. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-funzioni di trasformazione

### <a name="categorical-variable-handling"></a>Gestione di variabili categoriche

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | Converte una colonna di testo in categorie. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | Esegue l'hashing e converte una colonna di testo in categorie. |

### <a name="schema-manipulation"></a>Manipolazione dello schema

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | Concatena più colonne in un singolo vettore. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | Elimina le colonne da un set di dati. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | Mantiene le colonne di un set di dati. |


### <a name="variable-selection"></a>selezione di variabili

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |Selezione delle funzioni basata sui conteggi. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | Selezione delle funzioni in base alle informazioni reciproche. |


### <a name="text-analytics"></a>Analisi del testo

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | Converte le colonne di testo in funzionalità numeriche. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | Analisi dei sentimenti. |


### <a name="image-analytics"></a>Analisi delle immagini 

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | Carica un'immagine. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | Ridimensiona un'immagine. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | Estrae i pixel da un'immagine. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Converte un'immagine in funzionalità. |

### <a name="featurization-functions"></a>Funzioni conteggi

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | Trasformazione dei dati per le origini dati |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3-funzioni di Punteggio

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Punteggi usando un modello di Microsoft Machine Learning |

## <a name="how-to-call-microsoftml"></a>Come chiamare microsoftml

Le funzioni in **microsoftml** possono essere richiamate nel codice Python incapsulato nelle stored procedure. La maggior parte degli sviluppatori compila le soluzioni **microsoftml** localmente e quindi esegue la migrazione del codice Python completato alle stored procedure come esercizio di distribuzione.

Il pacchetto **microsoftml** per Python viene installato per impostazione predefinita ma, a differenza di **revoscalepy**, non viene caricato per impostazione predefinita quando si avvia una sessione Python usando i file eseguibili di Python installati con SQL Server.

Come primo passaggio, importare il pacchetto **microsoftml** e importare **revoscalepy** se è necessario usare contesti di calcolo remoti o oggetti di connettività o origine dati correlati. Quindi, fare riferimento alle singole funzioni necessarie.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di Python](../tutorials/sql-server-python-tutorials.md)
+ [Esercitazione: Incorporare codice Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Guida di riferimento a Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

