---
title: Set di dati iris demo per Python e R - esercitazioni di SQL Server Machine Learning
Description: Creare un database che contiene il set di dati Iris e una tabella per archiviare i modelli. Questo set di dati viene utilizzata negli esercizi che illustra come eseguire il wrapping di codice Python o linguaggio R in una stored procedure SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f4a57f89a89ed8d5cbf81cc3d63fc1f19b42e51a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510098"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>Dati di iris demo per le esercitazioni di Python e R in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questo esercizio, creare un database di SQL Server per archiviare i dati dal [set di dati dei fiori Iris](https://en.wikipedia.org/wiki/Iris_flower_data_set) e modelli basati sugli stessi dati. I dati iris sono incluso nelle distribuzioni di R e Python installate da SQL Server e viene usati nelle esercitazioni di machine learning per SQL Server. 

Per completare questo esercizio, è necessario disporre [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) o un altro strumento che è possibile eseguire query T-SQL.

Esercitazioni e guide introduttive utilizzano questo set di dati seguenti:

+  [Guida introduttiva: Creare, eseguire il training e usare un modello Python con le stored procedure in SQL Server](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>Creare il database

1. Avviare SQL Server Management Studio e aprire una nuova **Query** finestra.  

2. Creare un nuovo database per questo progetto e modificare il contesto dei **Query** finestra da utilizzare il nuovo database.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > Se si ha familiarità con SQL Server o si sta lavorando in un server si è proprietari, è un errore comune per accedere e iniziare a lavorare senza che vengano rilevate in cui si trova il **master** database. Per verificare che si usa il database corretto, specificare sempre il contesto utilizzando la `USE <database name>` istruzione (ad esempio, `use irissql`).

3. Aggiungere alcune tabelle vuote: uno per archiviare i dati e uno per archiviare i modelli con training. Il **iris_models** tabella viene usata per archiviare i modelli serializzati generati in altri tipi di addestramento.

    Il codice seguente crea la tabella per i dati di training.

    ```sql
    DROP TABLE IF EXISTS iris_data;
    GO
    CREATE TABLE iris_data (
      id INT NOT NULL IDENTITY PRIMARY KEY
      , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
      , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
      , "Species" VARCHAR(100) NOT NULL, "SpeciesId" INT NOT NULL
    );
    ```

    > [!TIP] 
    > Se si ha familiarità con T-SQL, è opportuno memorizzare le `DROP...IF` istruzione. Quando si prova a creare una tabella e ne esiste già, SQL Server restituisce un errore: "Si è già un oggetto denominato 'iris_data' nel database." Un modo per evitare tali errori consiste nell'eliminare tutte le tabelle esistenti o altri oggetti come parte del codice.

4. Eseguire il codice seguente per creare la tabella utilizzata per archiviare il modello con training. Per salvare i modelli di Python (o R) in SQL Server, devono essere serializzati e archiviati in una colonna di tipo **varbinary (max)**. 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Oltre al contenuto del modello, in genere, è necessario anche aggiungere le colonne di altri metadati utili, ad esempio il nome del modello, la data che è stato eseguito il training, l'algoritmo di origine e i parametri, dati di origine e così via. Per il momento si sarà tutto più semplice e usare semplicemente il nome del modello.

## <a name="populate-the-table"></a>Popolare la tabella

È possibile ottenere i dati Iris predefinite da R o Python. È possibile usare R o Python per caricare i dati in un frame di dati e quindi inserirla in una tabella nel database. Lo spostamento dei dati di training da una sessione esterna in una tabella di SQL Server è un processo in più passaggi:

+ Progettazione di una stored procedure che ottiene i dati desiderati.
+ Eseguire la stored procedure per ottenere effettivamente i dati.
+ Costruire un'istruzione INSERT per specificare dove salvare i dati recuperati.

1. Nei sistemi con l'integrazione di Python, creare la stored procedure seguente che usa codice Python per caricare i dati.

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    from sklearn import datasets
    iris = datasets.load_iris()
    iris_data = pandas.DataFrame(iris.data)
    iris_data["Species"] = pandas.Categorical.from_codes(iris.target, iris.target_names)
    iris_data["SpeciesId"] = iris.target
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

    Quando si esegue questo codice, è necessario ottenere il messaggio "Comandi riusciti" Tutto ciò significa è che la stored procedure sia stata creata in base alle specifiche.

2. In alternativa, nei sistemi con integrazione di R, creare una routine che usa invece R.

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'R', 
    @script = N'
    library(RevoScaleR)
    data(iris)
    iris$SpeciesID <- c(unclass(iris$Species))
    iris_data <- iris
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

3. Per popolare la tabella, eseguire la stored procedure e specificare la tabella dove devono essere scritti i dati. Quando eseguito, la stored procedure esegue il codice Python o R, che carica il set di dati Iris predefinito e quindi inserisce i dati nella **iris_data** tabella.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Se si ha familiarità con T-SQL, tenere presente che l'istruzione INSERT inserisce solo nuovi dati. non verificare la presenza di dati esistenti, o eliminare e ricompilare la tabella. Per evitare di ricevere più copie degli stessi dati in una tabella, è possibile eseguire questa istruzione prima di tutto: `TRUNCATE TABLE iris_data`. L'istruzione T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) istruzione elimina i dati esistenti ma mantiene intatte la struttura della tabella.

    > [!TIP]
    > Per modificare la stored procedure in un secondo momento, non devi rimuoverla e ricrearla. Usare la [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) istruzione. 


## <a name="query-the-data"></a>Eseguire query sui dati

Come passaggio di convalida, eseguire una query per verificare che i dati è stati caricati.

1. In Esplora oggetti, nel database, fare doppio clic il **irissql** , del database e avviare una nuova query.

2. Eseguire alcune semplici query:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>Passaggi successivi

Nella seguente Guida introduttiva, si verrà creare un modello di machine learning e salvarlo in una tabella e quindi usare il modello per generare i risultati stimati.

+ [Guida introduttiva: Creare, eseguire il training e usare un modello Python con le stored procedure in SQL Server](quickstart-python-train-score-in-tsql.md)
