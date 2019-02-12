---
title: Linguaggio R e integrazione delle funzionalità Python - servizi di SQL Server Machine Learning
description: Linguaggio R e le funzionalità di Python in SQL Server, l'integrazione con i dati relazionali per l'analisi scientifica dei dati e modellazione statistica, modelli di machine learning, analitica predittiva, visualizzazione dei dati e altro ancora.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 283f39efa34721aea7613ac1a9cba115dc3311a8
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032952"
---
# <a name="machine-learning-services-r-python-in-sql-server-2017"></a>Machine Learning Services (R, Python) in SQL Server 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Machine Learning Services di SQL Server 2017 è un componente aggiuntivo a un'istanza di motore di database, utilizzato per l'esecuzione di codice R e Python in SQL Server. La funzionalità include [pacchetti di Microsoft R e Python](#components) per prestazioni elevate analitica predittiva e machine learning. Codice viene eseguito in un framework di estendibilità, isolata da processi del motore di base, ma completamente disponibile per i dati relazionali come stored procedure, come script T-SQL contenente le istruzioni di R o Python o R o Python codice contenente T-SQL. 

Se è stato usato in precedenza [SQL Server 2016 R Services](r/sql-server-r-services.md), servizi di Machine Learning in SQL Server 2017 è la prossima generazione di supporto di R, con le versioni aggiornate di base R, RevoScaleR, MicrosoftML, e altre librerie introdotti nel 2016. 

Nel Database SQL di Azure [Machine Learning Services (con R)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) è attualmente in anteprima pubblica.

La proposta di valore della chiave di servizi di Machine Learning è la potenza dei pacchetti Python e R enterprise per offrire l'analitica avanzata a livello di scalabilità e la possibilità di trasferire i calcoli e l'elaborazione di dove risiedono i dati, eliminando la necessità di estrarre i dati tra la rete.

<a name="components"></a>

## <a name="components"></a>Componenti

SQL Server 2017 supporta R e Python. Nella tabella seguente vengono descritti i componenti.

| Componente | Descrizione |
|-----------|-------------|
| Servizio Launchpad di SQL Server | Un servizio che gestisce le comunicazioni tra i runtime di R e Python esterni e l'istanza del motore di database. |
| Pacchetti R | [**RevoScaleR** ](r/ref-r-revoscaler.md) è la libreria primaria per funzioni R. scalabile in questa raccolta sono tra i più diffusi. Le trasformazioni dei dati e la manipolazione, riepilogo statistico, visualizzazione e molte forme di analisi e modellazione sono disponibili in queste librerie. Inoltre, le funzioni in queste librerie distribuisce automaticamente i carichi di lavoro tra memorie centrali disponibili per l'elaborazione parallela, con la possibilità di operare su blocchi di dati coordinati e gestiti dal motore di calcolo.  <br/>[**MicrosoftML (R)** ](r/ref-r-microsoftml.md) aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del sentiment, analisi delle immagini e analisi del testo. <br/>[**sqlRUtils** ](r/ref-r-sqlrutils.md) fornisce funzioni helper per l'inserimento di script R in una stored procedure T-SQL archiviate, la registrazione di una stored procedure con un database e l'esecuzione della stored procedure da un ambiente di sviluppo R.<br/>[**olapR** ](r/ref-r-olapr.md) è per la compilazione o l'esecuzione di una query MDX nello script R.|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) è distribuzione open source di Microsoft di R. Sono inclusi il pacchetto e dell'interprete. Usare sempre la versione di MRO installato dal programma di installazione. |
| Strumenti R | Prompt dei comandi e le finestre della console R sono gli strumenti standard in una distribuzione di R.  |
| Esempi di R e gli script |  Pacchetti open source di R e RevoScaleR includono set di dati incorporato in modo che è possibile creare ed eseguire lo script usando i dati pre-installati. |
| Pacchetti Python | [**revoscalepy** ](python/ref-py-revoscalepy.md) è la libreria primaria per Python scalabile con funzioni di manipolazione dei dati, trasformazione, visualizzazione e analisi. <br/>[**microsoftml (Python)** ](python/ref-py-microsoftml.md) aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del sentiment, analisi delle immagini e analisi del testo.  |
| Strumenti Python | Lo strumento della riga di comando di Python predefinito è utile per test ad hoc e attività.  |
| Anaconda | Anaconda è una distribuzione open source di Python e i pacchetti essenziali. |
| Gli script ed esempi di Python | Come con R, Python include set di dati incorporato e gli script.  |
| Modelli con training preliminare in R e Python | I modelli con training preliminare vengono creati per casi d'uso specifici e gestiti per il team di progettazione di analisi scientifica dei dati in Microsoft. È possibile usare i modelli con training preliminare come-consiste nell'assegnare un punteggio del sentiment negativo positivo in testo o funzionalità vengono rilevati in immagini usando nuovi input di dati fornito. I modelli eseguiti in servizi di Machine Learning, ma non possono essere installati tramite il programma di installazione di SQL Server. Per altre informazioni, vedere [Install con training preliminare modelli di machine learning in SQL Server](install/sql-pretrained-models-install.md). |

