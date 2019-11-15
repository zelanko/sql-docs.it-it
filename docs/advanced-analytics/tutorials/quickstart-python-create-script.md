---
title: 'Avvio rapido: Creare script Python'
titleSuffix: SQL Server Machine Learning Services
description: Creare ed eseguire semplici script Python in un'istanza di SQL Server con Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8409eaf8129d7c8eb2eecd5a1157a17444341734
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727029"
---
# <a name="quickstart-create-and-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>Avvio rapido: Creare ed eseguire semplici script Python con Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo argomento di avvio rapido verrà creato ed eseguito un set di semplici script Python con [Machine Learning Services per SQL Server](../what-is-sql-server-machine-learning.md). Si apprenderà come eseguire il wrapping di uno script Python ben formato nella stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) ed eseguire lo script in un'istanza di SQL Server.

## <a name="prerequisites"></a>Prerequisites

- Questo argomento di avvio rapido richiede l'accesso a un'istanza di SQL Server con [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) con il linguaggio Python installato.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script Python. È possibile eseguire questi script usando qualsiasi strumento di gestione del database o di query, purché possa connettersi a un'istanza di SQL Server, nonché eseguire una query T-SQL o una stored procedure. In questo argomento di avvio rapido viene usato [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Eseguire uno script semplice

Per eseguire uno script Python, è necessario passarlo come argomento alla stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Questa stored procedure di sistema avvia il runtime Python nel contesto di SQL Server, passa i dati a Python, gestisce le sessioni utente di Python in modo sicuro e restituisce i risultati al client.

Nei passaggi successivi si eseguirà questo script Python di esempio nell'istanza di SQL Server:

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. In **SQL Server Management Studio** aprire una nuova finestra di query connessa all'istanza di SQL Server.

1. Passare lo script Python completo alla stored procedure `sp_execute_external_script`.

   Lo script viene passato tramite l'argomento `@script`. Tutti gli elementi all'interno dell'argomento `@script` devono essere costituiti da codice Python valido.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. Il risultato corretto viene calcolato e la funzione Python `print` restituisce il risultato nella finestra **Messaggi**.

   Il risultato sarà simile al seguente.

    **Risultati**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Eseguire uno script Hello World

Uno script di esempio tipico è quello che restituisce come output la stringa "Hello World". Eseguire il comando seguente.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

Gli input per la stored procedure `sp_execute_external_script` includono:

| | |
|-|-|
| @language | Definisce l'estensione del linguaggio da chiamare, in questo caso Python |
| @script | Definisce i comandi passati al runtime Python<br>L'intero script Python deve essere incluso in questo argomento come testo Unicode. È anche possibile aggiungere il testo a una variabile di tipo **nvarchar** e quindi chiamare la variabile |
| @input_data_1 | Dati restituiti dalla query, passati al runtime Python, che restituisce i dati a SQL Server come frame di dati |
|WITH RESULT SETS | Clausola che definisce lo schema della tabella dati restituita per SQL Server, in questo caso aggiungendo "Hello World" come nome di colonna e **int** per il tipo di dati |

Il comando restituisce il testo seguente:

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Usare input e output

Per impostazione predefinita, `sp_execute_external_script` accetta un singolo set di dati come input, che in genere viene fornito sotto forma di query SQL valida. Restituisce quindi un singolo frame di dati Python come output.

Per il momento, verranno usate le variabili di input e di output predefinite di `sp_execute_external_script`: **InputDataSet** e **OutputDataSet**.

1. Creare una piccola tabella di dati di test.

    ```sql
    CREATE TABLE PythonTestData (col1 INT NOT NULL)
    
    INSERT INTO PythonTestData
    VALUES (1);
    
    INSERT INTO PythonTestData
    VALUES (10);
    
    INSERT INTO PythonTestData
    VALUES (100);
    GO
    ```

1. Usare l'istruzione `SELECT` per eseguire una query sulla tabella.
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **Risultati**

    ![Contenuto della tabella PythonTestData](./media/select-pythontestdata.png)

