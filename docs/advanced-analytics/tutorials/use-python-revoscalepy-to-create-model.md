---
title: Usare Python con revoscalepy per creare un modello
description: Scrivere script Python usando le funzioni revoscalepy per creare modelli di data science eseguiti in modalità remota in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 596e5f6b5145dc258c781ca7b88a69fc962d7021
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714717"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Usare Python con revoscalepy per creare un modello che viene eseguito in modalità remota su SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La libreria Python di [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) di Microsoft fornisce Data Science algoritmi per l'esplorazione, la visualizzazione, le trasformazioni e l'analisi dei dati. Questa libreria ha una priorità strategica negli scenari di integrazione con Python in SQL Server. In un server multicore, le funzioni **revoscalepy** possono essere eseguite in parallelo. In un'architettura distribuita con un server centrale e workstation client (computer fisici distinti, tutti con la stessa libreria **revoscalepy** ), è possibile scrivere codice Python che viene avviato localmente, ma sposta l'esecuzione a un'istanza di SQL Server remota dove si trovano i dati.

È possibile trovare **revoscalepy** nei prodotti e nelle distribuzioni Microsoft seguenti:

+ [SQL Server Machine Learning Services (in-database)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (non SQL, server autonomo)](https://docs.microsoft.com/machine-learning-server/index)
+ [Librerie Python sul lato client (per workstation di sviluppo)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

Questo esercizio illustra come creare un modello di regressione lineare basato su [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), uno degli algoritmi in **revoscalepy** che accetta il contesto di calcolo come input. Il codice che verrà eseguito in questo esercizio sposta l'esecuzione del codice da un ambiente di elaborazione locale a quello remoto, abilitato dalle funzioni **revoscalepy** che abilitano un contesto di calcolo remoto.

Completando questa esercitazione, si apprenderà come:

> [!div class="checklist"]
> * Usare **revoscalepy** per creare un modello lineare
> * Operazioni di spostamento dal contesto di calcolo locale a quello remoto

## <a name="prerequisites"></a>Prerequisiti

I dati di esempio usati in questo esercizio sono il database [**FlightData**](demo-data-airlinedemo-in-sql.md) .

È necessario un IDE per eseguire il codice di esempio in questo articolo e l'IDE deve essere collegato al file eseguibile di Python.

Per eseguire un cambio di contesto di calcolo, è necessario disporre di una [workstation locale](../python/setup-python-client-tools-sql.md) e di un'istanza del motore di database SQL Server con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) e Python abilitati. 

> [!Tip]
> Se non si dispone di due computer, è possibile simulare un contesto di calcolo remoto in un computer fisico installando le applicazioni pertinenti. In primo luogo, un'installazione di [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) funge da istanza "remota". In secondo luogo, un'installazione delle [librerie client Python funziona](../python/setup-python-client-tools-sql.md) come client. Si disporrà di due copie della stessa distribuzione di Python e delle librerie Microsoft Python nello stesso computer. Sarà necessario tenere traccia dei percorsi di file e della copia di Python. exe utilizzata per completare correttamente l'esercizio.

## <a name="remote-compute-contexts-and-revoscalepy"></a>Contesti di calcolo remoti e revoscalepy

Questo esempio illustra il processo di creazione di un modello Python in un contesto di calcolo remoto, che consente di lavorare da un client, ma scegliere un ambiente remoto, ad esempio SQL Server, Spark o Machine Learning Server, in cui vengono effettivamente eseguite le operazioni. L'obiettivo del contesto di calcolo remoto è quello di portare i calcoli in cui risiedono i dati.

Per eseguire il codice Python in SQL Server richiede il pacchetto **revoscalepy** . Si tratta di un pacchetto python speciale fornito da Microsoft, simile al pacchetto **RevoScaleR** per il linguaggio R. Il pacchetto **revoscalepy** supporta la creazione di contesti di calcolo e fornisce l'infrastruttura per il passaggio di dati e modelli tra una workstation locale e un server remoto. La funzione **revoscalepy** che supporta l'esecuzione di codice nel database è [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

In questa lezione vengono usati i dati in SQL Server per eseguire il training di un modello lineare basato su [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), una funzione in **revoscalepy** che supporta la regressione su set di dati di grandi dimensioni. 

Questa lezione illustra anche le nozioni di base per la configurazione e quindi l'uso di un **SQL Server contesto di calcolo** in Python. Per informazioni sul funzionamento dei contesti di calcolo con altre piattaforme e sui contesti di calcolo supportati, vedere [contesto di calcolo per l'esecuzione di script in Machine Learning server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).


## <a name="run-the-sample-code"></a>Eseguire il codice di esempio

Dopo aver preparato il database e avere i dati per il training archiviati in una tabella, aprire un ambiente di sviluppo Python ed eseguire l'esempio di codice.

Il codice esegue i passaggi seguenti:

1. Importa le librerie e le funzioni richieste.
2. Crea una connessione a SQL Server. Crea oggetti **origine dati** per l'utilizzo dei dati.
3. Modifica i dati utilizzando le trasformazioni in modo che possano essere utilizzati dall'algoritmo di regressione logistica.
4. Chiama `rx_lin_mod` e definisce la formula utilizzata per adattarsi al modello.
5. Genera un set di stime basate sui dati originali.
6. Crea un riepilogo basato sui valori stimati.

Tutte le operazioni vengono eseguite utilizzando un'istanza di SQL Server come contesto di calcolo.

> [!NOTE]
> Per una dimostrazione di questo esempio eseguito dalla riga di comando, vedere questo video: [SQL Server 2017 analisi avanzata con Python](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>Codice di esempio

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=sqlpy;Trusted_Connection=True;'
    print("connectionString={0!s}".format(sql_connection_string))

    data_source = RxSqlServerData(
        sql_query = "select top 10 * from airlinedemosmall",
        connection_string = sql_connection_string,

        column_info = {
            "ArrDelay" : { "type" : "integer" },
            "DayOfWeek" : {
                "type" : "factor",
                "levels" : [ "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" ]
            }
        })

    sql_compute_context = RxInSqlServer(
        connection_string = sql_connection_string,
        num_tasks = 4,
        auto_cleanup = False
        )

    #
    # Run linmod locally
    #
    linmod_local = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source)
    #
    # Run linmod remotely
    #
    linmod = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)

    # Predict results
    # 
    predict = rx_predict(linmod, data = rx_import(input_data = data_source))
    summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)
