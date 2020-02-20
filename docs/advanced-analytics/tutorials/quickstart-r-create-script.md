---
title: 'Avvio rapido: Eseguire gli script R'
description: Eseguire un set di semplici script R con Machine Learning Services per SQL Server. Informazioni su come usare la stored procedure sp_execute_external_script per eseguire lo script in un'istanza di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 495bb56cf76391c8baa1734665d5064b586d4be8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "76831786"
---
# <a name="quickstart-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>Avvio rapido: Eseguire semplici script R con Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo argomento di avvio rapido verrà seguito un set di semplici script R con [Machine Learning Services per SQL Server](../what-is-sql-server-machine-learning.md). Si apprenderà come usare la stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) per eseguire lo script in un'istanza di SQL Server.

## <a name="prerequisites"></a>Prerequisites

- Questo argomento di avvio rapido richiede l'accesso a un'istanza di SQL Server con [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) con il linguaggio R installato.

  L'istanza di SQL Server può essere in una macchina virtuale di Azure o in locale. Tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, quindi potrebbe essere necessario [abilitare lo scripting esterno](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che il **servizio Launchpad di SQL Server** sia in esecuzione prima di iniziare.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script R. È possibile eseguire questi script usando qualsiasi strumento di gestione del database o di query, purché possa connettersi a un'istanza di SQL Server, nonché eseguire una query T-SQL o una stored procedure. In questo argomento di avvio rapido viene usato [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Eseguire uno script semplice

Per eseguire uno script R, passarlo come argomento alla stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Questa stored procedure di sistema avvia il runtime R nel contesto di SQL Server, passa i dati a R, gestisce le sessioni utente di R in modo sicuro e restituisce i risultati al client.

Nei passaggi successivi si eseguirà questo script R di esempio nell'istanza di SQL Server:

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. Aprire **SQL Server Management Studio** e connettersi all'istanza di SQL Server.

1. Passare lo script R completo alla stored procedure `sp_execute_external_script`.

   Lo script viene passato tramite l'argomento `@script`. Tutti gli elementi all'interno dell'argomento `@script` devono essere costituiti da codice R valido.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. Viene calcolato il risultato corretto e la funzione `print` di R restituisce il risultato nella finestra **Messaggi**.

   Il risultato sarà simile al seguente.

    **Risultati**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Eseguire uno script Hello World

Uno script di esempio tipico è quello che restituisce come output la stringa "Hello World". Eseguire il comando seguente.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

Gli input per la stored procedure `sp_execute_external_script` includono:

| | |
|-|-|
| @language | Definisce l'estensione del linguaggio da chiamare, in questo caso R |
| @script | Definisce i comandi passati al runtime R. L'intero script R deve essere incluso in questo argomento, come testo Unicode. È anche possibile aggiungere il testo a una variabile di tipo **nvarchar** e quindi chiamare la variabile |
| @input_data_1 | Dati restituiti dalla query, passati al runtime R, che restituisce i dati a SQL Server come frame di dati |
|WITH RESULT SETS | Clausola che definisce lo schema della tabella dati restituita per SQL Server, aggiungendo "Hello World" come nome di colonna e **int** per il tipo di dati |

Il comando restituisce il testo seguente:

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Usare input e output

Per impostazione predefinita, `sp_execute_external_script` accetta un singolo set di dati come input, che in genere viene fornito sotto forma di query SQL valida. Restituisce quindi un singolo frame di dati R come output.

Per il momento, verranno usate le variabili di input e di output predefinite di `sp_execute_external_script`: **InputDataSet** e **OutputDataSet**.

1. Creare una piccola tabella di dati di test.

    ```sql
    CREATE TABLE RTestData (col1 INT NOT NULL)
    
    INSERT INTO RTestData
    VALUES (1);
    
    INSERT INTO RTestData
    VALUES (10);
    
    INSERT INTO RTestData
    VALUES (100);
    GO
    ```

1. Usare l'istruzione `SELECT` per eseguire una query sulla tabella.
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **Risultati**

    ![Contenuto della tabella RTestData](./media/select-rtestdata.png)

1. Eseguire lo script R seguente. Questo script recupera i dati dalla tabella usando l'istruzione `SELECT`, li passa nel runtime R e restituisce i dati come frame di dati. La clausola `WITH RESULT SETS` definisce lo schema della tabella dati restituita per SQL, aggiungendo il nome di colonna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Risultati**

    ![Output dello script R che restituisce i dati di una tabella](./media/r-output-rtestdata.png)

1. Modificare ora i nomi delle variabili di input e di output. I nomi delle variabili di input e di output predefiniti sono **InputDataSet** e **OutputDataSet**. Questo script cambia i nomi in **SQL_in** e **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Si noti che R fa distinzione tra maiuscole e minuscole. Le variabili di input e di output usate nello script R (**SQL_out**, **SQL_in**) devono corrispondere ai nomi definiti con `@input_data_1_name` e `@output_data_1_name`, inclusa la distinzione tra maiuscole e minuscole.

   > [!TIP]
   > È possibile passare come parametro un solo set di dati di input e si può restituire un solo set di dati. Tuttavia, è possibile chiamare altri set di dati dall'interno del codice R e restituire output di altri tipi in aggiunta al set di dati. È anche possibile aggiungere la parola chiave OUTPUT a qualsiasi parametro per fare in modo che venga restituito con i risultati.

1. È anche possibile generare i valori usando solo lo script R senza dati di input (`@input_data_1` è impostato su un valore vuoto).

   Lo script seguente restituisce il testo "hello" e "world".

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    mytextvariable <- c("hello", " ", "world");
    OutputDataSet <- as.data.frame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **Risultati**

    ![Risultati di query con @script come input](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>Controllare la versione di R

Se si vuole verificare quale versione di R è installata nell'istanza di SQL Server, eseguire lo script seguente.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

La funzione R `print` restituisce la versione nella finestra **Messaggi**. Nell'output di esempio seguente si può notare che in questo caso è installata la versione di R 3.4.4.

**Risultati**

```text
STDOUT message(s) from external script:
                   _
platform       x86_64-w64-mingw32
arch           x86_64
os             mingw32
system         x86_64, mingw32
status
major          3
minor          4.4
year           2018
month          03
day            15
svn rev        74408
language       R
version.string R version 3.4.4 (2018-03-15)
nickname       Someone to Lean On
```

## <a name="list-r-packages"></a>Elencare i pacchetti R

Microsoft fornisce una serie di pacchetti R preinstallati con Machine Learning Services per SQL Server.

Per visualizzare un elenco dei pacchetti R installati, incluse le informazioni su versione, dipendenze, licenza e percorso della libreria, eseguire lo script seguente.

```SQL
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((
            Package NVARCHAR(255)
            , Version NVARCHAR(100)
            , Depends NVARCHAR(4000)
            , License NVARCHAR(1000)
            , LibPath NVARCHAR(2000)
            ));
```

L'output proviene da `installed.packages()` in R e viene restituito come set di risultati.

**Risultati**

![Pacchetti installati in R](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come usare le strutture di dati quando si usa R in Machine Learning Services per SQL Server, seguire questo argomento di avvio rapido:

> [!div class="nextstepaction"]
> [Gestire tipi di dati e oggetti usando R in Machine Learning Services per SQL Server](quickstart-r-data-types-and-objects.md)

Per altre informazioni sull'uso di R in Machine Learning Services per SQL Server, vedere gli articoli seguenti:

- [Scrivere funzioni R avanzate con Machine Learning Services per SQL Server](quickstart-r-functions.md)
- [Creare un modello predittivo e assegnare punteggi in R con Machine Learning Services per SQL Server](quickstart-r-train-score-model.md)
- [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
