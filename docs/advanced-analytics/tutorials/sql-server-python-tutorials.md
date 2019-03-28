---
title: Panoramica dell'esercitazione di SQL Server 2017 Python - SQL Server Machine Learning
description: Introduzione alle esercitazioni di Python per analitica nel database di SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f31da296bf55b7da55a4e5a8398d411bc5a5b0ea
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510318"
---
# <a name="sql-server-2017-python-tutorials"></a>Esercitazioni di SQL Server 2017 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive le esercitazioni su Python nel database analitica [Machine Learning Services di SQL Server 2017](../install/sql-machine-learning-services-windows-install.md). 

+ Informazioni su come eseguire il wrapping ed eseguire codice Python in stored procedure.
+ Serializzare e salvare i modelli basati su Python in database di SQL Server.
+ Informazioni sui contesti di calcolo remoti e locali e quando utilizzarle.
+ Esplorare i moduli di Python di Microsoft per l'analisi scientifica dei dati e attività di machine learning.

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Esercitazioni e guide introduttive per Python

| Collegamento | Descrizione |
|------|-------------|
| [Guida introduttiva: Script di Python "Hello world" in SQL Server](quickstart-python-run-using-t-sql.md) | Informazioni di base di come chiamare Python in T-SQL. |
| [Guida introduttiva: Creare, eseguire il training e usare un modello Python con le stored procedure in SQL Server](quickstart-python-train-score-in-tsql.md) | Illustra la meccanica dell'incorporamento di codice Python in una stored procedure, fornire gli input e l'esecuzione di stored procedure. |
| [Esercitazione: Creare un modello usando revoscalepy](use-python-revoscalepy-to-create-model.md) | Viene illustrato come eseguire il codice da un terminale Python remoto, usando il contesto di calcolo di SQL Server. Verrà visualizzata una certa familiarità con gli ambienti e gli strumenti Python. Codice di esempio viene specificato che crea un modello utilizzando **rxLinMod**, dalla nuova **revoscalepy** libreria. |
| [Esercitazione: Informazioni su analitica di Python nel Database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md) | Questa procedura dettagliata end-to-end viene illustrato il processo di compilazione di una soluzione completa di Python tramite le procedure di T-SQL archiviate. Tutto il codice Python è incluso.|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Esempi di codice

Questi esempi e demo fornite dal team di sviluppo di SQL Server evidenziano che modo è possibile usare analitica incorporata in applicazioni reali.

| Collegamento | Descrizione |
|------|-------------|
| [Creare un modello predittivo usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Informazioni su come un noleggio di sci potrebbe usare machine learning per prevedere i noleggi futuri, che consente al piano aziendale e personale per soddisfare la domanda futura. |
| [Clienti di eseguire il clustering con Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Informazioni su come usare l'algoritmo Kmeans per eseguire il clustering non supervisionato dei clienti. |

## <a name="see-also"></a>Vedere anche

+ [Estensione di Python per SQL Server](../concepts/extension-python.md)
+ [Esercitazioni di SQL Server Machine Learning Services](machine-learning-services-tutorials.md)