1. Eseguire lo script Python seguente. Questo script recupera i dati dalla tabella usando l'istruzione `SELECT`, li passa nel runtime Python e restituisce i dati come frame di dati. La clausola `WITH RESULT SETS` definisce lo schema della tabella dati restituita per SQL, aggiungendo il nome di colonna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Risultati**

    ![Output dello script Python che restituisce i dati di una tabella](./media/python-output-pythontestdata.png)

1. Modificare ora i nomi delle variabili di input e di output. I nomi delle variabili di input e di output predefiniti sono **InputDataSet** e **OutputDataSet**. Lo script seguente cambia i nomi in **SQL_in** e **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Si noti che Python fa distinzione tra maiuscole e minuscole. Le variabili di input e di output usate nello script Python (**SQL_out**, **SQL_in**) devono corrispondere ai nomi definiti con `@input_data_1_name` e `@output_data_1_name`, inclusa la distinzione tra maiuscole e minuscole.

   > [!TIP]
   > È possibile passare come parametro un solo set di dati di input ed è possibile restituire un solo set di dati. È tuttavia possibile chiamare altri set di dati dall'interno del codice Python e restituire output di altri tipi oltre al set di dati. È anche possibile aggiungere la parola chiave OUTPUT a qualsiasi parametro in modo che venga restituito con i risultati.

1. È anche possibile generare i valori usando solo lo script Python senza dati di input (`@input_data_1` è impostato su un valore vuoto).

   Lo script seguente restituisce il testo "hello" e "world".

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   mytextvariable = pandas.Series(["hello", " ", "world"]);
   OutputDataSet = pd.DataFrame(mytextvariable);
   '
       , @input_data_1 = N''
   WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
   ```

   **Risultati**

   ![Risultati di query con @script come input](./media/python-data-generated-output.png)

> [!NOTE]
> Python usa gli spazi iniziali per raggruppare le istruzioni. Quindi, quando lo script Python incorporato si estende su più righe, come nello script precedente, non provare a far rientrare i comandi Python in modo che siano allineati con i comandi SQL. Ad esempio, questo script genera un errore:

  ```text
  EXECUTE sp_execute_external_script @language = N'Python'
      , @script = N'
      import pandas as pd
      mytextvariable = pandas.Series(["hello", " ", "world"]);
      OutputDataSet = pd.DataFrame(mytextvariable);
      '
      , @input_data_1 = N''
  WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
  ```

## <a name="check-python-version"></a>Controllare la versione di Python

Se si vuole verificare quale versione di Python è installata nell'istanza di SQL Server, eseguire lo script seguente.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

La funzione Python `print` restituisce la versione nella finestra **Messaggi**. Nell'output di esempio seguente si può notare che in questo caso è installata la versione di Python 3.5.2.

**Risultati**

```text
STDOUT message(s) from external script: 
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Elencare i pacchetti Python

Microsoft fornisce una serie di pacchetti Python preinstallati con Machine Learning Services per SQL Server nell'istanza di SQL Server.

Per visualizzare un elenco dei pacchetti Python installati, inclusa la versione, eseguire lo script seguente.

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pip
for i in pip.get_installed_distributions():
    print(i)
'
GO
```

L'output proviene da `pip.get_installed_distributions()` in Python e viene restituito come messaggi `STDOUT`.

**Risultati**

```text
STDOUT message(s) from external script:
xlwt 1.2.0
XlsxWriter 0.9.6
xlrd 1.0.0
win-unicode-console 0.5
widgetsnbextension 2.0.0
wheel 0.29.0
Werkzeug 0.12.1
wcwidth 0.1.7
unicodecsv 0.14.1
traitlets 4.3.2
tornado 4.4.2
toolz 0.8.2
. . .
```

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come usare le strutture di dati quando si usa Python in Machine Learning Services per SQL Server, seguire questo argomento di avvio rapido:

> [!div class="nextstepaction"]
> [Gestire tipi di dati e oggetti usando Python in Machine Learning Services per SQL Server](quickstart-python-data-structures.md)

Per altre informazioni sull'uso di Python in Machine Learning Services per SQL Server, vedere gli articoli seguenti:

- [Scrivere funzioni Python avanzate con Machine Learning Services per SQL Server](quickstart-python-functions.md)
- [Creare e assegnare i punteggi a un modello predittivo in Python con Machine Learning Services per SQL Server](quickstart-python-train-score-model.md)
- [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
