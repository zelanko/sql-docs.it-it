---
title: Esercitazioni di R
description: Introduzione alle esercitazioni sul linguaggio R per l'analisi nel database SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c71ebfbda37e66050f868fa7676d0247e84840e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74119232"
---
# <a name="sql-server-r-language-tutorials"></a>Esercitazioni sul linguaggio R per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive le esercitazioni sul linguaggio R per l'analisi nel database in [R Services per SQL Server 2016](../install/sql-r-services-windows-install.md) o [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md).

+ Informazioni su come effettuare il wrapping ed eseguire codice R in stored procedure.
+ Procedure per serializzare e salvare modelli basati su R in database SQL Server.
+ Informazioni sui contesti di calcolo locali e remoti e su quando usarli.
+ Modalità di esplorazione delle librerie Microsoft R per le attività di data science e Machine Learning.

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
+ [Esercitazioni su Machine Learning Services per SQL Server](machine-learning-services-tutorials.md)

