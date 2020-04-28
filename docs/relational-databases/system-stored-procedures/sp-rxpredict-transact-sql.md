---
title: sp_rxPredict | Microsoft Docs
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
ms.openlocfilehash: 9663b4cd51a7aca9e9e30ccafcdcb0652ec4229a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488540"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly.md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Genera un valore stimato per un input specificato costituito da un modello di apprendimento automatico archiviato in un formato binario in un database SQL Server.

Fornisce l'assegnazione dei punteggi ai modelli di apprendimento automatico R e Python in tempo quasi reale. `sp_rxPredict`è `rxPredict` un stored procedure fornito come wrapper per la funzione R in [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) e [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)e la funzione Python [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) in [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). Viene scritto in C++ ed è ottimizzato in modo specifico per le operazioni di assegnazione dei punteggi.

Anche se il modello deve essere creato con R o Python, una volta serializzato e archiviato in un formato binario in un'istanza del motore di database di destinazione, può essere utilizzato da tale istanza del motore di database anche quando l'integrazione con R o Python non è installata. Per ulteriori informazioni, vedere Assegnazione di [punteggi in tempo reale con sp_rxPredict](https://docs.microsoft.com/sql/machine-learning/real-time-scoring).

## <a name="syntax"></a>Sintassi

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argomenti

**model**

Modello sottoposto a training in un formato supportato. 

**input**

Una query SQL valida

### <a name="return-values"></a>Valori restituiti

Viene restituita una colonna score, nonché tutte le colonne pass-through dell'origine dati di input.
È possibile restituire colonne con punteggio aggiuntivo, ad esempio intervallo di confidenza, se l'algoritmo supporta la generazione di tali valori.

## <a name="remarks"></a>Osservazioni

Per abilitare l'utilizzo del stored procedure, SQLCLR deve essere abilitato nell'istanza di.

> [!NOTE]
> Questa opzione presenta implicazioni di sicurezza per enabing. Utilizzare un'implementazione alternativa, ad esempio la funzione di [stima Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017) , se non è possibile abilitare SQLCLR nel server.

L'utente deve `EXECUTE` disporre dell'autorizzazione per il database.

### <a name="supported-algorithms"></a>Algoritmi supportati

Per creare ed eseguire il training del modello, usare uno degli algoritmi supportati per R o Python, fornito da [SQL Server Machine Learning Services (r o Python)](https://docs.microsoft.com/sql/machine-learning/sql-server-machine-learning-services), [SQL Server 2016 R Services](https://docs.microsoft.com/sql/machine-learning/r/sql-server-r-services), [SQL Server machine learning Server (autonomo) (r o python)](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone)o [SQL Server 2016 R Server (standalone)](https://docs.microsoft.com/sql/machine-learning/r/r-server-standalone?view=sql-server-2016).

#### <a name="r-revoscaler-models"></a>R: modelli RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: modelli MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: trasformazioni fornite da MicrosoftML

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

I tipi di modello seguenti non sono supportati:

+ Modelli con gli `rxGlm` algoritmi `rxNaiveBayes` o in RevoScaleR
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

Oltre a essere una query SQL valida, i dati di input in * \@inputData* devono includere le colonne compatibili con le colonne nel modello archiviato.

`sp_rxPredict`supporta solo i tipi di colonna .NET seguenti: Double, float, short, ushort, Long, ULONG e String. Potrebbe essere necessario filtrare i tipi non supportati nei dati di input prima di usarli per l'assegnazione dei punteggi in tempo reale. 

  Per informazioni sui tipi SQL corrispondenti, vedere [Mapping del tipo SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [Mapping dei dati dei parametri CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

