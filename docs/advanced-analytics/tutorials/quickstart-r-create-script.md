---
title: Creare ed eseguire script R semplici
titleSuffix: SQL Server Machine Learning Services
description: Creare ed eseguire script R semplici in un'istanza di SQL Server con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d723fa9b90659eb31e96626a3a85c1299c17fa2f
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/20/2019
ms.locfileid: "71150314"
---
# <a name="quickstart-create-and-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>Avvio rapido: Creare ed eseguire script R semplici con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa Guida introduttiva si creerà ed eseguirà un set di semplici script R usando [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md). Si apprenderà come eseguire il wrapping di uno script R ben formato nel stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) ed eseguire lo script in un'istanza di SQL Server.

## <a name="prerequisites"></a>Prerequisiti

- Questa Guida introduttiva richiede l'accesso a un'istanza di SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con il linguaggio R installato.

  L'istanza di SQL Server può trovarsi in una macchina virtuale di Azure o in locale. È sufficiente tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, pertanto potrebbe essere necessario abilitare l'esecuzione di [script esterni](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che **launchpad di SQL Server servizio** sia in esecuzione prima di iniziare.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script R. È possibile eseguire questi script utilizzando qualsiasi strumento di gestione del database o query, purché sia possibile connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o stored procedure. Questa Guida introduttiva usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Eseguire uno script semplice

Per eseguire uno script R, è possibile passarlo come argomento al stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Questo stored procedure di sistema avvia il runtime di R nel contesto di SQL Server, passa i dati a R, gestisce le sessioni utente di R in modo sicuro e restituisce tutti i risultati al client.

Nei passaggi seguenti si eseguirà questo script R di esempio nell'istanza di SQL Server:

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. Aprire **SQL Server Management Studio** e connettersi all'istanza di SQL Server.

1. Passare lo script R completo al `sp_execute_external_script` stored procedure.

   Lo script viene passato tramite l' `@script` argomento. Tutti gli elementi `@script` all'interno dell'argomento devono essere codice R valido.

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

1. Viene calcolato il risultato corretto e la funzione `print` R restituisce il risultato nella finestra **messaggi** .

   Dovrebbe avere un aspetto simile al seguente.

    **Risultati**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Eseguire uno script di Hello World

Uno script di esempio tipico è quello che restituisce solo la stringa "Hello World". Eseguire il comando seguente.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

Gli input per `sp_execute_external_script` il stored procedure includono:

| | |
|-|-|
| @language | definisce l'estensione del linguaggio da chiamare, in questo caso R |
| @script | definisce i comandi passati al runtime di R. L'intero script R deve essere incluso in questo argomento come testo Unicode. È anche possibile aggiungere il testo a una variabile di tipo **nvarchar** e chiamare la variabile |
| @input_data_1 | dati restituiti dalla query, passati al runtime di R, che restituisce i dati da SQL Server come frame di dati |
|CON SET DI RISULTATI | la clausola definisce lo schema della tabella dati restituita per SQL Server, aggiungendo "Hello World" come nome di colonna, **int** per il tipo di dati |

Il comando restituisce il testo seguente:

| Salve, mondo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Usare input e output

Per impostazione predefinita `sp_execute_external_script` , accetta un singolo set di dati come input, che in genere viene fornito sotto forma di una query SQL valida. Restituisce quindi un singolo frame di dati R come output.

Per il momento, verranno usate le variabili di input e output predefinite `sp_execute_external_script`di: **InputDataSet** e **OutputDataSet**.

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

1. Utilizzare l' `SELECT` istruzione per eseguire una query sulla tabella.
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **Risultati**

    ![Contenuto della tabella RTestData](./media/select-rtestdata.png)

1. Eseguire lo script R seguente. Recupera i dati dalla tabella usando l' `SELECT` istruzione, li passa attraverso il runtime di R e restituisce i dati come frame di dati. La `WITH RESULT SETS` clausola definisce lo schema della tabella dati restituita per SQL, aggiungendo il nome della colonna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Risultati**

    ![Output dello script R che restituisce i dati di una tabella](./media/r-output-rtestdata.png)

1. A questo punto è possibile modificare i nomi delle variabili di input e di output. I nomi delle variabili di input e output predefiniti sono **InputDataSet** e **OutputDataSet**, questo script modifica i nomi in **SQL_in** e **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Si noti che R distingue tra maiuscole e minuscole. Le variabili di input e di output utilizzate nello script R (**SQL_out**, **SQL_in**) devono corrispondere ai nomi definiti con `@input_data_1_name` e `@output_data_1_name`, inclusa la distinzione tra maiuscole e minuscole.

   > [!TIP]
   > È possibile passare come parametro un solo set di dati di input ed è possibile restituire un solo set di dati. È tuttavia possibile chiamare altri set di dati dall'interno del codice R e restituire output di altri tipi oltre al set di dati. È anche possibile aggiungere la parola chiave OUTPUT a qualsiasi parametro in modo che venga restituito con i risultati.

1. È anche possibile generare valori usando solo lo script R senza dati di input (`@input_data_1` è impostato su blank).

   Lo script seguente restituisce il testo "Hello" e "World".

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

    ![Risultati della query @script utilizzando come input](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>Controllare la versione di R

Se si vuole vedere quale versione di R è installata nell'istanza di SQL Server, eseguire lo script seguente.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

La funzione `print` R restituisce la versione alla finestra **messages** . Nell'output di esempio seguente si noterà che, in questo caso, è installato R Version 3.4.4.

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

Microsoft offre una serie di pacchetti R preinstallati con SQL Server Machine Learning Services.

Per visualizzare un elenco dei pacchetti R installati, incluse le informazioni sulla versione, le dipendenze, la licenza e il percorso della libreria, eseguire lo script seguente.

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

L'output è da `installed.packages()` in R e viene restituito come set di risultati.

**Risultati**

![Pacchetti installati in R](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>Passaggi successivi

Per creare un modello di Machine Learning usando R in SQL Server, seguire questa Guida introduttiva:

> [!div class="nextstepaction"]
> [Creare e assegnare un punteggio a un modello predittivo in R con SQL Server Machine Learning Services](quickstart-r-train-score-model.md)

Per ulteriori informazioni su SQL Server Machine Learning Services, vedere gli articoli seguenti.

- [Gestire i tipi di dati e gli oggetti usando R in SQL Server Machine Learning Services](quickstart-r-data-types-and-objects.md)
- [Scrivere funzioni R avanzate con SQL Server Machine Learning Services](quickstart-r-functions.md)
- [Che cos'è SQL Server Machine Learning Services (Python e R)?](../what-is-sql-server-machine-learning.md)
