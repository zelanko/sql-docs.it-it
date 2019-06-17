---
title: Rendere operativo il codice R tramite stored procedure - servizi di SQL Server Machine Learning
description: Incorporare il codice del linguaggio R in una stored procedure SQL Server per renderlo disponibile per qualsiasi applicazione client che possono accedere a un database di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2d00e96162b492d28f0c0ec107612023c8e15e48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642035"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>Rendere operativo il codice R tramite stored procedure in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Quando si usa la funzionalità R e Python in SQL Server Machine Learning Services, incorporamento di codice nelle stored procedure è l'approccio più comune per lo spostamento di soluzioni in un ambiente di produzione. Questo articolo riepiloga i punti chiave per gli sviluppatori SQL che assicuri messa in funzione il codice R con SQL Server.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>Distribuire lo script di produzione usando T-SQL e stored procedure

In genere, l'integrazione delle soluzioni di analisi scientifica dei dati ha lo scopo ricodifica esteso per supportare le prestazioni e l'integrazione. Servizi di SQL Server Machine Learning semplifica questa attività perché il codice R e Python può essere eseguito in SQL Server e richiamato tramite le stored procedure. Per altre informazioni sui meccanismi di incorporamento di codice nelle stored procedure, vedere:

+ [Guida introduttiva: Script R di "Hello world" in SQL Server](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

Un esempio più dettagliato di distribuzione del codice R nell'ambiente di produzione usando le stored procedure è reperibile in [esercitazione: Analitica di dati R per sviluppatori SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>Linee guida per l'ottimizzazione di codice R per SQl

Conversione del codice R in SQL è più semplice se alcune ottimizzazioni vengono eseguite in anticipo nel codice R o Python. Sono inclusi come evitare i tipi di dati che causano problemi, evitando le conversioni di dati non necessari e la riscrittura del codice R come una singola chiamata di funzione che può essere facilmente aggiunti parametri. Per altre informazioni, vedere:

+ [Librerie e tipi di dati R](r-libraries-and-data-types.md)
+ [Conversione di codice R per l'uso in R Services](converting-r-code-for-use-in-sql-server.md)
+ [Usare funzioni di supporto sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integrazione di R e Python con applicazioni

Poiché è possibile eseguire R o Python da una stored procedure, è possibile eseguire gli script da qualsiasi applicazione che può inviare un'istruzione T-SQL e gestire i risultati. Ad esempio, si potrebbe ripetere il training di un modello in base a una pianificazione utilizzando il [attività T-SQL Execute](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) in Integration Services o con un'altra utilità di pianificazione processi che è possibile eseguire una stored procedure.

Assegnazione dei punteggi è un'importante attività che può facilmente essere automatizzate o avviata da applicazioni esterne. Il training del modello in anticipo, tramite R o Python o una stored procedure, e [salvataggio del modello in formato binario](../tutorials/walkthrough-build-and-save-the-model.md) a una tabella. Quindi, è possibile caricare il modello in una variabile come parte della chiamata di stored procedure, tramite una di queste opzioni per il punteggio di T-SQL:

+ [In tempo reale](../real-time-scoring.md) assegnazione dei punteggi, ottimizzato per i batch piccoli
+ Assegnazione dei punteggi, in cui viene chiamato da un'applicazione a singola riga
+ [Assegnazione dei punteggi nativa](../sql-native-scoring.md), per le stime batch veloce da SQL Server senza rivolgersi a R

Questa procedura dettagliata vengono forniti esempi di assegnazione dei punteggi tramite una stored procedure in batch e modalità riga singola:

+ [-To-end procedura dettagliata di analisi scientifica dei dati per R in SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Visualizzare questi modelli di soluzione per esempi su come integrare l'assegnazione dei punteggi in un'applicazione:

+ [Previsione delle vendite al dettaglio](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Rilevamento di frodi](https://github.com/Microsoft/r-server-fraud-detection)
+ [Clustering dei clienti](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Aumentare le prestazioni e scalabilità

Nonostante il linguaggio R open source è noto che le limitazioni per quanto riguarda grandi set di dati, il [API del pacchetto RevoScaleR](ref-r-revoscaler.md) incluso con il servizio SQL Server Machine Learning possono operare su grandi set di dati e trarre vantaggio da multi-thread , multicore, multiprocesso calcoli nel database.

Se la soluzione R Usa aggregazioni complesse o comporta grandi set di dati, è possibile sfruttare le aggregazioni in memoria altamente efficienti e gli indici columnstore di SQL Server e lasciare che il codice R gestisca i calcoli statistici e di assegnazione dei punteggi.

Per altre informazioni su come migliorare le prestazioni in SQL Server Machine Learning, vedere:

+ [Ottimizzazione delle prestazioni per SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Suggerimenti di ottimizzazione delle prestazioni](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Contesti di calcolo o adattare il codice R per altre piattaforme

Lo stesso codice R che viene eseguito sui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati possono essere usati su altre origini dati, ad esempio Spark su HDFS, quando si usa la [opzione di server autonomi](../install/sql-machine-learning-standalone-windows-install.md) nel programma di installazione di SQL Server o quando si installa il prodotto con marchio di non-SQL, Microsoft Machine Learning Server (precedentemente noto come **Microsoft R Server**):

+ [Documentazione di Machine Learning Server](https://docs.microsoft.com/r-server/)

+ [Esplorare R a RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [Scrivere algoritmi la suddivisione in blocchi](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Calcolo con big data in R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Sviluppare il proprio algoritmo parallelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

