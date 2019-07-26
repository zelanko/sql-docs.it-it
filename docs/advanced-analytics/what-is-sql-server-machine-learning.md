---
title: Panoramica di SQL Server Machine Learning Services (R, Python)
description: Panoramica della funzionalità Machine Learning Services in SQL Server, in cui è possibile integrare Python e R con dati relazionali per data science e la modellazione statistica, modelli di apprendimento automatico, analisi predittiva, visualizzazione dei dati e altro ancora.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ead0dd3d9ba69a4bf0079fe8065a2d5aa7a11d3e
ms.sourcegitcommit: 63c6f3758aaacb8b72462c2002282d3582460e0b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68495402"
---
# <a name="sql-server-machine-learning-services-r-python"></a>SQL Server Machine Learning Services (R, Python)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services è una funzionalità di SQL Server, usata per l'esecuzione di script R e Python nel database. La funzionalità include i [pacchetti Microsoft R e Python](#components) per l'analisi predittiva ad alte prestazioni e l'apprendimento automatico. I dati relazionali possono essere usati negli script R e Python tramite stored procedure, script T-SQL contenenti istruzioni R e Python o codice R e Python contenente T-SQL.

Se in precedenza è stato usato [SQL Server 2016 r Services](r/sql-server-r-services.md), Machine Learning Services in SQL Server 2017 e versioni successive è la nuova generazione del supporto r, con le versioni aggiornate di base r, RevoScaleR, MicrosoftML e altre librerie introdotte in 2016.

Nel database SQL di Azure [Machine Learning Services (con R)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) è attualmente disponibile in anteprima pubblica.

## <a name="bring-compute-power-to-the-data"></a>Portare la potenza di calcolo ai dati

La proposta di valore chiave di Machine Learning Services è la potenza dei pacchetti R e Python aziendali per offrire analisi avanzate su larga scala e la possibilità di portare calcoli ed elaborazioni in cui risiedono i dati, eliminando la necessità di eseguire il pull dei dati tra rete. Questo offre diversi vantaggi:

+ Sicurezza dei dati. L'esecuzione di R e Python più vicino all'origine dei dati evita lo spostamento di dati dispendiosi o non sicuri.
+ Velocità. I database sono ottimizzati per le operazioni basate su set. Le innovazioni recenti nei database, ad esempio le tabelle in memoria, rendono i riepiloghi e le aggregazioni fulmine e costituiscono un complemento perfetto per data science.
+ Facilità di distribuzione e integrazione. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]è il punto centrale delle operazioni per molte altre applicazioni e attività di gestione dei dati. Usando i dati che si trovano nel database o nel warehouse di report, si garantisce che i dati usati dalle soluzioni di Machine Learning siano coerenti e aggiornati. 
+ Efficienza nel cloud e in locale. Anziché elaborare i dati nelle sessioni R o Python, è possibile usare pipeline di dati aziendali, tra [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] cui e Azure Data Factory. La creazione di report con i risultati o l'analisi è semplice con Power BI o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].

Con la giusta combinazione di SQL e R per le diverse attività di elaborazione e analisi di dati, sia i data scientist che gli sviluppatori possono essere più produttivi.

<a name="components"></a>

## <a name="components"></a>Componenti

SQL Server 2017 supporta R e Python. Nella tabella seguente vengono descritti i componenti di.

