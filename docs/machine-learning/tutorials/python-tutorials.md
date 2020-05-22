---
title: Esercitazioni di Python
titleSuffix: SQL machine learning
description: Questo articolo descrive le esercitazioni di Python per Machine Learning in SQL. Informazioni su come eseguire gli script e creare modelli di Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7127be209c9637eb0c1cc701d16f0d157f90be54
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83605793"
---
# <a name="python-tutorials-for-sql-machine-learning"></a>Esercitazioni di Python per Machine Learning in SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Questo articolo descrive le esercitazioni e gli argomenti di avvio rapido di Python per [Machine Learning Services in SQL Server](../sql-server-machine-learning-services.md) e in [cluster Big Data](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Questo articolo descrive le esercitazioni e gli argomenti di avvio rapido di Python per [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md).
::: moniker-end

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Esercitazioni di Python

| Esercitazione | Descrizione |
|-|-|
| [Stimare il noleggio di sci tramite la regressione lineare](python-ski-rental-linear-regression.md) | Usare Python e la regressione lineare per stimare il numero di noleggi di sci. Usare notebook in Azure Data Studio per preparare i dati ed eseguire il training del modello e T-SQL per distribuire il modello. |
| [Categorizzazione dei clienti tramite clustering K-means](python-clustering-model.md) | Usare Python per sviluppare e distribuire un modello di clustering K-means per categorizzare i clienti. Usare notebook in Azure Data Studio per preparare i dati ed eseguire il training del modello e T-SQL per distribuire il modello. |
| [Creare un modello tramite revoscalepy](use-python-revoscalepy-to-create-model.md) | Illustra come eseguire codice da un client Python remoto usando SQL Server come contesto di calcolo. Nell'esercitazione viene creato un modello usando **rxLinMod** dalla libreria **revoscalepy**. |
| [Analisi dei dati Python per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md) | Questa procedura dettagliata end-to-end illustra il processo di creazione di una soluzione Python completa con T-SQL. |

## <a name="python-quickstarts"></a>Avvio rapido di Python

Se non si ha familiarità con Machine Learning in SQL, è possibile provare anche gli argomenti di avvio rapido di Python.

| Guida introduttiva | Descrizione |
|-|-|
| [Eseguire script Python semplici](quickstart-python-create-script.md) | Informazioni di base su come chiamare Python in T-SQL usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Strutture di dati e oggetti con Python](quickstart-python-data-structures.md) | Descrive come SQL usa il pacchetto pandas di Python per gestire strutture di dati. |
| [Creare e assegnare i punteggi a un modello predittivo in Python](quickstart-python-train-score-model.md) | Illustra come creare, eseguire il training e usare un modello Python per effettuare stime a partire da nuovi dati. |

## <a name="next-steps"></a>Passaggi successivi

+ [Estensione Python in SQL Server](../concepts/extension-python.md)
