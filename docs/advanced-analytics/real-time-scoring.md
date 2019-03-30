---
title: Assegnazione del punteggio utilizzando sp_rxPredict stored procedure - servizi di SQL Server Machine Learning in tempo reale
description: Generare stime usando sp_rxPredict, assegnazione dei punteggi dei dati di input in base a un modello con training preliminare scritte in R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 22f6c48aec0c9434b17ceda0a2b729f6e63bf136
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645473"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>In tempo reale di assegnazione dei punteggi con sp_rxPredict in SQL Server machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In tempo reale di assegnazione dei punteggi viene utilizzata la [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) sistema stored procedure e le funzionalità di estensione CLR in SQL Server per le stime a prestazioni elevate o punteggi in previsione dei carichi di lavoro. Assegnazione dei punteggi in tempo reale è indipendente dal linguaggio e viene eseguita senza dipendenze in R o Python esecuzioni. Supponendo che un modello creato e sottoposto a training usando funzioni di Microsoft e quindi serializzati in un formato binario in SQL Server, è possibile usare l'assegnazione di punteggi in tempo reale per generare i risultati stimati in nuovi input di dati nelle istanze di SQL Server che non è il componente aggiuntivo R o Python installato.

## <a name="how-real-time-scoring-works"></a>Funzionamento di assegnazione dei punteggi in tempo reale come

Assegnazione dei punteggi in tempo reale è supportato in SQL Server 2017 e SQL Server 2016, sui tipi di modello specifico basati, ad esempio le funzioni RevoScaleR o MicrosoftML [(RevoScaleR) rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). Usa le librerie C++ native per generare punteggi, in base all'input fornito a un modello di machine learning archiviato in un particolare formato binario.

Poiché un modello con training può essere usato per la valutazione senza dover chiamare un runtime di linguaggio esterno, viene ridotto l'overhead di più processi. Ciò supporta ottenere migliori prestazioni di stima per gli scenari di assegnazione dei punteggi di produzione. Poiché i dati non oltrepassino mai SQL Server, i risultati possono essere generati e inseriti in una nuova tabella senza conversione dei dati tra R e SQL.

Assegnazione dei punteggi in tempo reale è un processo in più passaggi:

1. È necessario abilitare le stored procedure che esegue l'assegnazione dei punteggi in base al database.
2. Caricare il modello con training preliminare in formato binario.
3. È fornire nuovi dati di input a cui assegnare un punteggio, righe tabulari o singole, come input per il modello.
4. Per generare i punteggi, chiamare il [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) stored procedure.

## <a name="prerequisites"></a>Prerequisiti

+ [Abilitare l'integrazione CLR di SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ [Abilitare l'assegnazione dei punteggi in tempo reale](#bkmk_enableRtScoring).

+ Il modello deve essere sottoposto a training in anticipo usando uno degli **rx** algoritmi. Per R, in tempo reale con di assegnazione dei punteggi `sp_rxPredict` funziona con [RevoScaleR e MicrosoftML supportati gli algoritmi](#bkmk_rt_supported_algos). Per Python, vedere [revoscalepy e microsoftml supportati gli algoritmi](#bkmk_py_supported_algos)

+ Serializzare il modello usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) per R, e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) per Python. Queste funzioni di serializzazione sono state ottimizzate per supportare l'assegnazione dei punteggi veloce.

+ Salvare il modello all'istanza del motore di database da cui si desidera chiamarlo. Questa istanza non è necessario avere l'estensione di runtime di R o Python.

> [!Note]
> Assegnazione dei punteggi in tempo reale è attualmente ottimizzato per le stime rapide in un set di dati più piccolo, compreso tra alcune righe e centinaia di migliaia di righe. In grandi set di dati, tramite [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) potrebbe risultare più veloce.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>Algoritmi supportati

### <a name="python-algorithms-using-real-time-scoring"></a>Algoritmi di Python usando l'assegnazione dei punteggi in tempo reale

+ modelli revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  Modelli contrassegnati con \* supportano anche l'assegnazione dei punteggi nativa con la funzione PREDICT.

+ modelli di microsoftml

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Trasformazioni fornite da microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>Algoritmi di R usando l'assegnazione dei punteggi in tempo reale

+ Modelli di RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  Modelli contrassegnati con \* supportano anche l'assegnazione dei punteggi nativa con la funzione PREDICT.

+ Modelli di MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ Trasformazioni fornite da MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>Tipi di modello non supportato

