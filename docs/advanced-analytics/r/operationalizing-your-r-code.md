---
title: Rendere operativo codice R tramite stored procedure
description: Incorporare il codice del linguaggio R in un SQL Server stored procedure per renderlo disponibile a qualsiasi applicazione client che abbia accesso a un database SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 248a2e12199466cfaf686bcfcf10341a75981ef7
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149894"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>Rendere operativo codice R usando stored procedure in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Quando si usano le funzionalità di R e Python in SQL Server Machine Learning Services, l'approccio più comune per lo spostamento di soluzioni in un ambiente di produzione consiste nell'incorporare il codice nelle stored procedure. Questo articolo riepiloga i punti chiave per lo sviluppatore SQL da considerare quando operatività codice R usando SQL Server.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>Distribuire script pronti per la produzione con T-SQL e stored procedure

Tradizionalmente, l'integrazione delle soluzioni data science ha comportato una ricodifica completa per supportare le prestazioni e l'integrazione. SQL Server Machine Learning Services semplifica questa attività perché il codice R e Python può essere eseguito in SQL Server e chiamato usando stored procedure. Per ulteriori informazioni sui meccanismi di incorporamento del codice nelle stored procedure, vedere:

+ [Creare ed eseguire script R semplici in SQL Server](../tutorials/quickstart-r-create-script.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

Un esempio più completo della distribuzione del codice R nell'ambiente di produzione tramite stored procedure è disponibile [in Esercitazione: Analisi dei dati R per sviluppatori SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>Linee guida per l'ottimizzazione del codice R per SQl

La conversione del codice R in SQL è più semplice se alcune ottimizzazioni vengono eseguite in anticipo nel codice R o Python. Questi includono l'evitare i tipi di dati che provocano problemi, evitando conversioni di dati non necessarie e riscrivendo il codice R come una singola chiamata di funzione che può essere facilmente parametrizzata. Per altre informazioni, vedere:

+ [Librerie e tipi di dati R](r-libraries-and-data-types.md)
+ [Conversione del codice R per l'uso in R Services](converting-r-code-for-use-in-sql-server.md)
+ [Usare le funzioni di supporto sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integrare R e Python con le applicazioni

Poiché è possibile eseguire R o Python da una stored procedure, è possibile eseguire script da qualsiasi applicazione in grado di inviare un'istruzione T-SQL e gestire i risultati. Ad esempio, è possibile ripetere il training di un modello in base a una pianificazione utilizzando l' [attività Esegui istruzione T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) in Integration Services o utilizzando un'altra utilità di pianificazione del processo in grado di eseguire una stored procedure.

Il Punteggio è un'attività importante che può essere facilmente automatizzata o avviata da applicazioni esterne. È necessario eseguire il training del modello in anticipo, usando R o Python o un stored procedure e [salvare il modello in formato binario in](../tutorials/walkthrough-build-and-save-the-model.md) una tabella. Quindi, è possibile caricare il modello in una variabile come parte di una chiamata di stored procedure, usando una di queste opzioni per l'assegnazione dei punteggi da T-SQL:

+ [Punteggio in tempo reale, ottimizzato per piccoli batch
+ Assegnazione di punteggi a riga singola, per la chiamata da un'applicazione
+ Assegnazione dei [punteggi nativi](../sql-native-scoring.md), per la stima batch veloce da SQL Server senza chiamare R

In questa procedura dettagliata vengono forniti esempi di assegnazione dei punteggi utilizzando un stored procedure in modalità batch e a riga singola:

+ [Procedura dettagliata data science end-to-end per R in SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Vedere questi modelli di soluzione per esempi di come integrare i punteggi in un'applicazione:

+ [Previsione delle vendite al dettaglio](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Rilevamento di frodi](https://github.com/Microsoft/r-server-fraud-detection)
+ [Clustering dei clienti](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Migliorare le prestazioni e la scalabilità

Anche se il linguaggio R Open Source presenta limitazioni note per quanto riguarda i set di dati di grandi dimensioni, le [API del pacchetto RevoScaleR](ref-r-revoscaler.md) incluse in SQL Server machine learning servizio possono operare su set di dati di grandi dimensioni e trarre vantaggio da multithreading, multicore, calcoli nel database a più processi.

Se la soluzione R USA aggregazioni complesse o include set di impostazioni di grandi dimensioni, è possibile sfruttare le aggregazioni in memoria e gli indici columnstore a elevata efficienza SQL Server e consentire al codice R di gestire i calcoli statistici e il punteggio.

Per ulteriori informazioni su come migliorare le prestazioni in SQL Server Machine Learning, vedere:

+ [Ottimizzazione delle prestazioni per R Services per SQL Server](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Suggerimenti e consigli per l'ottimizzazione delle prestazioni](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adattare il codice R per altre piattaforme o contesti di calcolo

Lo stesso codice R che viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sui dati può essere usato con altre origini dati, ad esempio Spark su HDFS, quando si usa l' [opzione server autonomo](../install/sql-machine-learning-standalone-windows-install.md) nel programma di installazione di SQL Server o quando si installa il prodotto con marchio non SQL, Microsoft Machine Learning Server (precedentemente noto come **Microsoft R server**):

+ [Documentazione di Machine Learning Server](https://docs.microsoft.com/r-server/)

+ [Esplora R per RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [Scrivere algoritmi di suddivisione in blocchi](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Calcolo con Big Data in R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Sviluppare un algoritmo parallelo personalizzato](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