| Componente | Descrizione |
|-----------|-------------|
| Servizio Launchpad di SQL Server | Un servizio che gestisce le comunicazioni tra i runtime R e Python esterni e l'istanza del motore di database. |
| Pacchetti R | [**RevoScaleR**](r/ref-r-revoscaler.md) è la libreria primaria per R scalabile. le funzioni in questa libreria sono tra i più diffusi. In queste librerie sono disponibili le trasformazioni e la manipolazione dei dati, il riepilogo statistico, la visualizzazione e molte forme di modellazione e analisi. Inoltre, le funzioni in queste librerie distribuiscono automaticamente i carichi di lavoro tra i core disponibili per l'elaborazione parallela, con la possibilità di lavorare su blocchi di dati coordinati e gestiti dal motore di calcolo.  <br/>[**MicrosoftML (R)** ](r/ref-r-microsoftml.md) aggiunge algoritmi di apprendimento automatico per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi dei sentimenti. <br/>[**sqlRUtils**](r/ref-r-sqlrutils.md) fornisce funzioni di supporto per l'inserimento di script R in un stored procedure T-SQL, la registrazione di una stored procedure con un database e l'esecuzione del stored procedure da un ambiente di sviluppo r.<br/>[**olapr**](r/ref-r-olapr.md) è per la compilazione o l'esecuzione di una query MDX nello script R.|
| Microsoft R Open (MRO) | [**Riparazione**](https://mran.microsoft.com/open) è una distribuzione open source di Microsoft di R. Il pacchetto e l'interprete sono inclusi. Usare sempre la versione di installazione di installazione. |
| Strumenti R | Le finestre della console R e i prompt dei comandi sono strumenti standard in una distribuzione R.  |
| Esempi e script R |  I pacchetti R e RevoScaleR Open Source includono set di dati predefiniti, in modo che sia possibile creare ed eseguire script con dati preinstallati. |
| Pacchetti Python | [**revoscalepy**](python/ref-py-revoscalepy.md) è la libreria primaria per Python scalabile con funzioni per la manipolazione, la trasformazione, la visualizzazione e l'analisi dei dati. <br/>[**microsoftml (Python)** ](python/ref-py-microsoftml.md) aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi dei sentimenti.  |
| Strumenti Python | Lo strumento da riga di comando Python incorporato è utile per i test e le attività ad hoc.  |
| Anaconda | Anaconda è una distribuzione open source di Python e di pacchetti essenziali. |
| Esempi e script Python | Come con R, Python include set di dati e script predefiniti.  |
| Modelli con training preliminare in R e Python | I modelli con training preliminare vengono creati per casi d'uso specifici e gestiti dal team di progettazione di data science in Microsoft. È possibile usare i modelli con training preliminare così come sono per assegnare punteggi positivi negativi nel testo o per rilevare le funzionalità nelle immagini, usando i nuovi input di dati forniti. I modelli vengono eseguiti in Machine Learning Services, ma non possono essere installati tramite SQL Server programma di installazione. Per altre informazioni, vedere [installare modelli di apprendimento automatico pre-addestrati in SQL Server](install/sql-pretrained-models-install.md). |

## <a name="using-sql-mls"></a>Uso di SQL MLS

Gli sviluppatori e gli analisti spesso hanno codice in esecuzione su un'istanza di SQL Server locale. Aggiungendo Machine Learning Services e abilitando l'esecuzione di script esterni, è possibile eseguire codice R e Python in modalità SQL Server: wrapping di script in stored procedure, archiviazione di modelli in una tabella SQL Server o combinazione di funzioni T-SQL e R o Python nelle query.

L'esecuzione dello script è entro i limiti del modello di sicurezza dei dati: le autorizzazioni per il database relazionale costituiscono la base per l'accesso ai dati nello script. Un utente che esegue lo script R o Python non dovrebbe essere in grado di usare i dati a cui l'utente può accedere in una query SQL. Sono necessarie le autorizzazioni di lettura e scrittura del database standard, oltre a un'autorizzazione aggiuntiva per l'esecuzione di script esterni. I modelli e il codice scritti per i dati relazionali vengono racchiusi in stored procedure o serializzati in un formato binario e archiviati in una tabella oppure caricati dal disco se il flusso di byte non elaborati viene serializzato in un file.

L'approccio più comune per l'analisi nel database consiste nell'usare [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), passando lo script R o Python come parametro di input.

Le interazioni client-server classiche sono un altro approccio. Da qualsiasi workstation client che dispone di un IDE, è possibile installare [Microsoft R client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) o le [librerie Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter), quindi scrivere codice per eseguire il push dell'esecuzione (denominata *contesto di calcolo remoto*) ai dati e alle operazioni in una SQL Server remota. 

Infine, se si usa un [server autonomo](r/r-server-standalone.md) e l'edizione Developer, è possibile compilare soluzioni in una workstation client usando le stesse librerie e gli stessi interpreti e quindi distribuire il codice di produzione in SQL Server Machine Learning Services (in-database). 

## <a name="how-to-get-started"></a>Come iniziare

### <a name="step-1-install-the-software"></a>Passaggio 1: Installare il software

+ [SQL Server Machine Learning Services (in-database)](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>Passaggio 2: Configurare uno strumento di sviluppo

I data scientist usano in genere R o Python nel proprio computer portatile o nella workstation di sviluppo, per esplorare i dati e compilare e ottimizzare i modelli predittivi fino a quando non si raggiunge un modello predittivo valido. Con l'analisi nel database in SQL Server, non è necessario modificare questo processo. Al termine dell'installazione, è possibile eseguire il codice R o Python su SQL Server localmente e in remoto.

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **Usare l'IDE preferito**. Puoi collegare le librerie R e Python allo strumento di sviluppo che preferisci. Per altre informazioni, vedere [configurare gli strumenti R](r/set-up-a-data-science-client.md) e [configurare gli strumenti di Python](python/setup-python-client-tools-sql.md).  

+ **Lavorare in modalità remota o locale**. I data scientist possono connettersi a SQL Server e portare i dati nel client per l'analisi locale, come di consueto. Tuttavia, una soluzione migliore consiste nell'usare le API **RevoScaleR** o **revoscalepy** per eseguire il push di calcoli nel computer SQL Server, evitando lo spostamento di dati costosi e non sicuri.

+ **Incorporare script R o Python in SQL Server stored procedure**. Quando il codice è completamente ottimizzato, eseguirne il wrapping in una stored procedure per evitare lo spostamento dei dati non necessari e ottimizzare le attività di elaborazione dei dati.

### <a name="step-3-write-your-first-script"></a>Passaggio 3: Scrivere il primo script

Chiamare funzioni R o Python dall'interno dello script T-SQL:

+ [R Informazioni sulle analisi nel database con R](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [R Procedura dettagliata end-to-end con R](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python Eseguire python con T-SQL](tutorials/run-python-using-t-sql.md)
+ [Python Informazioni sulle analisi nel database con Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

Scegliere la lingua migliore per l'attività. R è ideale per calcoli statistici difficili da implementare con SQL. Per le operazioni basate su set sui dati, è possibile sfruttare la potenza di SQL Server per ottenere le massime prestazioni. Usare il motore di database in memoria per calcoli molto veloci sulle colonne.

### <a name="step-4-optimize-your-solution"></a>Passaggio 4: Ottimizzare la soluzione

Quando il modello è pronto per la scalabilità sui dati aziendali, il data scientist collabora spesso con l'amministratore di database o con lo sviluppatore SQL per ottimizzare i processi, ad esempio:

+ Progettazione delle funzioni
+ Inserimento di dati e trasformazione dei dati
+ Punteggio

Tradizionalmente, i data scientist che usano R hanno riscontrato problemi di prestazioni e scalabilità, soprattutto quando si usa un set di dati di grandi dimensioni. Ciò è dovuto al fatto che l'implementazione di Common Runtime è a thread singolo e può contenere solo i set di dati che rientrano nella memoria disponibile sul computer locale. L'integrazione con SQL Server Machine Learning Services offre più funzionalità per migliorare le prestazioni, con più dati:

+ **RevoScaleR**: Questo pacchetto R contiene le implementazioni di alcune delle funzioni R più diffuse, riprogettate per garantire parallelismo e scalabilità. Il pacchetto include anche funzioni che migliorano le prestazioni e la scalabilità tramite il push dei calcoli nel computer SQL Server, che in genere ha una potenza di memoria e di calcolo molto maggiore.

+ **revoscalepy**. Questa libreria Python implementa le funzioni più diffuse in RevoScaleR, ad esempio i contesti di calcolo remoti e molti algoritmi che supportano l'elaborazione distribuita.

Per ulteriori informazioni sulle prestazioni, vedere questo [Case Study di prestazioni](r/performance-case-study-r-services.md) e [R e ottimizzazione dei dati](r/r-and-data-optimization-r-services.md).

### <a name="step-5-deploy-and-consume"></a>Passaggio 5: Distribuzione e utilizzo

Quando lo script o il modello è pronto per l'uso in produzione, uno sviluppatore di database potrebbe incorporare il codice o il modello in un stored procedure in modo che il codice R o Python salvato possa essere chiamato da un'applicazione. L'archiviazione e l'esecuzione di codice R da SQL Server presenta molti vantaggi: è possibile usare la comoda interfaccia SQL Server e tutti i calcoli avvengono nel database, evitando spostamenti di dati non necessari.

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **Sicura ed estendibile**. SQL Server usa una nuova architettura di estendibilità che garantisce la sicurezza del motore di database e l'isolamento delle sessioni R e Python. È inoltre possibile controllare gli utenti che possono eseguire script ed è possibile specificare i database a cui è possibile accedere tramite codice. È possibile controllare la quantità di risorse allocate al runtime, per evitare che calcoli di grandi dimensioni compromettano le prestazioni complessive del server.

+ **Pianificazione e controllo**. Quando i processi di script esterni vengono eseguiti in SQL Server, è possibile controllare e controllare i dati usati dai data scientist. È anche possibile pianificare i processi e creare flussi di lavoro contenenti script R o Python esterni, proprio come per qualsiasi altro processo T-SQL o stored procedure.

Per sfruttare i vantaggi delle funzionalità di gestione delle risorse e di sicurezza in SQL Server, è possibile che il processo di distribuzione includa le seguenti attività:

+ Conversione del codice in una funzione che può essere eseguita in modo ottimale in una stored procedure
+ Impostazione della sicurezza e blocco dei pacchetti utilizzati da una determinata attività
+ Abilitazione della governance delle risorse (richiede Enterprise Edition)

Per altre informazioni, vedere [governance delle risorse per r](r/resource-governance-for-r-services.md) e [r gestione pacchetti per SQL Server](r/install-additional-r-packages-on-sql-server.md).

## <a name="version-history"></a>Cronologia delle versioni

SQL Server 2017 Machine Learning Services è la nuova generazione di SQL Server 2016 R Services, ottimizzato per includere Python. La tabella seguente è un elenco completo di tutte le versioni del prodotto, dall'inizio alla versione corrente. 

| Nome prodotto | Versione motore | Data di rilascio |
|--------------|---------|--------------|
| SQL Server 2017 Machine Learning Services (in-database) | R Server 9.2.1 <br/> Server Python 9,2 | Ottobre 2017 |
| SQL Server 2017 Machine Learning Server (autonomo) | R Server 9.2.1 <br/> Server Python 9,2 | Ottobre 2017 |
| SQL Server 2016 R Services (in-database) | R Server 9,1  | Luglio 2017  |
| SQL Server 2016 R Server (autonomo)  |  R Server 9,1 | Luglio 2017 |

Per le versioni dei pacchetti per versione, vedere la mappa delle versioni in [aggiornare i componenti R e Python](install/upgrade-r-and-python.md#version-map).

## <a name="portability-and-related-products"></a>Portabilità e prodotti correlati

La portabilità del codice R e Python personalizzato viene risolta tramite la distribuzione e gli interpreti dei pacchetti incorporati in più prodotti. Gli stessi pacchetti inclusi in SQL Server sono disponibili anche in molti altri prodotti e servizi Microsoft, inclusa una versione non SQL denominata [Microsoft Machine Learning server](https://docs.microsoft.com/machine-learning-server/). 

I client gratuiti che includono gli interpreti R e Python sono [Microsoft R client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) e le [librerie di Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter).

In Azure, i pacchetti e gli interpreti R e Python di Microsoft sono disponibili anche su Azure Machine Learning e servizi di Azure come [HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview)e [macchine virtuali di Azure](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux). Il [Data Science Virtual Machine](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) include una workstation di sviluppo completamente attrezzata con strumenti di più fornitori, nonché librerie e interpreti di Microsoft.

## <a name="see-also"></a>Vedere anche

[Installare SQL Server Machine Learning Services](install/sql-machine-learning-services-windows-install.md)
