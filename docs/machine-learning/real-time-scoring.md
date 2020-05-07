---
title: Assegnazione dei punteggi in tempo reale tramite sp_rxPredict
description: Generare stime usando sp_rxPredict, assegnando punteggi agli input di dati in base a un modello con training preliminare scritto in R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/30/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f46b27019d85084b572dced79e786033b30c2aec
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719290"
---
# <a name="real-time-scoring-with-sp_rxpredict-in-sql-server-machine-learning"></a>Assegnazione dei punteggi in tempo reale con sp_rxPredict in SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

L'assegnazione dei punteggi in tempo reale si basa sulla stored procedure di sistema [sp_rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) e sulle funzionalità di estensione CLR in SQL Server per eseguire stime ad alte prestazioni o assegnare punteggi per i carichi di lavoro di previsione. L'assegnazione dei punteggi in tempo reale è indipendente dal linguaggio e viene eseguita senza dipendenze dai runtime di R o Python. Presupponendo che un modello sia stato creato e sottoposto a training usando le funzioni Microsoft e quindi serializzato in un formato binario in SQL Server, è possibile usare l'assegnazione dei punteggi in tempo reale per generare risultati stimati su nuovi input di dati in istanze di SQL Server che non hanno installato il componente aggiuntivo R o Python.

## <a name="how-real-time-scoring-works"></a>Funzionamento dell'assegnazione dei punteggi in tempo reale

L'assegnazione dei punteggi in tempo reale è supportata in tipi di modelli specifici in base alle funzioni RevoScaleR o MicrosoftML, ad esempio [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) e [rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). Usa librerie C++ native per generare punteggi, in base all'input dell'utente fornito a un modello di Machine Learning archiviato in un formato binario speciale.

Essendo possibile usare un modello sottoposto a training per l'assegnazione dei punteggi senza dover chiamare un runtime di linguaggio esterno, viene ridotto il sovraccarico di più processi. Ciò supporta prestazioni di stima molto più veloci per gli scenari di assegnazione dei punteggi di produzione. Poiché i dati non escono mai da SQL Server, è possibile generare e inserire i risultati in una nuova tabella senza alcuna conversione dei dati tra R e SQL.

L'assegnazione dei punteggi in tempo reale è un processo in più passaggi:

1. La stored procedure che esegue l'assegnazione dei punteggi deve essere abilitata per ogni singolo database.
2. Il modello con training preliminare viene caricato in formato binario.
3. Si forniscono nuovi dati di input a cui assegnare un punteggio, sia in formato tabulare che come righe singole, come input per il modello.
4. Per generare i punteggi, chiamare la stored procedure [sp_rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql).

## <a name="prerequisites"></a>Prerequisiti

