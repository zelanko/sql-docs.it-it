---
title: Libreria di funzioni R RevoScaleR
description: Introduzione alla libreria di funzioni RevoScaleR in R Services per SQL Server 2016 e in Machine Learning Services per SQL Server con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7b24d5499e618a09c4d80e8614b08219e6c6f788
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "73706757"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (libreria R in SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RevoScaleR** è una libreria di funzioni di data science a prestazioni elevate di Microsoft. Le funzioni supportano l'importazione dei dati, la trasformazione dei dati, il riepilogo, la visualizzazione e l'analisi.

Diversamente dalle funzioni R di base, le operazioni RevoScaleR possono essere eseguite su set di dati molto grandi, in parallelo e in file system distribuiti. Le funzioni possono operare su set di dati che non rientrano nella memoria usando la divisione in blocchi e riassemblando i risultati al termine delle operazioni.

Le funzioni RevoScaleR vengono indicate con un prefisso **rx** o **Rx** che ne facilita l'identificazione.

RevoScaleR funge da piattaforma per la data science distribuita. È ad esempio possibile usare i contesti di calcolo e le trasformazioni di RevoScaleR con gli algoritmi all'avanguardia in [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). È anche possibile usare [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) per eseguire le funzioni R di base in parallelo.

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

La libreria **RevoScaleR** è distribuita in più prodotti Microsoft, ma l'utilizzo è lo stesso indipendentemente dal fatto che sia inclusa in SQL Server o in un altro prodotto. Poiché le funzioni sono le stesse, la [documentazione per le singole funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) viene pubblicata in una sola posizione nelle [informazioni di riferimento per R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per Microsoft Machine Learning Server. In caso di comportamenti specifici per un prodotto, le discrepanze verranno indicate nella pagina della Guida delle funzioni in questione.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

La libreria **RevoScaleR** è basata su R 3.4.3 ed è disponibile solo quando si installa uno dei prodotti o download Microsoft seguenti:

+ [R Services per SQL Server 2016](../install/sql-r-services-windows-install.md)
+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R Client](set-up-a-data-science-client.md)

