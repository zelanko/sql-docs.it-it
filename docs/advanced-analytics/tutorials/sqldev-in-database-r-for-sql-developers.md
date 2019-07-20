---
title: Esercitazione per l'analisi nel database con R
description: Informazioni su come incorporare il codice del linguaggio di programmazione R in SQL Server stored procedure e funzioni T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 64995cc5de7bb3609f1923b7755be9b33b55e764
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345910"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>Esercitazione: Analisi dei dati R per sviluppatori SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa esercitazione per i programmatori SQL, informazioni sull'integrazione di R mediante la compilazione e la distribuzione di una soluzione di apprendimento automatico basata su R usando un database [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) in SQL Server. Si useranno T-SQL, SQL Server Management Studio e un'istanza del motore di database con [Machine Learning Services] ([Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) e il supporto del linguaggio R

Questa esercitazione presenta le funzioni R usate in un flusso di lavoro di modellazione dei dati. I passaggi includono l'esplorazione dei dati, la compilazione e il training di un modello di classificazione binaria e la distribuzione del modello. Il modello che verrà compilato prevede se è probabile che un viaggio provochi un suggerimento basato sull'ora del giorno, sulla distanza percorsa e sulla posizione di prelievo. 

Tutto il codice R usato in questa esercitazione viene incluso nelle stored procedure create ed eseguite in Management Studio.

## <a name="background-for-sql-developers"></a>Background per sviluppatori SQL

Il processo di creazione di una soluzione di apprendimento automatico è un sistema complesso che può coinvolgere più strumenti e il coordinamento di esperti in materia in diverse fasi:

+ recupero e pulizia dei dati
+ esplorazione dei dati e creazione di funzionalità utili per la modellazione
+ Training e ottimizzazione del modello
+ distribuzione in produzione

Lo sviluppo e il test del codice effettivo vengono eseguiti in modo ottimale usando un ambiente di sviluppo R dedicato. Tuttavia, dopo che lo script è stato testato completamente, è possibile distribuirlo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)] modo semplice utilizzando le stored procedure nell' [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ambiente familiare di.

Lo scopo di questa esercitazione in più parti è un'introduzione a un flusso di lavoro tipico per la migrazione di "codice R terminato" per SQL Server. 

- [Lezione 1: Esplorare e visualizzare la forma e la distribuzione dei dati chiamando le funzioni R nelle stored procedure](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lezione 2: Creare funzionalità di dati usando R in funzioni T-SQL](sqldev-create-data-features-using-t-sql.md)
  
- [Lezione 3: Eseguire il training e salvare un modello R usando funzioni e stored procedure](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lezione 4: Stimare potenziali risultati usando un modello R in un stored procedure](../tutorials/sqldev-operationalize-the-model.md)

Dopo che il modello è stato salvato nel database, chiamare il modello per le stime da [!INCLUDE[tsql](../../includes/tsql-md.md)] tramite stored procedure.

## <a name="prerequisites"></a>Prerequisiti

Tutte le attività possono essere eseguite [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzando stored procedure [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]in.

Questa esercitazione presuppone una certa familiarità con le operazioni di database di base, ad esempio la creazione di database e tabelle, l'importazione di dati e la scrittura di query SQL. Non si presuppone che l'utente conosca R. Di conseguenza, viene fornito tutto il codice R. 

+ [SQL Server 2016 r Services](../install/sql-r-services-windows-install.md#verify-installation) o [SQL Server 2017 Machine Learning Services con R abilitato](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Librerie R](../package-management/installed-package-information.md)

+ [Autorizzazioni](../security/user-permission.md)

+ [Database demo di NYC Taxi](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esplorare e visualizzare i dati usando le funzioni R nelle stored procedure](../tutorials/sqldev-explore-and-visualize-the-data.md)
