---
title: Libreria di funzioni RevoScaleR R
description: Introduzione alla libreria di funzioni RevoScaleR in SQL Server 2016 R Services e SQL Server Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b5dcd2f14d1a1d8e23a62be299b1ff6f41814041
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715059"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (libreria R in SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RevoScaleR** è una libreria di funzioni di Data Science a prestazioni elevate di Microsoft. Le funzioni supportano l'importazione, la trasformazione dei dati, il riepilogo, la visualizzazione e l'analisi dei dati.

Diversamente dalle funzioni R di base, le operazioni RevoScaleR possono essere eseguite su set di impostazioni di grandi dimensioni, in parallelo e in file system distribuiti. Le funzioni possono operare su set di dati che non rientrano nella memoria utilizzando la suddivisione in blocchi e riassemblando i risultati al termine delle operazioni.

Le funzioni RevoScaleR sono contrassegnate da un prefisso **RX** o **RX** per facilitarne l'identificazione.

RevoScaleR funge da piattaforma per Distributed data science. Ad esempio, è possibile usare i contesti di calcolo e le trasformazioni di RevoScaleR con gli algoritmi all'avanguardia in [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). È anche possibile usare [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) per eseguire le funzioni di base di R in parallelo.

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

La libreria **RevoScaleR** viene distribuita in più prodotti Microsoft, ma l'utilizzo è lo stesso se si ottiene la libreria in SQL Server o in un altro prodotto. Poiché le funzioni sono uguali, la [documentazione per le singole funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) viene pubblicata in una sola posizione sotto il [riferimento R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per Microsoft Machine Learning server. Se sono presenti comportamenti specifici del prodotto, le discrepanze verranno indicate nella pagina della guida della funzione.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

