---
title: SQL Server esercitazioni su R e Python
description: Esempi ed esercitazioni per gli script R e Python in SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: d901d11b11019a19d5e26e12956e9ba520e33e8f
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469624"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>SQL Server Machine Learning esercitazioni in R e Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fornisce un elenco completo delle esercitazioni e degli esempi di codice che illustrano le funzionalità di Machine Learning di [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md). 

+ Le guide introduttive usano dati incorporati o nessun dato per un'esplorazione veloce con minor sforzo.
+ Le esercitazioni sono più approfondite con più attività, set di impostazioni più grandi e spiegazioni più lunghe.
+ Gli esempi e le soluzioni sono destinati agli sviluppatori che preferiscono iniziare a usare il codice, lavorando all'indietro per i concetti e le lezioni per colmare le lacune della conoscenza.

Si apprenderà come usare le librerie R e Python con dati relazionali residenti nello stesso contesto operativo, come usare SQL Server stored procedure per l'esecuzione e la distribuzione di codice personalizzato e come chiamare le librerie Microsoft R e Python per i dati ad alte prestazioni attività scientifiche e di machine learning.

Come primo passaggio, esaminare i concetti fondamentali relativi all'integrazione R e Python di Microsoft con SQL Server.

## <a name="concepts"></a>Concetti

L'analisi nel database si riferisce al supporto nativo per R e Python in SQL Server quando si installa SQL Server Machine Learning Services o SQL Server 2016 R Services (solo R) come componente aggiuntivo del motore di database. L'integrazione di R e Python include distribuzioni open source di base, oltre a librerie specifiche di Microsoft per l'analisi delle prestazioni elevate.

Da un punto di partenza dell'architettura, il codice viene eseguito come processo esterno nella casella per mantenere l'integrità del motore di database. Tuttavia, tutti gli accessi e la sicurezza dei dati vengono eseguiti tramite SQL Server autorizzazioni e ruoli del database, il che significa che qualsiasi applicazione con accesso a SQL Server può accedere allo script R e Python quando lo si distribuisce come stored procedure o serializza e salva un modello sottoposto a training in un SQL Database del server.

Le principali differenze tra il supporto di R e Python in SQL Server rispetto al supporto di lingue equivalenti in altri prodotti e servizi Microsoft includono:

+ Possibilità di eseguire il "pacchetto" del codice nelle stored procedure o come modelli binari.
+ Scrivere codice che chiama le librerie Microsoft R e Python installate localmente con i file di programma SQL Server.
+ Applicare l'architettura di sicurezza del database di SQL Server alle soluzioni R e Python.
+ Sfrutta SQL Server infrastruttura e il supporto amministrativo per le tue soluzioni personalizzate.

## <a name="quickstarts"></a>Guide introduttive

Iniziare da qui per informazioni su come eseguire R o Python da T-SQL e come rendere operativo il codice R e Python per un ambiente di produzione SQL.

+ [Python Eseguire python con T-SQL](run-python-using-t-sql.md)
+ [R Hello World in R e SQL](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R Gestire input e output](rtsql-working-with-inputs-and-outputs.md)
+ [R Gestire tipi di dati e oggetti](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [R Uso delle funzioni R](rtsql-using-r-functions-with-sql-server-data.md)
+ [R Creazione di un modello predittivo](rtsql-create-a-predictive-model-r.md)
+ [R Stimare e tracciare il modello](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>Esercitazioni

Sviluppa la tua prima esperienza con R e Python e T-SQL, esaminando più da vicino i pacchetti Microsoft e operazioni più specializzate, ad esempio lo spostamento da contesti di calcolo locali a quelli remoti.

+ [Esercitazioni di Python](sql-server-python-tutorials.md)
+ [Esercitazioni di R](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>Esempi

Questi esempi e demo forniti dal team di sviluppo SQL Server e R Server evidenziano i modi in cui è possibile usare l'analisi incorporata in applicazioni reali.

| Collegamento | Descrizione | 
|------|-------------|
| [Eseguire il clustering dei clienti usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Usare l'apprendimento non supervisionato per segmentare i clienti in base ai dati di vendita. Questo esempio usa l'algoritmo rxKmeans scalabile di Microsoft R per compilare il modello di clustering. |
| [Eseguire il clustering dei clienti con Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Informazioni su come usare l'algoritmo Kmeans per eseguire il clustering senza supervisione dei clienti. Questo esempio usa il linguaggio Python nel database.| SQL Server 2017 |
| [Creare un modello predittivo usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Scopri in che modo un'azienda di noleggio di sci può usare Machine Learning per prevedere i noleggi futuri, che consente al piano aziendale e al personale di soddisfare la domanda futura. Questo esempio usa gli algoritmi Microsoft per creare modelli di regressione logistica e di alberi delle decisioni. | 
| [Creazione di un modello predittivo con Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Consente di creare l'applicazione di analisi noleggio sci con Python per pianificare la richiesta futura. Questo esempio usa la nuova libreria Python, **revoscalepy**, per creare un modello di regressione lineare. | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>Modelli di soluzioni

Il team di Data Science di Microsoft ha fornito modelli di soluzioni personalizzabili che possono essere usati per avviare soluzioni per scenari comuni. Ogni soluzione è adatta a un problema specifico dell'attività o del settore. La maggior parte delle soluzioni è progettata per essere eseguita in SQL Server o in un ambiente cloud, ad esempio Azure Machine Learning. Altre soluzioni possono essere eseguite in Linux o nei cluster Spark o Hadoop usando Microsoft R Server o Machine Learning Server.

Viene fornito tutto il codice, oltre a istruzioni su come eseguire il training e distribuire un modello per il punteggio utilizzando SQL Server stored procedure.

+ [Rilevamento di frodi](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Stima personalizzata del trasferimento](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Manutenzione predittiva](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Stimare la durata dell'ospedale](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

