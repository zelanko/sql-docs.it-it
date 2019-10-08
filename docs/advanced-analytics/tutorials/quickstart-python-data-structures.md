---
title: Usare i tipi di dati e gli oggetti di Python e SQL
titleSuffix: SQL Server Machine Learning Services
description: Questa Guida introduttiva illustra come usare i tipi di dati e gli oggetti dati in Python e SQL Server con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c09c9ad4625520054f2d3f103ec055c37764aed2
ms.sourcegitcommit: 84e6922a57845a629391067ca4803e8d03e0ab90
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2019
ms.locfileid: "72008425"
---
# <a name="quickstart-handle-data-types-and-objects-using-python-in-sql-server-machine-learning-services"></a>Avvio rapido: Gestire tipi di dati e oggetti usando Python in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa Guida introduttiva illustra come usare le strutture di dati quando si usa Python in SQL Server Machine Learning Services.

SQL Server si basa sul pacchetto **Pandas** di Python, ideale per l'utilizzo di dati tabulari. Tuttavia, non è possibile passare un valore scalare da Python a SQL Server e aspettarsi che sia "semplicemente funzionante". In questa Guida introduttiva verranno esaminate alcune definizioni dei tipi di dati di base per preparare eventuali problemi aggiuntivi che possono verificarsi durante il passaggio di dati tabulari tra Python e SQL Server.

I concetti di cui tenere conto prima includono:

- Un frame di dati è una tabella con _più_ colonne.
- Una singola colonna di un frame di dati è un oggetto simile a un elenco denominato serie.
- Un singolo valore di un frame di dati viene chiamato cella ed è accessibile in base all'indice.

Come è possibile esporre il singolo risultato di un calcolo come frame di dati, se un frame di dati richiede una struttura tabulare? Una risposta consiste nel rappresentare il singolo valore scalare come una serie, che è facilmente convertibile in un frame di dati. 

> [!NOTE]
> Quando si restituiscono date, Python in SQL utilizza DATETIME con un intervallo di date limitato di 1753-01-01 (-53690) a 9999-12-31 (2958463). 

## <a name="prerequisites"></a>Prerequisiti

- Questa Guida introduttiva richiede l'accesso a un'istanza di SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con il linguaggio Python installato.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script Python. È possibile eseguire questi script utilizzando qualsiasi strumento di gestione del database o query, purché sia possibile connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o stored procedure. Questa Guida introduttiva usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="scalar-value-as-a-series"></a>Valore scalare sotto forma di serie

Questo esempio esegue alcune operazioni matematiche semplici e converte un valore scalare in una serie.

1. Una serie richiede un indice, che è possibile assegnare manualmente, come illustrato di seguito, o a livello di codice.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   print(c)
   s = pandas.Series(c, index =["simple math example 1"])
   print(s)
   '
   ```

   Poiché la serie non è stata convertita in un frame di dati, i valori vengono restituiti nella finestra messaggi, ma è possibile vedere che i risultati sono in un formato tabulare.

   **Risultati**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. Per aumentare la lunghezza della serie, è possibile aggiungere nuovi valori usando una matrice. 

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   '
   ```

   Se non si specifica un indice, viene generato un indice con valori che iniziano con 0 e che terminano con la lunghezza della matrice.

   **Risultati**

   ```text
   STDOUT message(s) from external script: 
   0    0.5
   1    2.0
   dtype: float64
   ```

1. Se si aumenta il numero di valori di **Indice** , ma non si aggiungono nuovi valori di **dati** , i valori dei dati vengono ripetuti per riempire la serie.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   '
   ```

   **Risultati**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   simple math example 2    0.5
   dtype: float64
   ```

## <a name="convert-series-to-data-frame"></a>Converti serie in frame di dati

Dopo aver convertito i risultati matematici scalari in una struttura tabulare, è comunque necessario convertirli in un formato che possa essere gestito da SQL Server.

1. Per convertire una serie in un frame di dati, chiamare il metodo Pandas [dataframe](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) .

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s)
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   Il risultato è illustrato di seguito. Anche se si usa l'indice per ottenere valori specifici dal data. frame, i valori dell'indice non fanno parte dell'output.

   **Risultati**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>Valori di output in data. frame

Verranno ora restituiti valori specifici di due serie di risultati matematici in un data. frame. Il primo ha un indice di valori sequenziali generati da Python. Il secondo usa un indice arbitrario di valori stringa.

1. Nell'esempio seguente viene ottenuto un valore dalla serie utilizzando un indice Integer.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s, index=[1])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **Risultati**

   |ResultValue|
   |------|
   |2.0|

   Tenere presente che l'indice generato automaticamente inizia da 0. Provare a usare un valore di indice non compreso nell'intervallo per vedere cosa accade.

1. Ottenere ora un singolo valore dall'altro frame di dati usando un indice di stringa.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   df = pd.DataFrame(s, index=["simple math example 1"])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **Risultati**

   |ResultValue|
   |------|
   |0.5|

   Se si tenta di usare un indice numerico per ottenere un valore da questa serie, viene ricevuto un errore.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni sulla scrittura di funzioni Python avanzate in SQL Server, seguire questa Guida introduttiva:

> [!div class="nextstepaction"]
> [Scrivere funzioni Python avanzate con SQL Server Machine Learning Services](quickstart-python-functions.md)

Per altre informazioni sull'uso di Python in SQL Server Machine Learning Services, vedere gli articoli seguenti:

- [Creare e assegnare punteggi a un modello predittivo in Python](quickstart-python-train-score-model.md)
- [Che cos'è SQL Server Machine Learning Services (Python e R)?](../what-is-sql-server-machine-learning.md)
