---
title: Guida introduttiva per l'uso di input e output in R
description: In questa Guida introduttiva per script R in SQL Server, informazioni su come strutturare input e output per il sistema sp_execute_external_script stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4e9e7efe6143d35e627abef4272281aad4b5b184
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469153"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>Avvio rapido: Gestire input e output usando R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa Guida introduttiva illustra come gestire input e output quando si usa R in SQL Server Machine Learning Services o R Services.

Quando si vuole eseguire codice R in SQL Server, è necessario eseguire il wrapping dello script R in una stored procedure. È possibile scriverne uno o passare uno script R a [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Questa stored procedure di sistema viene usata per avviare il runtime di R nel contesto di SQL Server, che passa i dati a R, gestisce le sessioni utente di R in modo sicuro e restituisce tutti i risultati al client.

Per impostazione predefinita, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) accetta un singolo set di dati di input, che in genere viene fornito sotto forma di query SQL valida. Altri tipi di input possono essere passati come variabili SQL.

Il stored procedure restituisce un singolo frame di dati R come output, ma è anche possibile restituire scalari e modelli come variabili. Ad esempio, è possibile generare un modello sottoposto a training come variabile binaria e passarlo a un'istruzione T-SQL INSERT, per scrivere tale modello in una tabella. È anche possibile generare grafici (in formato binario) o scalari (singoli valori, ad esempio la data e l'ora, il tempo trascorso per il training del modello e così via).

## <a name="prerequisites"></a>Prerequisiti

Una guida introduttiva precedente, [Verify R exists in SQL Server](quickstart-r-verify.md), fornisce informazioni e collegamenti per la configurazione dell'ambiente R necessario per questa Guida introduttiva.

## <a name="create-the-source-data"></a>Creare i dati di origine

Creare una piccola tabella di dati di test eseguendo l'istruzione T-SQL seguente:

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)
INSERT INTO RTestData VALUES (1);
INSERT INTO RTestData VALUES (10);
INSERT INTO RTestData VALUES (100);
GO
```

Dopo aver creato la tabella, usare questa istruzione per eseguire una query sulla tabella:
  
```sql
SELECT * FROM RTestData
```

**Risultati**

![Contenuto della tabella RTestData](./media/select-rtestdata.png)

## <a name="inputs-and-outputs"></a>Input e output

Esaminiamo le variabili di input e output predefinite di sp_execute_external_script: `InputDataSet` e. `OutputDataSet`

1. È possibile ottenere i dati dalla tabella come input per lo script R. Eseguire l'istruzione seguente. Ottiene i dati dalla tabella, rende un round trip tramite il runtime di R e restituisce i valori con il nome di colonna *NewColName*.

    I dati restituiti dalla query vengono passati al runtime di R, che restituisce i dati al database SQL come frame di dati. La clausola WITH RESULT SETS definisce lo schema della tabella dati restituiti per il database SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Risultati**

    ![Output dello script R che restituisce i dati di una tabella](./media/r-output-rtestdata.png)

2. Modificare il nome delle variabili di input o di output. Lo script precedente usava i nomi delle variabili di input e output predefinite, _InputDataSet_ e _OutputDataSet_. Per definire i dati di input associati a _InputDatSet_, usare la *@input_data_1* variabile.

    In questo script, i nomi delle variabili di input e di output per il stored procedure sono stati modificati in *SQL_out* e *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    Si noti che R fa distinzione tra maiuscole e minuscole, quindi il caso delle variabili `@input_data_1_name` di `@output_data_1_name` input e output in e deve corrispondere a quelli nel `@script`codice r in. 

    È possibile passare come parametro un solo set di dati di input ed è possibile restituire un solo set di dati. È tuttavia possibile chiamare altri set di dati dall'interno del codice R e restituire output di altri tipi oltre al set di dati. È anche possibile aggiungere la parola chiave OUTPUT a qualsiasi parametro in modo che venga restituito con i risultati. 

    L' `WITH RESULT SETS` istruzione definisce lo schema per i dati utilizzati in SQL Server. È necessario fornire tipi di dati compatibili con SQL per ogni colonna restituita da R. È possibile usare la definizione dello schema per fornire nuovi nomi di colonna, perché non è necessario usare i nomi di colonna del frame di dati R.

3. È anche possibile generare valori usando lo script R e lasciare vuota la stringa di query _@input_data_1_ di input.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Risultati**

    ![Risultati della query @script utilizzando come input](./media/r-data-generated-output.png)

## <a name="next-steps"></a>Passaggi successivi

Esaminare alcuni dei problemi che potrebbero verificarsi durante il passaggio di dati tra R e SQL Server, ad esempio le conversioni implicite e le differenze nei dati tabulari tra R e SQL.

> [!div class="nextstepaction"]
> [Avvio rapido: Gestire tipi di dati e oggetti](quickstart-r-data-types-and-objects.md)