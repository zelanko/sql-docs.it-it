---
title: 'Esercitazione su Python: Preparare i dati'
description: In questa esercitazione si useranno Python e la regressione lineare in Machine Learning Services per SQL Server per stimare il numero di noleggi di sci. I dati verranno preparati da un database SQL Server tramite Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6424a453bff2f0f6d62caa8c9870ccc2ec10d578
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727061"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Esercitazione su Python: Preparare i dati per il training di un modello di regressione lineare in Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Nella seconda parte di questa serie di esercitazioni in quattro parti verranno preparati i dati da un database SQL Server tramite Python. Più avanti nel corso della serie questi dati verranno usati per eseguire il training e la distribuzione di un modello di regressione lineare in Python con Machine Learning Services per SQL Server.

In questo articolo si apprenderà come:

> [!div class="checklist"]
> * Caricare i dati dal database SQL Server in un frame di dati **pandas**
> * Preparare i dati in Python rimuovendo alcune colonne

Nella [prima parte](python-ski-rental-linear-regression.md) si è appreso come ripristinare il database di esempio.

Nella [terza parte](python-ski-rental-linear-regression-train-model.md) si apprenderà come eseguire il training di un modello di Machine Learning di regressione lineare in Python.

Nella [quarta parte](python-ski-rental-linear-regression-deploy-model.md) si apprenderà come archiviare il modello in SQL Server e creare stored procedure dagli script Python sviluppati nella seconda e nella terza parte. Le stored procedure verranno quindi eseguite in SQL Server per eseguire stime basate sui nuovi dati.

## <a name="prerequisites"></a>Prerequisites

* Per poter eseguire la seconda parte di questa esercitazione si presuppone che sia stata completata la [prima parte](python-ski-rental-linear-regression.md) e i rispettivi prerequisiti.

## <a name="explore-and-prepare-the-data"></a>Esplorare e preparare i dati

Per poter usare i dati in Python, sarà necessario caricare i dati dal database SQL Server in un frame di dati pandas.

Creare un nuovo notebook Python in Azure Data Studio ed eseguire lo script seguente. Sostituire `<SQL Server>` con il nome dell'istanza personale di SQL Server.

Lo script Python seguente consente di importare il set di dati dalla tabella **dbo.rental_data** del database in un frame di dati pandas **df**.

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

I risultati visualizzati saranno simili ai seguenti:

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

* Caricare i dati dal database SQL Server in un frame di dati **pandas**
* Preparare i dati in Python rimuovendo alcune colonne

Per eseguire il training di un modello di Machine Learning che usa i dati del database TutorialDB, seguire la terza parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione su Python: Eseguire il training di un modello di regressione lineare](python-ski-rental-linear-regression-train-model.md)