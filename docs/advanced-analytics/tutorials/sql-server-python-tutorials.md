---
title: Panoramica dell'esercitazione su Python SQL Server 2017
description: Introduzione alle esercitazioni su Python per l'analisi del database SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86c5eaa600da0dbe9106278dd36b21eba322e2b7
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345970"
---
# <a name="sql-server-2017-python-tutorials"></a>Esercitazioni su Python SQL Server 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive le esercitazioni di Python per l'analisi del database in [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md). 

+ Informazioni su come eseguire il wrapping e l'esecuzione di codice Python nelle stored procedure.
+ Serializzare e salvare i modelli basati su Python per SQL Server database.
+ Informazioni sui contesti di calcolo locali e remoti e su quando usarli.
+ Esplora i moduli Microsoft Python per le attività di data science e machine learning.

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Guide introduttive ed esercitazioni su Python

| Collegamento | Descrizione |
|------|-------------|
| [Avvio rapido: Script Python "Hello World" in SQL Server](quickstart-python-run-using-t-sql.md) | Informazioni di base su come chiamare Python in T-SQL. |
| [Avvio rapido: Creare, eseguire il training e usare un modello Python con stored procedure in SQL Server](quickstart-python-train-score-in-tsql.md) | Vengono illustrati i meccanismi di incorporamento del codice Python in una stored procedure, fornendo input e stored procedure l'esecuzione. |
| [Esercitazione: Creare un modello usando revoscalepy](use-python-revoscalepy-to-create-model.md) | Viene illustrato come eseguire il codice da un terminale Python remoto, usando SQL Server contesto di calcolo. È necessario avere familiarità con gli strumenti e gli ambienti Python. Viene fornito codice di esempio che consente di creare un modello utilizzando **rxLinMod**dalla nuova libreria **revoscalepy** . |
| [Esercitazione: Informazioni su Python Analytics in-database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md) | Questa procedura dettagliata end-to-end illustra il processo di creazione di una soluzione Python completa con le stored procedure T-SQL. Tutto il codice Python è incluso.|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Esempi di codice

Questi esempi e demo forniti dal team di sviluppo SQL Server evidenziano i modi in cui è possibile usare l'analisi incorporata in applicazioni reali.

| Collegamento | Descrizione |
|------|-------------|
| [Creazione di un modello predittivo con Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Scopri in che modo un'azienda di noleggio di sci può usare Machine Learning per prevedere i noleggi futuri, che consente al piano aziendale e al personale di soddisfare la domanda futura. |
| [Eseguire il clustering dei clienti con Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Informazioni su come usare l'algoritmo Kmeans per eseguire il clustering senza supervisione dei clienti. |

## <a name="see-also"></a>Vedere anche

+ [Estensione Python per SQL Server](../concepts/extension-python.md)
+ [Esercitazioni SQL Server Machine Learning Services](machine-learning-services-tutorials.md)
