---
title: 'Esercitazione per Python: Distribuisci modello (regressione lineare)'
description: In questa esercitazione si userà Python e la regressione lineare in SQL Server Machine Learning Services per prevedere il numero di noleggi di sci. Si distribuirà un modello di regressione lineare sviluppato in Python in un database SQL Server usando Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08f5d19af93ab180c660a264d5aaabc538d527a5
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242519"
---
# <a name="python-tutorial-deploy-a-linear-regression-model-to-sql-server-machine-learning-services"></a>Esercitazione per Python: Distribuire un modello di regressione lineare per SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nella quarta parte di questa serie di esercitazioni in quattro parti, verrà distribuito un modello di regressione lineare sviluppato in Python in un database SQL Server usando Machine Learning Services.

L'articolo spiega come:

> [!div class="checklist"]
> * Creare una stored procedure che genera il modello di Machine Learning
> * Archiviare il modello in una tabella di database
> * Creare una stored procedure che esegue stime tramite il modello
> * Eseguire il modello con nuovi dati

Nella [prima parte](python-ski-rental-linear-regression.md)si è appreso come ripristinare il database di esempio.

Nella [seconda parte](python-ski-rental-linear-regression-prepare-data.md)si è appreso come caricare i dati da SQL Server in un frame di dati Python e preparare i dati in Python.

Nella [terza parte](python-ski-rental-linear-regression-train-model.md)si è appreso come eseguire il training di un modello di apprendimento automatico di regressione lineare in Python.

## <a name="prerequisites"></a>Prerequisiti

* Nella quarta parte di questa esercitazione si presuppone che sia stata completata la [parte 1](python-ski-rental-linear-regression.md) e i relativi prerequisiti.

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Creare un stored procedure che genera il modello

Ora, usando gli script Python sviluppati, creare un stored procedure **generate_rental_rx_model** che esegue il training e genera il modello di regressione lineare usando LinearRegression da Scikit-learn.

Eseguire l'istruzione T-SQL seguente in Azure Data Studio per creare il stored procedure per eseguire il training del modello.

```sql
-- Stored procedure that trains and generates a Python model using the rental_data and a decision tree algorithm
DROP PROCEDURE IF EXISTS generate_rental_py_model;
go
CREATE PROCEDURE generate_rental_py_model (@trained_model varbinary(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
from sklearn.linear_model import LinearRegression
import pickle

df = rental_train_data

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Store the variable well be predicting on.
target = "RentalCount"

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(df[columns], df[target])

# Before saving the model to the DB table, convert it to a binary object
trained_model = pickle.dumps(lin_model)'

, @input_data_1 = N'select "RentalCount", "Year", "Month", "Day", "WeekDay", "Snow", "Holiday" from dbo.rental_data where Year < 2015'
, @input_data_1_name = N'rental_train_data'
, @params = N'@trained_model varbinary(max) OUTPUT'
, @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>Archiviare il modello in una tabella di database

Creare una tabella nel database TutorialDB, quindi salvare il modello nella tabella.

1. Eseguire l'istruzione T-SQL seguente in Azure Data Studio per creare una tabella denominata **dbo. rental_py_models** utilizzata per archiviare il modello.

    ```sql
    USE TutorialDB;
    DROP TABLE IF EXISTS dbo.rental_py_models;
    GO
    CREATE TABLE dbo.rental_py_models (
        model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY,
        model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

1. Salvare il modello nella tabella come oggetto binario, con il nome del modello **linear_model**.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC generate_rental_py_model @model OUTPUT;
    
    INSERT INTO rental_py_models (model_name, model) VALUES('linear_model', @model);
    ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>Creare una stored procedure che esegue stime

1. Creare una stored procedure **py_predict_rentalcount** che esegue stime usando il modello sottoposto a training e un set di nuovi dati. Eseguire l'istruzione T-SQL seguente in Azure Data Studio.

    ```sql
    DROP PROCEDURE IF EXISTS py_predict_rentalcount;
    GO
    CREATE PROCEDURE py_predict_rentalcount (@model varchar(100))
    AS
    BEGIN
        DECLARE @py_model varbinary(max) = (select model from rental_py_models where model_name = @model);
    
        EXEC sp_execute_external_script
                    @language = N'Python',
                    @script = N'
    
    # Import the scikit-learn function to compute error.
    from sklearn.metrics import mean_squared_error
    import pickle
    import pandas as pd
    
    rental_model = pickle.loads(py_model)
    
    df = rental_score_data
    
    # Get all the columns from the dataframe.
    columns = df.columns.tolist()
    
    # Variable you will be predicting on.
    target = "RentalCount"
    
    # Generate the predictions for the test set.
    lin_predictions = rental_model.predict(df[columns])
    print(lin_predictions)
    
    # Compute error between the test predictions and the actual values.
    lin_mse = mean_squared_error(lin_predictions, df[target])
    #print(lin_mse)
    
    predictions_df = pd.DataFrame(lin_predictions)
    
    OutputDataSet = pd.concat([predictions_df, df["RentalCount"], df["Month"], df["Day"], df["WeekDay"], df["Snow"], df["Holiday"], df["Year"]], axis=1)
    '
    , @input_data_1 = N'Select "RentalCount", "Year" ,"Month", "Day", "WeekDay", "Snow", "Holiday"  from rental_data where Year = 2015'
    , @input_data_1_name = N'rental_score_data'
    , @params = N'@py_model varbinary(max)'
    , @py_model = @py_model
    with result sets (("RentalCount_Predicted" float, "RentalCount" float, "Month" float,"Day" float,"WeekDay" float,"Snow" float,"Holiday" float, "Year" float));
    
    END;
    GO
    ```

1. Creare una tabella per l'archiviazione delle stime.

    ```sql
    DROP TABLE IF EXISTS [dbo].[py_rental_predictions];
    GO

    CREATE TABLE [dbo].[py_rental_predictions](
     [RentalCount_Predicted] [int] NULL,
     [RentalCount_Actual] [int] NULL,
     [Month] [int] NULL,
     [Day] [int] NULL,
     [WeekDay] [int] NULL,
     [Snow] [int] NULL,
     [Holiday] [int] NULL,
     [Year] [int] NULL
    ) ON [PRIMARY]
    GO
    ```

1. Esegui il stored procedure per stimare i conteggi di noleggio

    ```sql
    --Insert the results of the predictions for test set into a table
    INSERT INTO py_rental_predictions
    EXEC py_predict_rentalcount 'linear_model';

    -- Select contents of the table
    SELECT * FROM py_rental_predictions;
    ```

È stato creato, sottoposto a training e distribuito un modello in un SQL Server Machine Learning Services. Il modello è stato quindi usato in una stored procedure per stimare i valori in base ai nuovi dati.

## <a name="next-steps"></a>Passaggi successivi

Nella quarta parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Creare una stored procedure che genera il modello di Machine Learning
* Archiviare il modello in una tabella di database
* Creare una stored procedure che esegue stime tramite il modello
* Eseguire il modello con nuovi dati

Per altre informazioni sull'uso di Python in SQL Server Machine Learning Services, vedere:

+ [Esercitazioni su Python per SQL Server Machine Learning Services](sql-server-python-tutorials.md)