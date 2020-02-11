---
title: Distribuire il codice R nelle stored procedure
description: Incorporare il codice del linguaggio R in una stored procedure di SQL Server per renderlo disponibile per qualsiasi applicazione client abbia accesso a un database SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 15c3406d6745802ece620942bf51b23c4d3643ee
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727452"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>Rendere operativo il codice R usando le stored procedure in Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Quando si usano le caratteristiche di R e Python in Machine Learning Services per SQL Server, l'approccio più comune per spostare le soluzioni in un ambiente di produzione consiste nell'incorporare il codice nelle stored procedure. Questo articolo riepiloga i punti chiave che uno sviluppatore SQL deve tenere presenti quando rende operativo il codice R usando SQL Server.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>Distribuire uno script pronto per la produzione con T-SQL e le stored procedure

In passato l'integrazione di soluzioni data science richiedeva di riscrivere completamente il codice per supportare le prestazioni e l'integrazione. Machine Learning Services per SQL Server semplifica questa attività perché il codice R e Python può essere eseguito in SQL Server e chiamato usando le stored procedure. Per altre informazioni sui meccanismi di incorporamento del codice nelle stored procedure, vedere:

+ [Creare ed eseguire script R semplici in SQL Server](../tutorials/quickstart-r-create-script.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

Un esempio più completo della distribuzione del codice R nell'ambiente di produzione tramite stored procedure è disponibile in [Esercitazione: Analisi dei dati R per sviluppatori SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>Linee guida per l'ottimizzazione del codice R per SQL

La conversione del codice R in SQL è più semplice se alcune ottimizzazioni vengono eseguite in anticipo nel codice R o Python, come, ad esempio, evitare i tipi di dati che provocano problemi, evitare conversioni di dati non necessarie e riscrivere il codice R come una singola chiamata di funzione che può essere parametrizzata. Per altre informazioni, vedere:

+ [Librerie e tipi di dati R](r-libraries-and-data-types.md)
+ [Conversione di codice R per l'uso in R Services](converting-r-code-for-use-in-sql-server.md)
+ [Usare le funzioni helper sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integrare R e Python con le applicazioni

Poiché è possibile eseguire R o Python da una stored procedure, è possibile eseguire gli script da qualsiasi applicazione in grado di inviare un'istruzione T-SQL e gestire i risultati. È ad esempio possibile ripetere il training di un modello in base a una pianificazione usando l'[attività di esecuzione T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) in Integration Services oppure usando un'altra utilità di pianificazione dei processi che può eseguire una stored procedure.

L'assegnazione dei punteggi è un'attività importante che può essere facilmente automatizzata o avviata da applicazioni esterne. Si esegue il training del modello in anticipo, usando R o Python oppure una stored procedure, e si [salva il modello in formato binario](../tutorials/walkthrough-build-and-save-the-model.md) in una tabella. Il modello può quindi essere caricato in una variabile durante una chiamata di stored procedure, usando una di queste opzioni per l'assegnazione dei punteggi da T-SQL:

+ Assegnazione dei punteggi in tempo reale, ottimizzata per piccoli batch
+ Assegnazione dei punteggi alle singole righe, per la chiamata da un'applicazione
+ [Assegnazione dei punteggi nativa](../sql-native-scoring.md), per la stima in batch veloce da SQL Server senza chiamare R

Questa procedura dettagliata fornisce esempi di assegnazione dei punteggi tramite una stored procedure in modalità batch e a riga singola:

+ [Procedura dettagliata di data science end-to-end per R in SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Vedere questi modelli di soluzione per esempi di come integrare l'assegnazione dei punteggi in un'applicazione:

+ [Retail forecasting](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md) (Previsione di vendita al dettaglio)
+ [Rilevamento di frodi](https://github.com/Microsoft/r-server-fraud-detection)
+ [Customer clustering](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering) (Clustering dei clienti)

## <a name="boost-performance-and-scale"></a>Migliorare le prestazioni e la scalabilità

Nonostante il linguaggio R open source presenti alcune limitazioni note relative ai set di dati di grandi dimensioni, le [API del pacchetto RevoScaleR](ref-r-revoscaler.md) incluse in Machine Learning Services per SQL Server possono operare su set di dati di grandi dimensioni e trarre vantaggio da calcoli con thread, core e processi multipli nel database.

Se la soluzione R usa aggregazioni complesse o comporta grandi set di dati, è possibile sfruttare le efficienti aggregazioni in memoria e gli indici columnstore di SQL Server e lasciare che il codice R gestisca i calcoli statistici e l'assegnazione dei punteggi.

Per altre informazioni su come migliorare le prestazioni in SQL Server Machine Learning, vedere:

+ [Ottimizzazione delle prestazioni per R Services per SQL Server](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Suggerimenti per l'ottimizzazione delle prestazioni](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adattare il codice R per altre piattaforme o contesti di calcolo

Lo stesso codice R eseguito sui dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere usato con altre origini dati, ad esempio Spark su HDFS, quando si usa l'[opzione di server autonomo](../install/sql-machine-learning-standalone-windows-install.md) nella configurazione di SQL Server o quando si installa il prodotto senza marchio SQL, Microsoft Machine Learning Server (noto in precedenza come **Microsoft R Server**):

+ [Documentazione di Machine Learning Server](https://docs.microsoft.com/r-server/)

+ [Esplorare da R a RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [Scrivere algoritmi di divisione in blocchi](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Calcolo con Big Data in R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Sviluppare un algoritmo parallelo personalizzato](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

