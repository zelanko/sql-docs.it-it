---
title: 'Esercitazione su R + T-SQL: Sviluppare un modello'
description: Informazioni su come incorporare codice del linguaggio di programmazione R in stored procedure di SQL Server e funzioni T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9669b2c38d2e8b571ef7e519100b13cf5a63a10d
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81115984"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>Esercitazione: Analisi dei dati R per sviluppatori SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa esercitazione per programmatori SQL vengono fornite informazioni sull'integrazione di R mediante la creazione e la distribuzione di una soluzione di Machine Learning basata su R usando un database [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) in SQL Server. Si useranno T-SQL, SQL Server Management Studio e un'istanza del motore di database con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) e il supporto del linguaggio R.

Questa esercitazione presenta le funzioni R usate in un flusso di lavoro di modellazione dei dati. I passaggi includono l'esplorazione dei dati, la creazione e il training di un modello di classificazione binaria e la distribuzione del modello. Il modello che verrà compilato consente di stimare se è probabile che per una corsa venga lasciata una mancia, in base all'ora del giorno, alla distanza percorsa e al luogo di partenza della corsa. 

Viene eseguito il wrapping di tutto il codice R usato in questa esercitazione in stored procedure create ed eseguite in Management Studio.

## <a name="background-for-sql-developers"></a>Background per sviluppatori SQL

Il processo di creazione di una soluzione di Machine Learning è complesso e può richiedere l'uso di più strumenti e il coordinamento di esperti in materia in diverse fasi:

+ recupero e pulizia dei dati
+ esplorazione dei dati e creazione di caratteristiche utili per la modellazione
+ training e ottimizzazione del modello
+ distribuzione nell'ambiente di produzione

Per lo sviluppo e i test del codice effettivo è opportuno usare un ambiente di sviluppo R dedicato. Dopo che lo script è stato testato, è tuttavia possibile distribuirlo facilmente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] nell'ambiente familiare di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Scopo di questa esercitazione in più parti è quello di illustrare un flusso di lavoro tipico per la migrazione di "codice R completato" in SQL Server. 

- [Lezione 1: Esplorare e visualizzare la forma e la distribuzione dei dati chiamando funzioni R in stored procedure](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [Lezione 2: Creare caratteristiche dei dati con R in funzioni T-SQL](sqldev-create-data-features-using-t-sql.md)
  
- [Lezione 3: Eseguire il training e il salvataggio di un modello R usando funzioni e stored procedure](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [Lezione 4: Stimare i risultati potenziali usando un modello R in una stored procedure](../tutorials/sqldev-operationalize-the-model.md)

Dopo aver salvato il modello nel database, chiamarlo per eseguire stime da [!INCLUDE[tsql](../../includes/tsql-md.md)] usando le stored procedure.

## <a name="prerequisites"></a>Prerequisiti

Tutte le attività possono essere eseguite usando stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Questa esercitazione presuppone una certa familiarità con le operazioni di database di base, ad esempio la creazione di database e tabelle, l'importazione di dati e la scrittura di query SQL. Non si presuppone che l'utente abbia familiarità con il linguaggio R. Viene quindi fornito tutto il codice R necessario. 

+ [R Services per SQL Server 2016](../install/sql-r-services-windows-install.md#verify-installation) o [Machine Learning Services per SQL Server con R abilitato](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Librerie R](../package-management/r-package-information.md)

+ [Autorizzazioni](../security/user-permission.md)

+ [Database demo NYC Taxi](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esplorare e visualizzare i dati con funzioni R in stored procedure](../tutorials/sqldev-explore-and-visualize-the-data.md)
