---
title: Esercitazioni di R
titleSuffix: SQL machine learning
description: Questo articolo descrive le esercitazioni di R per Machine Learning in SQL. Informazioni su come eseguire gli script e creare modelli di Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/04/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 63c271c4e1d59c9446495607b42b0b5ad13ea246
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606923"
---
# <a name="r-tutorials-for-sql-machine-learning"></a>Esercitazioni di R per Machine Learning in SQL

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Questo articolo descrive le esercitazioni e gli argomenti di avvio rapido di R per [Machine Learning Services in SQL Server](../sql-server-machine-learning-services.md) e in [cluster Big Data](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Questo articolo descrive le esercitazioni e gli argomenti di avvio rapido di R per [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Questo articolo descrive le esercitazioni e gli argomenti di avvio rapido di R per [R Services per SQL Server 2016](../r/sql-server-r-services.md).
::: moniker-end

<a name="bkmk_sqltutorials"></a>

## <a name="r-tutorials"></a>Esercitazioni di R

| Esercitazione | Descrizione |
|------|-------------|
| [Stimare il noleggio di sci con l'albero delle decisioni](r-predictive-model-introduction.md) | Usare R e un modello di albero delle decisioni per stimare il numero di noleggi di sci in futuro. Usare notebook in Azure Data Studio per preparare i dati ed eseguire il training del modello e T-SQL per distribuire il modello. |
| [Categorizzazione dei clienti tramite clustering K-means](r-clustering-model-introduction.md) | Usare R per sviluppare e distribuire un modello di clustering K-Means per categorizzare i clienti. Usare notebook in Azure Data Studio per preparare i dati ed eseguire il training del modello e T-SQL per distribuire il modello. |
| [Analisi R nel database per data scientist](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Destinata agli sviluppatori R che non hanno familiarità con SQL Server, questa esercitazione illustra come eseguire le principali attività di data science in SQL Server. Descrive come caricare e visualizzare dati, eseguire il training e il salvataggio di un modello in SQL Server e usare il modello per l'analisi predittiva. |
| [Analisi R nel database per sviluppatori SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Fornisce le istruzioni per creare e distribuire una soluzione R completa usando solo strumenti [!INCLUDE[tsql](../../includes/tsql-md.md)]. Descrive nel dettaglio il passaggio di una soluzione all'ambiente di produzione. Si apprenderà come eseguire il wrapping del codice R in una stored procedure, come salvare un modello R in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e come effettuare chiamate con parametri al modello R per la creazione di stime. |

## <a name="r-quickstarts"></a>Argomenti di avvio rapido di R

Se non si ha familiarità con Machine Learning in SQL, è possibile provare anche gli argomenti di avvio rapido di R.

| Guida introduttiva | Descrizione |
|-|-|
| [Eseguire script R semplici](quickstart-r-create-script.md) | Informazioni di base su come chiamare R in T-SQL usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). |
| [Strutture di dati e oggetti con R](quickstart-r-data-types-and-objects.md) | Descrive come SQL usa il linguaggio R per gestire strutture di dati. |
| [Creare e assegnare i punteggi a un modello predittivo in R](quickstart-r-data-types-and-objects.md) | Illustra come creare, sottoporre a training e usare un modello R per eseguire stime in base ai nuovi dati. |

## <a name="next-steps"></a>Passaggi successivi

Per informazioni più tecniche su R in SQL Server, vedere [Estensione del linguaggio R in SQL Server](../concepts/extension-r.md).
