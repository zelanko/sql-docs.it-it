---
title: Guida introduttiva per l'utilizzo di input e output in R - SQL Server Machine Learning
description: In questa Guida introduttiva per lo script R in SQL Server, informazioni su come strutturare gli input e output per la stored procedure sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1672cdeb59dfe35e313c999549e46f3fd76b688e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962004"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>Avvio rapido: Gestire gli input e output usano R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questa Guida introduttiva illustra come gestire gli input e restituisce quando si usano R in SQL Server Machine Learning Services o R Services.

Quando si desidera eseguire il codice R in SQL Server, è necessario eseguire il wrapping dello script R in una stored procedure. È possibile scrivere uno o passare script R [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Questo sistema stored procedure viene utilizzata per avviare il runtime di R nel contesto di SQL Server, che passa i dati in R, gestisce le sessioni utente di R in modo sicuro e restituisce gli eventuali risultati al client.

Per impostazione predefinita [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) accetta un singolo set di dati input, che in genere è fornire sotto forma di una query SQL valida. Altri tipi di input possono essere passati come variabili di SQL.

La stored procedure restituisce un singolo frame di dati R come output, ma è anche possibile restituire valori scalari e i modelli come variabili. Ad esempio, è possibile restituire un modello con training come una variabile binaria e che passare a un'istruzione T-SQL INSERT, per scrivere tale modello in una tabella. È anche possibile generare grafici (in formato binario) o valori scalari (valori singoli, ad esempio la data e ora, il tempo trascorso per il training del modello e così via).

## <a name="prerequisites"></a>Prerequisiti

Una Guida introduttiva precedente [R verificare esiste nel Server SQL](quickstart-r-verify.md), vengono fornite informazioni e collegamenti per configurare l'ambiente R necessario per questa Guida introduttiva.

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

Esaminiamo l'impostazione predefinita le variabili di input e outpue di sp_execute_external_script: `InputDataSet` e `OutputDataSet`.

1. È possibile ottenere i dati dalla tabella come input per lo script R. Eseguire l'istruzione seguente. Ottiene i dati dalla tabella, effettua un round trip tramite il runtime R e restituisce i valori con il nome della colonna *NewColName*.

    I dati restituiti dalla query vengono passati al runtime di R, che restituisce i dati al Database SQL come frame di dati. La clausola WITH RESULT SETS definisce lo schema della tabella di dati restituiti per il Database SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Risultati**

    ![Output dello script R che restituisce i dati da una tabella](./media/r-output-rtestdata.png)

2. È possibile modificare il nome delle variabili di input o outpue. Lo script precedente usato l'input predefinito e i nomi delle variabili, di output _InputDataSet_ e _OutputDataSet_. Per definire i dati di input associati _InputDatSet_, si utilizza il *@input_data_1* variabile.

    In questo script, i nomi dell'output e le variabili di input per la stored procedure sono stati modificati per *SQL_out* e *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    Si noti che R sia tra maiuscole e minuscole, pertanto il caso delle variabili di input e outpue in `@input_data_1_name` e `@output_data_1_name` devono corrispondere a quelli nel codice R in `@script`. 

    È possibile passare come parametro un solo set di dati di input ed è possibile restituire un solo set di dati. È tuttavia possibile chiamare altri set di dati dall'interno del codice R e restituire output di altri tipi oltre al set di dati. È anche possibile aggiungere la parola chiave OUTPUT a qualsiasi parametro in modo che venga restituito con i risultati. 

    Il `WITH RESULT SETS` istruzione definisce lo schema per i dati che viene usati in SQL Server. È necessario specificare i tipi di dati compatibili con SQL per ogni colonna restituita da R. È possibile usare la definizione dello schema per fornire nuovi nomi di colonna troppo perché non è necessaria usare i nomi di colonna dal frame di dati R.

3. È anche possibile generare valori usando lo script R e lasciare la stringa di query di input nel _@input_data_1_ vuoto.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Risultati**

    ![I risultati della query usando @script come input](./media/r-data-generated-output.png)

## <a name="next-steps"></a>Passaggi successivi

Esaminare alcuni dei problemi che possono verificarsi quando si passano dati tra R e SQL Server, ad esempio le conversioni implicite e le differenze nei dati tabulari tra R e SQL.

> [!div class="nextstepaction"]
> [Avvio rapido: Gestire gli oggetti e tipi di dati](quickstart-r-data-types-and-objects.md)