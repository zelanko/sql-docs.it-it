---
title: Assegnazione di punteggi in tempo reale con sp_rxPredict stored procedure
description: Generare stime usando sp_rxPredict, assegnando punteggi ai dati in base a un modello con training preliminare scritto in R su SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/26/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 26701ac6e538d195a5a85ad66af9578848889d23
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715643"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>Assegnazione di punteggi in tempo reale con sp_rxPredict in SQL Server machine learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Il Punteggio in tempo reale usa il stored procedure di sistema [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) e le funzionalità di estensione CLR in SQL Server per stime a prestazioni elevate o punteggi nei carichi di lavoro di previsione. Il Punteggio in tempo reale è indipendente dal linguaggio e viene eseguito senza dipendenze dai tempi di esecuzione di R o Python. Supponendo che un modello sia stato creato e sottoposto a training usando le funzioni Microsoft e quindi serializzato in un formato binario in SQL Server, è possibile usare il punteggio in tempo reale per generare risultati stimati in nuovi input di dati in istanze di SQL Server che non hanno il componente aggiuntivo R o Python installato.

## <a name="how-real-time-scoring-works"></a>Funzionamento del punteggio in tempo reale

Il Punteggio in tempo reale è supportato su tipi di modello specifici in base alle funzioni RevoScaleR o MicrosoftML, ad esempio [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). USA librerie native C++ per generare punteggi, in base all'input dell'utente fornito a un modello di Machine Learning archiviato in un formato binario speciale.

Poiché un modello sottoposto a training può essere utilizzato per l'assegnazione dei punteggi senza dover chiamare un runtime di linguaggio esterno, viene ridotto l'overhead di più processi. Questo supporta prestazioni di stima molto più veloci per gli scenari di assegnazione dei punteggi di produzione. Poiché i dati non lasciano mai SQL Server, è possibile generare e inserire i risultati in una nuova tabella senza alcuna conversione dei dati tra R e SQL.

Il Punteggio in tempo reale è un processo in più passaggi:

1. Il stored procedure che esegue il punteggio deve essere abilitato per ogni singolo database.
2. Il modello con training preliminare viene caricato in formato binario.
3. I nuovi dati di input devono essere classificati, tabulari o singole righe, come input per il modello.
4. Per generare i punteggi, chiamare il stored procedure [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) .

## <a name="prerequisites"></a>Prerequisiti

+ [Abilitare SQL Server l'integrazione con CLR](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ [Abilita Punteggio in tempo reale](#bkmk_enableRtScoring).

+ Il training del modello deve essere eseguito in anticipo utilizzando uno degli algoritmi **RX** supportati. Per R, i punteggi in tempo reale `sp_rxPredict` con funzionano con gli [algoritmi supportati RevoScaleR e MicrosoftML](#bkmk_rt_supported_algos). Per Python, vedere [algoritmi supportati revoscalepy e microsoftml](#bkmk_py_supported_algos)

+ Serializzare il modello usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) per R e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) per Python. Queste funzioni di serializzazione sono state ottimizzate per supportare il Punteggio rapido.

+ Salvare il modello nell'istanza del motore di database da cui si desidera chiamarlo. Per questa istanza non è necessario avere l'estensione di runtime R o Python.

> [!Note]
> Il Punteggio in tempo reale è attualmente ottimizzato per stime rapide su set di dati più piccoli, che vanno da poche righe a centinaia di migliaia di righe. Nei set di grandi dimensioni, l'uso di [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) potrebbe essere più veloce.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>Algoritmi supportati

### <a name="python-algorithms-using-real-time-scoring"></a>Algoritmi Python che usano il punteggio in tempo reale

+ modelli revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  I modelli contrassegnati \* con supportano anche il Punteggio nativo con la funzione Predict.

+ modelli microsoftml

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

### <a name="r-algorithms-using-real-time-scoring"></a>Algoritmi R che usano il punteggio in tempo reale

+ Modelli RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  I modelli contrassegnati \* con supportano anche il Punteggio nativo con la funzione Predict.

+ Modelli MicrosoftML

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

### <a name="unsupported-model-types"></a>Tipi di modello non supportati

