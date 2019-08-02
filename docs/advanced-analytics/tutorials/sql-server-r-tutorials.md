---
title: Panoramica di SQL Server R tutorial
description: Introduzione alle esercitazioni sul linguaggio R per SQL Server analisi nel database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ff1027a3a791ef0151e61982445cafff7be40329
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715427"
---
# <a name="sql-server-r-language-tutorials"></a>Esercitazioni sul linguaggio R SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive le esercitazioni sul linguaggio R per l'analisi nel database in [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md).

+ Informazioni su come eseguire il wrapping e l'esecuzione del codice R nelle stored procedure.
+ Serializzare e salvare i modelli basati su r per SQL Server database.
+ Informazioni sui contesti di calcolo locali e remoti e su quando usarli.
+ Esplora le librerie Microsoft R per le attività di data science e machine learning.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>Guide introduttive ed esercitazioni di R

| Collegamento | Descrizione |
|------|-------------|
| [Avvio rapido: Uso di R in T-SQL](rtsql-using-r-code-in-transact-sql-quickstart.md) | Prima di diverse guide introduttive, in cui è illustrata la sintassi di base per chiamare una funzione R usando un editor di query T-SQL, ad esempio SQL Server Management Studio. |
| [Esercitazione: Informazioni sul database R Analytics per data scientist](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | Per gli sviluppatori R che non hanno familiarità con SQL Server, in questa esercitazione viene illustrato come eseguire le attività comuni di data science in SQL Server. Caricare e visualizzare i dati, eseguire il training e salvare un modello in SQL Server e usare il modello per l'analisi predittiva. |
| [Esercitazione: Informazioni sul database R Analytics per sviluppatori SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) | Compila e Distribuisci una soluzione R completa, usando [!INCLUDE[tsql](../../includes/tsql-md.md)] solo gli strumenti. Si concentra sullo spostare una soluzione nell'ambiente di produzione. Si apprenderà come eseguire il wrapping del codice R in una stored procedure, come salvare un modello R in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e come effettuare chiamate con parametri al modello R per la creazione di stime. |
| [Esercitazione: Approfondimento su RevoScalepR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | Informazioni su come usare le funzioni nei pacchetti RevoScaleR. Spostare i dati tra R e SQL Server e cambiare i contesti di calcolo per adattarli a un'attività specifica. Creare modelli e tracciati e spostarli tra l'ambiente di sviluppo e il server di database. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>Esempi di codice

| Collegamento | Descrizione |
|------|-------------|
| [Creare un modello predittivo usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Scopri in che modo un'azienda di noleggio di sci può usare Machine Learning per prevedere i noleggi futuri, che consente al piano aziendale e al personale di soddisfare la domanda futura. |
| [Eseguire il clustering dei clienti usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Usare l'apprendimento non supervisionato per segmentare i clienti in base ai dati di vendita. |

## <a name="see-also"></a>Vedere anche

+ [Estensione R per SQL Server](../concepts/extension-r.md)
+ [Esercitazioni SQL Server Machine Learning Services](machine-learning-services-tutorials.md)

