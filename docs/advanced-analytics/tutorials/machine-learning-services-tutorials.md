---
title: SQL Server R e Python - esercitazioni di SQL Server Machine Learning
description: Esempi ed esercitazioni per R e Python in SQL Server Machine Learning Services di scripting.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6d68d7f36ea6539142bab0ea0e4b50ef6dca8444
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645403"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>Esercitazioni di SQL Server Machine Learning in R e Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo fornisce un elenco completo delle esercitazioni ed esempi di codice che illustrano le funzionalità di apprendimento [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) oppure [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md). 

+ Guide introduttive per usano dati incorporati o nessun dato per l'esplorazione rapida con il minimo sforzo.
+ Esercitazioni di approfondimento altre attività, i set di dati più grande e spiegazioni più lungo.
+ Esempi e le soluzioni sono destinate agli sviluppatori che si preferiscono iniziare con il codice, lavorare con le versioni precedenti a concetti e le lezioni per riempire i gap della Knowledge Base.

Si apprenderà come usare le librerie di R e Python con dati relazionali residenti nel contesto operativo stesso, come usare stored procedure SQL Server per l'esecuzione e distribuisce il codice personalizzato e come chiamare Microsoft R e librerie Python per i dati ad alte prestazioni Scienza e attività di machine learning.

Come primo passaggio, esaminare i concetti fondamentali, il backup di Microsoft integration R e Python con SQL Server.

## <a name="concepts"></a>Concetti

Analitica nel database si intende il supporto nativo per R e Python in SQL Server quando si installa SQL Server Machine Learning Services o SQL Server 2016 R Services (solo R) come componente aggiuntivo per il motore di database. Integrazione di R e Python include le distribuzioni open source di base, le librerie specifiche di Microsoft per analitica a prestazioni elevate.

Da un punto di supporto ad architettura, il codice viene eseguito come un processo esterno sulla casella per mantenere l'integrità del motore di database. Tuttavia, tutti i dati di accesso e sicurezza tramite ruoli predefiniti del database SQL Server e autorizzazioni, che significa che qualsiasi applicazione con accesso a SQL Server possano accedere lo script R e Python quando si è distribuito come una stored procedure, oppure serializzare e salvare un modello con Training in un database SQL Database del server.

Supportano di differenze principali tra R e Python in SQL Server rispetto a supporto delle lingue equivalente in altri prodotti Microsoft e i servizi includono:

+ Possibilità di eseguire codice "package" nelle stored procedure o come modello binario.
+ Scrivere codice che chiama le librerie di Microsoft R e Python installate localmente con i file di programma di SQL Server.
+ Applicare l'architettura di sicurezza del database di SQL Server alle soluzioni R e Python.
+ Sfruttare l'infrastruttura di SQL Server e supporto amministrativo per soluzioni personalizzate.

## <a name="quickstarts"></a>Guide introduttive

Iniziare da qui per informazioni su come eseguire R o Python da T-SQL e come rendere operativo il codice R e Python per un ambiente di produzione di SQL.

+ [Python: Eseguire Python con T-SQL](run-python-using-t-sql.md)
+ [R: Hello World in R e SQL](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R: Gestire gli input e output](rtsql-working-with-inputs-and-outputs.md)
+ [R: Gestire gli oggetti e tipi di dati](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [R: Uso delle funzioni R](rtsql-using-r-functions-with-sql-server-data.md)
+ [R: Creare un modello predittivo](rtsql-create-a-predictive-model-r.md)
+ [R: Stimare e creare un tracciato dal modello](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>Esercitazioni

Grazie all'uso approfondito i pacchetti di Microsoft e le operazioni più specializzate, ad esempio lo spostamento da locale a contesti di calcolo remoti si basano su della prima esperienza con R e Python e T-SQL.

+ [Esercitazioni di Python](sql-server-python-tutorials.md)
+ [Esercitazioni di R](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>Esempi

Questi esempi e demo fornite dal team di sviluppo di SQL Server e R Server evidenziano che modo è possibile usare analitica incorporata in applicazioni reali.

| Collegamento | Descrizione | 
|------|-------------|
| [Clienti di eseguire il clustering con R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | Usare apprendimento non supervisionato per segmentare i clienti basate sui dati di vendita. In questo esempio Usa l'algoritmo rxKmeans scalabili di Microsoft R per compilare il modello di clustering. |
| [Clienti di eseguire il clustering con Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Informazioni su come usare l'algoritmo Kmeans per eseguire il clustering non supervisionato dei clienti. Questo esempio Usa il linguaggio di Python nel database.| SQL Server 2017 |
| [Compilare un modello predittivo con R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Informazioni su come un noleggio di sci potrebbe usare machine learning per prevedere i noleggi futuri, che consente al piano aziendale e personale per soddisfare la domanda futura. In questo esempio Usa gli algoritmi di Microsoft per compilare la regressione logistica e modelli di albero delle decisioni. | 
| [Creare un modello predittivo usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Compilare l'applicazione di analisi di noleggio di sci usando Python, per semplificare la pianificazione per la domanda futura. Questo esempio Usa la nuova libreria di Python **revoscalepy**, per creare un modello di regressione lineare. | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>Modelli di soluzioni

Il Team di Data Science di Microsoft ha fornito i modelli di soluzioni personalizzabili che possono essere utilizzati per avviare rapidamente le soluzioni per scenari comuni. Ogni soluzione personalizzata in base a un problema specifico di attività o del settore. La maggior parte delle soluzioni sono progettata per l'esecuzione in SQL Server o in un ambiente cloud, ad esempio Azure Machine Learning. Altre soluzioni possono eseguire in Linux o in cluster di Spark o Hadoop usando Microsoft R Server o Machine Learning Server.

Viene fornito tutto il codice, oltre a istruzioni su come eseguire il training e distribuire un modello per l'assegnazione del punteggio utilizzando stored procedure SQL Server.

+ [Rilevamento di frodi](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Stima personalizzata del trasferimento](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Manutenzione predittiva](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Prevedi la ospedale durata della degenza](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

