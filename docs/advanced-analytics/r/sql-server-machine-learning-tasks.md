---
title: Ciclo di vita e processo per i team - SQL Server Machine Learning Services di Machine learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2218034dd6ac4cc3e7926b214c5c021815e57ed3
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432204"
---
# <a name="machine-learning-lifecycle-and-personas"></a>Gli utenti tipo e il ciclo di vita di machine learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Progetti di Machine learning possono essere complessi, poiché richiedono le proprie conoscenze e collaborazione di un set diverso di professionisti. Questo articolo descrive le attività dell'entità di machine learning del ciclo di vita, il tipo di professionisti di dati che sono impegnati in machine learning e modo in cui SQL Server supporta le esigenze.

> [!TIP]
> 
> Prima di iniziare a su un progetto di machine learning, è consigliabile rivedere gli strumenti e le procedure consigliate fornite dal [Microsoft Team Data Science Process](https://blogs.technet.microsoft.com/machinelearning/2017/10/09/the-microsoft-team-data-science-process-tdsp-recent-updates/), o TDSP. Questo processo è stato creato di machine learning i consulenti Microsoft per consolidare le procedure consigliate per la pianificazione e l'iterazione di progetti di machine learning. Il TDSP ha le sue radici nella standard di settore come CRISP-DM, ma prevede procedure di recente, ad esempio DevOps e la visualizzazione.

## <a name="machine-learning-life-cycle"></a>Ciclo di vita di Machine learning

Machine learning è un processo complesso che interessa tutti gli aspetti dei dati aziendali e molti progetti di apprendimento automatico alla fine richiede più tempo e che sia più complessa previsto. Ecco alcuni dei metodi di apprendimento richiede il supporto dei professionisti di dati nell'organizzazione:

+ Apprendimento automatico inizia con l'identificazione degli obiettivi e le regole di business.
+ I professionisti di Machine learning necessario considerare i criteri per l'archiviazione e l'estrazione di dati di controllo.
+ Raccolta di dati potenzialmente applicabili è successivo.  Origini dati devono essere identificate ed estratti i dati appropriati da sensori e applicazioni aziendali. 
+ La qualità delle attività di machine learning è altamente dipendente da non solo il tipo di dati che sono disponibili, ma i processi molto usati per l'estrazione, l'elaborazione e l'archiviazione dei dati. 
+ Nessun progetto di machine learning sarebbe incompleta senza una strategia per la creazione di report e analisi e probabilmente il coinvolgimento dei clienti e i suggerimenti.

SQL Server consente di colmare molte delle lacune tra esperti di machine learning e professionisti di dati dell'organizzazione:

+ I dati possono essere archiviati in locale o nel cloud
+ SQL Server è integrato in ogni fase dell'elaborazione dei dati aziendali, tra cui reporting ed ETL
+ SQL Server supporta la protezione dei dati, la ridondanza dei dati e controllo
+ Fornisce governance delle risorse

## <a name="data-scientists"></a>I data Scientist

I data Scientist usano un'ampia gamma di strumenti per machine learning, che vanno da Excel o piattaforme open source gratuite, a Suite statistiche costose che richiedono conoscenze tecniche approfondite e analisi dei dati. Tuttavia, tramite R o Python con SQL Server offre alcuni vantaggi esclusivi rispetto a questi strumenti tradizionali:

+ È possibile sviluppare e testare una soluzione tramite l'ambiente di sviluppo preferito, quindi distribuire il codice R o Python come parte del codice T-SQL.
+ Spostare i calcoli complessi il portatile dell'esperto di dati e al server, evitando spostamenti di dati per soddisfare i criteri di sicurezza aziendali.
+ Scalabilità e prestazioni vengono migliorate attraverso API e pacchetti R speciali. Si è più alcuna limitazione per l'architettura a thread singolo associata alla memoria di R e lavorare con grandi set di dati e calcoli multithread, multicore e multiprocesso.
+ Portabilità del codice: Le soluzioni possono eseguire in SQL Server o in Hadoop o Linux, usando [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Codice una sola volta, ma distribuito ovunque.

## <a name="application-and-database-developers"></a>Sviluppatori di applicazioni e database

Gli sviluppatori di database si occupano di integrare più tecnologie e raggruppare i risultati in modo che possano essere condivisi in tutta l'organizzazione. Lo sviluppatore del database funziona con gli sviluppatori di applicazioni, SQL, data Scientist e sviluppatori per progettare soluzioni, metodi di gestione dati, è consigliabile e definire l'architettura o distribuire soluzioni.

Integrazione con SQL Server offre numerosi vantaggi agli sviluppatori di dati:

+ I data scientist può lavorare in RStudio, mentre lo sviluppatore di dati consente di distribuire la soluzione usando SQL Server Management Studio. Non è più ricodifica delle soluzioni R o Python.
+ Ottimizza le soluzioni usando il meglio di T-SQL, R e Python. Operazioni complesse su grandi set di dati possono essere eseguite in modo molto più efficiente usando SQL Server che in R. usare la conoscenza dei tuoi professionisti di database per migliorare le prestazioni delle soluzioni di machine learning, con gli indici columnstore in memoria, e aggregazioni tramite operazioni basate su set SQL. 
+ Automatizzare facilmente le attività che devono essere eseguito più volte su grandi quantità di dati, ad esempio la generazione di punteggi di stima sui dati di produzione. 
+ Accesso con parametri dello script R o Python da qualsiasi applicazione che usa [!INCLUDE[tsql](../../includes/tsql-md.md)]. Semplicemente chiamare una stored procedure per eseguire il training di un modello, generare un grafico o stime di output.
+ Le API possono trasmettere grandi set di dati e trarre vantaggio da calcoli nel database multithread, multicore, multiprocesso.

Per informazioni sulle attività correlate, vedere:
+ [Operatività del codice R](../../advanced-analytics/r/operationalizing-your-r-code.md)

### <a name="database-administrators"></a>Amministratori di database

Gli amministratori del database devono integrare progetti e priorità in concorrenza all'interno di un singolo punto di contatto: il server di database. È necessario specificare l'accesso ai dati non solo per gli esperti, ma per un'ampia gamma di sviluppatori di report, analisti aziendali e fruitori dei dati aziendali, mantenendo l'integrità degli archivi dei dati operativi e dei report. Nell'organizzazione, l'amministratore di database è una parte fondamentale della compilazione e distribuzione di un'infrastruttura efficace per l'analisi scientifica dei dati. 

SQL Server fornisce funzionalità univoche per l'amministratore di database che deve supportare il ruolo della scienza dei dati:

+ Sicurezza da SQL Server: L'architettura di [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] mantiene i database protetti e isola l'esecuzione delle sessioni di script esterni dall'operazione dell'istanza del database. È possibile specificare a chi è autorizzato a eseguire gli script di machine learning e usare i ruoli del database per gestire i pacchetti.

+ Le sessioni di R e Python sono eseguite in un processo separato per garantire che il server continui a funzionare normalmente anche se vengono riscontrati problemi in script esterno.

+ Governance delle risorse utilizzando SQL Server consente di controllare la memoria e processi allocati al runtime esterni, per evitare che calcoli di grande da entità possano compromettere le prestazioni complessive del server.

Per informazioni sulle attività correlate, vedere:
+ [Gestione e monitoraggio delle soluzioni di apprendimento automatico](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

## <a name="architects-and-data-engineers"></a>Gli architetti e i dati tecnici

Gli architetti progettano flussi di lavoro integrati che si estendono su tutti gli aspetti del ciclo di vita di machine learning. Data Engineer di progettazione e compilano soluzioni ETL e determinare come ottimizzare le attività di progettazione di funzionalità di machine learning. L'intera piattaforma dati deve essere progettata per bilanciare le esigenze aziendali concorrenti.

Grazie alla stretta integrazione di [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] con altri strumenti Microsoft, come lo stack di data warehouse e business intelligence, strumenti di mobilità e cloud aziendali e Hadoop, gli ingegneri dei dati o agli architetti di sistema che vogliono promuovere analisi avanzate hanno a disposizione numerosi vantaggi.

+ Chiamare uno script Python o R tramite stored procedure di sistema, per popolare i set di dati, generare grafici o ottenere stime. Nessun ulteriori Progettazione flussi di lavoro paralleli in analisi scientifica dei dati e gli strumenti ETL. Supporto per Azure Data Factory e Database SQL di Azure rende più semplice utilizzare le origini dati cloud in flussi di lavoro di apprendimento automatico.

+ Per la pianificazione e gestione delle attività di machine learning, usare i flussi di lavoro di automazione standard in SQL Server, basata su Integration Services, SQL Agent o Azure Data Factory. In alternativa, usare il [funzionalità di messa in funzione](https://docs.microsoft.com/machine-learning-server/operationalize/how-to-deploy-web-service-publish-manage-in-r) in Machine Learning Server.

Per informazioni sulle attività correlate, vedere:

+ [Creazione di flussi di lavoro di machine learning in SQL Server](../../advanced-analytics/r/creating-workflows-that-use-r-in-sql-server.md)