## <a name="using-sql-mls"></a>Uso di servizio per inserzioni multiple SQL

Analisti e sviluppatori hanno spesso il codice in esecuzione su un'istanza di SQL Server locale. Aggiunta di servizi di Machine Learning e abilitando l'esecuzione dello script esterno, si ottengono la possibilità di eseguire codice R e Python in SQL Server tramite: eseguire il wrapping dello script in stored procedure, l'archiviazione dei modelli in una tabella di SQL Server o la combinazione di funzioni R o Python e T-SQL nelle query.

L'esecuzione dello script trova entro i limiti del modello di sicurezza dei dati: le autorizzazioni per i database relazionale costituiscono la base dell'accesso ai dati nello script. Un utente che esegue lo script R o Python non deve essere in grado di usare tutti i dati che non sono accessibile da tale utente in una query SQL. È necessario leggere i database standard e le autorizzazioni di scrittura, oltre a un'autorizzazione aggiuntiva per l'esecuzione dello script esterno. Modelli e codice scritto per i dati relazionali vengono eseguito il wrapping nelle stored procedure, serializzati in un formato binario e archiviati in una tabella o caricati dal disco se è serializzato il flusso di byte non elaborati in un file.

L'approccio più comune per analitica nel database consiste nell'usare [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), il passaggio di script R o Python come parametro di input.

Le interazioni classiche client-server sono un altro approccio. Da qualsiasi workstation client che dispone di un IDE, è possibile installare [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) o nella [librerie Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)e quindi scrivere codice che effettua il push di esecuzione (detta un *calcolo remoto contesto*) dei dati e alle operazioni a un Server SQL remoto. 

Infine, se si usa un' [server autonomo](r/r-server-standalone.md) e l'edizione Developer, è possibile creare soluzioni in una workstation client utilizzando le stesse librerie e gli interpreti e quindi distribuire codice di produzione in SQL Server Machine Learning Servizi (In-Database). 

## <a name="how-to-get-started"></a>Come iniziare a usare

### <a name="step-1-install-the-software"></a>Passaggio 1: Installare il software