La libreria **RevoScaleR** è basata su R 3.4.3 ed è disponibile solo quando si installa uno dei seguenti prodotti o download Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> Le versioni di rilascio complete del prodotto sono solo Windows, a partire da SQL Server 2017. Il supporto Linux per **RevoScaleR** è una novità di [SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funzioni per categoria

In questa sezione vengono elencate le funzioni per categoria per fornire un'idea del modo in cui vengono utilizzate. È anche possibile usare il [Sommario](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per trovare le funzioni in ordine alfabetico.

## <a name="1-data-source-and-compute"></a>1-origine dati e calcolo

**RevoScaleR** include funzioni per la creazione di origini dati e l'impostazione della posizione o del *contesto di calcolo*in cui vengono eseguiti i calcoli. Un oggetto origine dati è un contenitore che specifica una stringa di connessione con il set di dati desiderato, definito come tabella, vista o query. Le chiamate di stored procedure non sono supportate. Nella tabella seguente sono elencate le funzioni rilevanti per gli scenari SQL Server.

In alcuni casi SQL Server e R usano tipi di dati diversi. Per un elenco dei mapping tra i tipi di dati SQL e R, vedere [tipi di dati r-to-SQL](r-libraries-and-data-types.md).

| Funzione| Descrizione|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  Creare un oggetto contesto di calcolo SQL Server per eseguire il push di calcoli in un'istanza remota. Diverse funzioni **RevoScaleR** accettano il contesto di calcolo come argomento. |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Ottiene o imposta il contesto di calcolo attivo. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | Creare un oggetto dati basato su una query o una tabella SQL Server. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | Creare un'origine dati basata su una connessione ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | Creare un'origine dati basata su un file XDF locale. I file XDF vengono spesso usati per l'offload dei dati in memoria su disco. Un file XDF può essere utile quando si utilizzano più dati rispetto a quelli che possono essere trasferiti dal database in un unico batch o più dati di quelli che possono essere contenuti nella memoria. Se, ad esempio, si spostano regolarmente grandi quantità di dati da un database a una workstation locale, anziché eseguire ripetutamente query sul database per ogni operazione R, è possibile usare il file XDF come un tipo di cache per salvare i dati localmente e quindi usarli nell'area di lavoro di R.|

> [!TIP]
> Se non si ha familiarità con l'idea di origini dati o contesti di calcolo, è consigliabile iniziare con l' [elaborazione distribuita](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) nella documentazione di Microsoft Machine Learning server.

### <a name="perform-ddl-statements"></a>Esegui istruzioni DDL

È possibile eseguire istruzioni DDL da R, se si dispone delle autorizzazioni necessarie per l'istanza e il database. Nelle funzioni seguenti vengono utilizzate le chiamate ODBC per eseguire istruzioni DDL o recuperare lo schema del database.

| Funzione| Descrizione|
| ------- | ---------- |
| [rxSqlServerTableExists e rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | Eliminare una [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] tabella o verificare l'esistenza di una tabella o di un oggetto di database. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | Eseguire un comando DDL (Data Definition Language) che consente di definire o modificare gli oggetti di database. Questa funzione non può restituire dati e viene utilizzata solo per recuperare o modificare lo schema o i metadati dell'oggetto.|

## <a name="2-data-manipulation-etl"></a>2-manipolazione dei dati (ETL)

Dopo aver creato un oggetto origine dati, è possibile utilizzare l'oggetto per caricare i dati, trasformare i dati o scrivere nuovi dati nella destinazione specificata. A seconda delle dimensioni dei dati nell'origine, è anche possibile definire le dimensioni del batch come parte dell'origine dati e spostare i dati in blocchi.

| Funzione | Descrizione |
|----------|-------------|
| [rxOpen-metodi](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | Controllare se un'origine dati è disponibile, aprire o chiudere un'origine dati, leggere dati da un'origine, scrivere dati nella destinazione e chiudere un'origine dati.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | Spostare i dati da un'origine dati in un archivio di file o in un frame di dati.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | Trasformare i dati mentre lo si trasferisce tra le origini dati.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3-funzioni grafiche

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |Crea un istogramma dai dati. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |Crea un tracciato di linea dai dati. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |Calcola una curva di Lorenz che può essere tracciata. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcola e traccia le curve ROC da dati effettivi e stimati. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4-Statistiche descrittive

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |Calcola quantili approssimative per i file con estensione XDF e i frame di dati senza ordinamento. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |Statistiche di riepilogo di base dei dati, inclusi i calcoli per gruppo. La scrittura mediante calcoli di gruppo nel file con estensione XDF non è supportata. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |Tabulazione incrociata basata su formule di dati. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |Tabulazione incrociata basata su formula alternativa progettata per una rappresentazione efficiente che restituisce risultati del cubo. La scrittura dell'output nel file con estensione XDF non è supportata. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |Riepiloghi marginali di tabulazioni incrociate. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Converte i risultati della tabulazione incrociata in un oggetto xtabs. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Esegue il test chi quadrato nell'oggetto xtabs. Usato con set di dati di piccole dimensioni e non suddivide i dati. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Esegue il test esatto di Fisher sull'oggetto xtabs. Usato con set di dati di piccole dimensioni e non suddivide i dati. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Calcola il coefficiente di correlazione Tau Rank di Kendall usando l'oggetto xtabs. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Applicare una funzione a pairwise combinazioni di righe e colonne di un oggetto xtabs. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcolare il rischio relativo per un oggetto xtabs due per due. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcolare il rapporto di probabilità per un oggetto xtabs due per due. | 

<sup>*</sup>Indica le funzioni più diffuse in questa categoria.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5-funzioni di stima

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |Consente di adattare un modello lineare ai dati. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |Consente di adattare un modello di regressione logistica ai dati. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |Consente di adattare un modello lineare generalizzato ai dati. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |Calcolare la covarianza, la correlazione o la somma di una matrice di quadrati/prodotto incrociato per un set di variabili. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |Consente di adattare i dati a un albero di classificazione o di regressione. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |Consente di adattare una foresta delle decisioni di classificazione o regressione ai dati usando un algoritmo di boosting a gradienti stocastici. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |Consente di adattare i dati a una foresta delle decisioni di classificazione o di regressione. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |Calcola le stime per i modelli adattati. L'output deve essere un'origine dati XDF. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |Esegue il clustering k-means. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Esegue la classificazione Naive Bayes. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |Calcolare la matrice di covarianza per un set di variabili. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcolare la matrice di correlazione per un set di variabili. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcolare la somma di matrice di quadrati/prodotto incrociato per un set di variabili. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcoli delle caratteristiche operative del ricevitore (ROC) che usano valori effettivi e stimati dal sistema di classificazione binario. | 

<sup>*</sup>Indica le funzioni più diffuse in questa categoria.


## <a name="how-to-work-with-revoscaler"></a>Come usare RevoScaleR

Le funzioni in **RevoScaleR** possono essere richiamate nel codice R incapsulato nelle stored procedure. La maggior parte degli sviluppatori compila le soluzioni **RevoScaleR** localmente e quindi esegue la migrazione del codice R completato alle stored procedure come esercizio di distribuzione.

Quando si esegue localmente, in genere si esegue uno script R dalla riga di comando o da un ambiente di sviluppo R e si specifica un SQL Server contesto di calcolo usando una delle funzioni **RevoScaleR** . È possibile usare il contesto di calcolo remoto per l'intero codice o per le singole funzioni. Ad esempio, potrebbe essere necessario eseguire l'offload del training del modello nel server per usare i dati più recenti ed evitare lo spostamento dei dati.

Quando si è pronti per incapsulare lo script R all'interno di una stored procedure, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), è consigliabile riscrivere il codice come una singola funzione con input e output chiaramente definiti. 

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di R](../tutorials/sql-server-r-tutorials.md)
+ [Informazioni su come usare i contesti di calcolo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R per sviluppatori SQL: Eseguire il training e il rendere operativo di un modello](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Esempi di prodotti Microsoft su GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Guida di riferimento a R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
