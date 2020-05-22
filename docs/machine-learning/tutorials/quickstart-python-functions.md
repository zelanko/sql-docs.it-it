---
title: 'Guida introduttiva: Funzioni Python'
description: Questo argomento di avvio rapido descrive come usare funzioni matematiche e di utilità Python con Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/28/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6afe1685956c43e30ace59f3e5cc794a2abbd88f
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606705"
---
# <a name="quickstart-python-functions-with-sql-server-machine-learning-services"></a>Guida introduttiva: Funzioni Python con Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Questo argomento di avvio rapido descrive come usare funzioni matematiche e di utilità Python con [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md) o in [cluster Big Data](../../big-data-cluster/machine-learning-services.md). Le funzioni statistiche sono spesso complesse da implementare in T-SQL, ma possono essere eseguite in Python con poche righe di codice.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Questo argomento di avvio rapido descrive come usare funzioni matematiche e di utilità Python con [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md). Le funzioni statistiche sono spesso complesse da implementare in T-SQL, ma possono essere eseguite in Python con poche righe di codice.
::: moniker-end

## <a name="prerequisites"></a>Prerequisiti

- Questo argomento di avvio rapido richiede l'accesso a un'istanza di SQL Server con [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) con il linguaggio Python installato.

  L'istanza di SQL Server può essere in una macchina virtuale di Azure o in locale. Tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, quindi potrebbe essere necessario [abilitare lo scripting esterno](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che il **servizio Launchpad di SQL Server** sia in esecuzione prima di iniziare.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script Python. È possibile eseguire questi script usando qualsiasi strumento di gestione del database o di query, purché possa connettersi a un'istanza di SQL Server, nonché eseguire una query T-SQL o una stored procedure. In questo argomento di avvio rapido si usa [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Creare una stored procedure per generare numeri casuali

Per semplicità, usare il pacchetto Python `numpy`, che viene installato e caricato per impostazione predefinita in Machine Learning Services per SQL Server con Python installato. Il pacchetto contiene centinaia di funzioni per le attività statistiche comuni, tra cui la funzione `random.normal`, che genera una quantità specificata di numeri casuali usando la distribuzione normale, in base a una deviazione e a una media standard.

Ad esempio, il codice Python seguente restituisce 100 numeri, in una media di 50, in base alla deviazione standard 3.

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

Per chiamare questa riga di codice Python da T-SQL, aggiungere la funzione Python nel parametro di script Python di `sp_execute_external_script`. L'output prevede un frame di dati, che può essere convertito con `pandas`.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=100, loc=50, scale=3));
'
    , @input_data_1 = N'   ;'
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

Si vuole semplificare la generazione di un set diverso di numeri casuali?

Questa operazione è facile se eseguita in combinazione con SQL Server. Si definisce una stored procedure che ottiene gli argomenti dall'utente e quindi si passano tali argomenti nello script Python come variabili.

```sql
CREATE PROCEDURE MyPyNorm (
      @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=mynumbers, loc=mymean, scale=mysd));
'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- La prima riga definisce ognuno dei parametri di input SQL necessari quando viene eseguita la stored procedure.

- La riga che inizia con `@params` definisce tutte le variabili usate dal codice Python e i tipi di dati SQL corrispondenti.

- Le righe immediatamente successive eseguono il mapping dei nomi dei parametri SQL ai nomi delle variabili Python corrispondenti.

Dopo aver eseguito il wrapping della funzione Python in una stored procedure, è possibile chiamare facilmente la funzione e passare valori diversi, in questo modo:

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>Usare funzioni di utilità Python per la risoluzione dei problemi

I pacchetti Python forniscono un'ampia gamma di funzioni di utilità per l'analisi dell'ambiente Python corrente. Queste funzioni possono essere utili se si riscontrano discrepanze nell'esecuzione del codice Python in SQL Server e in ambienti esterni.

È possibile, ad esempio, usare le funzioni di calcolo del tempo di sistema disponibili nel pacchetto di `time` per misurare la quantità di tempo usata dai processi Python e analizzare i problemi di prestazioni.

```sql
EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
import time
start_time = time.time()

# Run Python processes

elapsed_time = time.time() - start_time
'
    , @input_data_1 = N' ;';
```

## <a name="next-steps"></a>Passaggi successivi

Per creare un modello di Machine Learning usando Python in SQL Server, seguire questo argomento di avvio rapido:

> [!div class="nextstepaction"]
> [Avvio rapido: Creare e assegnare un punteggio a un modello predittivo in Python con SQL Server Machine Learning Services](quickstart-python-train-score-model.md)

Per altre informazioni su Machine Learning Services per SQL Server, vedere:

- [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../sql-server-machine-learning-services.md)
