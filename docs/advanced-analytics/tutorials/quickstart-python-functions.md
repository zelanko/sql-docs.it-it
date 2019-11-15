---
title: 'Avvio rapido: Scrivere funzioni Python'
titleSuffix: SQL Server Machine Learning Services
description: Questo argomento di avvio rapido illustra come scrivere una funzione Python per il calcolo statistico avanzato con Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08f43c6406d0ca2c95cc21a207cae63af6e86902
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727005"
---
# <a name="quickstart-write-advanced-python-functions-with-sql-server-machine-learning-services"></a>Avvio rapido: Scrivere funzioni Python avanzate con Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo argomento di avvio rapido descrive come incorporate funzioni matematiche e di utilità Python in una stored procedure SQL con Machine Learning Services per SQL Server. Le funzioni statistiche avanzate complesse da implementare in T-SQL possono essere eseguite in Python con una singola riga di codice.

## <a name="prerequisites"></a>Prerequisites

- Questo argomento di avvio rapido richiede l'accesso a un'istanza di SQL Server con [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) con il linguaggio Python installato.

  L'istanza di SQL Server può essere in una macchina virtuale di Azure o in locale. Tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, quindi potrebbe essere necessario [abilitare lo scripting esterno](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che il **servizio Launchpad di SQL Server** sia in esecuzione prima di iniziare.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script Python. È possibile eseguire questi script usando qualsiasi strumento di gestione del database o di query, purché possa connettersi a un'istanza di SQL Server, nonché eseguire una query T-SQL o una stored procedure. In questo argomento di avvio rapido viene usato [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

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

- [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
