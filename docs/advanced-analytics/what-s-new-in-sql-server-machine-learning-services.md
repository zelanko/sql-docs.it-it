---
title: Cosa&#39;nuovo - s SQL Server Machine Learning Services
description: Nuovo gli annunci di funzionalità per ogni versione di SQL Server 2016 R Services, R Server, servizi Machine Learning di SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/18/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 4a3450b308918e51b370865db4ad2bedeb8e004c
ms.sourcegitcommit: e3f5b70bbb4c66294df8c7b2c70186bdf2365af9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2019
ms.locfileid: "54397620"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>Novità in servizi di SQL Server Machine Learning 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Funzionalità di Machine learning vengono aggiunti a SQL Server in ogni versione per continuare a espandere, estendere e approfondire l'integrazione tra la piattaforma dati, analitica avanzate e analisi scientifica dei dati. 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>Novità in preview di SQL Server 2019

Questa versione aggiunge le funzionalità di richiesta per R e Python operazioni di machine learning in SQL Server. Per altre informazioni su tutte le funzionalità in questa versione, vedere [What ' s New in SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) e [note sulla versione di SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

| Versione | Aggiornamento delle funzionalità |
|---------|----------------|
| CTP 2.0 | Supporto della piattaforma Linux per R e Python di machine learning. Introduzione [installare SQL Server Machine Learning Services in Linux](../linux/sql-server-linux-setup-machine-learning.md). |
|   | [Estensione del linguaggio Java](java/extension-java.md) sia Windows che Linux è stata introdotta in anteprima di SQL Server 2019. È possibile rendere Java compilata di codice disponibili per SQL Server assegnando autorizzazioni e impostazione del percorso. App client con accesso a SQL Server può usare i dati ed eseguire il codice chiamando [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), la stessa procedura usata per l'integrazione di R e Python in SQL Server. | 
|  | Il [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) introduce due nuovi parametri che consentono di generare facilmente più modelli di dati partizionati. Altre informazioni in questa esercitazione [creare i modelli basati su partizioni in R](tutorials/r-tutorial-create-models-per-partition.md). |
|   | Supporto per il cluster di failover è ora supportato in Windows e Linux, presupponendo che il servizio Launchpad di SQL Server viene avviato in tutti i nodi. Per altre informazioni, vedere [installazione di cluster di failover di SQL Server](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md). |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>Novità di SQL Server 2017

Questa versione aggiunge [supporto di Python e leader di settore algoritmi di machine learning](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Rinominati per riflettere il nuovo ambito, l'introduzione di segni di SQL Server 2017 [SQL Server Machine Learning Services (In-Database)](what-is-sql-server-machine-learning.md), con supporto del linguaggio per Python e R. 

Per funzionalità annunci completa, vedere [What ' s New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

### <a name="r-enhancements"></a>Miglioramenti di R

Il componente di R di Machine Learning Services di SQL Server 2017 è la prossima generazione di SQL Server 2016 R Services, con le versioni aggiornate di altri pacchetti R di base e RevoScaler.

Le nuove funzionalità per R includono [ **Gestione pacchetti**](r/install-additional-r-packages-on-sql-server.md), con le caratteristiche principali seguenti: 

+ Ruoli predefiniti del database consentono gli amministratori di database di gestire i pacchetti e assegnare le autorizzazioni per l'installazione del pacchetto.
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) gli amministratori di database consente di gestire i pacchetti nel familiare linguaggio T-SQL.
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) funzioni consentono di installare, rimuovere o elencare i pacchetti di proprietà da parte degli utenti. Per altre informazioni, vedere [pacchetti di come usare funzioni RevoScaleR per trovare o installare R in SQL Server](r/use-revoscaler-to-manage-r-packages.md).

### <a name="r-libraries"></a>Librerie di R

| Pacchetto | Descrizione |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | In questa versione, MicrosoftML è incluso in un'installazione di R predefinita, eliminando la fase di aggiornamento richiesto nella precedente di SQL Server 2016 R Services. MicrosoftML offre d'avanguardia di machine learning algoritmi e trasformazioni dei dati che possono essere ridimensionate o eseguire in contesti di calcolo remoti. Gli algoritmi sono personalizzabili reti neurali profonde, alberi delle decisioni veloci e foreste delle decisioni, regressione lineare e la regressione logistica.  |

### <a name="python-integration-for-in-database-analytics"></a>Integrazione di Python per analitica nel database

Python è un linguaggio che offre una notevole flessibilità e potenza per un'ampia gamma di attività di machine learning. Librerie open source per Python includono diverse piattaforme per le reti neurali personalizzabile, nonché librerie comunemente diffuse per elaborazione in linguaggio naturale. A questo punto, questo linguaggio diffuso è supportato in SQL Server 2017 Machine Learning.

Poiché Python è integrato con il motore di database, puoi mantenere analitica vicino ai dati ed eliminare i costi e rischi di sicurezza associati allo spostamento dei dati. È possibile distribuire soluzioni di machine learning basate su Python usando strumenti come Visual Studio. Le applicazioni di produzione possono ottenere stime, modelli, o gli oggetti visivi dal runtime di Python 3.5 usando i dati di SQL Server di accesso ai metodi.

Integrazione di T-SQL e Python è supportata tramite il [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure di sistema. È possibile chiamare qualsiasi codice Python tramite questa stored procedure. Codice viene eseguito in un'architettura sicura e duale che consente la distribuzione aziendale di script, è possibile chiamare da un'applicazione usando una semplice stored procedure e modelli di Python. È possibile ottenere miglioramenti aggiuntivi relativi alle prestazioni da dati di streaming da SQL per processi Python e la parallelizzazione di anello MPI.

È possibile usare l'istruzione T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) funzione eseguire [assegnazione dei punteggi nativa](sql-native-scoring.md) su un modello con training preliminare che è stato salvato in precedenza nel formato binario richiesto.

### <a name="python-libraries"></a>Librerie Python

| Pacchetto | Descrizione |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Python equivalente di RevoScaleR. È possibile creare modelli di Python per la regressione lineare e logistica, alberi delle decisioni, alberi con Boosting e foreste casuali, tutti eseguibili in parallelo e in grado di in esecuzione in contesti di calcolo remoti. Questo pacchetto supporta l'utilizzo di più origini dati e contesti di calcolo remoti. I data scientist o sviluppatore può eseguire codice Python in un Server SQL remoto, per esplorare i dati e compilare modelli senza spostare i dati. |
|[**microsoftml**](python/ref-py-microsoftml.md) |Python-equivalente del pacchetto MicrosoftML R. |

### <a name="pre-trained-models"></a>Modelli con training preliminare

[**I modelli con training preliminare** ](install/sql-pretrained-models-install.md) sono disponibili per Python e R. questi modelli per il riconoscimento di immagini e analisi del sentiment negativo positivo, utilizzati per generare stime usando dati personalizzati. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>Server autonomo come funzionalità condivisa nel programma di installazione di SQL Server

Questa versione aggiunge inoltre [SQL Server Machine Learning Server (Standalone)](r/r-server-standalone.md), un server di analisi scientifica dei dati completamente indipendenti, che supporta analitica predittiva e statistiche in R e Python. Come con R Services. per questo server è la prossima versione di SQL Server 2016 R Server (Standalone). Con il server autonomo, è possibile distribuire e ridimensionare le soluzioni R o Python senza dipendenze in SQL Server.
::: moniker-end

## <a name="new-in-sql-server-2016"></a>Novità di SQL Server 2016

Questa versione introdotte funzionalità di machine learning in SQL Server attraverso **SQL Server 2016 R Services**, un motore di analitica nel database per lo script di elaborazione R sui dati residenti all'interno di un'istanza del motore di database.

È inoltre **SQL Server 2016 R Server (Standalone)** è stato rilasciato come un modo per installare R Server in un server di Windows. Il programma di installazione di SQL Server fornite inizialmente, l'unico modo per installare R Server per Windows. Nelle versioni successive, gli sviluppatori e data Scientist che volevano R Server in Windows è stato possibile usare un altro programma di installazione autonomo per ottenere lo stesso scopo. Il server autonomo di SQL Server è funzionalmente equivalente al prodotto server autonomo, [Microsoft R Server per Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Per funzionalità annunci completa, vedere [What ' s New in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

| Versione |Aggiornamento delle funzionalità |
|---------|----------------|
| CU aggiunte | [**Assegnazione dei punteggi in tempo reale** ](real-time-scoring.md) si basa sulle librerie di C++ native per leggere un modello archiviato in un formato binario ottimizzato e quindi generare stime senza la necessità di chiamare il runtime R. Questo rende molto più veloci le operazioni di assegnazione dei punteggi. Con l'assegnazione dei punteggi in tempo reale, è possibile eseguire una stored procedure o assegnazione dei punteggi in tempo reale dal codice R. Assegnazione dei punteggi in tempo reale è disponibile anche per SQL Server 2016, se l'istanza viene aggiornato alla versione più recente di [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]. |
| Versione iniziale | [**Integrazione di R per analitica nel database**](r/sql-server-r-services.md). <br/><br/> I pacchetti R per R chiamante funzioni in T-SQL e viceversa. Funzioni RevoScaleR forniscono analitica R su larga scala tramite la suddivisione in blocchi di dati in parti di componente, il coordinamento e gestione di elaborazione distribuita e l'aggregazione di risultati. In SQL Server 2016 R Services (In-Database), il motore di RevoScaleR è integrato con un'istanza del motore di database, salamoia insieme nello stesso contesto di elaborazione analitica e dati. <br/><br/>Integrazione di T-SQL e R attraverso [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). È possibile chiamare qualsiasi codice R tramite questa stored procedure. Questa infrastruttura protetta consente la distribuzione aziendale di Rn modelli e gli script che possono essere chiamati da un'applicazione con una semplice stored procedure. È possibile ottenere miglioramenti aggiuntivi relativi alle prestazioni da dati di streaming da SQL ai processi R e la parallelizzazione di anello MPI. <br/><br/>È possibile usare l'istruzione T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md) funzione eseguire [assegnazione dei punteggi nativa](sql-native-scoring.md) su un modello con training preliminare che è stato salvato in precedenza nel formato binario richiesto.|

## <a name="linux-support-roadmap"></a>Guida di orientamento per supporto Linux

SQL Server 2019 CTP 2.0 aggiunge il supporto Linux per R, Python e Java durante l'installazione di machine learning i pacchetti con un'istanza del motore di database. Per altre informazioni, vedere [installare SQL Server Machine Learning Services in Linux](../linux/sql-server-linux-setup-machine-learning.md).

In Linux, SQL Server 2017 è privo di integrazione di R o Python, ma è possibile usare [assegnazione dei punteggi nativa](sql-native-scoring.md) in Linux perché tale funzionalità è disponibile tramite T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md), che viene eseguita in Linux. Punteggio nativo consente a prestazioni elevate di assegnazione dei punteggi da un modello con training preliminare, senza chiamare o anche richiedere un runtime di R.

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Servizi di Database SQL di Azure Machine Learning

Servizi di Machine Learning (con R) nel Database SQL di Azure è disponibile in anteprima pubblica. Per altre informazioni, vedere [Guida introduttiva: Usare Machine Learning Services (con R) nel Database SQL di Azure (anteprima)](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-r).

## <a name="next-steps"></a>Passaggi successivi

+ [Installare SQL Server 2017 Machine Learning Services (In-Database)](install/sql-machine-learning-services-windows-install.md)
+ [Esempi ed esercitazioni di machine learning](tutorials/machine-learning-services-tutorials.md)
