---
title: Guida introduttiva per l'utilizzo di strutture dei dati in Python - SQL Server Machine Learning
description: In questa Guida introduttiva per lo script di Python in SQL Server, informazioni su come usare le strutture di dati con le procedure di sistema archiviata sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ffbbd39c08221db4afa6427626ca618e04617166
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962086"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>Avvio rapido: Strutture di dati di Python in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questa Guida introduttiva illustra come usare le strutture di dati quando si usano Python in SQL Server Machine Learning Services.

SQL Server si basa su Python **pandas** pacchetto, che è ideale per l'utilizzo di dati tabulari. Tuttavia, è possibile passare un valore scalare da Python a SQL Server e aspettarsi che "funzionano". In questa Guida introduttiva, verranno esaminate alcune definizioni dei tipi di dati di base, per prepararti per altri problemi che possono verificarsi quando si passano dati tabulari tra codice Python e SQL Server.

+ Un frame di dati è una tabella con _più_ colonne.
+ Una singola colonna di un frame di dati, è un oggetto di tipo elenco denominato una serie.
+ Un singolo valore è una cella di un frame di dati e deve essere chiamata in base all'indice.

Come si esporrà il singolo risultato di un calcolo come frame di dati, se un frame di dati richiede una struttura tabulare? Una risposta è per rappresentare il valore scalare singolo come una serie, che viene facilmente convertita in un frame di dati. 

## <a name="prerequisites"></a>Prerequisiti

Una Guida introduttiva precedente [Python verificare esiste nel Server SQL](quickstart-python-verify.md), vengono fornite informazioni e collegamenti per la configurazione dell'ambiente di Python necessario per questa Guida introduttiva.

## <a name="scalar-value-as-a-series"></a>Valore scalare come una serie

In questo esempio esegue alcuni calcoli matematici semplici e converte un valore scalare in una serie.

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

2. Poiché la serie non è stata convertita in un frame di dati, vengono restituiti i valori nella finestra dei messaggi, ma è possibile notare che i risultati sono in formato tabulare più.

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Per aumentare la lunghezza della serie, è possibile aggiungere nuovi valori, utilizzando una matrice. 

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

    Se non si specifica un indice, viene generato un indice che dispone di valori a partire da 0 e termina con la lunghezza della matrice.

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. Se si aumenta il numero di **indice** valori, ma non aggiungere nuovi **dati** valori, i valori dei dati vengono ripetuti per riempire la serie.

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

## <a name="convert-series-to-data-frame"></a>Convertire serie in frame di dati

Visto convertito risultati matematici scalari in una struttura tabulare, è comunque necessario convertirli in un formato che può gestire SQL Server. 

1. Per convertire una serie in un frame di dati, chiamare il pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) (metodo).

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

2. Il risultato è illustrato di seguito. Anche se si utilizza l'indice per ottenere valori specifici dal frame di dati, i valori di indice non fanno parte dell'output.

    **Risultati**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>Valori di output in frame di dati

Di seguito viene illustrato come la conversione in un frame di dati funziona con due serie che contiene i risultati delle operazioni matematiche semplici. Il primo ha un indice di valori sequenziali generati da Python. Il secondo Usa un indice di valori di stringa arbitrario.

1. In questo esempio Ottiene un valore dalla serie che utilizza un indice integer.

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

    Tenere presente che l'indice generato automaticamente inizia da 0. Provare a usare un valore di indice di intervallo fuori e vedere cosa succede.

2. A questo punto è possibile ottenere un singolo valore da altri frame di dati che include un indice stringa. 

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

    Se si prova a usare un indice numerico per ottenere un valore di questa serie, viene visualizzato un errore.

## <a name="next-steps"></a>Passaggi successivi

Successivamente, si creerà un modello predittivo usando Python in SQL Server.

> [!div class="nextstepaction"]
> [Creare, eseguire il training e usare un modello Python con le stored procedure in SQL Server](quickstart-python-train-score-in-tsql.md)