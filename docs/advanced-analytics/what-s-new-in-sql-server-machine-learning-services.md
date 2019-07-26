---
title: Novità | Microsoft Docs
description: Nuovi annunci di funzionalità per ogni versione di SQL Server 2016 R Services, R Server SQL Server 2017 Machine Learning Services.
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: c466c7e039e515be4ef65b4f5680ece2e1d861a8
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468980"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>Novità di SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Le funzionalità di Machine Learning vengono aggiunte a SQL Server in ogni versione Man volta che si continua a espandere, estendere e approfondire l'integrazione tra la piattaforma dati, l'analisi avanzata e la data science. 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>Novità di SQL Server 2019 Preview

Questa versione aggiunge le funzionalità principali richieste per le operazioni R e Python Machine Learning in SQL Server. Per ulteriori informazioni su tutte le funzionalità di questa versione, vedere Novità di [SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) e [Note sulla versione per SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

> [!NOTE]
> Per informazioni sulle novità di Java in SQL Server 2019, vedere la pagina relativa alle [novità di SQL Server Language Extensions?](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new)

| Versione | Aggiornamento delle funzionalità |
|---------|----------------|
| CTP 3.0 | Nessuna modifica. |
| CTP 2.5 | Nessuna modifica. |
| CTP 2.4 | Supporto Linux per [Create external Library (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) per R e Python. |
| CTP 2.3 | Solo in Windows, è possibile accedere al codice Python in una libreria esterna usando l'istruzione [Create external Library (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) . |
| CTP 2.2 | Nessuna modifica. |
| CTP 2.1 | Nessuna modifica. |
| CTP 2.0 | Supporto della piattaforma Linux per R e Python Machine Learning. Introduzione all' [installazione di SQL Server Machine Learning Services in Linux](../linux/sql-server-linux-setup-machine-learning.md). |
|  | [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) introduce due nuovi parametri che consentono di generare facilmente più modelli da dati partizionati. Per altre informazioni, vedere l'esercitazione [creare modelli basati su partizioni in R](tutorials/r-tutorial-create-models-per-partition.md). |
|   | Il supporto per i cluster di failover è ora supportato in Windows e Linux, presupponendo che Launchpad di SQL Server servizio venga avviato in tutti i nodi. Per ulteriori informazioni, vedere [SQL Server installazione del cluster di failover](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md). |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>Novità di SQL Server 2017

Questa versione aggiunge il [supporto Python e gli algoritmi di Machine Learning leader del settore](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/). Rinominata per riflettere il nuovo ambito, SQL Server 2017 contrassegna l'introduzione del [Machine Learning Services di SQL Server (in-database)](what-is-sql-server-machine-learning.md)con il supporto del linguaggio per Python e R. 

Per gli annunci di funzionalità, vedere Novità [di SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

### <a name="r-enhancements"></a>Miglioramenti di R

Il componente R di SQL Server 2017 Machine Learning Services è la nuova generazione di SQL Server 2016 R Services, con versioni aggiornate di base R, RevoScaler e altri pacchetti.

Le nuove funzionalità per R includono la [**gestione dei pacchetti**](r/install-additional-r-packages-on-sql-server.md), con le caratteristiche seguenti: 

+ I ruoli del database consentono DBA di gestire i pacchetti e di assegnare le autorizzazioni per l'installazione del pacchetto.
+ [Create external Library](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) consente a DBA di gestire i pacchetti nel linguaggio T-SQL familiare.
+ Le funzioni [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md) consentono di installare, rimuovere o elencare i pacchetti di proprietà degli utenti. Per altre informazioni, vedere [How to use RevoScaleR Functions to find or install R packages on SQL Server](r/use-revoscaler-to-manage-r-packages.md).

### <a name="r-libraries"></a>Librerie R

| Pacchetto | Descrizione |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | In questa versione, MicrosoftML è incluso in un'installazione di R predefinita, eliminando la fase di aggiornamento necessaria nei SQL Server precedenti 2016 R Services. MicrosoftML fornisce algoritmi di apprendimento automatico e trasformazioni dei dati all'avanguardia che possono essere ridimensionati o eseguiti in contesti di calcolo remoti. Gli algoritmi includono reti neurali profonde personalizzabili, alberi delle decisioni e foreste delle decisioni rapide, regressione lineare e regressione logistica.  |

### <a name="python-integration-for-in-database-analytics"></a>Integrazione di Python per l'analisi nel database

Python è un linguaggio che offre grande flessibilità e potenza per un'ampia gamma di attività di machine learning. Le librerie open source per Python includono diverse piattaforme per le reti neurali personalizzabili, nonché le librerie più diffuse per l'elaborazione del linguaggio naturale. Questo linguaggio ampiamente usato è ora supportato in SQL Server 2017 Machine Learning.

Poiché Python è integrato con il motore di database, è possibile gestire le analisi vicine ai dati ed eliminare i costi e i rischi di protezione associati allo spostamento dei dati. È possibile distribuire soluzioni di Machine Learning basate su Python usando strumenti come Visual Studio. Le applicazioni di produzione possono ottenere stime, modelli o oggetti visivi dal runtime Python 3,5 usando SQL Server metodi di accesso ai dati.

L'integrazione con T-SQL e Python è supportata tramite il sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure. È possibile chiamare qualsiasi codice Python usando questo stored procedure. Il codice viene eseguito in un'architettura duale sicura che consente la distribuzione di livello aziendale di script e modelli Python, richiamabili da un'applicazione usando una semplice stored procedure. I miglioramenti delle prestazioni aggiuntivi si ottengono tramite lo streaming dei dati da SQL ai processi Python e la parallelizzazione degli anelli MPI.

È possibile usare la funzione T-SQL [Predict](../t-sql/queries/predict-transact-sql.md) per eseguire il [Punteggio nativo](sql-native-scoring.md) in un modello con training preliminare salvato in precedenza nel formato binario richiesto.

### <a name="python-libraries"></a>Librerie Python

| Pacchetto | Descrizione |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Python equivalente a RevoScaleR. È possibile creare modelli Python per regressioni lineari e logistiche, alberi delle decisioni, alberi con boosting e foreste casuali, tutti eseguibili e in grado di essere eseguiti in contesti di calcolo remoti. Questo pacchetto supporta l'uso di più origini dati e contesti di calcolo remoti. Il data scientist o lo sviluppatore può eseguire codice Python su un SQL Server remoto, per esplorare i dati o creare modelli senza trasferire i dati. |
|[**microsoftml**](python/ref-py-microsoftml.md) |Python: equivalente del pacchetto R MicrosoftML. |

### <a name="pre-trained-models"></a>Modelli con training preliminare

Sono disponibili [**modelli con training preliminare**](install/sql-pretrained-models-install.md) per Python e R. usare questi modelli per il riconoscimento delle immagini e l'analisi dei sentimenti negativi positivi, per generare stime sui propri dati. 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>Server autonomo come funzionalità condivisa nell'installazione di SQL Server

Questa versione aggiunge anche [SQL Server machine learning Server (autonomo)](r/r-server-standalone.md), un server Data Science completamente indipendente, che supporta l'analisi statistica e predittiva in R e Python. Come per R Services, questo server è la versione successiva di SQL Server 2016 R Server (standalone). Con il server autonomo è possibile distribuire e ridimensionare soluzioni R o Python senza dipendenze da SQL Server.
::: moniker-end

## <a name="new-in-sql-server-2016"></a>Novità di SQL Server 2016

Questa versione ha introdotto le funzionalità di Machine Learning in SQL Server tramite **2016 SQL Server r Services**, un motore di analisi nel database per l'elaborazione di script R sui dati residenti all'interno di un'istanza del motore di database.

Inoltre, **SQL Server 2016 R Server (standalone)** è stato rilasciato come modo per installare R server in un server Windows. Inizialmente, SQL Server installazione ha fornito l'unico modo per installare R Server per Windows. Nelle versioni successive, gli sviluppatori e i data scientist che volevano R Server in Windows potevano usare un altro programma di installazione autonomo per ottenere lo stesso obiettivo. Il server autonomo in SQL Server è equivalente dal punto di vista funzionale al prodotto server autonomo, [Microsoft R server per Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Per gli annunci di funzionalità, vedere Novità [di SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

| Versione |Aggiornamento delle funzionalità |
|---------|----------------|
| Aggiunte CU | Il [**punteggio in tempo reale**](real-time-scoring.md) si basa sulle C++ librerie native per leggere un modello archiviato in un formato binario ottimizzato e quindi genera stime senza dover chiamare il runtime di R. Questo rende più veloci le operazioni di assegnazione dei punteggi. Con l'assegnazione dei punteggi in tempo reale, è possibile eseguire un stored procedure o eseguire il punteggio in tempo reale dal codice R. Il Punteggio in tempo reale è disponibile anche per SQL Server 2016, se l'istanza viene aggiornata alla versione più recente [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]di. |
| Versione iniziale | [**Integrazione di R per l'analisi nel database**](r/sql-server-r-services.md). <br/><br/> Pacchetti r per la chiamata di funzioni R in T-SQL e viceversa. Le funzioni RevoScaleR forniscono analisi R su larga scala suddividendo i dati in parti componenti, coordinando e gestendo l'elaborazione distribuita e aggregando i risultati. In SQL Server 2016 R Services (in-database), il motore RevoScaleR è integrato con un'istanza del motore di database, l'analisi dei dati e l'analisi dei dati nello stesso contesto di elaborazione. <br/><br/>Integrazione di T-SQL e R tramite [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). È possibile chiamare qualsiasi codice R usando questo stored procedure. Questa infrastruttura sicura consente la distribuzione di livello aziendale di modelli e script RN che possono essere chiamati da un'applicazione usando una semplice stored procedure. I miglioramenti delle prestazioni aggiuntivi si ottengono tramite il flusso dei dati dai processi SQL ai processi R e dalla parallelizzazione degli anelli MPI. <br/><br/>È possibile usare la funzione T-SQL [Predict](../t-sql/queries/predict-transact-sql.md) per eseguire il [Punteggio nativo](sql-native-scoring.md) in un modello con training preliminare salvato in precedenza nel formato binario richiesto.|

## <a name="linux-support-roadmap"></a>Guida di orientamento per Linux

SQL Server 2019 CTP 2,3 aggiunge il supporto Linux per R e Python quando si installano i pacchetti di Machine Learning con un'istanza del motore di database. Per altre informazioni, vedere [Install SQL Server Machine Learning Services on Linux](../linux/sql-server-linux-setup-machine-learning.md).

In Linux SQL Server 2017 non ha l'integrazione con R o Python, ma è possibile usare il [Punteggio nativo](sql-native-scoring.md) in Linux perché tale funzionalità è disponibile tramite la [stima](../t-sql/queries/predict-transact-sql.md)T-SQL, che viene eseguita in Linux. Il Punteggio nativo consente il punteggio a prestazioni elevate da un modello pretrainato, senza chiamare o persino richiedere un runtime R.

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Machine Learning Services nel database SQL di Azure

Machine Learning Services (con R) nel database SQL di Azure è in anteprima pubblica. Per altre informazioni, vedere [database SQL di Azure Machine Learning Services con R (anteprima)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview).

## <a name="next-steps"></a>Passaggi successivi

+ [Installare SQL Server Machine Learning Services 2017 (in-database)](install/sql-machine-learning-services-windows-install.md)
+ [Esercitazioni ed esempi di Machine Learning](tutorials/machine-learning-services-tutorials.md)