```

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>Definizione di un'origine dati rispetto alla definizione di un contesto di calcolo

Un'origine dati è diversa da un contesto di calcolo. L' *origine dati* definisce i dati utilizzati nel codice. Il contesto di calcolo definisce la posizione in cui verrà eseguito il codice. Tuttavia, usano alcune delle stesse informazioni:

+ Le variabili di Python, `sql_query` ad `sql_connection_string`esempio e, definiscono l'origine dei dati. 

    Passare queste variabili al costruttore [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) per implementare l' **oggetto origine dati** denominato `data_source`.

+ Per creare un **oggetto contesto di calcolo** , è possibile usare il costruttore [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) . L' **oggetto contesto di calcolo** risultante è denominato `sql_cc`.

    In questo esempio viene riutilizzata la stessa stringa di connessione utilizzata nell'origine dati, presupposto che i dati si trovino nella stessa istanza di SQL Server che verrà utilizzata come contesto di calcolo. 
    
    Tuttavia, l'origine dati e il contesto di calcolo potrebbero trovarsi in server diversi.
 
### <a name="changing-compute-contexts"></a>Modifica di contesti di calcolo

Dopo aver definito un contesto di calcolo, è necessario impostare il **contesto di calcolo attivo**. 

Per impostazione predefinita, la maggior parte delle operazioni viene eseguita localmente, il che significa che se non si specifica un contesto di calcolo diverso, i dati verranno recuperati dall'origine dati e il codice verrà eseguito nell'ambiente Python corrente.

Esistono due modi per impostare il contesto di calcolo attivo:
+ Come argomento di un metodo o di una funzione
+ Chiamando`rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Impostare il contesto di calcolo come argomento di un metodo o di una funzione

In questo esempio si imposta il contesto di calcolo usando un argomento della singola funzione **RX** .
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Questo contesto di calcolo viene riusato nella chiamata a [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Impostare un contesto di calcolo in modo esplicito tramite rx_set_compute_context

La funzione [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) consente di passare tra i contesti di calcolo già definiti.

Dopo aver impostato il contesto di calcolo attivo, rimane attivo fino a quando non viene modificato.

### <a name="using-parallel-processing-and-streaming"></a>Uso di elaborazione parallela e streaming

Quando si definisce il contesto di calcolo, è anche possibile impostare parametri che controllano il modo in cui i dati vengono gestiti dal contesto di calcolo. Questi parametri variano a seconda del tipo di origine dati.

Per SQL Server contesti di calcolo, è possibile impostare le dimensioni del batch o fornire suggerimenti sul grado di parallelismo da usare nelle attività in esecuzione.

+ L'esempio è stato eseguito in un computer con quattro processori, quindi `num_tasks` il parametro è impostato su 4 per consentire l'utilizzo massimo delle risorse. 
+ Se si imposta questo valore su 0, SQL Server utilizza l'impostazione predefinita, ovvero l'esecuzione di tutte le attività in parallelo, in base alle impostazioni MAXDOP correnti per il server. Tuttavia, il numero esatto di attività che possono essere allocate dipende da molti altri fattori, ad esempio le impostazioni del server e altri processi in esecuzione.

## <a name="next-steps"></a>Passaggi successivi

Questi esempi ed esercitazioni di Python aggiuntivi illustrano scenari end-to-end che usano origini dati più complesse, nonché l'uso di contesti di calcolo remoti.

+ [Python nel database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Creazione di un modello predittivo con Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
