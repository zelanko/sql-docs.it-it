---
title: 'Guida introduttiva: Strutture dei dati di Python'
description: Questo argomento di avvio rapido illustra come usare le strutture di dati e gli oggetti dati in Python e Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3023287504cbb7b25e194b53d0957e82405d1ea8
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606693"
---
# <a name="quickstart-data-structures-and-objects-using-python-in-sql-server-machine-learning-services"></a>Guida introduttiva: Strutture di dati e oggetti quando si usa Python in Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Questo argomento di avvio rapido descrive come usare le strutture di dati e i tipi di dati quando si usa Python in [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md) oppure in [cluster Big Data](../../big-data-cluster/machine-learning-services.md). Si apprenderà come trasferire i dati tra Python e SQL Server e verranno illustrati i problemi comuni che potrebbero verificarsi.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Questo argomento di avvio rapido descrive come usare le strutture di dati e i tipi di dati quando si usa Python in [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md). Si apprenderà come trasferire i dati tra Python e SQL Server e verranno illustrati i problemi comuni che potrebbero verificarsi.
::: moniker-end

SQL Server si basa sul pacchetto Python **pandas**, ideale per lavorare con dati tabulari. Tuttavia, non si può passare un valore scalare da Python a SQL Server e aspettarsi semplicemente che funzioni. In questo argomento di avvio rapido verranno esaminate alcune definizioni di base delle strutture di dati prepararsi per eventuali problemi aggiuntivi che possono verificarsi durante il passaggio di dati tabulari tra Python e SQL Server.

Ecco alcuni concetti da tenere in considerazione:

- Un frame di dati è una tabella con _più colonne_.
- Una singola colonna di un frame di dati è un oggetto simile a un elenco denominato serie.
- Un singolo valore di un frame di dati è detto cella ed è accessibile in base all'indice.

Come si può esporre il singolo risultato di un calcolo come frame di dati, se un frame di dati richiede una struttura tabulare? Una risposta consiste nel rappresentare il singolo valore scalare come una serie, che è facilmente convertibile in un frame di dati. 

> [!NOTE]
> Per restituire date, Python in SQL usa DATETIME, che ha un intervallo di date limitato incluso tra 01-01-1753 (-53690) e 31-12-9999 (2958463). 

## <a name="prerequisites"></a>Prerequisiti

Per completare questo argomento di avvio rapido è necessario soddisfare i prerequisiti seguenti.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
- Machine Learning Services per SQL Server. Per informazioni su come installare Machine Learning Services, vedere la [guida all'installazione di Windows](../install/sql-machine-learning-services-windows-install.md) o la [guida all'installazione di Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json). È anche possibile [abilitare Machine Learning Services in cluster Big Data di SQL Server](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
- Machine Learning Services per SQL Server. Per informazioni su come installare Machine Learning Services, vedere la [guida all'installazione di Windows](../install/sql-machine-learning-services-windows-install.md). 
::: moniker-end
- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script Python. È possibile eseguire questi script usando qualsiasi strumento di gestione del database o di query, purché possa connettersi a un'istanza di SQL Server, nonché eseguire una query T-SQL o una stored procedure. In questo argomento di avvio rapido viene usato [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio).

## <a name="scalar-value-as-a-series"></a>Valore scalare come serie

Questo esempio esegue una semplice operazione matematica e converte un valore scalare in una serie.

1. Una serie richiede un indice, che può essere assegnato manualmente, come illustrato di seguito, o a livello di codice.

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

   Poiché la serie non è stata convertita in un frame di dati, i valori vengono restituiti nella finestra Messaggi, ma come si può vedere i risultati sono in un formato più tabulare.

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

   Se non si specifica un indice, ne viene generato uno con valori che iniziano con 0 e che terminano con la lunghezza della matrice.

   **Risultati**

   ```text
   STDOUT message(s) from external script: 
   0    0.5
   1    2.0
   dtype: float64
   ```

1. Se si aumenta il numero di valori di **Indice**, ma non si aggiungono nuovi valori di **dati**, i valori di dati vengono ripetuti per riempire la serie.

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

## <a name="convert-series-to-data-frame"></a>Convertire la serie in un frame di dati

Dopo aver convertito i risultati dell'operazione matematica sul valore scalare in una struttura tabulare, è comunque necessario convertirli in un formato che possa essere gestito da SQL Server.

1. Per convertire una serie in un frame di dati, chiamare il metodo pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe).

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

   Il risultato è illustrato di seguito. Anche se si usa l'indice per ottenere valori specifici dal frame di dati, i valori dell'indice non fanno parte dell'output.

   **Risultati**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>Restituire i valori in un frame di dati

Verranno ora restituiti valori specifici di due serie di risultati matematici in un frame di dati. La prima serie ha un indice di valori sequenziali generati da Python. La seconda usa un indice arbitrario di valori stringa.

1. L'esempio seguente ottiene un valore dalla serie usando un indice Integer.

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

   Tenere presente che l'indice generato automaticamente inizia da 0. Provare a usare un valore di indice non compreso nell'intervallo per vedere cosa succede.

1. Ottenere ora un singolo valore dall'altro frame di dati usando un indice stringa.

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

   Se si prova a usare un indice numerico per ottenere un valore da questa serie, si riceve un errore.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni sulla scrittura di funzioni Python avanzate in SQL Server, seguire questo argomento di avvio rapido:

> [!div class="nextstepaction"]
> [Scrivere funzioni Python avanzate con Machine Learning Services per SQL Server](quickstart-python-functions.md)

Per altre informazioni sull'uso di Python in Machine Learning Services per SQL Server, vedere gli articoli seguenti:

- [Creare e assegnare i punteggi a un modello predittivo in Python](quickstart-python-train-score-model.md)
- [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../sql-server-machine-learning-services.md)
