---
title: Guida introduttiva per l'uso di input e output in Python
description: In questa Guida introduttiva per script Python in SQL Server, informazioni su come strutturare input e output per il sistema sp_execute_external_script stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 10c62f78ff2ac23e33ad251a07ed8f3689f79843
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715459"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>Avvio rapido: Gestire input e output usando Python in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa Guida introduttiva illustra come gestire input e output quando si usa Python in SQL Server Machine Learning Services.

Per impostazione predefinita, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) accetta un singolo set di dati di input, che in genere viene fornito sotto forma di query SQL valida.

Altri tipi di input possono essere passati come variabili SQL: ad esempio, è possibile passare un modello sottoposto a training come variabile, usando una funzione di serializzazione, ad esempio [Pickle](https://docs.python.org/3.0/library/pickle.html) o [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) , per scrivere il modello in un formato binario.

Il stored procedure restituisce un singolo frame di dati di Python [Pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) come output, ma è anche possibile restituire scalari e modelli come variabili. Ad esempio, è possibile generare un modello sottoposto a training come variabile binaria e passarlo a un'istruzione T-SQL INSERT, per scrivere tale modello in una tabella. È anche possibile generare grafici (in formato binario) o scalari (singoli valori, ad esempio la data e l'ora, il tempo trascorso per il training del modello e così via).

## <a name="prerequisites"></a>Prerequisiti

Una guida introduttiva precedente, [Verify Python exists in SQL Server](quickstart-python-verify.md), fornisce informazioni e collegamenti per la configurazione dell'ambiente Python necessario per questa Guida introduttiva.

## <a name="create-the-source-data"></a>Creare i dati di origine

Creare una piccola tabella di dati di test eseguendo l'istruzione T-SQL seguente:

```sql
CREATE TABLE PythonTestData (col1 INT NOT NULL)
INSERT INTO PythonTestData VALUES (1);
INSERT INTO PythonTestData VALUES (10);
INSERT INTO PythonTestData VALUES (100);
GO
```

Dopo aver creato la tabella, usare questa istruzione per eseguire una query sulla tabella:
  
```sql
SELECT * FROM PythonTestData
```

**Risultati**

![Contenuto della tabella PythonTestData](./media/select-pythontestdata.png)

## <a name="inputs-and-outputs"></a>Input e output

Esaminiamo le variabili di input e output predefinite di sp_execute_external_script: `InputDataSet` e. `OutputDataSet`

1. È possibile ottenere i dati dalla tabella come input per lo script Python. Eseguire l'istruzione seguente. Ottiene i dati dalla tabella, esegue una round trip tramite il runtime di Python e restituisce i valori con il nome di colonna *NewColName*.

    I dati restituiti dalla query vengono passati al runtime di Python, che restituisce i dati al database SQL come frame di dati Pandas. La clausola WITH RESULT SETS definisce lo schema della tabella dati restituiti per il database SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Risultati**

    ![Output dello script Python che restituisce i dati da una tabella](./media/python-output-pythontestdata.png)

2. Modificare il nome delle variabili di input o di output. Lo script precedente usava i nomi delle variabili di input e output predefinite, _InputDataSet_ e _OutputDataSet_. Per definire i dati di input associati a _InputDataSet_, usare la *@input_data_1* variabile.

    In questo script, i nomi delle variabili di input e di output per il stored procedure sono stati modificati in *SQL_out* e *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    Il caso delle variabili di input e output in `@input_data_1_name` e `@output_data_1_name` deve corrispondere al caso di quelli nel codice Python in, in `@script`quanto Python fa distinzione tra maiuscole e minuscole.

    È possibile passare come parametro un solo set di dati di input ed è possibile restituire un solo set di dati. Tuttavia, è possibile chiamare altri set di dati dall'interno del codice Python ed è possibile restituire output di altri tipi oltre al set di dati. È anche possibile aggiungere la parola chiave OUTPUT a qualsiasi parametro in modo che venga restituito con i risultati. 

    L' `WITH RESULT SETS` istruzione definisce lo schema per i dati utilizzati in SQL Server. È necessario fornire tipi di dati compatibili con SQL per ogni colonna restituita da Python. È possibile usare la definizione dello schema per fornire nuovi nomi di colonna, perché non è necessario usare i nomi di colonna del frame di dati Python.

3. È anche possibile generare valori usando lo script Python e lasciare vuota la stringa di query _@input_data_1_ di input.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'Python'
    , @script = N'
    import pandas as pd
    mytextvariable = pandas.Series(["hello", " ", "world"]);
    OutputDataSet = pd.DataFrame(mytextvariable);'
    , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Risultati**

    ![Risultati della query @script utilizzando come input](./media/python-data-generated-output.png)

## <a name="next-steps"></a>Passaggi successivi

Esaminare alcuni dei problemi che potrebbero verificarsi durante il passaggio di dati tabulari tra Python e SQL Server.

> [!div class="nextstepaction"]
> [Avvio rapido: Strutture di dati Python in SQL Server](quickstart-python-data-structures.md)
