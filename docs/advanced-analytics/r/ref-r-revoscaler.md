---
title: Libreria di funzioni RevoScaleR R - servizi di SQL Server Machine Learning
description: Introduzione alla libreria di funzioni RevoScaleR in SQL Server 2016 R Services e SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3745c6cd8c340ce4ad89cac84c5b6286126e3f89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641918"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (libreria R in SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**RevoScaleR** è una libreria di funzioni di analisi scientifica dei dati ad alte prestazioni da Microsoft. Funzioni supportano l'importazione dei dati, la trasformazione dei dati, attività di riepilogo, visualizzazione e analisi.

A differenza delle funzioni R di base, operazioni di RevoScaleR possono essere eseguite su set di dati molto grandi, in parallelo e su sistemi di file distribuito. Le funzioni possono operare su set di dati che non rientrano nella memoria usando la suddivisione in blocchi e il riassemblaggio risultati una volta completate le operazioni.

Funzioni RevoScaleR sono contrassegnate con un **rx** oppure **Rx** prefisso per renderli facilmente identificabile.

RevoScaleR funge da una piattaforma per l'analisi scientifica dei dati distribuiti. Ad esempio, è possibile utilizzare le trasformazioni e contesti di calcolo di RevoScaleR con gli algoritmi d'avanguardia [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). È anche possibile usare [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) per eseguire funzioni di base R in parallelo.

## <a name="full-reference-documentation"></a>Documentazione di riferimento complete

Il **RevoScaleR** libreria distribuita in vari prodotti Microsoft, ma che utilizzo è lo stesso sia ottenere la libreria in SQL Server o un altro prodotto. Perché le funzioni sono uguali, [documentazione per le singole funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) pubblicata in un'unica posizione sotto il [riferimento R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per Microsoft Machine Learning Server. Qualsiasi prodotto specifico deve comportamenti esistono, verranno indicate nella pagina della Guida funzione discrepanze.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

