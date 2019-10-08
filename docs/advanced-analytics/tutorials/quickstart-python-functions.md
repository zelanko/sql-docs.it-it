---
title: Scrivere funzioni avanzate di Python
titleSuffix: SQL Server Machine Learning Services
description: Questa Guida introduttiva illustra come scrivere una funzione Python per un calcolo statistico avanzato con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e369e83c99543cc31287932a25949c2ddec98e89
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007721"
---
# <a name="quickstart-write-advanced-python-functions-with-sql-server-machine-learning-services"></a>Avvio rapido: Scrivere funzioni Python avanzate con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa Guida introduttiva descrive come incorporare funzioni matematiche e di utilità Python in un stored procedure SQL con SQL Server Machine Learning Services. Le funzioni statistiche avanzate complesse da implementare in T-SQL possono essere eseguite in Python con una sola riga di codice.

## <a name="prerequisites"></a>Prerequisiti

- Questa Guida introduttiva richiede l'accesso a un'istanza di SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con il linguaggio Python installato.

  L'istanza di SQL Server può trovarsi in una macchina virtuale di Azure o in locale. È sufficiente tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, pertanto potrebbe essere necessario abilitare l'esecuzione di [script esterni](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che **launchpad di SQL Server servizio** sia in esecuzione prima di iniziare.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script Python. È possibile eseguire questi script utilizzando qualsiasi strumento di gestione del database o query, purché sia possibile connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o stored procedure. Questa Guida introduttiva usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Creare una stored procedure per generare numeri casuali

Per semplicità, viene usato il pacchetto python `numpy`, che viene installato e caricato per impostazione predefinita in SQL Server Machine Learning Services con Python installato. Il pacchetto contiene centinaia di funzioni per le attività statistiche comuni, tra cui la funzione `random.normal`, che genera una quantità specificata di numeri casuali usando la distribuzione normale, in base a una deviazione e a una media standard.

Ad esempio, il codice Python seguente restituisce 100 numeri su una media di 50, data una deviazione standard di 3.

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

Per chiamare questa riga di Python da T-SQL, aggiungere la funzione Python nel parametro di script Python di `sp_execute_external_script`. L'output prevede un frame di dati, quindi usare `pandas` per convertirlo.

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

Questa operazione è facile se combinata con SQL Server. Definire un stored procedure che ottiene gli argomenti dall'utente, quindi passarli nello script Python come variabili.

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

- Le linee che seguono immediatamente eseguono il mapping dei nomi dei parametri SQL ai nomi delle variabili Python corrispondenti.

Ora che è stato eseguito il wrapper della funzione Python in una stored procedure, è possibile chiamare facilmente la funzione e passare valori diversi, come indicato di seguito:

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>Usare le funzioni di utilità Python per la risoluzione dei problemi

I pacchetti Python forniscono un'ampia gamma di funzioni di utilità per l'analisi dell'ambiente Python corrente. Queste funzioni possono essere utili se si trovano discrepanze nel modo in cui il codice Python viene eseguito in SQL Server e in ambienti esterni.

Ad esempio, è possibile usare le funzioni di temporizzazione del sistema nel pacchetto `time` per misurare la quantità di tempo usata dai processi Python e analizzare i problemi di prestazioni.

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

Per creare un modello di Machine Learning con Python in SQL Server, seguire questa Guida introduttiva:

> [!div class="nextstepaction"]
> [Avvio rapido: Creare e assegnare un punteggio a un modello predittivo in Python con SQL Server Machine Learning Services @ no__t-0

Per ulteriori informazioni su SQL Server Machine Learning Services, vedere:

- [Che cos'è SQL Server Machine Learning Services (Python e R)?](../what-is-sql-server-machine-learning.md)