Assegnazione dei punteggi in tempo reale non utilizza un interprete; Pertanto, qualsiasi funzionalità che potrebbero richiedere un interprete non è supportata durante il passaggio di assegnazione dei punteggi.  Tali proprietà possono includere:

  + I modelli usando la `rxGlm` o `rxNaiveBayes` algoritmi non sono supportati.

  + I modelli usando una funzione di trasformazione o una formula che contiene una trasformazione, ad esempio <code>A ~ log(B)</code> non sono supportati nell'assegnazione dei punteggi in tempo reale. Per usare un modello di questo tipo, è consigliabile eseguire la trasformazione sui dati di input prima di passarli all'assegnazione dei punteggi in tempo reale.


## <a name="example-sprxpredict"></a>Example: sp_rxPredict

In questa sezione vengono descritti i passaggi necessari per configurare **in tempo reale** stima e viene fornito un esempio in R di come chiamare la funzione di T-SQL.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>Passaggio 1. Abilitare la procedura di assegnazione dei punteggi in tempo reale

È necessario abilitare questa funzionalità per ogni database che si desidera utilizzare per l'assegnazione dei punteggi. L'amministratore del server deve eseguire l'utilità della riga di comando, RegisterRExt.exe, che viene incluso nel pacchetto RevoScaleR.

> [!NOTE]
> Affinché il punteggio in tempo reale per funzionare, deve essere abilitato nell'istanza; la funzionalità di CLR SQL Inoltre, il database deve essere contrassegnato come attendibile. Quando si esegue lo script, queste azioni vengono eseguite automaticamente. Tuttavia, prendere in considerazione le implicazioni di sicurezza aggiuntiva prima di procedere.

1. Aprire un prompt dei comandi con privilegi elevati e passare alla cartella in cui si trova RegisterRExt.exe. In un'installazione predefinita, è possibile utilizzare il percorso seguente:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Eseguire il comando seguente, sostituendo il nome dell'istanza e database di destinazione in cui si desidera abilitare le stored procedure estese:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Ad esempio, per aggiungere la stored procedure estesa al database CLRPredict nell'istanza predefinita, digitare:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    Il nome dell'istanza è facoltativo se il database nell'istanza predefinita. Se si usa un'istanza denominata, è necessario specificare il nome dell'istanza.

3. RegisterRExt.exe crea gli oggetti seguenti:

    + Assembly attendibili
    + La stored procedure `sp_rxPredict`
    + Un nuovo ruolo del database, `rxpredict_users`. L'amministratore del database è possibile usare questo ruolo per concedere autorizzazioni agli utenti che usano la funzionalità di assegnazione dei punteggi in tempo reale.

4. Aggiungere gli utenti che dovranno essere eseguiti `sp_rxPredict` al nuovo ruolo.

> [!NOTE]
> 
> In SQL Server 2017, le misure di sicurezza aggiuntive sono disponibili per evitare problemi di integrazione con CLR. Queste misure impongono restrizioni aggiuntive per l'uso di questa stored procedure. 

### <a name="step-2-prepare-and-save-the-model"></a>Passaggio 2. Preparare e salvare il modello

Il formato binario richiesto da sp\_rxPredict corrisponde al formato richiesto per usare la funzione PREDICT. Pertanto, nel codice R, includere una chiamata a [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)e assicurarsi di specificare `realtimeScoringOnly = TRUE`, come in questo esempio:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Passaggio 3. Call sp_rxPredict

Si chiama sp\_rxPredict come si procederebbe per un stored procedure. Nella versione corrente, la stored procedure accetta solo due parametri:  _\@model_ per il modello in formato binario, e  _\@inputData_ per i dati da utilizzare nell'assegnazione dei punteggi, definito come una query SQL valida.

Poiché il formato binario è uguale a quello usato dalla funzione di stima, è possibile usare la tabella di modelli e i dati dell'esempio precedente.

```sql
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> La chiamata a sp\_rxPredict ha esito negativo se i dati di input per il punteggio non includono colonne che corrispondono ai requisiti del modello. Attualmente, sono supportati solo i seguenti tipi di dati .NET: double, float, short, ushort, long, ulong e stringa.
> 
> Di conseguenza, potrebbe essere necessario filtrare i tipi non supportati nei dati di input prima di usarlo per assegnare i punteggi in tempo reale.
> 
> Per informazioni sui tipi SQL corrispondenti, vedere [Mapping dei tipi SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) oppure [Mapping dei dati dei parametri CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Disabilita l'assegnazione dei punteggi in tempo reale

Per disabilitare la funzionalità di assegnazione dei punteggi in tempo reale, aprire un prompt dei comandi con privilegi elevati ed eseguire il comando seguente: `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'assegnazione dei punteggi in SQL Server, vedere [come generare le stime in SQL Server machine Learning Services](r/how-to-do-realtime-scoring.md).
