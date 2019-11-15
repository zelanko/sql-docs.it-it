---
title: Esercitazioni di Python
description: Questo articolo descrive le esercitazioni di Python per Machine Learning Services per SQL Server. Informazioni su come eseguire script Python. Compilare, eseguire il training e distribuire modelli Python in SQL Server. Informazioni sui contesti di calcolo remoti e locali. Esplorare i pacchetti Microsoft Python per le attività di data science e Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 80f714810acd8c04c80fe0b8abe5214a456f6dd6
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199401"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>Esercitazioni di Python per Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive le esercitazioni e gli argomenti di avvio rapido di Python per [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md).

+ Informazioni su come eseguire script Python.
+ Compilare, eseguire il training e distribuire modelli Python in SQL Server.
+ Informazioni sui contesti di calcolo remoti e locali.
+ Esplorare i pacchetti Microsoft Python per le attività di data science e Machine Learning.

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Esercitazioni di Python

| Esercitazione | Descrizione |
|-|-|
| [Stimare il noleggio di sci tramite la regressione lineare](python-ski-rental-linear-regression.md) | Usare Python e la regressione lineare per stimare il numero di noleggi di sci. Usare notebook in Azure Data Studio per preparare i dati ed eseguire il training del modello e T-SQL per distribuire il modello. |
| [Categorizzazione dei clienti tramite clustering K-means](python-clustering-model.md) | Usare Python per sviluppare e distribuire un modello di clustering K-means per categorizzare i clienti. Usare notebook in Azure Data Studio per preparare i dati ed eseguire il training del modello e T-SQL per distribuire il modello. |
| [Creare un modello tramite revoscalepy](use-python-revoscalepy-to-create-model.md) | Illustra come eseguire codice da un client Python remoto usando SQL Server come contesto di calcolo. Nell'esercitazione viene creato un modello usando **rxLinMod** dalla libreria **revoscalepy**. |
| [Analisi dei dati Python per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md) | Questa procedura dettagliata end-to-end illustra il processo di creazione di una soluzione Python completa con T-SQL. |

## <a name="python-quickstarts"></a>Avvio rapido di Python

Se non si ha familiarità con Machine Learning Services per SQL Server, è possibile provare anche gli argomenti di avvio rapido di Python.

| Guida introduttiva | Descrizione |
|-|-|
| [Hello World in Python e SQL Server](quickstart-python-create-script.md) | Informazioni di base su come chiamare Python in T-SQL usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Gestire tipi di dati e oggetti usando Python in SQL Server](quickstart-python-data-structures.md) | Descrive come SQL Server usa il pacchetto pandas di Python per gestire strutture di dati. |
| [Creare e assegnare i punteggi a un modello predittivo in Python](quickstart-python-train-score-model.md) | Illustra come creare, eseguire il training e usare un modello Python per effettuare stime a partire da nuovi dati. |

## <a name="next-steps"></a>Passaggi successivi

+ [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
+ [Estensione Python in SQL Server](../concepts/extension-python.md)