Il **RevoScaleR** libreria è basata su R 3.4.3 e disponibile solo quando si installa uno dei seguenti prodotti Microsoft o download:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> Sono versioni di rilascio versione completa del prodotto Windows sola, a partire da SQL Server 2017. Il supporto per Linux **RevoScaleR** sono le novità [anteprima di SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funzioni per categoria

In questa sezione elenca le funzioni in base alla categoria per farsi un'idea dell'utilizzo di ciascuna di esse. È anche possibile usare la [sommario](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per trovare le funzioni in ordine alfabetico.

## <a name="1-data-source-and-compute"></a>Risorse di calcolo e di origine dati 1

**RevoScaleR** include funzioni per la creazione di origini dati e impostazione del percorso, o *contesto di calcolo*, di cui vengono eseguiti i calcoli. Un oggetto origine dati è un contenitore che specifica una stringa di connessione con il set di dati desiderato, definito come tabella, vista o query. Le chiamate di stored procedure non sono supportate. Funzioni rilevanti per gli scenari di SQL Server sono elencate nella tabella seguente.

SQL Server e R usare diversi tipi di dati in alcuni casi. Per un elenco dei mapping tra tipi di dati SQL e R, vedere [tipi di dati R-to-SQL](r-libraries-and-data-types.md).

| Funzione| Descrizione|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  Creare un oggetto di contesto di calcolo di SQL Server per trasferire i calcoli a un'istanza remota. Numerosi **RevoScaleR** funzioni accettano il contesto di calcolo come argomento. |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Ottiene o imposta il contesto di calcolo attivo. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | Creare un oggetto di dati basato su una query di SQL Server o una tabella. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | Creare un'origine dati basata su una connessione ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | Creare un'origine dati basata su un file XDF locale. I file XDF vengono spesso utilizzati per l'offload dei dati in memoria su disco. Un file XDF può essere utile quando si utilizzano più dati possono essere trasferiti dal database in un unico batch, o altri dati che possono adattarsi alla memoria. Ad esempio, se si spostano regolarmente grandi quantità di dati da un database in una workstation locale, invece di query del database più volte per ogni operazione R, è possibile utilizzare il file XDF come un tipo di cache per salvare i dati in locale e quindi lavorare nell'area di lavoro R.|

> [!TIP]
> Se si ha familiarità con l'idea di origini dati o contesti di calcolo, è consigliabile iniziare con [elaborazione distribuita](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) nella documentazione di Microsoft Machine Learning Server.

### <a name="perform-ddl-statements"></a>Seguire le istruzioni DDL

È possibile eseguire istruzioni DDL da R, se si dispone delle autorizzazioni necessarie per l'istanza e database. Le funzioni seguenti utilizzano chiamate ODBC per eseguire istruzioni DDL o recuperare lo schema del database.

| Funzione| Descrizione|
| ------- | ---------- |
| [rxSqlServerTableExists e rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | Eliminare un [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] tabella oppure verificare l'esistenza di un oggetto o tabella di database. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | Eseguire un comando di definizione del linguaggio DDL (Data) che definisce o modifica gli oggetti di database. Questa funzione non può restituire dati e viene utilizzata solo per recuperare o modificare lo schema di oggetti o metadati.|

## <a name="2-data-manipulation-etl"></a>Manipolazione dei dati-2 (ETL)

Dopo aver creato un oggetto origine dati, è possibile usare l'oggetto per caricare i dati al suo interno, la trasformazione dei dati oppure scrivere nuovi dati nella destinazione specificata. A seconda delle dimensioni dei dati nell'origine, è anche possibile definire le dimensioni del batch come parte dell'origine dati e spostare i dati in blocchi.

| Funzione | Descrizione |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | Controllare se un'origine dati è disponibile, aprire o chiudere un'origine dati, leggere i dati da un'origine, scrivere i dati di destinazione e chiude un'origine dati.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | Spostare dati da un'origine dati in archiviazione file o in un frame di dati.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | Trasformare i dati durante lo spostamento tra le origini dati.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3-Creazione di grafici di funzioni

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |Crea un istogramma dai dati. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |Crea un tracciato di linea dai dati. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |Calcola una curva di Lorenz che può essere tracciata. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcola e traccia curve ROC da dati effettivi e stimati. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>Statistiche descrittive-4

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |Risorse di calcolo approssimativo i quantili per i file con estensione xdf e frame di dati senza ordinamento. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |Base le statistiche di riepilogo dei dati, inclusi calcoli per gruppo. Scrittura da parte i calcoli di gruppo per file con estensione xdf non è supportato. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |Basato su formula tabulazione incrociata di dati. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |Alternativo basato su formula tabulazione incrociata progettata per un'efficiente rappresentazione restituzione dei risultati del cubo. Scrittura dell'output al file con estensione xdf non supportato. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |Riepilogo marginale per tra tabelle. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Converte incrociata i risultati della tabulazione in un oggetto xtabs. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Esegue il Test del chi quadrato xtabs objektu. Utilizzato con piccoli set di dati e non suddividere i dati. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Esegue Test esatto di Fisher xtabs objektu. Utilizzato con piccoli set di dati e non suddividere i dati. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Calcola Tau classifica il coefficiente di correlazione di Kendall utilizzando xtabs oggetto. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Applica una funzione a combinazioni pairwise di righe e colonne di un oggetto xtabs. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcola il rischio di probabilità di un oggetto xtabs due per due. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcolare il rapporto di probabilità in un oggetto xtabs due per due. | 

<sup>*</sup> Indica funzioni più diffuse in questa categoria.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>Funzioni di stima di 5

| Nome funzione | Descrizione |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |Adatta un modello lineare ai dati. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |Adatta un modello di regressione logistica a dati. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |Adatta un modello lineare generalizzato ai dati. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |Calcolare la covarianza, correlazione o somma dei quadrati / prodotto incrociato matrice per un set di variabili. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |È appropriato per un albero di classificazione o regressione ai dati. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |È appropriato per una foresta delle decisioni di classificazione o regressione per i dati usando un algoritmo di Boosting dei gradienti stocastica. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |È appropriato per una foresta delle decisioni di classificazione o regressione ai dati. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |Calcola le stime per i modelli adattati. Output deve essere un'origine dati XDF. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |Esegue il clustering k-means. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Esegue la classificazione Naive Bayes. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |Calcola la matrice di covarianza per un set di variabili. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcola la matrice di correlazione per un set di variabili. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcolare la somma dei quadrati / prodotto incrociato matrice per un set di variabili. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcoli operativo caratteristica (ROC) ricevitore usando i valori effettivi e stimati dal sistema di classificazione binaria. | 

<sup>*</sup> Indica funzioni più diffuse in questa categoria.


## <a name="how-to-work-with-revoscaler"></a>Come lavorare con RevoScaleR

Le funzioni nello **RevoScaleR** possono essere chiamati nel codice R è incapsulato in stored procedure. La maggior parte degli sviluppatori di compilare **RevoScaleR** soluzioni in locale, e quindi eseguire la migrazione di codice R completato alle stored procedure come un esercizio di distribuzione.

Quando si esegue localmente, in genere eseguire uno script R da riga di comando o da un ambiente di sviluppo R e specificare un contesto di calcolo di SQL Server utilizzando uno dei **RevoScaleR** funzioni. È possibile usare il contesto di calcolo remoto per tutto il codice o per le singole funzioni. Ad esempio, è possibile eseguire l'offload di training del modello per il server di usare i dati più recenti e di evitare lo spostamento dei dati.

Quando si è pronti per lo script R all'interno di una stored procedure, incapsulare [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), si consiglia di riscrivere il codice come una singola funzione che è chiaramente definito gli input e output. 

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di R](../tutorials/sql-server-r-tutorials.md)
+ [Informazioni su come usare contesti di calcolo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R per sviluppatori SQL: Eseguire il training e come operazionalizzare un modello](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Esempi del prodotto Microsoft su GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Riferimento di R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
