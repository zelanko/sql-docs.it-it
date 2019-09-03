---
title: 'Esercitazione: Preparare i dati per eseguire il clustering in Python'
description: Nella seconda parte di questa serie di esercitazioni in quattro parti, si preparano i dati da un database di SQL Server per eseguire il clustering in Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a71d92023c76b7eafb25efba0bb13b1d1da1f695
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211965"
---
# <a name="tutorial-prepare-data-to-perform-clustering-in-python-with-sql-server-machine-learning-services"></a>Esercitazione: Preparare i dati per eseguire il clustering in Python con SQL Server Machine Learning Services

Nella seconda parte di questa serie di esercitazioni in quattro parti, verranno importati e preparati i dati da un database SQL tramite Python. Più avanti in questa serie questi dati verranno usati per eseguire il training e la distribuzione di un modello di clustering in Python con SQL Server Machine Learning Services.

L'articolo spiega come:

> [!div class="checklist"]
> * Separare i clienti con dimensioni diverse con Python
> * Caricare i dati dal database SQL in un frame di dati Python

Nella [prima parte](tutorial-python-clustering-model.md), sono stati installati i prerequisiti e il database di esempio è stato importato.

Nella [terza parte](tutorial-python-clustering-model-build.md)verrà illustrato come creare ed eseguire il training di un modello di clustering K-means in Python.

Nella [quarta parte](tutorial-python-clustering-model-deploy.md)verrà illustrato come creare un stored procedure in un database SQL in grado di eseguire il clustering in Python in base ai nuovi dati.

## <a name="prerequisites"></a>Prerequisiti

* Nella seconda parte di questa esercitazione si presuppone che siano stati soddisfatti i prerequisiti della [**parte 1**](tutorial-python-clustering-model.md).

## <a name="separate-customers"></a>Clienti distinti

Per preparare il clustering dei clienti, è necessario innanzitutto separare i clienti con le dimensioni seguenti:

* **orderRatio** = rapporto ordine restituito (numero totale di ordini parzialmente o completamente restituiti rispetto al numero totale di ordini)
* **itemsRatio** = restituzione elemento ratio (numero totale di elementi restituiti rispetto al numero di elementi acquistati)
* **monetaryRatio** = rapporto quantità restituzione (quantità monetaria totale di elementi restituiti rispetto alla quantità acquistata)
* **Frequency** = frequenza di ritorno

Aprire un nuovo notebook in Azure Data Studio e immettere lo script seguente.

Nella stringa di connessione sostituire i dettagli della connessione in base alle esigenze.

```python
# Load packages.
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import revoscalepy as revoscale
from scipy.spatial import distance as sci_distance
from sklearn import cluster as sk_cluster

################################################################################################

## Connect to DB and select data

################################################################################################

# Connection string to connect to SQL Server named instance.
conn_str = 'Driver=SQL Server;Server=localhost;Database=tpcxbb_1gb;Trusted_Connection=True;'

input_query = '''SELECT
ss_customer_sk AS customer,
ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) AS orderRatio,
ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) AS itemsRatio,
ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) AS monetaryRatio,
COALESCE(returns_count, 0) AS frequency
FROM
(
  SELECT
    ss_customer_sk,
    -- return order ratio
    COUNT(distinct(ss_ticket_number)) AS orders_count,
    -- return ss_item_sk ratio
    COUNT(ss_item_sk) AS orders_items,
    -- return monetary amount ratio
    SUM( ss_net_paid ) AS orders_money
  FROM store_sales s
  GROUP BY ss_customer_sk
) orders
LEFT OUTER JOIN
(
  SELECT
    sr_customer_sk,
    -- return order ratio
    count(distinct(sr_ticket_number)) as returns_count,
    -- return ss_item_sk ratio
    COUNT(sr_item_sk) as returns_items,
    -- return monetary amount ratio
    SUM( sr_return_amt ) AS returns_money
FROM store_returns
GROUP BY sr_customer_sk ) returned ON ss_customer_sk=sr_customer_sk'''


# Define the columns we wish to import.
column_info = {
    "customer": {"type": "integer"},
    "orderRatio": {"type": "integer"},
    "itemsRatio": {"type": "integer"},
    "frequency": {"type": "integer"}
}
```

## <a name="load-the-data-into-a-data-frame"></a>Caricare i dati in un frame di dati

I risultati della query vengono restituiti a Python usando la funzione revoscalepy **RxSqlServerData** . Come parte del processo, verranno usate le informazioni sulle colonne definite nello script precedente.

```python
data_source = revoscale.RxSqlServerData(sql_query=input_query, column_Info=column_info,
                                        connection_string=conn_str)
revoscale.RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)
# import data source and convert to pandas dataframe.
customer_data = pd.DataFrame(revoscale.rx_import(data_source))
```

A questo punto, visualizzare l'inizio del frame di dati per verificarne l'aspetto corretto.

```python
print("Data frame:", customer_data.head(n=5))
```

```results
Rows Read: 37336, Total Rows Processed: 37336, Total Chunk Time: 0.172 seconds
Data frame:     customer  orderRatio  itemsRatio  monetaryRatio  frequency
0    29727.0    0.000000    0.000000       0.000000          0
1    97643.0    0.068182    0.078176       0.037034          3
2    57247.0    0.000000    0.000000       0.000000          0
3    32549.0    0.086957    0.068657       0.031281          4
4     2040.0    0.000000    0.000000       0.000000          0
```

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si intende continuare con questa esercitazione, eliminare il database tpcxbb_1gb da SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Nella seconda parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Separare i clienti con dimensioni diverse con Python
* Caricare i dati dal database SQL in un frame di dati Python

Per creare un modello di Machine Learning che usa i dati dei clienti, seguire la terza parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione: Creare un modello predittivo in Python con SQL Server Machine Learning Services](tutorial-python-clustering-model-build.md)
