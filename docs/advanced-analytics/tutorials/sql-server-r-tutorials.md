---
title: Panoramica dell'esercitazione di SQL Server R - SQL Server Machine Learning
description: Introduzione alle esercitazioni di linguaggio R per analitica nel database di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 99dc3aa20bd3f31766ed66a6cdabea5cf38553f6
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510158"
---
# <a name="sql-server-r-language-tutorials"></a>Esercitazioni sul linguaggio di SQL Server R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive le esercitazioni di linguaggio R per analitica nel database [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) oppure [Machine Learning Services di SQL Server 2017](../install/sql-machine-learning-services-windows-install.md).

+ Informazioni su come eseguire il wrapping ed eseguire codice R nelle stored procedure.
+ Serializzare e salvare i modelli basati su r nel database di SQL Server.
+ Informazioni sui contesti di calcolo remoti e locali e quando utilizzarle.
+ Esplorare le librerie di Microsoft R per l'analisi scientifica dei dati e attività di machine learning.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>Esercitazioni e guide introduttive di R

| Collegamento | Descrizione |
|------|-------------|
| [Guida introduttiva: Uso di R in T-SQL](rtsql-using-r-code-in-transact-sql-quickstart.md) | Primo di più guide introduttive, con quella che illustra la sintassi di base per chiamare una funzione R usando un editor di query T-SQL, ad esempio SQL Server Management Studio. |
| [Esercitazione: Informazioni su analitica di R nel database per i data Scientist](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Per gli sviluppatori di R per SQL Server, questa esercitazione viene illustrato come eseguire attività comuni di data science in SQL Server. Caricare e visualizzare i dati, eseguire il training e salvare un modello in SQL Server e utilizzare il modello di analitica predittiva. |
| [Esercitazione: Informazioni su analitica di R nel database per sviluppatori SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Compilare e distribuire una soluzione completa di R, usando solo [!INCLUDE[tsql](../../includes/tsql-md.md)] strumenti. Si concentra sullo spostamento di una soluzione nell'ambiente di produzione. Si apprenderà come eseguire il wrapping del codice R in una stored procedure, come salvare un modello R in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e come effettuare chiamate con parametri al modello R per la creazione di stime. |
| [Esercitazione: Approfondimento RevoScalepR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | Informazioni su come usare le funzioni nei pacchetti RevoScaleR. Spostare dati tra R e SQL Server e commutatore contesti di calcolo per soddisfare una determinata attività. Creare modelli e tracciati e quindi spostati tra l'ambiente di sviluppo e il server di database. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Esempi di codice

| Collegamento | Descrizione |
|------|-------------|
| [Compilare un modello predittivo con R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Informazioni su come un noleggio di sci potrebbe usare machine learning per prevedere i noleggi futuri, che consente al piano aziendale e personale per soddisfare la domanda futura. |
| [Clienti di eseguire il clustering con R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Usare apprendimento non supervisionato per segmentare i clienti basate sui dati di vendita. |

## <a name="see-also"></a>Vedere anche

+ [Estensione di R a SQL Server](../concepts/extension-r.md)
+ [Esercitazioni di SQL Server Machine Learning Services](machine-learning-services-tutorials.md)

