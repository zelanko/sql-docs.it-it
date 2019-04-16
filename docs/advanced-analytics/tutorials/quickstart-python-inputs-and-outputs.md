---
title: Guida introduttiva per l'utilizzo di input e output in Python - SQL Server Machine Learning
description: In questa Guida introduttiva per script di Python in SQL Server, informazioni su come strutturare gli input e output per la stored procedure sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a778c4a65b9e3f4cbf4ed77cff46e9061d4b6a8a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583224"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>Avvio rapido: Gestire gli input e output con Python in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questa Guida introduttiva illustra come gestire gli input e restituisce quando si usano Python in SQL Server Machine Learning Services.

Per impostazione predefinita [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) accetta un singolo set di dati input, che in genere è fornire sotto forma di una query SQL valida.

Altri tipi di input possono essere passati come variabili SQL: ad esempio, è possibile passare un modello con training come una variabile, usando una funzione di serializzazione, ad esempio [pickle](https://docs.python.org/3.0/library/pickle.html) oppure [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) per scrivere il modello un formato binario.

La stored procedure restituisce un singolo Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) frame di dati come output, ma è anche possibile restituire valori scalari e i modelli come variabili. Ad esempio, è possibile restituire un modello con training come una variabile binaria e che passare a un'istruzione T-SQL INSERT, per scrivere tale modello in una tabella. È anche possibile generare grafici (in formato binario) o valori scalari (valori singoli, ad esempio la data e ora, il tempo trascorso per il training del modello e così via).

## <a name="prerequisites"></a>Prerequisiti

Una Guida introduttiva precedente [Python verificare esiste nel Server SQL](quickstart-python-verify.md), vengono fornite informazioni e collegamenti per la configurazione dell'ambiente di Python necessario per questa Guida introduttiva.

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

Esaminiamo l'impostazione predefinita le variabili di input e outpue di sp_execute_external_script: `InputDataSet` e `OutputDataSet`.

1. È possibile ottenere i dati dalla tabella come input per lo script R. Eseguire l'istruzione seguente. Ottiene i dati dalla tabella, effettua un round trip tramite il runtime R e restituisce i valori con il nome della colonna *NewColName*.

    I dati restituiti dalla query vengono passati al runtime di R, che restituisce i dati al Database SQL come frame di dati. La clausola WITH RESULT SETS definisce lo schema della tabella di dati restituiti per il Database SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Risultati**

    ![Output dello script Python che restituisce i dati da una tabella](./media/python-output-pythontestdata.png)

2. È possibile modificare il nome delle variabili di input o outpue. Lo script precedente usato l'input predefinito e i nomi delle variabili, di output _InputDataSet_ e _OutputDataSet_. Per definire i dati di input associati _InputDatSet_, si utilizza il *@input_data_1* variabile.

    In questo script, i nomi dell'output e le variabili di input per la stored procedure sono stati modificati per *SQL_out* e *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    Il caso delle variabili di input e outpue in `@input_data_1_name` e `@output_data_1_name` devono corrispondere il caso di quelli nel codice Python in `@script`, poiché Python è tra maiuscole e minuscole.

    È possibile passare come parametro un solo set di dati di input ed è possibile restituire un solo set di dati. Tuttavia, è possibile chiamare altri set di dati dall'interno del codice Python ed è possibile restituire output di altri tipi oltre il set di dati. È anche possibile aggiungere la parola chiave OUTPUT a qualsiasi parametro in modo che venga restituito con i risultati. 

    Il `WITH RESULT SETS` istruzione definisce lo schema per i dati che viene usati in SQL Server. È necessario specificare i tipi di dati compatibili con SQL per ogni colonna restituita da Python. È possibile usare la definizione dello schema per fornire nuovi nomi di colonna troppo perché non è necessaria usare i nomi di colonna dal frame di dati Python.

3. È anche possibile generare valori usando lo script Python e lasciare la stringa di query di input nel _@input_data_1_ vuoto.

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

    ![I risultati della query usando @script come input](./media/python-data-generated-output.png)

## <a name="next-steps"></a>Passaggi successivi

Esaminare alcuni dei problemi che possono verificarsi quando si passano dati tabulari tra codice Python e SQL Server.

> [!div class="nextstepaction"]
> [Guida introduttiva: Strutture di dati di Python in SQL Server](quickstart-python-data-structures.md)