+ [SQL Server Machine Learning Services (In-Database)](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>Passaggio 2: Configurare uno strumento di sviluppo

I data Scientist usano in genere R o Python nella workstation propri computer portatili o di sviluppo, per esplorare i dati, sviluppare e ottimizzare i modelli predittivi fino a raggiungere un modello predittivo soddisfacente. Con analitica nel database in SQL Server, non è necessario modificare questo processo. Al termine dell'installazione, è possibile eseguire codice R o Python in SQL Server locale e remota.

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **Usare l'IDE si preferisce**. È possibile collegare le librerie di R e Python per lo strumento di sviluppo preferito. Per altre informazioni, vedere [configurare gli strumenti R](r/set-up-a-data-science-client.md) e [configurare gli strumenti Python](python/setup-python-client-tools-sql.md).  

+ **Lavorare in remoto o in locale**. I data Scientist possono connettersi a SQL Server e inserire i dati al client per l'analisi locale, come di consueto. Tuttavia, una soluzione migliore consiste nell'usare la **RevoScaleR** oppure **revoscalepy** API per trasferire i calcoli nel computer di SQL Server, evitando spostamenti costosi e non sicuri.

+ **Incorporare script R o Python in stored procedure SQL Server**. Quando il codice è perfettamente ottimizzato, eseguirne il wrapping in una stored procedure per evitare lo spostamento dei dati non necessari e ottimizzare le attività di elaborazione dei dati.

### <a name="step-3-write-your-first-script"></a>Passaggio 3: Scrivere il primo script

Chiamare funzioni R o Python dall'interno di uno script T-SQL:

+ [R: Informazioni su analitica nel database con R](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [R: Procedura dettagliata end-to-end con R](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python: Eseguire Python con T-SQL](tutorials/run-python-using-t-sql.md)
+ [Python: Informazioni su analitica nel database usando Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

Scegliere il linguaggio migliore per l'attività. R è ideale per i calcoli statistici difficili da implementare tramite SQL. Per le operazioni sui dati basata su set, sfrutta i vantaggi di SQL Server per ottenere prestazioni ottimali. Usare il motore di database in memoria per i calcoli molto veloci su colonne.

### <a name="step-4-optimize-your-solution"></a>Passaggio 4: Ottimizzare la soluzione

Quando il modello è pronto per la scalabilità su dati aziendali, il data scientist spesso funziona con lo sviluppatore di amministratore di database o SQL per ottimizzare i processi, ad esempio:

+ Progettazione delle funzionalità
+ L'inserimento di dati e trasformazione dei dati
+ Assegnazione dei punteggi

Tradizionalmente, i data Scientist usano R hanno avuto problemi con le prestazioni e scalabilità, soprattutto quando si utilizzano set di dati di grandi dimensioni. Ciò avviene perché l'implementazione di common runtime è a thread singolo e può gestire solo i set di dati che rientrano nella memoria disponibile nel computer locale. Integrazione con servizi di SQL Server Machine Learning offre molte funzionalità per ottenere prestazioni migliori, più dati:

+ **RevoScaleR**: Questo pacchetto R contiene le implementazioni di alcune delle funzioni R più diffuse, riprogettate per garantire parallelismo e scalabilità. Il pacchetto include inoltre funzioni che incrementano scalabilità e prestazioni trasferendo i calcoli al computer SQL Server, dotato in genere più memoria e potenza di calcolo.

+ **revoscalepy**. Questa libreria Python implementa funzioni più diffuse in RevoScaleR, ad esempio contesti di calcolo remoti e molti algoritmi che supportano l'elaborazione distribuita.

Per altre informazioni sulle prestazioni, vedere questo [case study sulle prestazioni](r/performance-case-study-r-services.md) e [ottimizzazione R e i dati](r/r-and-data-optimization-r-services.md).

### <a name="step-5-deploy-and-consume"></a>Passaggio 5: Distribuire e usare

Dopo lo script o il modello è pronto per la produzione, uno sviluppatore di database può incorporare il codice o il modello in una stored procedure in modo che il codice R o Python salvato può essere chiamato da un'applicazione. L'archiviazione e l'esecuzione del codice R da SQL Server offre numerosi vantaggi: è possibile usare la comoda interfaccia SQL Server e tutti i calcoli avvengono nel database, evitando lo spostamento dei dati non necessari.

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **Sicuro ed estensibile**. SQL Server Usa una nuova architettura di estendibilità che protegge il motore di database e isola le sessioni di R e Python. Anche possibile gestire gli utenti autorizzati a eseguire gli script ed è possibile specificare i database che sono accessibili dal codice. È possibile controllare la quantità di risorse allocate al runtime, per evitare che calcoli di grande da entità possano compromettere le prestazioni complessive del server.

+ **Pianificazione e il controllo**. Quando vengono eseguiti i processi di script esterni in SQL Server, è possibile controllare e i dati usati dai data Scientist. È inoltre possibile pianificare i processi e creare flussi di lavoro contenenti script R o Python esterni, esattamente come qualsiasi altro processo T-SQL o stored procedure, è consigliabile pianificare.

Per sfruttare i vantaggi delle funzionalità di sicurezza e gestione delle risorse in SQL Server, il processo di distribuzione può includere queste attività:

+ Conversione del codice a una funzione che è possibile eseguire in modo ottimale in una stored procedure
+ L'impostazione della sicurezza e blocco dei pacchetti utilizzati da un'attività specifica
+ Abilitazione della governance delle risorse (richiede la versione Enterprise edition)

Per altre informazioni, vedere [governance delle risorse per R](r/resource-governance-for-r-services.md) e [gestione dei pacchetti R per SQL Server](r/install-additional-r-packages-on-sql-server.md).

## <a name="version-history"></a>Cronologia delle versioni

Servizi di SQL Server 2017 Machine Learning è la prossima generazione di SQL Server 2016 R Services, migliorata per includere Python. Nella tabella seguente è un elenco completo di tutte le versioni di prodotto, dalle fasi iniziali alla versione corrente. 

| Nome prodotto | Versione del motore | Data di rilascio |
|--------------|---------|--------------|
| SQL Server 2017 Machine Learning Services (In-Database) | R Server 9.2.1 <br/> Python Server 9.2 | Ottobre 2017 |
| SQL Server 2017 Machine Learning Server (Standalone) | R Server 9.2.1 <br/> Python Server 9.2 | Ottobre 2017 |
| SQL Server 2016 R Services (In-Database) | R Server 9.1  | Luglio 2017  |
| SQL Server 2016 R Server (Standalone)  |  R Server 9.1 | Luglio 2017 |

Per versioni del pacchetto dalla versione, vedere la versione di eseguire il mapping nel [i componenti di eseguire l'aggiornamento di R e Python](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md#version-map).

## <a name="portability-and-related-products"></a>Portabilità e prodotti correlati

Portabilità del codice R e Python personalizzato è stato risolto tramite la distribuzione dei pacchetti e interpreti incorporate in più prodotti. Gli stessi pacchetti forniti in SQL Server sono disponibili anche in diversi altri prodotti e servizi Microsoft, tra cui una versione non SQL chiamata [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/). 

I client gratuiti che includono i nostri interpreti R e Python sono [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) e il [librerie Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter).

In Azure, pacchetti R e Python di Microsoft e gli interpreti sono anche disponibili in Azure Machine Learning e servizi di Azure come [HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview), e [macchine virtuali di Azure](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux). Il [macchina virtuale Data Science](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) include una workstation di sviluppo completi con gli strumenti da più fornitori, nonché le librerie e gli interpreti da Microsoft.

## <a name="see-also"></a>Vedere anche

[Installare SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)
