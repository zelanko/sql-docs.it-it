---
title: 'Python + T-SQL: Sviluppare un modello'
description: Informazioni su come incorporare il codice Python in stored procedure di SQL Server e funzioni T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3bafc3a524ec854dc9bf1669660827d5a6bc80f7
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81115994"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>Esercitazione: Analisi dei dati Python per sviluppatori SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa esercitazione per programmatori SQL vengono fornite informazioni sull'integrazione di Python mediante la creazione e la distribuzione di una soluzione di Machine Learning basata su Python usando un database [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) in SQL Server. Si useranno T-SQL, SQL Server Management Studio e un'istanza del motore di database con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) e il supporto del linguaggio Python.

Questa esercitazione presenta le funzioni Python usate in un flusso di lavoro di modellazione dei dati. I passaggi includono l'esplorazione dei dati, la creazione e il training di un modello di classificazione binaria e la distribuzione del modello. Verranno usati i dati di esempio di New York City Taxi e Limosine Commission e il modello creato sarà in grado di stimare se è probabile che per una corsa venga lasciata una mancia, in base all'ora del giorno, alla distanza percorsa e al luogo di partenza della corsa. 

Viene eseguito il wrapping di tutto il codice Python usato in questa esercitazione in stored procedure create ed eseguite in Management Studio.

> [!NOTE]
> Questa esercitazione è disponibile sia in R che in Python. Per la versione R, vedere [Analisi nel database per sviluppatori R](sqldev-in-database-r-for-sql-developers.md).

## <a name="overview"></a>Panoramica

Il processo di creazione di una soluzione di Machine Learning è complesso e può richiedere l'uso di più strumenti e il coordinamento di esperti in materia in diverse fasi:

+ recupero e pulizia dei dati
+ esplorazione dei dati e creazione di caratteristiche utili per la modellazione
+ training e ottimizzazione del modello
+ distribuzione nell'ambiente di produzione

Per lo sviluppo e i test del codice effettivo è opportuno usare un ambiente di sviluppo dedicato. Dopo che lo script è stato testato, è tuttavia possibile distribuirlo facilmente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] nell'ambiente familiare di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Il wrapping del codice esterno nelle stored procedure è il meccanismo principale per rendere operativo il codice in SQL Server.

Questa esercitazione in più parti presenta un flusso di lavoro tipico per l'esecuzione di analisi nel database con Python e SQL Server ed è rivolta a programmatori SQL che non hanno familiarità con Python o sviluppatori Python che non hanno familiarità con SQL. 

+ [Lezione 1: Esplorare e visualizzare i dati usando Python](sqldev-py3-explore-and-visualize-the-data.md)

+ [Lezione 2: Creare caratteristiche dei dati usando funzioni SQL personalizzate](sqldev-py4-create-data-features-using-t-sql.md)

+ [Lezione 3: Eseguire il training e il salvataggio di un modello Python usando T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [Lezione 4: Stimare i risultati potenziali usando un modello Python in una stored procedure](sqldev-py6-operationalize-the-model.md)

Dopo aver salvato il modello nel database, è possibile chiamarlo per eseguire stime da [!INCLUDE[tsql](../../includes/tsql-md.md)] usando le stored procedure.

## <a name="prerequisites"></a>Prerequisiti

+ [Machine Learning Services per SQL Server con Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Autorizzazioni](../security/user-permission.md)

+ [Database demo NYC Taxi](demo-data-nyctaxi-in-sql.md)

Tutte le attività possono essere eseguite usando stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

Questa esercitazione presuppone una certa familiarità con le operazioni di database di base, ad esempio la creazione di database e tabelle, l'importazione di dati e la scrittura di query SQL. Non presuppone la conoscenza di Python. Per questo motivo, viene fornito tutto il codice Python. 

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esplorare e visualizzare i dati usando Python](sqldev-py3-explore-and-visualize-the-data.md)
