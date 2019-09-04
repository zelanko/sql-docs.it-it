---
title: 'Esercitazione per Python: Train Model (regressione lineare)'
description: In questa esercitazione si userà Python e la regressione lineare in SQL Server Machine Learning Services per prevedere il numero di noleggi di sci. Si eseguirà il training di un modello di regressione lineare in Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 30f390681dc63d6de9a95e805b6cc8f273b2b8d7
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242549"
---
# <a name="python-tutorial-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Esercitazione per Python: Eseguire il training di un modello di regressione lineare in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nella terza parte di questa serie di esercitazioni in quattro parti si eseguirà il training di un modello di regressione lineare in Python. Nella parte successiva di questa serie verrà distribuito questo modello in un database di SQL Server con Machine Learning Services.

L'articolo spiega come:

> [!div class="checklist"]
> * Eseguire il training di un modello di regressione lineare
> * Eseguire stime tramite il modello di regressione lineare

Nella [prima parte](python-ski-rental-linear-regression.md)si è appreso come ripristinare il database di esempio.

Nella [seconda parte](python-ski-rental-linear-regression-prepare-data.md)si è appreso come caricare i dati da SQL Server in un frame di dati Python e preparare i dati in Python.

Nella [quarta parte](python-ski-rental-linear-regression-deploy-model.md), si apprenderà come archiviare il modello in SQL Server, quindi creare stored procedure dagli script Python sviluppati in parti due e tre. Le stored procedure vengono eseguite in SQL Server per eseguire stime basate sui nuovi dati.

## <a name="prerequisites"></a>Prerequisiti

* Nella terza parte di questa esercitazione si presuppone che sia stata completata la [parte 1](python-ski-rental-linear-regression.md) e i relativi prerequisiti.

## <a name="train-the-model"></a>Eseguire il training del modello

Per stimare, è necessario trovare una funzione (modello) che meglio descriva la dipendenza tra le variabili nel set di dati. Questa operazione ha chiamato il training del modello. Il set di dati di training sarà un subset dell'intero set di dati del frame di dati Pandas **che è stato** creato nella seconda parte di questa serie.

Si eseguirà il training del modello **lin_model** usando un algoritmo di regressione lineare.

```python
# Store the variable we'll be predicting on.
target = "RentalCount"

# Generate the training set.  Set random_state to be able to replicate results.
train = df.sample(frac=0.8, random_state=1)

# Select anything not in the training set and put it in the testing set.
test = df.loc[~df.index.isin(train.index)]

# Print the shapes of both sets.
print("Training set shape:", train.shape)
print("Testing set shape:", test.shape)

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(train[columns], train[target])
```

Verranno visualizzati risultati simili ai seguenti.

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>Eseguire stime

Usare una funzione Predict per stimare i conteggi di noleggio usando il modello **lin_model**.

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

```results
Predictions: [  40.   38.  240.   39.  514.   48.  297.   25.  507.   24.   30.   54.
   40.   26.   30.   34.   42.  390.  336.   37.   22.   35.   55.  350.
  252.  370.  499.   48.   37.  494.   46.   25.  312.  390.   35.   35.
  421.   39.  176.   21.   33.  452.   34.   28.   37.  260.   49.  577.
  312.   24.   24.  390.   34.   64.   26.   32.   33.  358.  348.   25.
   35.   48.   39.   44.   58.   24.  350.  651.   38.  468.   26.   42.
  310.  709.  155.   26.  648.  617.   26.  846.  729.   44.  432.   25.
   39.   28.  325.   46.   36.   50.   63.]
Computed error: 3.59831533436e-26
```

## <a name="next-steps"></a>Passaggi successivi

Nella terza parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Eseguire il training di un modello di regressione lineare
* Eseguire stime tramite il modello di regressione lineare

Per distribuire il modello di Machine Learning creato, seguire la quarta parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione per Python: Distribuire un modello di Machine Learning](python-ski-rental-linear-regression-deploy-model.md)