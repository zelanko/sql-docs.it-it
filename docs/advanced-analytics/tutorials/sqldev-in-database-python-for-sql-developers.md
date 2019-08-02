---
title: Esercitazione per l'analisi Python nel database per sviluppatori SQL
description: Informazioni su come incorporare il codice Python in SQL Server stored procedure e funzioni T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9d3905ef9434bf4d3f887130c6f67ad68c6a6e36
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714758"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>Esercitazione: Analisi dei dati Python per sviluppatori SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa esercitazione per i programmatori SQL, informazioni sull'integrazione di Python mediante la compilazione e la distribuzione di una soluzione di apprendimento automatico basata su Python usando un database [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) in SQL Server. Si useranno T-SQL, SQL Server Management Studio e un'istanza del motore di database con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) e il supporto del linguaggio Python.

Questa esercitazione presenta le funzioni Python usate in un flusso di lavoro di modellazione dei dati. I passaggi includono l'esplorazione dei dati, la compilazione e il training di un modello di classificazione binaria e la distribuzione del modello. Verranno usati i dati di esempio di New York City taxi e limosine Commission e il modello che verrà compilato prevede se una corsa può comportare un suggerimento in base all'ora del giorno, alla distanza e alla località di ritiro. 

Tutto il codice Python utilizzato in questa esercitazione viene incluso nelle stored procedure create ed eseguite in Management Studio.

> [!NOTE]
> Questa esercitazione è disponibile in R e Python. Per la versione R, vedere [analisi nel database per sviluppatori r](sqldev-in-database-r-for-sql-developers.md).

## <a name="overview"></a>Panoramica

Il processo di creazione di una soluzione di apprendimento automatico è un sistema complesso che può coinvolgere più strumenti e il coordinamento di esperti in materia in diverse fasi:

+ recupero e pulizia dei dati
+ esplorazione dei dati e creazione di funzionalità utili per la modellazione
+ Training e ottimizzazione del modello
+ distribuzione in produzione

Lo sviluppo e il test del codice effettivo vengono eseguiti in modo ottimale usando un ambiente di sviluppo dedicato. Tuttavia, dopo che lo script è stato testato completamente, è possibile distribuirlo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)] modo semplice utilizzando le stored procedure nell' [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ambiente familiare di. Il wrapping del codice esterno nelle stored procedure è il meccanismo principale per il codice operatività in SQL Server.

Questa esercitazione in più parti introduce un flusso di lavoro tipico per l'esecuzione di analisi nel database con Python e SQL Server, se si è un programmatore SQL nuovo per Python o uno sviluppatore di Python nuovo in SQL. 

+ [Lezione 1: Esplorare e visualizzare i dati con Python](sqldev-py3-explore-and-visualize-the-data.md)

+ [Lezione 2: Creare funzionalità di dati usando funzioni SQL personalizzate](sqldev-py4-create-data-features-using-t-sql.md)

+ [Lezione 3: Eseguire il training e salvare un modello Python usando T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [Lezione 4: Stimare potenziali risultati usando un modello Python in un stored procedure](sqldev-py6-operationalize-the-model.md)

Dopo che il modello è stato salvato nel database, è possibile chiamare il modello per le stime da [!INCLUDE[tsql](../../includes/tsql-md.md)] tramite stored procedure.

## <a name="prerequisites"></a>Prerequisiti

+ [SQL Server Machine Learning Services con Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Autorizzazioni](../security/user-permission.md)

+ [Database demo di NYC Taxi](demo-data-nyctaxi-in-sql.md)

Tutte le attività possono essere eseguite [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzando stored procedure [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]in.

Questa esercitazione presuppone una certa familiarità con le operazioni di database di base, ad esempio la creazione di database e tabelle, l'importazione di dati e la scrittura di query SQL. Non presuppone che si conosca Python. Di conseguenza, viene fornito tutto il codice Python. 

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esplorare e visualizzare i dati con Python](sqldev-py3-explore-and-visualize-the-data.md)
