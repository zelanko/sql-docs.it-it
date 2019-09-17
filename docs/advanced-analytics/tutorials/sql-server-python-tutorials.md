---
title: Esercitazioni di Python
description: Questo articolo descrive le esercitazioni di Python per SQL Server Machine Learning Services. Informazioni su come eseguire gli script Python. Consente di compilare, eseguire il training e distribuire modelli Python per SQL Server. Informazioni sui contesti di calcolo locali e remoti. Esplora i pacchetti Microsoft Python per data science e machine learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cd458727fad637414d7c71865b2633f3caf80175
ms.sourcegitcommit: 949e55b32eff6610087819a93160a35af0c5f1c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/05/2019
ms.locfileid: "70383551"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>Esercitazioni su Python per SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive le esercitazioni e le guide introduttive di Python per [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md).

+ Informazioni su come eseguire gli script Python.
+ Consente di compilare, eseguire il training e distribuire modelli Python per SQL Server.
+ Informazioni sui contesti di calcolo locali e remoti.
+ Esplora i pacchetti Microsoft Python per data science e machine learning.

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Esercitazioni di Python

| Esercitazione | Descrizione |
|-|-|
| [Prevedere il noleggio di sci con regressione lineare](python-ski-rental-linear-regression.md) | Usare Python e la regressione lineare per prevedere il numero di noleggi di sci. Usare i notebook in Azure Data Studio per preparare i dati e il training del modello e T-SQL per la distribuzione del modello. |
| [Categorizzazione dei clienti con il clustering k-means](python-clustering-model.md) | Usare Python per sviluppare e distribuire un modello di clustering K-means per categorizzare i clienti. Usare i notebook in Azure Data Studio per preparare i dati e il training del modello e T-SQL per la distribuzione del modello. |
| [Creare un modello usando revoscalepy](use-python-revoscalepy-to-create-model.md) | Viene illustrato come eseguire il codice da un client Python remoto usando SQL Server come contesto di calcolo. L'esercitazione crea un modello usando **rxLinMod** dalla libreria **revoscalepy** . |
| [Analisi dei dati Python per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md) | Questa procedura dettagliata end-to-end illustra il processo di creazione di una soluzione Python completa con T-SQL. |

## <a name="python-quickstarts"></a>Guide introduttive per Python

Se non si ha familiarità con SQL Server Machine Learning Services, è anche possibile provare le guide introduttive di Python.

| Guida introduttiva | Descrizione |
|-|-|
| [Hello World in Python e SQL Server](quickstart-python-run-using-t-sql.md) | Informazioni di base su come chiamare Python in T-SQL. |
| [Gestire input e output usando Python in SQL Server](quickstart-python-inputs-and-outputs.md) | Informazioni su come gestire input e output per Python in [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Strutture di dati Python in SQL Server](quickstart-python-data-structures.md) | Mostra come SQL Server usa il pacchetto Pandas di Python per gestire le strutture dei dati. |
| [Esegui il training e usa il primo modello](quickstart-python-train-score-in-tsql.md) | Viene illustrato come creare, eseguire il training e usare un modello Python per stimare i nuovi dati. |

## <a name="next-steps"></a>Passaggi successivi

+ [Che cos'è SQL Server Machine Learning Services (Python e R)?](../what-is-sql-server-machine-learning.md)
+ [Estensione Python per SQL Server](../concepts/extension-python.md)