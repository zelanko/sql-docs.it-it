---
title: 'Esercitazione per Python: Preparare i dati (regressione lineare)'
description: In questa esercitazione si userà Python e la regressione lineare in SQL Server Machine Learning Services per prevedere il numero di noleggi di sci. Si preparano i dati da un database di SQL Server usando Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6c4d5fb4ffc5049f7e1325267b7623dc195e9d8
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242499"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Esercitazione per Python: Preparare i dati per il training di un modello di regressione lineare in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nella seconda parte di questa serie di esercitazioni in quattro parti, si preparano i dati da un database di SQL Server usando Python. Più avanti in questa serie questi dati verranno usati per eseguire il training e la distribuzione di un modello di regressione lineare in Python con SQL Server Machine Learning Services.

L'articolo spiega come:

> [!div class="checklist"]
> * Caricare i dati dal database SQL Server in un frame di dati **Pandas**
> * Preparare i dati in Python rimuovendo alcune colonne

Nella [prima parte](python-ski-rental-linear-regression.md)si è appreso come ripristinare il database di esempio.

Nella [terza parte](python-ski-rental-linear-regression-train-model.md)verrà illustrato come eseguire il training di un modello di apprendimento automatico di regressione lineare in Python.

Nella [quarta parte](python-ski-rental-linear-regression-deploy-model.md), si apprenderà come archiviare il modello in SQL Server, quindi creare stored procedure dagli script Python sviluppati in parti due e tre. Le stored procedure vengono eseguite in SQL Server per eseguire stime basate sui nuovi dati.

## <a name="prerequisites"></a>Prerequisiti

* Nella seconda parte di questa esercitazione si presuppone che sia stata completata la [parte 1](python-ski-rental-linear-regression.md) e i relativi prerequisiti.

## <a name="explore-and-prepare-the-data"></a>Esplorare e preparare i dati

Per usare i dati in Python, è necessario caricare i dati dal database SQL Server in un frame di dati Pandas.

Creare un nuovo notebook Python in Azure Data Studio ed eseguire lo script seguente. Sostituire `<SQL Server>` con il nome del SQL Server.

Lo script Python seguente importa il set di dati dalla tabella **dbo. rental_data** nel database a **un frame di**dati Pandas.

```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_import

# Connection string to your SQL Server instance
conn_str = 'Driver=SQL Server;Server=<SQL Server>;Database=TutorialDB;Trusted_Connection=True;'

# Define the columns you will import
 column_info = {
         "Year" : { "type" : "integer" },
         "Month" : { "type" : "integer" },
         "Day" : { "type" : "integer" },
         "RentalCount" : { "type" : "integer" },
         "WeekDay" : {
             "type" : "factor",
             "levels" : ["1", "2", "3", "4", "5", "6", "7"]
         },
         "Holiday" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         },
         "Snow" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         }
     }

# Get the data from the SQL Server table
data_source = RxSqlServerData(table="dbo.rental_data",
                               connection_string=conn_str, column_info=column_info)
computeContext = RxInSqlServer(
     connection_string = conn_str,
     num_tasks = 1,
     auto_cleanup = False
)

RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)

# import data source and convert to pandas dataframe
df = pd.DataFrame(rx_import(input_data = data_source))
print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

Verranno visualizzati risultati simili ai seguenti.

```results
Rows Processed: 453
Data frame:      Day  Holiday  Month  RentalCount  Snow  WeekDay  Year
0     20        1      1          445     2        2  2014
1     13        2      2           40     2        5  2014
2     10        2      3          456     2        1  2013
3     31        2      3           38     2        2  2014
4     24        2      4           23     2        5  2014
5     11        2      2           42     2        4  2015
6     28        2      4          310     2        1  2013
...
[453 rows x 7 columns]
```

## <a name="next-steps"></a>Passaggi successivi

Nella seconda parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Caricare i dati dal database SQL Server in un frame di dati **Pandas**
* Preparare i dati in Python rimuovendo alcune colonne

Per eseguire il training di un modello di apprendimento automatico che usa i dati del database TutorialDB, seguire la terza parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione per Python: Eseguire il training di un modello di regressione lineare](python-ski-rental-linear-regression-train-model.md)