---
title: proprietà sp_rxPredict . Documenti Microsoft
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 3c12349e48f474b53957ffac55415ccc0689eeca
ms.sourcegitcommit: fbe0ab88fa8d5aa3ea96629f4ccfa4da5caf74f4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/10/2020
ms.locfileid: "81012439"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly.md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Genera un valore stimato per un determinato input costituito da un modello di Machine Learning archiviato in un formato binario in un database di SQL Server.

Fornisce il punteggio sui modelli di machine learning R e Python quasi in tempo reale. `sp_rxPredict`è una stored procedure fornita `rxPredict` come wrapper per la funzione R in [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) e [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)e la [funzione rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) Python in [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). Esso è scritto in C , ed è ottimizzato in modo specifico per le operazioni di punteggio.

Anche se il modello deve essere creato utilizzando R o Python, una volta che viene serializzato e archiviato in un formato binario in un'istanza del motore di database di destinazione, può essere utilizzato da tale istanza del motore di database anche quando r o Python integrazione non è installato. Per ulteriori informazioni, consultate [Assegnazione del punteggio in tempo reale con sp_rxPredict](https://docs.microsoft.com/sql/machine-learning/real-time-scoring).

## <a name="syntax"></a>Sintassi

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argomenti

**model**

Un modello con training preliminare in un formato supportato. 

**Input**

Una query SQL valida

### <a name="return-values"></a>Valori restituiti

Viene restituita una colonna di punteggio, nonché tutte le colonne pass-through dall'origine dati di input.
È possibile restituire colonne di punteggio aggiuntive, ad esempio l'intervallo di confidenza, se l'algoritmo supporta la generazione di tali valori.

## <a name="remarks"></a>Osservazioni

Per abilitare l'utilizzo della stored procedure, sqlCLR deve essere abilitato nell'istanza.

> [!NOTE]
> L'integrazione di questa opzione ha implicazioni per la sicurezza. Utilizzare un'implementazione alternativa, ad esempio la funzione [Transact-SQL PREDICT,](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017) se SQLCLR non può essere abilitato nel server.

L'utente `EXECUTE` deve disporre dell'autorizzazione per il database.

### <a name="supported-algorithms"></a>Algoritmi supportati

Per creare ed eseguire il training del modello, usare uno degli algoritmi supportati per R o Python, fornito da [SQL Server Machine Learning Services (R o Python)](https://docs.microsoft.com/sql/machine-learning/what-is-sql-server-machine-learning), SQL Server [2016 R Services](https://docs.microsoft.com/sql/machine-learning/r/sql-server-r-services), SQL Server Machine Learning Server [(Autonomo) (R o Python)](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone)o [SQL Server 2016 R Server (Standalone).](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone?view=sql-server-2016)

#### <a name="r-revoscaler-models"></a>R: Modelli RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForesta](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: Modelli MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: Trasformazioni fornite da MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [Concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: modelli revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: modelli microsoftml

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python: trasformazioni fornite da microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [Concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>Tipi di modelli non supportati

I seguenti tipi di modello non sono supportati:

+ Modelli che `rxGlm` `rxNaiveBayes` utilizzano gli algoritmi o in RevoScaleR
+ Modelli PMML in R
+ Modelli creati con altre librerie di terze parti 

## <a name="examples"></a>Esempi

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

Oltre a essere una query SQL valida, i dati di input in * \@inputData* devono includere colonne compatibili con le colonne nel modello archiviato.

`sp_rxPredict`supporta solo i seguenti tipi di colonna .NET: double, float, short, ushort, long, ulong e string. Potrebbe essere necessario filtrare i tipi non supportati nei dati di input prima di utilizzarli per il punteggio in tempo reale. 

  Per informazioni sui tipi SQL corrispondenti, vedere [Mapping del tipo SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [Mapping dei dati dei parametri CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

