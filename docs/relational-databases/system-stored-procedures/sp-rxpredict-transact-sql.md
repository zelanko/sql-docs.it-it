---
title: sp_rxPredict | Microsoft Docs
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: HeidiSteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 0be8727541a74bc80ab19265b94cf2408330b1e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66454480"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Genera un valore stimato per un determinato input costituito da un modello di machine learning archiviato in un formato binario in un database di SQL Server.

Fornisce l'assegnazione dei punteggi in R e Python modelli di machine learning in tempo quasi reale. `sp_rxPredict` è una stored procedure fornita come wrapper per il `rxPredict` funzione R nel [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) e [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)e la [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) funzione Python nella [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). Scritta in C++ ed è ottimizzato in modo specifico per le operazioni di assegnazione dei punteggi.

Anche se il modello deve essere creato usando R o Python, una volta che viene serializzato e archiviato in un formato binario in un'istanza di motore di database di destinazione, può essere utilizzato da tale istanza del motore di database anche quando non è installato integrazione R o Python. Per altre informazioni, vedere [attribuzione dei punteggi in tempo reale con sp_rxPredict](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="syntax"></a>Sintassi

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argomenti

**model**

Un modello con training preliminare in un formato supportato. 

**input**

Una query SQL valida

### <a name="return-values"></a>Valori restituiti

Viene restituita una colonna di punteggio, e tutte le colonne pass-through dall'origine dati di input.
Ulteriori colonne di tipo, ad esempio l'intervallo di confidenza, può essere restituito se l'algoritmo supporta la generazione di tali valori.

## <a name="remarks"></a>Note

Per abilitare l'utilizzo della stored procedure, SQLCLR deve essere abilitato nell'istanza.

> [!NOTE]
> Esistono implicazioni di sicurezza per l'attivazione di questa opzione. Usare un'implementazione alternativa, ad esempio la [Transact-SQL stimare](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017) funzione, se nel server non possono essere abilitati SQLCLR.

Le esigenze degli utenti `EXECUTE` autorizzazione per il database.

### <a name="supported-algorithms"></a>Algoritmi supportati

Creare e il training del modello, usare uno degli algoritmi supportati per R o Python, fornito da [SQL Server 2016 R Services](https://docs.microsoft.com/sql/advanced-analytics/r/sql-server-r-services?view=sql-server-2017), [SQL Server 2016 R Server (Standalone)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2016), [macchina SQL Server 2017 Servizi (R o Python) di apprendimento](https://docs.microsoft.com//sql/advanced-analytics/what-is-sql-server-machine-learning?view=sql-server-2017), oppure [SQL Server 2017 Server (Standalone) (R o Python)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2017).

#### <a name="r-revoscaler-models"></a>R: Modelli di RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: Modelli di MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: Trasformazioni fornite da MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: i modelli revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: i modelli di microsoftml

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python: Trasformazioni fornite da microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>Tipi di modello non supportato

Non sono supportati i tipi di modello seguente:

+ I modelli usando la `rxGlm` o `rxNaiveBayes` algoritmi in RevoScaleR
+ Modelli di linguaggio PMML in R
+ Modelli creati con altre librerie di terze parti 

## <a name="examples"></a>Esempi

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

Oltre a essere una query SQL valida, dati di input *@inputData* deve includere colonne compatibili con le colonne del modello archiviato.

`sp_rxPredict` supporta solo i seguenti tipi di colonna .NET: double, float, short, ushort, long, ulong e stringa. Potrebbe essere necessario filtrare i tipi non supportati nei dati di input prima di usarlo per assegnare i punteggi in tempo reale. 

  Per informazioni sui tipi SQL corrispondenti, vedere [Mapping dei tipi SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) oppure [Mapping dei dati dei parametri CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