> [!NOTE]
> Le versioni complete del prodotto sono solo per Windows in SQL Server 2017. Sia Windows che Linux sono supportati per **RevoScaleR** in [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funzioni per categoria

Questa sezione elenca le funzioni per categoria per offrire un'idea di come vengono usate. È anche possibile usare il [sommario](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) per trovare le funzioni in ordine alfabetico.

## <a name="1-data-source-and-compute"></a>1 - Origine dati e calcolo

**RevoScaleR** include funzioni per la creazione di origini dati e l'impostazione della posizione, o *contesto di calcolo*, in cui vengono eseguiti i calcoli. Un oggetto origine dati è un contenitore che specifica una stringa di connessione con il set di dati desiderato, definito come tabella, vista o query. Le chiamate di stored procedure non sono supportate. Nella tabella seguente sono elencate le funzioni relative agli scenari con SQL Server.

In alcuni casi SQL Server e R usano tipi di dati diversi. Per un elenco dei mapping tra i tipi di dati SQL e R, vedere [Tipi di dati da R a SQL](r-libraries-and-data-types.md).

| Funzione| Descrizione|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  Crea un oggetto contesto di calcolo di SQL Server per eseguire il push dei calcoli in un'istanza remota. Diverse funzioni **RevoScaleR** accettano il contesto di calcolo come argomento. |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Ottiene o imposta il contesto di calcolo attivo. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | Crea un oggetto dati basato su una query o una tabella SQL Server. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | Crea un'origine dati basata su una connessione ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | Crea un'origine dati basata su un file XDF locale. I file XDF vengono spesso usati per l'offload dei dati in memoria su disco. Un file XDF può essere utile quando si usano più dati di quanti sia possibile trasferire dal database in un batch o più dati di quanti sia possibile archiviare in memoria. Se ad esempio si spostano regolarmente grandi quantità di dati da un database a una workstation locale, invece di eseguire ripetutamente query sul database per ogni operazione R, è possibile usare il file XDF come una sorta di cache per salvare i dati localmente e quindi lavorare nell'area di lavoro R.|

> [!TIP]
> Se non si ha familiarità con il concetto di origini dati o di contesti di calcolo, è consigliabile iniziare con il [calcolo distribuito](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) nella documentazione di Microsoft Machine Learning Server.

### <a name="perform-ddl-statements"></a>Eseguire istruzioni DDL

È possibile eseguire istruzioni DDL da R, se si hanno le autorizzazioni necessarie per l'istanza e il database. Le funzioni seguenti usano le chiamate ODBC per eseguire le istruzioni DDL o recuperare lo schema del database.

| Funzione| Descrizione|
| ------- | ---------- |
| [rxSqlServerTableExists e rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | Elimina una tabella di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] o verifica l'esistenza di un oggetto o una tabella di database. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | Esegue un comando DDL (Data Definition Language) che definisce o modifica gli oggetti di database. Questa funzione non può restituire dati e viene usata solo per recuperare o modificare lo schema o i metadati dell'oggetto.|

## <a name="2-data-manipulation-etl"></a>2 - Manipolazione dei dati (ETL)

Dopo aver creato un oggetto di origine dati, è possibile usare l'oggetto per caricarvi i dati, trasformare i dati o scrivere nuovi dati nella destinazione specificata. A seconda delle dimensioni dei dati nell'origine, è anche possibile definire le dimensioni del batch come parte dell'origine dati e spostare i dati in blocchi.

| Funzione | Descrizione |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | Controlla se un'origine dati è disponibile, apre o chiude un'origine dati, legge i dati da un'origine, scrive i dati nella destinazione e chiude un'origine dati.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | Sposta i dati da un'origine dati in una risorsa di archiviazione file o in un frame di dati.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | Trasforma i dati mentre li sposta tra le origini dati.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3 - Funzioni di creazione di grafici

| Nome della funzione | Descrizione |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |Crea un istogramma dai dati. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |Crea un tracciato di linea dai dati. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |Calcola una curva di Lorenz tracciabile. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcola e traccia curve ROC da dati effettivi e stimati. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4 - Statistiche descrittive

| Nome della funzione | Descrizione |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |Calcola i quantili approssimativi dei file XDF e dei frame di dati senza ordinamento. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |Statistiche di riepilogo di base dei dati, inclusi i calcoli per gruppo. La scrittura di calcoli per gruppo nel file XDF non è supportata. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |Tabulazione incrociata dei dati basata su formule. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |Tabulazione incrociata alternativa basata su formule progettata per una rappresentazione efficiente che restituisce i risultati del cubo. La scrittura dell'output nel file XDF non è supportata. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |Riepiloghi marginali delle tabulazioni incrociate. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Converte i risultati della tabulazione incrociata in un oggetto xtabs. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Esegue un test del chi quadrato sugli oggetti xtabs. Viene usata con set di dati di piccole dimensioni e non divide i dati in blocchi. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Esegue un test esatto di Fisher su un oggetto xtabs. Viene usata con set di dati di piccole dimensioni e non divide i dati in blocchi. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Calcola il coefficiente di correlazione tau per ranghi di Kendall usando un oggetto xtabs. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Applica una funzione a combinazioni pairwise di righe e colonne di un oggetto xtabs. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcola il rischio relativo di un oggetto xtabs due per due. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcola il rapporto di probabilità di un oggetto xtabs due per due. | 

<sup>*</sup> Indica le funzioni più usate di questa categoria.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5 - Funzioni di stima

| Nome della funzione | Descrizione |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |Adatta un modello lineare ai dati. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |Adatta un modello di regressione logistica ai dati. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |Adatta un modello lineare generalizzato ai dati. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |Calcola la covarianza, la correlazione o la matrice di somme di quadrati/prodotti vettoriali per un set di variabili. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |Adatta un albero di classificazione o di regressione ai dati. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |Adatta una foresta delle decisioni di classificazione o di regressione ai dati usando un algoritmo di gradient boosting stocastico. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |Adatta una foresta delle decisioni di classificazione o di regressione ai dati. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |Calcola le stime per i modelli adattati. L'output deve essere un'origine dati XDF. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |Esegue il clustering k-medie. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Esegue la classificazione bayesiana naif. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |Calcola la matrice delle covarianze per un set di variabili. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcola la matrice delle correlazioni per un set di variabili. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcola la matrice di somme di quadrati/prodotti vettoriali per un set di variabili. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcoli di curve ROC (Receiver Operating Characteristic) tramite valori effettivi e stimati del sistema di classificazione binaria. | 

<sup>*</sup> Indica le funzioni più usate di questa categoria.


## <a name="how-to-work-with-revoscaler"></a>Come utilizzare RevoScaleR

Le funzioni in **RevoScaleR** possono essere chiamate nel codice R incapsulato nelle stored procedure. La maggior parte degli sviluppatori compila in locale le soluzioni **RevoScaleR** e quindi esegue la migrazione del codice R completato alle stored procedure, come esercizio di distribuzione.

Durante un'esecuzione locale, si esegue in genere uno script R dalla riga di comando o da un ambiente di sviluppo R e si specifica un contesto di calcolo di SQL Server usando una delle funzioni di **RevoScaleR**. È possibile usare il contesto di calcolo remoto per l'intero codice o per singole funzioni. Ad esempio, potrebbe essere necessario eseguire l'offload del training del modello nel server per usare i dati più recenti ed evitare lo spostamento dati.

Quando si è pronti per incapsulare lo script R all'interno di una stored procedure, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), è consigliabile riscrivere il codice come una singola funzione con input e output chiaramente definiti. 

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di R](../tutorials/sql-server-r-tutorials.md)
+ [Informazioni su come usare i contesti di calcolo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R per sviluppatori SQL: eseguire il training e rendere operativo un modello](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Microsoft product samples on GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples) (Esempi di prodotti Microsoft in GitHub)
+ [Informazioni di riferimento su R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
