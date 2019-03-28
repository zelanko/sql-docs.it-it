---
title: 'Usare Python con revoscalepy per creare un modello: SQL Server Machine Learning'
description: Scrivere script Python usando revoscalepy funzioni per creare modelli di analisi scientifica dei dati che vengono eseguiti in modalità remota in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f0d9916414514e0ad0d73c3bb849b9c6e546289d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512453"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Usare Python con revoscalepy per creare un modello che viene eseguito in modalità remota in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Il [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) libreria Python di Microsoft fornisce gli algoritmi di analisi scientifica dei dati per l'esplorazione dei dati, visualizzazione, le trasformazioni e analisi. Questa libreria è di importanza strategica in scenari di integrazione di Python in SQL Server. In un server di multi-core **revoscalepy** funzioni eseguibili in parallelo. In un'architettura distribuita con una workstation client e server centrale (separare i computer fisici, tutti con lo stesso **revoscalepy** library), è possibile scrivere codice Python che avvia in locale, ma passa quindi l'esecuzione di un istanza remota di SQL Server in cui risiedono dati.

È possibile trovare **revoscalepy** nei seguenti prodotti Microsoft e le distribuzioni:

+ [SQL Server Machine Learning Services (in-database)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (non-SQL, server autonomo)](https://docs.microsoft.com/machine-learning-server/index)
+ [Librerie Python dal lato client (per le workstation di sviluppo)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

Questo esercizio viene illustrato come creare un modello di regressione lineare basato sul [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), uno degli algoritmi in **revoscalepy** che accetta il contesto di calcolo come input. Il codice che verrà eseguita in questo esercizio si sposta l'esecuzione di codice da una variabile locale all'ambiente di calcolo remoto, abilitata per **revoscalepy** contesto di calcolo di funzioni che consentono a un server remoto.

Completando questa esercitazione, si apprenderà come:

> [!div class="checklist"]
> * Uso **revoscalepy** per creare un modello lineare
> * Spostare le operazioni da locale al contesto di calcolo remoto

## <a name="prerequisites"></a>Prerequisiti

Dati di esempio usati in questo esercizio sono le [ **flightdata** ](demo-data-airlinedemo-in-sql.md) database.

È necessario un IDE per eseguire il codice di esempio in questo articolo, e l'IDE deve essere collegato a Python eseguibile.

Per provare un cambiamento di contesto di calcolo, è necessario un [workstation locale](../python/setup-python-client-tools-sql.md) e un'istanza del motore di database di SQL Server con [servizi di Machine Learning](../install/sql-machine-learning-services-windows-install.md) e Python abilitata. 

> [!Tip]
> Se non si dispone di due computer, è possibile simulare un contesto di calcolo remota in un computer fisico tramite l'installazione di applicazioni pertinenti. Per prima cosa, un'installazione di [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) funziona come l'istanza "remoto". In secondo luogo, un'installazione del [librerie client Python opera](../python/setup-python-client-tools-sql.md) del client. Si avranno due copie dei stessa distribuzione di Python e delle librerie di Python di Microsoft nello stesso computer. È necessario tenere traccia dei percorsi di file e quale copia del Python.exe si usa per completare correttamente l'esercizio.

## <a name="remote-compute-contexts-and-revoscalepy"></a>Contesti di calcolo remoti e revoscalepy

Questo esempio viene illustrato il processo di creazione di un modello Python in un contesto di calcolo remoto, che consente di lavorare da un client, ma scegliere un ambiente remoto, ad esempio SQL Server, Spark o Machine Learning Server, in cui le operazioni vengono effettivamente eseguite. L'obiettivo del contesto di calcolo remoto è portare calcolo da dove risiedono i dati.

Per eseguire il codice Python in SQL Server, è necessario il **revoscalepy** pacchetto. Si tratta di un pacchetto Python speciale fornito da Microsoft, simile al **RevoScaleR** pacchetto per il linguaggio R. Il **revoscalepy** pacchetto supporta la creazione di contesti di calcolo e fornisce l'infrastruttura per il trasferimento di dati e i modelli tra una workstation locale e un server remoto. Il **revoscalepy** funzione che supporta l'esecuzione di codice nel database viene [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

In questa lezione usare i dati in SQL Server per il training di un modello lineare basato su [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), una funzione in **revoscalepy** che supporta la regressione su set di dati molto grandi. 

In questa lezione illustra anche le nozioni di base di come configurare e quindi usare una **contesto di calcolo di SQL Server** in Python. Per informazioni su come usare contesti di calcolo con altre piattaforme e che i contesti di calcolo supportati, vedere [contesto di calcolo per l'esecuzione di script in Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).


## <a name="run-the-sample-code"></a>Eseguire il codice di esempio

Dopo aver preparato i database e avere i dati per il training, archiviato in una tabella, aprire un ambiente di sviluppo Python ed eseguire l'esempio di codice.

Il codice esegue i passaggi seguenti:

1. Consente di importare le librerie necessarie e le funzioni.
2. Crea una connessione a SQL Server. Consente di creare **zdroj dat** oggetti per l'uso con i dati.
3. Modifica dei dati mediante **trasformazioni** in modo che può essere utilizzato dall'algoritmo di regressione logistica.
4. Le chiamate `rx_lin_mod` e definisce la formula utilizzata per adattarlo al modello.
5. Genera un set di stime basate sui dati originali.
6. Crea un riepilogo in base ai valori stimati.

Tutte le operazioni vengono eseguite utilizzando un'istanza di SQL Server come contesto di calcolo.

> [!NOTE]
> Per una dimostrazione di questo esempio in esecuzione dalla riga di comando, vedere questo video: [SQL Server 2017 avanzate Analitica con Python](https://www.youtube.com/watch?v=FcoY795jTcc)

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

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>Definizione di un'origine dati e la definizione di un contesto di calcolo

Un'origine dati è diversa da un contesto di calcolo. Il *zdroj dat* definisce i dati usati nel codice. Consente di definire il contesto di calcolo in cui verrà eseguito il codice. Tuttavia, usano alcune delle stesse informazioni:

+ Le variabili di Python, ad esempio `sql_query` e `sql_connection_string`, definire l'origine dei dati. 

    Passare tali variabili per il [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) costruttore per implementare le **oggetto origine dati** denominato `data_source`.

+ Si crea una **oggetto contesto di calcolo** tramite il [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) costruttore. L'oggetto risultante **oggetto contesto di calcolo** denominata `sql_cc`.

    Questo esempio Usa nuovamente la stessa stringa di connessione utilizzata nell'origine dati, in base al presupposto che i dati sono nella stessa istanza di SQL Server che verrà utilizzato come contesto di calcolo. 
    
    Tuttavia, l'origine dati e il contesto di calcolo potrebbe essere in server diversi.
 
### <a name="changing-compute-contexts"></a>La modifica di contesti di calcolo

Dopo aver definito un contesto di calcolo, è necessario impostare il **contesto di calcolo attivo**. 

Per impostazione predefinita, la maggior parte delle operazioni vengono eseguite in locale, vale a dire che se non si specifica un contesto di calcolo diverse, verranno recuperati i dati dall'origine dati e il codice verrà eseguito nell'ambiente Python corrente.

Esistono due modi per impostare il contesto di calcolo attivo:
+ Come argomento di un metodo o funzione
+ Tramite la chiamata `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Impostare il contesto di calcolo come argomento di un metodo o funzione

In questo esempio, è impostato il contesto di calcolo usando un argomento dell'individuo **rx** (funzione).
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Questo contesto di calcolo viene riutilizzato nella chiamata a [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Impostare un contesto di calcolo in modo esplicito usando rx_set_compute_context

La funzione [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) consente di passare un contesto che è già stati definiti di calcolo.

Dopo aver impostato contesto di calcolo attive, rimane attivo fino alla successiva modifica.

### <a name="using-parallel-processing-and-streaming"></a>Tramite l'elaborazione parallela e streaming

Quando si definisce il contesto di calcolo, è anche possibile impostare i parametri che controllano la modalità di gestione dei dati per il contesto di calcolo. Questi parametri sono diversi a seconda del tipo di origine dati.

Per i contesti di calcolo di SQL Server, è possibile impostare le dimensioni del batch o fornire suggerimenti sul grado di parallelismo da utilizzare nell'esecuzione di attività.

+ L'esempio è stato eseguito in un computer con quattro processori, in modo che il `num_tasks` parametro è impostato su 4 per consentire l'utilizzo massimo delle risorse. 
+ Se si imposta questo valore su 0, SQL Server Usa l'impostazione predefinita, che consiste nell'eseguire qualsiasi numero di attività in parallelo possibili, in base alle impostazioni MAXDOP corrente per il server. Tuttavia, il numero esatto di attività che può essere allocata dipende molti altri fattori, ad esempio le impostazioni di server e altri processi in esecuzione.

## <a name="next-steps"></a>Passaggi successivi

Questi esempi Python ed esercitazioni aggiuntive illustrano scenari end-to-end usando origini dati più complesse, nonché l'uso di contesti di calcolo remoti.

+ [Python nel Database per sviluppatori SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Creare un modello predittivo usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