+ [Abilitare l'integrazione CLR in SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ [Abilitare l'assegnazione dei punteggi in tempo reale](#bkmk_enableRtScoring).

+ Il training del modello deve essere eseguito in anticipo tramite uno degli algoritmi **rx** supportati. Per R, l'assegnazione dei punteggi in tempo reale con `sp_rxPredict` funziona con gli [algoritmi supportati di RevoScaleR e MicrosoftML](#bkmk_rt_supported_algos). Per Python, vedere [Algoritmi supportati di revoscalepy e microsoftml](#bkmk_py_supported_algos).

+ Serializzare il modello usando [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) per R e [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) per Python. Queste funzioni di serializzazione sono state ottimizzate per supportare l'assegnazione rapida dei punteggi.

+ Salvare il modello nell'istanza del motore di database da cui si vuole chiamarlo. Per questa istanza non è necessario avere l'estensione di runtime R o Python.

> [!Note]
> L'assegnazione dei punteggi in tempo reale è attualmente ottimizzata per stime rapide su set di dati più piccoli, che vanno da poche righe a centinaia di migliaia di righe. Nei set di grandi dimensioni potrebbe essere più veloce usare [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict).

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>Algoritmi supportati

### <a name="python-algorithms-using-real-time-scoring"></a>Algoritmi Python che usano l'assegnazione dei punteggi in tempo reale

+ Modelli revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  I modelli contrassegnati con \* supportano anche l'assegnazione dei punteggi nativa con la funzione PREDICT.

+ Modelli microsoftml

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
  
  I modelli contrassegnati con \* supportano anche l'assegnazione dei punteggi nativa con la funzione PREDICT.

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

### <a name="unsupported-model-types"></a>Tipi di modelli non supportati

L'assegnazione dei punteggi in tempo reale non usa un interprete, pertanto qualsiasi funzionalità che potrebbe richiedere un interprete non è supportata durante il passaggio di assegnazione dei punteggi.  Ad esempio:

  + I modelli che usano gli algoritmi `rxGlm` o `rxNaiveBayes` non sono supportati.

  + I modelli che usano una funzione di trasformazione o una formula contenente una trasformazione, ad esempio <code>A ~ log(B)</code>, non sono supportati per l'assegnazione dei punteggi in tempo reale. Per usare un modello di questo tipo, si consiglia di eseguire la trasformazione sui dati di input prima di passare i dati a un punteggio in tempo reale.


## <a name="example-sp_rxpredict"></a>Esempio: sp_rxPredict

In questa sezione vengono descritti i passaggi necessari per configurare la stima **in tempo reale** e viene fornito un esempio in R di come chiamare la funzione da T-SQL.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>Passaggio 1. Abilitare la procedura di assegnazione dei punteggi in tempo reale

È necessario abilitare questa funzionalità per ogni database che si vuole usare per l'assegnazione dei punteggi. L'amministratore del server deve eseguire l'utilità da riga di comando RegisterRExt.exe, inclusa nel pacchetto RevoScaleR.

> [!NOTE]
> Per consentire il funzionamento dell'assegnazione dei punteggi in tempo reale, è necessario abilitare la funzionalità CLR SQL nell'istanza. Inoltre, è necessario contrassegnare il database come attendibile. Quando si esegue lo script, queste operazioni vengono eseguite automaticamente. Tuttavia, prima di procedere, prendere in considerazione le ulteriori implicazioni in termini di sicurezza.

1. Aprire un prompt dei comandi con privilegi elevati e passare alla cartella in cui si trova RegisterRExt.exe. Il percorso seguente può essere usato in un'installazione predefinita:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Eseguire il comando seguente, sostituendo il nome dell'istanza e il database di destinazione in cui si vogliono abilitare le stored procedure estese:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Ad esempio, per aggiungere la stored procedure estesa al database CLRPredict nell'istanza predefinita, digitare:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    Il nome dell'istanza è facoltativo se il database si trova nell'istanza predefinita. Se si usa un'istanza denominata, è necessario specificare il nome dell'istanza.

3. RegisterRExt.exe crea gli oggetti seguenti:

    + Assembly attendibili
    + Stored procedure `sp_rxPredict`
    + Nuovo ruolo del database `rxpredict_users`, che l'amministratore del database può usare per concedere l'autorizzazione agli utenti che usano la funzionalità di assegnazione dei punteggi in tempo reale.

4. Aggiungere tutti gli utenti che devono eseguire `sp_rxPredict` al nuovo ruolo.

> [!NOTE]
> 
> In SQL Server 2017 sono disponibili misure di sicurezza aggiuntive per evitare problemi con l'integrazione CLR. Queste misure impongono anche ulteriori restrizioni sull'uso di questa stored procedure. 

### <a name="step-2-prepare-and-save-the-model"></a>Passaggio 2. Preparare e salvare il modello

Il formato binario richiesto da sp\_rxPredict è uguale al formato necessario per usare la funzione PREDICT. Includere quindi nel codice R una chiamata a [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) e assicurarsi di specificare `realtimeScoringOnly = TRUE`, come nell'esempio seguente:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sp_rxpredict"></a>Passaggio 3. Chiamare sp_rxPredict

sp\_rxPredict viene chiamata come qualsiasi altra stored procedure. Nella versione corrente la stored procedure accetta solo due parametri: _\@model_ per il modello in formato binario e _\@inputData_ per i dati da usare per l'assegnazione dei punteggi, definiti come query SQL valida.

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
> La chiamata a sp\_rxPredict ha esito negativo se i dati di input per l'assegnazione dei punteggi non includono colonne che soddisfano i requisiti del modello. Attualmente sono supportati solo i tipi di dati .NET seguenti: double, float, short, ushort, long, ulong e string.
> 
> Potrebbe quindi essere necessario filtrare ed escludere i tipi non supportati nei dati di input prima di usarli per l'assegnazione dei punteggi in tempo reale.
> 
> Per informazioni sui tipi SQL corrispondenti, vedere [Mapping del tipo SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [Mapping dei dati dei parametri CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Disabilitare l'assegnazione dei punteggi in tempo reale

Per disabilitare la funzionalità di assegnazione dei punteggi in tempo reale, aprire un prompt dei comandi con privilegi elevati ed eseguire il comando seguente: `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come assegnare i punteggi in SQL Server, vedere [Come generare stime in SQL Server Machine Learning](r/how-to-do-realtime-scoring.md).
