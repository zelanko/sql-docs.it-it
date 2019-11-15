---
title: 'Esercitazione su Python: Eseguire il training del modello'
description: In questa esercitazione si useranno Python e la regressione lineare in Machine Learning Services per SQL Server per stimare il numero di noleggi di sci. Si eseguirà quindi il training di un modello di regressione lineare in Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5f83fe37890c997865c44198cbe30bc13cdea4e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727051"
---
# <a name="python-tutorial-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Esercitazione su Python: Eseguire il training di un modello di regressione lineare in Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nella terza parte di questa serie di esercitazioni in quattro parti verrà eseguito il training di un modello di regressione lineare in Python. Nella parte successiva della serie questo modello verrà distribuito in un database di SQL Server con Machine Learning Services.

In questo articolo si apprenderà come:

> [!div class="checklist"]
> * Eseguire il training di un modello di regressione lineare
> * Eseguire stime tramite un modello di regressione lineare

Nella [prima parte](python-ski-rental-linear-regression.md) si è appreso come ripristinare il database di esempio.

Nella [seconda parte](python-ski-rental-linear-regression-prepare-data.md) si è appreso come caricare i dati da SQL Server in un frame di dati Python e come preparare i dati in Python.

Nella [quarta parte](python-ski-rental-linear-regression-deploy-model.md) si apprenderà come archiviare il modello in SQL Server e creare stored procedure dagli script Python sviluppati nella seconda e nella terza parte. Le stored procedure verranno quindi eseguite in SQL Server per eseguire stime basate sui nuovi dati.

## <a name="prerequisites"></a>Prerequisites

* Per poter eseguire la terza parte di questa esercitazione si presuppone che sia stata completata la [prima parte](python-ski-rental-linear-regression.md) e i rispettivi prerequisiti.

## <a name="train-the-model"></a>Eseguire il training del modello

Per eseguire una stima, è necessario trovare una funzione (modello) che descriva al meglio la dipendenza tra le variabili del set di dati. In questo modo viene eseguito il training del modello. Il set di dati di training sarà costituito da un subset dell'intero set di dati del frame di dati pandas **df** creato nella seconda parte di questa serie.

Verrà eseguito il training del modello **lin_model** usando un algoritmo di regressione lineare.

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

I risultati visualizzati saranno simili ai seguenti:

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>Effettuare stime

Usare una funzione Predict per stimare il numero di noleggi usando il modello **lin_model**.

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
* Eseguire stime tramite un modello di regressione lineare

Per distribuire il modello di Machine Learning creato, seguire la quarta parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione su Python: Distribuire un modello di Machine Learning](python-ski-rental-linear-regression-deploy-model.md)