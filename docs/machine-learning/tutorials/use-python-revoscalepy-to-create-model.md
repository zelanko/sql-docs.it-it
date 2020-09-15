---
title: Creare un modello Python - revoscalepy
description: Scrivere script Python usando le funzioni revoscalepy per creare modelli di data science eseguiti in remoto in SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5f5cebd0fa6f45530ea5853cf365ea60a4c535ad
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179710"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Usare Python con revoscalepy per creare un modello che viene eseguito in remoto in SQL Server
[!INCLUDE [SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

La libreria Python [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) fornita da Microsoft contiene algoritmi di data science per l'esplorazione, la visualizzazione, la trasformazione e l'analisi dei dati. Questa libreria ha un'importanza strategica negli scenari di integrazione di Python in SQL Server. In un server multicore, le funzioni **revoscalepy** possono essere eseguite in parallelo. In un'architettura distribuita con un server centrale e workstation client (computer fisici distinti, tutti con la stessa libreria **revoscalepy**), è possibile scrivere codice Python che viene avviato in locale, ma poi sposta l'esecuzione in un'istanza di SQL Server remota in cui risiedono i dati.

È possibile trovare **revoscalepy** nei prodotti e nelle distribuzioni Microsoft seguenti:

+ [Machine Learning Services per SQL Server (In-Database)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (server autonomo non SQL)](https://docs.microsoft.com/machine-learning-server/index)
+ [Librerie Python lato client (per workstation di sviluppo)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

Questo esercizio illustra come creare un modello di regressione lineare basato su [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), uno degli algoritmi in **revoscalepy** che accetta come input il contesto di calcolo. Il codice che si eseguirà in questo esercizio sposta l'esecuzione del codice da un ambiente di elaborazione locale a uno remoto, con l'ausilio di funzioni **revoscalepy** che abilitano un contesto di calcolo remoto.

In questa esercitazione verranno illustrate le procedure per:

> [!div class="checklist"]
> * Usare **revoscalepy** per creare un modello lineare
> * Spostare le operazioni dal contesto di calcolo locale a un contesto remoto

## <a name="prerequisites"></a>Prerequisiti

In questo esercizio vengono usati i dati di esempio del database [**flightdata**](demo-data-airlinedemo-in-sql.md).

Per eseguire il codice di esempio in questo articolo è necessario un IDE collegato all'eseguibile Python.

Per provare eseguire uno spostamento del contesto di calcolo sono necessari una [workstation locale](../python/setup-python-client-tools-sql.md) e un'istanza del motore di database di SQL Server con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) e Python abilitati. 

> [!Tip]
> Se non si dispone di due computer, è possibile simulare un contesto di calcolo remoto in un computer fisico installando le applicazioni pertinenti. Prima di tutto, un'installazione di [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) che funge da istanza "remota". In secondo luogo, un'installazione delle [librerie client Python](../python/setup-python-client-tools-sql.md) che funge da client. Si avranno due copie della stessa distribuzione di Python e delle librerie Microsoft Python nello stesso computer. Per completare correttamente l'esercizio sarà necessario tenere traccia dei percorsi dei file e della copia di Python.exe utilizzata.

## <a name="remote-compute-contexts-and-revoscalepy"></a>Contesti di calcolo remoti e revoscalepy

Questo esempio illustra il processo di creazione di un modello Python in un contesto di calcolo remoto, che consente di lavorare da un client scegliendo però un ambiente remoto, ad esempio SQL Server, Spark o Machine Learning Server, in cui eseguire effettivamente le operazioni. L'obiettivo del contesto di calcolo remoto è quello di spostare i calcoli nella posizione in cui risiedono i dati.

Per eseguire codice Python in SQL Server è necessario il pacchetto **revoscalepy**. Si tratta di un pacchetto Python speciale fornito da Microsoft, simile al pacchetto **RevoScaleR** per il linguaggio R. Il pacchetto **revoscalepy** supporta la creazione di contesti di calcolo e fornisce l'infrastruttura per il passaggio di dati e modelli tra una workstation locale e un server remoto. La funzione **revoscalepy** che supporta l'esecuzione di codice nel database è [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

In questa lezione si usano i dati in SQL Server per eseguire il training di un modello lineare basato su [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), una funzione in **revoscalepy** che supporta la regressione su set di dati di grandi dimensioni. 

La lezione illustra anche i concetti di base per la configurazione e l'uso di un **contesto di calcolo di SQL Server** in Python. Per informazioni sul funzionamento dei contesti di calcolo con altre piattaforme e sui contesti di calcolo supportati, vedere [Contesto di calcolo per l'esecuzione di script in Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).


## <a name="run-the-sample-code"></a>Eseguire il codice di esempio

Dopo aver preparato il database e aver archiviato i dati per il training in una tabella, aprire un ambiente di sviluppo Python ed eseguire l'esempio di codice.

Il codice esegue i passaggi seguenti:

1. Importa le librerie e le funzioni necessarie.
2. Crea una connessione a SQL Server. Crea oggetti **origine dati** per l'utilizzo dei dati.
3. Modifica i dati usando **trasformazioni** in modo che possano essere usati dall'algoritmo di regressione logistica.
4. Chiama `rx_lin_mod` e definisce la formula usata per adattare il modello.
5. Genera un set di stime basate sui dati originali.
6. Crea un riepilogo basato sui valori stimati.

Tutte le operazioni vengono eseguite usando un'istanza di SQL Server come contesto di calcolo.

> [!NOTE]
> Per una dimostrazione dei questo esempio eseguito dalla riga di comando, vedere questo video: [SQL Server 2017 Advanced Analytics with Python](https://www.youtube.com/watch?v=FcoY795jTcc) (SQL Server 2017 - Analisi avanzata con Python)

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

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>Differenza tra definizione di un'origine dati e definizione di un contesto di calcolo

Un'origine dati è diversa da un contesto di calcolo. L'*origine dati* definisce i dati usati nel codice. Il contesto di calcolo definisce la posizione in cui verrà eseguito il codice. Tuttavia, alcune delle informazioni usate sono le stesse:

+ Le variabili Python, ad esempio `sql_query` e `sql_connection_string`, definiscono l'origine dei dati. 

    Passare queste variabili al costruttore [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) per implementare l'**oggetto origine dati** denominato `data_source`.

+ Si crea un **oggetto contesto di calcolo** usando il costruttore [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver). L'**oggetto contesto di calcolo** risultante è denominato `sql_cc`.

    In questo esempio viene riutilizzata la stessa stringa di connessione usata nell'origine dati, con il presupposto che i dati si trovino nella stessa istanza di SQL Server che si userà come contesto di calcolo. 
    
    Tuttavia, l'origine dati e il contesto di calcolo potrebbero trovarsi in server diversi.
 
### <a name="changing-compute-contexts"></a>Modifica del contesto di calcolo

Dopo aver definito un contesto di calcolo, è necessario impostare il **contesto di calcolo attivo**. 

Per impostazione predefinita, la maggior parte delle operazioni viene eseguita localmente, il che significa che se non si specifica un contesto di calcolo diverso, i dati verranno recuperati dall'origine dati e il codice verrà eseguito nell'ambiente Python corrente.

Si può impostare il contesto di calcolo attivo in due modi:
+ Come argomento di un metodo o di una funzione
+ Chiamando `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Impostare il contesto di calcolo come argomento di un metodo o di una funzione

In questo esempio si imposta il contesto di calcolo usando un argomento della funzione **rx**.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Questo contesto di calcolo viene riutilizzato nella chiamata a [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rx_set_compute_context"></a>Impostare un contesto di calcolo in modo esplicito usando rx_set_compute_context

La funzione [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) consente di passare tra contesti di calcolo già definiti.

Una volta specificato, il contesto di calcolo resta attivo fino a quando non lo si modifica.

### <a name="using-parallel-processing-and-streaming"></a>Uso di elaborazione parallela e streaming

Quando si definisce il contesto di calcolo, è anche possibile impostare parametri che controllano il modo in cui il contesto di calcolo gestisce i dati. Questi parametri variano in base al tipo di origine dati.

Per i contesti di calcolo di SQL Server, è possibile impostare le dimensioni dei batch o fornire suggerimenti sul grado di parallelismo da usare nelle attività in esecuzione.

+ L'esempio è stato eseguito in un computer con quattro processori, quindi il parametro `num_tasks` è impostato su 4 per consentire l'utilizzo massimo delle risorse. 
+ Se si imposta questo valore su 0, SQL Server usa l'impostazione predefinita, ovvero l'esecuzione parallela del massimo numero possibile di attività, in base alle impostazioni MAXDOP correnti per il server. Tuttavia, il numero esatto di attività che potrebbero essere allocate dipende da molti altri fattori, ad esempio le impostazioni del server e gli altri processi in esecuzione.

## <a name="next-steps"></a>Passaggi successivi

Gli esempi e le esercitazioni su Python seguenti illustrano scenari end-to-end con l'uso di origini dati più complesse, nonché l'uso di contesti di calcolo remoti.

+ [Python nel database per sviluppatori SQL](python-taxi-classification-introduction.md)
+ [Creare un modello predittivo usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
