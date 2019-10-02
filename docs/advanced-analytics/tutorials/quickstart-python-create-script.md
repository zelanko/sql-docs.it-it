---
title: Creazione ed esecuzione di script Python semplici
titleSuffix: SQL Server Machine Learning Services
description: Creazione ed esecuzione di script Python semplici in un'istanza di SQL Server con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6f7fe62f746a8f6e74ebdf9f766b76c0edc720a
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2019
ms.locfileid: "71204298"
---
# <a name="quickstart-create-and-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>Avvio rapido: Creazione ed esecuzione di script Python semplici con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa Guida introduttiva verrà creato ed eseguito un set di script Python semplici usando [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md). Si apprenderà come eseguire il wrapping di uno script Python ben formato nel stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) ed eseguire lo script in un'istanza di SQL Server.

## <a name="prerequisites"></a>Prerequisiti

- Questa Guida introduttiva richiede l'accesso a un'istanza di SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con il linguaggio Python installato.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script Python. È possibile eseguire questi script utilizzando qualsiasi strumento di gestione del database o query, purché sia possibile connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o stored procedure. Questa Guida introduttiva usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Eseguire uno script semplice

Per eseguire uno script Python, viene passato come argomento all'stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Questo stored procedure di sistema avvia il runtime di Python nel contesto di SQL Server, passa i dati a Python, gestisce le sessioni utente di Python in modo sicuro e restituisce i risultati al client.

Nei passaggi seguenti si eseguirà questo script Python di esempio nell'istanza di SQL Server:

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. Aprire una nuova finestra di query in **SQL Server Management Studio** connessa all'istanza di SQL Server.

1. Passare lo script Python completo al `sp_execute_external_script` stored procedure.

   Lo script viene passato tramite l' `@script` argomento. Tutti gli elementi `@script` all'interno dell'argomento devono essere codice Python valido.

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

1. Viene calcolato il risultato corretto e la funzione `print` Python restituisce il risultato nella finestra **messaggi** .

   Dovrebbe avere un aspetto simile al seguente.

    **Risultati**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Eseguire uno script di Hello World

Uno script di esempio tipico è quello che restituisce solo la stringa "Hello World". Eseguire il comando seguente.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

Gli input per `sp_execute_external_script` il stored procedure includono:

| | |
|-|-|
| @language | definisce l'estensione del linguaggio da chiamare, in questo caso Python |
| @script | definisce i comandi passati al runtime di Python<br>L'intero script Python deve essere racchiuso in questo argomento, come testo Unicode. È anche possibile aggiungere il testo a una variabile di tipo **nvarchar** e chiamare la variabile |
| @input_data_1 | dati restituiti dalla query, passati al runtime di Python, che restituisce i dati da SQL Server come frame di dati |
|WITH RESULT SETS | la clausola definisce lo schema della tabella dati restituita per SQL Server, in questo caso l'aggiunta di "Hello World" come nome di colonna e **int** per il tipo di dati |

Il comando restituisce il testo seguente:

| Salve, mondo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Usare input e output

Per impostazione predefinita `sp_execute_external_script` , accetta un singolo set di dati come input, che in genere viene fornito sotto forma di una query SQL valida. Restituisce quindi un singolo frame di dati Python come output.

Per il momento, verranno usate le variabili di input e output predefinite `sp_execute_external_script`di: **InputDataSet** e **OutputDataSet**.

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

1. Utilizzare l' `SELECT` istruzione per eseguire una query sulla tabella.
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **Risultati**

    ![Contenuto della tabella PythonTestData](./media/select-pythontestdata.png)

1. Eseguire lo script Python seguente. Recupera i dati dalla tabella usando l' `SELECT` istruzione, li passa attraverso il runtime di Python e restituisce i dati come frame di dati. La `WITH RESULT SETS` clausola definisce lo schema della tabella dati restituita per SQL, aggiungendo il nome della colonna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Risultati**

    ![Output dello script Python che restituisce i dati da una tabella](./media/python-output-pythontestdata.png)

1. Modificare ora i nomi delle variabili di input e di output. I nomi delle variabili di input e output predefiniti sono **InputDataSet** e **OutputDataSet**, lo script seguente modifica i nomi in **SQL_in** e **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Si noti che Python distingue tra maiuscole e minuscole. Le variabili di input e di output utilizzate nello script Python (**SQL_out**, **SQL_in**) devono corrispondere ai nomi definiti con `@input_data_1_name` e `@output_data_1_name`, inclusa la distinzione tra maiuscole e minuscole.

   > [!TIP]
   > È possibile passare come parametro un solo set di dati di input ed è possibile restituire un solo set di dati. Tuttavia, è possibile chiamare altri set di dati dall'interno del codice Python ed è possibile restituire output di altri tipi oltre al set di dati. È anche possibile aggiungere la parola chiave OUTPUT a qualsiasi parametro in modo che venga restituito con i risultati.

1. È anche possibile generare valori usando solo lo script Python senza dati di input (`@input_data_1` è impostato su blank).

   Lo script seguente restituisce il testo "Hello" e "World".

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

   ![Risultati della query @script utilizzando come input](./media/python-data-generated-output.png)

> [!NOTE]
> Python usa gli spazi iniziali per raggruppare le istruzioni. Quindi, quando lo script Python incorporato si estende su più righe, come nello script precedente, non provare a rientrare i comandi Python in linea con i comandi SQL. Ad esempio, lo script genera un errore:

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

Se si vuole vedere quale versione di Python è installata nell'istanza di SQL Server, eseguire lo script seguente.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

La funzione `print` Python restituisce la versione alla finestra **messages** . Nell'output di esempio seguente è possibile notare che in questo caso è installata la versione di Python 3.5.2.

**Risultati**

```text
STDOUT message(s) from external script: 
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Elenca pacchetti Python

Microsoft fornisce una serie di pacchetti Python preinstallati con SQL Server Machine Learning Services nell'istanza di SQL Server.

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

L'output è da `pip.get_installed_distributions()` in Python e restituito come `STDOUT` messaggi.

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

Per creare un modello di Machine Learning con Python in SQL Server, seguire questa Guida introduttiva:

> [!div class="nextstepaction"]
> [Creare e assegnare un punteggio a un modello predittivo in Python con SQL Server Machine Learning Services](quickstart-python-train-score-model.md)

Per ulteriori informazioni su SQL Server Machine Learning Services, vedere gli articoli seguenti.

- [Gestire tipi di dati e oggetti usando Python in SQL Server Machine Learning Services](quickstart-python-data-structures.md)
- [Che cos'è SQL Server Machine Learning Services (Python e R)?](../what-is-sql-server-machine-learning.md)
