---
title: 'Esercitazione su Python: Preparazione dei dati'
description: Nella seconda parte di questa serie di esercitazioni in quattro parti si userà Python per preparare i dati per prevedere i noleggi di sci in Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9aeefb0b6fd9ca1a744d132fccf1eedfedbaa6e7
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116424"
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

## <a name="prerequisites"></a>Prerequisiti

* Per poter eseguire la seconda parte di questa esercitazione si presuppone che sia stata completata la [prima parte](python-ski-rental-linear-regression.md) e i rispettivi prerequisiti.

## <a name="explore-and-prepare-the-data"></a>Esplorare e preparare i dati

Per poter usare i dati in Python, sarà necessario caricare i dati dal database SQL Server in un frame di dati pandas.

Creare un nuovo notebook Python in Azure Data Studio ed eseguire lo script seguente. Sostituire `<SQL Server>` con il nome dell'istanza personale di SQL Server.

Lo script Python seguente consente di importare il set di dati dalla tabella **dbo.rental_data** del database in un frame di dati pandas **df**.

Nella stringa di connessione sostituire i dettagli della connessione in base alle esigenze.

```python
import pyodbc
import pandas
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Connection string to your SQL Server instance
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=localhost; DATABASE=TutorialDB; Trusted_Connection=yes')

query_str = 'SELECT Year, Month, Day, Rentalcount, Weekday, Holiday, Snow FROM dbo.rental_data'

df = pandas.read_sql(sql=query_str, con=conn_str)

print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

I risultati visualizzati saranno simili ai seguenti:

```results
Data frame:      Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
0    2014      1   20          445        2        1     0
1    2014      2   13           40        5        0     0
2    2013      3   10          456        1        0     0
3    2014      3   31           38        2        0     0
4    2014      4   24           23        5        0     0
..    ...    ...  ...          ...      ...      ...   ...
448  2013      2   19           57        3        0     1
449  2015      3   18           26        4        0     0
450  2015      3   24           29        3        0     1
451  2014      3   26           50        4        0     1
452  2015     12    6          377        1        0     1

[453 rows x 7 columns]
```

## <a name="next-steps"></a>Passaggi successivi

Nella seconda parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Caricare i dati dal database SQL Server in un frame di dati **pandas**
* Preparare i dati in Python rimuovendo alcune colonne

Per eseguire il training di un modello di Machine Learning che usa i dati del database TutorialDB, seguire la terza parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione su Python: Eseguire il training di un modello di regressione lineare](python-ski-rental-linear-regression-train-model.md)