Il Punteggio in tempo reale non usa un interprete; Pertanto, qualsiasi funzionalità che potrebbe richiedere un interprete non è supportata durante il passaggio di assegnazione dei punteggi.  Questi possono includere:

  + I modelli che `rxGlm` usano `rxNaiveBayes` gli algoritmi o non sono supportati.

  + <code>A ~ log(B)</code> I modelli che utilizzano una funzione di trasformazione o una formula contenente una trasformazione, ad esempio, non sono supportati in un punteggio in tempo reale. Per usare un modello di questo tipo, è consigliabile eseguire la trasformazione sui dati di input prima di passare i dati a un punteggio in tempo reale.


## <a name="example-sprxpredict"></a>Example: sp_rxPredict

In questa sezione vengono descritti i passaggi necessari per configurare la stima in **tempo reale** e viene fornito un esempio in R di come chiamare la funzione da T-SQL.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>Passaggio 1. Abilitare la procedura di assegnazione dei punteggi in tempo reale

È necessario abilitare questa funzionalità per ogni database che si desidera utilizzare per l'assegnazione dei punteggi. L'amministratore del server deve eseguire l'utilità da riga di comando RegisterRExt. exe, inclusa nel pacchetto RevoScaleR.

> [!NOTE]
> Per consentire il funzionamento del punteggio in tempo reale, è necessario abilitare la funzionalità CLR SQL nell'istanza di. Inoltre, è necessario contrassegnare il database come attendibile. Quando si esegue lo script, queste azioni vengono eseguite. Prima di procedere, considerare tuttavia le implicazioni di sicurezza aggiuntive.

1. Aprire un prompt dei comandi con privilegi elevati e passare alla cartella in cui si trova RegisterRExt. exe. Il percorso seguente può essere usato in un'installazione predefinita:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Eseguire il comando seguente, sostituendo il nome dell'istanza di e il database di destinazione in cui si desidera abilitare le stored procedure estese:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Ad esempio, per aggiungere il stored procedure esteso al database CLRPredict nell'istanza predefinita, digitare:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    Il nome dell'istanza è facoltativo se il database si trova nell'istanza predefinita. Se si utilizza un'istanza denominata, è necessario specificare il nome dell'istanza.

3. RegisterRExt. exe crea gli oggetti seguenti:

    + Assembly attendibili
    + stored procedure`sp_rxPredict`
    + Un nuovo ruolo del database `rxpredict_users`,. L'amministratore del database può utilizzare questo ruolo per concedere l'autorizzazione agli utenti che utilizzano la funzionalità di assegnazione dei punteggi in tempo reale.

4. Aggiungere tutti gli utenti che devono eseguire `sp_rxPredict` al nuovo ruolo.

> [!NOTE]
> 
> In SQL Server 2017 sono disponibili misure di sicurezza aggiuntive per evitare problemi con l'integrazione con CLR. Queste misure impongono restrizioni aggiuntive sull'uso di questo stored procedure. 

### <a name="step-2-prepare-and-save-the-model"></a>Passaggio 2. Preparare e salvare il modello

Il formato binario richiesto da SP\_rxPredict è uguale al formato necessario per utilizzare la funzione Predict. Nel codice R, quindi, includere una chiamata a [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)e assicurarsi di specificare `realtimeScoringOnly = TRUE`, come nell'esempio seguente:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Passaggio 3. Chiama sp_rxPredict

È possibile chiamare\_SP rxPredict come qualsiasi altra stored procedure. Nella versione corrente, il stored procedure accetta solo due parametri:  _\@Model_ per il modello in formato binario e  _\@inputData_ per i dati da usare per il punteggio, definito come una query SQL valida.

Poiché il formato binario è lo stesso usato dalla funzione PREDICT, è possibile usare i modelli e la tabella dati dell'esempio precedente.

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
> La chiamata a SP\_rxPredict ha esito negativo se i dati di input per il punteggio non includono colonne che soddisfano i requisiti del modello. Attualmente sono supportati solo i tipi di dati .NET seguenti: Double, float, short, ushort, Long, ULONG e String.
> 
> Quindi, potrebbe essere necessario filtrare i tipi non supportati nei dati di input prima di usarli per l'assegnazione dei punteggi in tempo reale.
> 
> Per informazioni sui tipi SQL corrispondenti, vedere [mapping del tipo SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [mapping dei dati dei parametri CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Disabilitare il punteggio in tempo reale

Per disabilitare la funzionalità di assegnazione dei punteggi in tempo reale, aprire un prompt dei comandi con privilegi elevati ed eseguire il comando seguente:`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>Passaggi successivi

Per informazioni più approfondite sull'assegnazione dei punteggi in SQL Server, vedere [How to generate Predictions in SQL Server machine learning](r/how-to-do-realtime-scoring.md).
