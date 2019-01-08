---
title: Rendere operativo il codice R tramite stored procedure - servizi di SQL Server Machine Learning
description: Incorporare il codice del linguaggio R in una stored procedure SQL Server per renderlo disponibile per qualsiasi applicazione client che possono accedere a un database di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3fc96e57fffb3e000a7e1a19887ed27651df9009
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432184"
---
# <a name="operationalize-r-code-machine-learning-services"></a>Rendere operativo il codice R (servizi di Machine Learning)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Gli sviluppatori di database si occupano di integrare più tecnologie e raggruppare i risultati in modo che possano essere condivisi in tutta l'organizzazione. Lo sviluppatore del database funziona con gli sviluppatori di applicazioni, SQL, data Scientist e sviluppatori di progettare e distribuire le soluzioni.

Questo articolo riepiloga i punti chiave per lo sviluppatore del database da considerare quando si messa in funzione il codice R con SQL Server.

## <a name="get-started-with-r-code-in-sql-server"></a>Iniziare con codice R in SQL Server

In genere, l'integrazione di soluzioni di machine learning è sinonimo ricodifica esteso per supportare le prestazioni e l'integrazione. Tuttavia, lo spostamento di codice R e Python in un ambiente di produzione è molto più facile in servizi di SQL Server Machine Learning, in quanto il codice può essere eseguito in SQL Server e richiamato tramite le stored procedure. È possibile continuare a usare strumenti familiari e non è necessario installare un ambiente di sviluppo R. 

Per altre informazioni sulla sintassi di base, vedere:

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [Usare il codice R in SQL](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Per un esempio di come è possibile distribuire codice R nell'ambiente di produzione usando le stored procedure, vedere:

+ [Analitica nel Database per sviluppatori SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="optimize-your-r-code"></a>Ottimizzare il codice R

Conversione del codice R in SQL è certamente più semplice se alcune ottimizzazioni vengono eseguite in anticipo nel codice R o Python. Sono inclusi come evitare i tipi di dati che causano problemi, evitando le conversioni di dati non necessari e la riscrittura del codice R come una singola chiamata di funzione che può essere facilmente aggiunti parametri. Per altre informazioni, vedere:

+ [Librerie e tipi di dati R](r-libraries-and-data-types.md)

+ [Conversione di codice R per l'uso in R Services](converting-r-code-for-use-in-sql-server.md)

+ [Usare funzioni di supporto sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integrazione di R e Python con applicazioni

Poiché è possibile avviare i servizi di Machine Learning da una stored procedure, è possibile eseguire script R o Python da qualsiasi applicazione che può inviare un'istruzione T-SQL e gestire i risultati.

Ad esempio, si potrebbe ripetere il training di un modello in base a una pianificazione utilizzando l'attività Esegui T-SQL in Integration Services, oppure usando un'altra utilità di pianificazione processi che è possibile eseguire una stored procedure.

Assegnazione dei punteggi è un'importante attività che può facilmente essere automatizzate o avviata da applicazioni esterne. Il training del modello in anticipo, tramite R o Python o una stored procedure e salvare il modello in formato binario in una tabella. Quindi, è possibile caricare il modello in una variabile come parte della chiamata di stored procedure, tramite una di queste opzioni per il punteggio di T-SQL:

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

Nonostante sia noto che il linguaggio R open source presenta alcune limitazioni, il pacchetto RevoScaleR API possono operare su grandi set di dati e trarre vantaggio da calcoli nel database multithread, multicore, multiprocesso.

Se la soluzione R Usa aggregazioni complesse o comporta grandi set di dati, è possibile sfruttare le aggregazioni in memoria altamente efficienti e gli indici columnstore di SQL Server e lasciare che il codice R gestisca i calcoli statistici e di assegnazione dei punteggi.

Per altre informazioni su come migliorare le prestazioni in SQL Server Machine Learning, vedere:

+ [Ottimizzazione delle prestazioni per SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Suggerimenti di ottimizzazione delle prestazioni](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Contesti di calcolo o adattare il codice R per altre piattaforme

Lo stesso codice R che viene eseguito sui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati può essere usati da altre origini dati, ad esempio Hadoop e in altri contesti di calcolo.

Per altre informazioni sulle piattaforme supportate da Microsoft R, vedere:

+ [Introduzione a Microsoft R](https://docs.microsoft.com/r-server/)

+ [Esplorare RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

Per altre informazioni su come è possibile ottimizzare le soluzioni R Microsoft eseguita su dati di grandi dimensioni o più piattaforme, vedere:

+ [Scrivere algoritmi la suddivisione in blocchi](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Calcolo con big data in R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Sviluppare il proprio algoritmo parallelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

