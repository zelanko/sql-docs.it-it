---
title: Guida introduttiva per l'uso di strutture di dati in Python
description: In questa Guida introduttiva per script Python in SQL Server, informazioni su come usare le strutture di dati con il sistema sp_execute_external_script stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 13fb37bee355ce1d379d8348734293baaeb481d8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714804"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>Avvio rapido: Strutture di dati Python in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa Guida introduttiva illustra come usare le strutture di dati quando si usa Python in SQL Server Machine Learning Services.

SQL Server si basa sul pacchetto **Pandas** di Python, ideale per l'utilizzo di dati tabulari. Tuttavia, non è possibile passare un valore scalare da Python a SQL Server e aspettarsi che sia "semplicemente funzionante". In questa Guida introduttiva verranno esaminate alcune definizioni dei tipi di dati di base per preparare l'utente in caso di problemi aggiuntivi che potrebbero verificarsi durante il passaggio di dati tabulari tra Python e SQL Server.

+ Un frame di dati è una tabella con _più_ colonne.
+ Una singola colonna di un dataframe è un oggetto simile a un elenco denominato serie.
+ Un singolo valore è una cella di un frame di dati e deve essere chiamato da index.

Come è possibile esporre il singolo risultato di un calcolo come frame di dati, se un frame di dati richiede una struttura tabulare? Una risposta consiste nel rappresentare il singolo valore scalare come una serie, che è facilmente convertibile in un frame di dati. 

## <a name="prerequisites"></a>Prerequisiti

Una guida introduttiva precedente, [Verify Python exists in SQL Server](quickstart-python-verify.md), fornisce informazioni e collegamenti per la configurazione dell'ambiente Python necessario per questa Guida introduttiva.

## <a name="scalar-value-as-a-series"></a>Valore scalare sotto forma di serie

Questo esempio esegue alcune operazioni matematiche semplici e converte un valore scalare in una serie.

1. Una serie richiede un indice, che è possibile assegnare manualmente, come illustrato di seguito, o a livello di codice.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    s = pandas.Series(c, index =["simple math example 1"])
    print(s)
    '
    ```

2. Poiché la serie non è stata convertita in un frame di dati, i valori vengono restituiti nella finestra messaggi, ma è possibile vedere che i risultati sono in un formato tabulare.

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Per aumentare la lunghezza della serie, è possibile aggiungere nuovi valori usando una matrice. 

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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

4. Se si aumenta il numero di valori di **Indice** , ma non si aggiungono nuovi valori di **dati** , i valori dei dati vengono ripetuti per riempire la serie.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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

1. Per convertire una serie in un frame di dati, chiamare il metodo Pandas [dataframe](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe).

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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
    WITH RESULT SETS (( ResultValue float ))
    ```

2. Il risultato è illustrato di seguito. Anche se si usa l'indice per ottenere valori specifici dal data. frame, i valori dell'indice non fanno parte dell'output.

    **Risultati**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>Valori di output in data. frame

Viene ora illustrato in che modo la conversione in un data. frame funziona con le due serie contenenti i risultati delle semplici operazioni matematiche. Il primo ha un indice di valori sequenziali generati da Python. Il secondo usa un indice arbitrario di valori stringa.

1. Questo esempio Mostra come ottenere un valore dalla serie che usa un indice Integer.

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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
    WITH RESULT SETS (( ResultValue float ))
    ```

    Tenere presente che l'indice generato automaticamente inizia da 0. Provare a usare un valore di indice non compreso nell'intervallo per vedere cosa accade.

2. A questo punto, è possibile ottenere un singolo valore dall'altro frame di dati con un indice di stringa. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    **Risultati**

    |ResultValue|
    |------|
    |0.5|

    Se si tenta di usare un indice numerico per ottenere un valore da questa serie, viene ricevuto un errore.

## <a name="next-steps"></a>Passaggi successivi

Successivamente, si creerà un modello predittivo usando Python in SQL Server.

> [!div class="nextstepaction"]
> [Creare, eseguire il training e usare un modello Python con stored procedure in SQL Server](quickstart-python-train-score-in-tsql.md)