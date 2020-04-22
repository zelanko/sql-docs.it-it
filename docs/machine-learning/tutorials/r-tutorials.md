---
title: Esercitazioni di R
description: Questo articolo descrive le esercitazioni e gli argomenti di avvio rapido di R per Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/13/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 952a33eb5a160acae44b5d1ae674c75b8d74cca5
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487290"
---
# <a name="r-tutorials-for-sql-server-machine-learning-services"></a>Esercitazioni di R per Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive le esercitazioni e gli argomenti di avvio rapido di R per [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md).

+ Informazioni su come eseguire script R.
+ Compilare, eseguire il training e distribuire modelli R in SQL Server.
+ Informazioni sui contesti di calcolo remoti e locali.
+ Esplorare i pacchetti Microsoft R per le attività di data science e Machine Learning.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>Argomenti di avvio rapido ed esercitazioni su R

| Collegamento | Descrizione |
|------|-------------|
| [Avvio rapido: Creare ed eseguire script R semplici](quickstart-r-create-script.md) | Primo di una serie completa, in questo argomento di avvio rapido viene illustrata la sintassi di base per chiamare una funzione R usando un editor di query T-SQL, ad esempio SQL Server Management Studio. |
| [Esercitazione: Analisi R nel database per data scientist](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Destinata agli sviluppatori R che non hanno familiarità con SQL Server, questa esercitazione illustra come eseguire le principali attività di data science in SQL Server. Descrive come caricare e visualizzare dati, eseguire il training e il salvataggio di un modello in SQL Server e usare il modello per l'analisi predittiva. |
| [Esercitazione: Analisi R nel database per sviluppatori SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Fornisce le istruzioni per creare e distribuire una soluzione R completa usando solo strumenti [!INCLUDE[tsql](../../includes/tsql-md.md)]. Descrive nel dettaglio il passaggio di una soluzione all'ambiente di produzione. Si apprenderà come eseguire il wrapping del codice R in una stored procedure, come salvare un modello R in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e come effettuare chiamate con parametri al modello R per la creazione di stime. |
| [Esercitazione: Approfondimento di RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | Spiega come usare le funzioni nei pacchetti RevoScaleR, nonché come spostare dati tra R e SQL Server e come cambiare il contesto di calcolo per adattarlo a un'attività specifica. Descrive inoltre come creare modelli e tracciati e come spostarli tra l'ambiente di sviluppo e il server di database. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Esempi di codice

| Collegamento | Descrizione |
|------|-------------|
| [Creare un modello predittivo usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Si descrive come una società di noleggio di sci potrebbe usare modelli di Machine Learning per stimare i noleggi futuri, in modo da aiutare il piano aziendale e il personale a soddisfare la domanda futura. |
| [Eseguire il clustering dei clienti con R ed SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Si ricorre all'apprendimento non supervisionato per classificare i clienti in base ai dati di vendita. |

## <a name="see-also"></a>Vedere anche

+ [Estensione R in SQL Server](../concepts/extension-r.md)