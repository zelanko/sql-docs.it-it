---
title: Pacchetto microsoftml per Python
description: microsoftml è un pacchetto Python di Microsoft che fornisce algoritmi di Machine Learning con prestazioni elevate. Include funzioni per il training e le trasformazioni, l'assegnazione dei punteggi, l'analisi di testo e immagini e l'estrazione di caratteristiche per la derivazione di valori da dati esistenti. Il pacchetto è incluso in Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c638b3c32af037b8c597c840d4bdf388aad56efc
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178588"
---
# <a name="microsoftml-python-package-in-sql-server-machine-learning-services"></a>microsoftml (pacchetto Python in Machine Learning Services per SQL Server)
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

**microsoftml** è un pacchetto Python di Microsoft che fornisce algoritmi di Machine Learning con prestazioni elevate. Include funzioni per il training e le trasformazioni, l'assegnazione dei punteggi, l'analisi di testo e immagini e l'estrazione di caratteristiche per la derivazione di valori da dati esistenti. Il pacchetto è incluso in [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md) e offre prestazioni elevate per i Big Data, con l'elaborazione multicore e un flusso dei dati rapido.

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

Il pacchetto **microsoftml** è distribuito in più prodotti Microsoft, ma l'utilizzo è lo stesso indipendentemente dal fatto che sia incluso in SQL Server o in un altro prodotto. Poiché le funzioni sono le stesse, la [documentazione per le singole funzioni di microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) viene pubblicata in una sola posizione nelle [informazioni di riferimento per Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per Microsoft Machine Learning Server. In caso di comportamenti specifici per un prodotto, le discrepanze verranno indicate nella pagina della Guida delle funzioni in questione.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

Il modulo **microsoftml** è basato su Python 3.5 ed è disponibile solo quando si installa uno dei prodotti o download Microsoft seguenti:

+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Librerie client Python per un client di data science](setup-python-client-tools-sql.md)

> [!NOTE]
> Le versioni complete del prodotto sono solo per Windows in SQL Server 2017. Sia Windows che Linux sono supportati per **microsoftml** in [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dipendenze dei pacchetti

Gli algoritmi in **microsoftml** dipendono da [revoscalepy](ref-py-revoscalepy.md) per:

+ Oggetti di origine dati. I dati utilizzati dalle funzioni di **microsoftml** vengono creati usando le funzioni di **revoscalepy**.
+ Elaborazione remota (spostamento dell'esecuzione delle funzioni in un'istanza di SQL Server remota). Il pacchetto **revoscalepy** fornisce funzioni per la creazione e l'attivazione di un contesto di calcolo remoto per SQL Server.

Nella maggior parte dei casi, i pacchetti vengono caricati insieme ogni volta che si usa **microsoftml**.

## <a name="functions-by-category"></a>Funzioni per categoria

Questa sezione elenca le funzioni per categoria per offrire un'idea di come vengono usate. È anche possibile usare il [sommario](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per trovare le funzioni in ordine alfabetico.

## <a name="1-training-functions"></a>1 - Funzioni di training

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | Esegue il training di un insieme di modelli. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | Foresta casuale. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | Modello lineare con crescita a doppia coordinata stocastica. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | Alberi con boosting. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | Regressione logistica. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | Rete neurale. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | Rilevamento di anomalie. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2 - Funzioni di trasformazione

### <a name="categorical-variable-handling"></a>Gestione delle variabili di categoria

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
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |Seleziona le caratteristiche in base a conteggi. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | Seleziona le caratteristiche in base a informazioni reciproche. |


### <a name="text-analytics"></a>Analisi del testo

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | Converte le colonne di testo in caratteristiche numeriche. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | Esegue l'analisi del sentiment. |


### <a name="image-analytics"></a>Analisi delle immagini 

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | Carica un'immagine. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | Ridimensiona un'immagine. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | Estrae i pixel da un'immagine. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Converte un'immagine in caratteristiche. |

### <a name="featurization-functions"></a>Funzioni di definizione delle caratteristiche

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | Trasformazione dei dati per le origini dati |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3 - Funzioni di assegnazione dei punteggi

| Funzione | Descrizione |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Assegna punteggi usando un modello di Machine Learning Microsoft |

## <a name="how-to-call-microsoftml"></a>Come chiamare microsoftml

Le funzioni in **microsoftml** possono essere chiamate nel codice Python incapsulato nelle stored procedure. La maggior parte degli sviluppatori compila in locale le soluzioni **microsoftml** e quindi esegue la migrazione del codice Python completato alle stored procedure, come esercizio di distribuzione.

Il pacchetto **microsoftml** per Python viene installato per impostazione predefinita, ma a differenza di **revoscalepy**, non viene caricato per impostazione predefinita quando si avvia una sessione Python usando i file eseguibili di Python installati con SQL Server.

Per prima cosa, importare il pacchetto **microsoftml** e quindi importare **revoscalepy** se è necessario usare contesti di calcolo remoti oppure oggetti di origine dati o connettività correlati. Fare quindi riferimento alle singole funzioni necessarie.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di Python](../tutorials/sql-server-python-tutorials.md)
+ [Informazioni di riferimento su Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

