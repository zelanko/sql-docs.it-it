---
title: Set di dati demo Iris per le esercitazioni
Description: Creare un database contenente il set di dati Iris e i modelli predittivi. Questo set di dati viene usato nelle esercitazioni di R e Python per Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c87b5c9fede3a8a9ab72add650447d1b02ac89c7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "74908757"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>Dati demo Iris per le esercitazioni su Python e R in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo esercizio si creerà un database di SQL Server in cui archiviare i dati del [set di dati Iris](https://en.wikipedia.org/wiki/Iris_flower_data_set) e i modelli basati sugli stessi dati. I dati Iris sono inclusi nelle distribuzioni R e Python installate da SQL Server e vengono usati nelle esercitazioni sul machine learning per SQL Server. 

Per completare questo esercizio, è necessario avere [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) o un altro strumento in grado di eseguire query T-SQL.

Le esercitazioni e le guide di avvio rapido che usano questo set di dati includono:

+  [Avvio rapido: Creare, eseguire il training e assegnare i punteggi a un modello predittivo in Python con Machine Learning Services per SQL Server](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>Creare il database

1. Avviare SQL Server Management Studio e aprire una nuova finestra **Query**.  

2. Creare un nuovo database per questo progetto e cambiare il contesto della finestra **Query** per usare il nuovo database.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > Se non si ha familiarità con SQL Server o si sta usando un server di cui si è proprietari, un errore comune è quello di eseguire l'accesso e iniziare a lavorare senza accorgersi di essere nel **database master**. Per assicurarsi di usare il database corretto, specificare sempre il contesto usando l'istruzione `USE <database name>`, ad esempio `use irissql`.

3. Aggiungere alcune tabelle vuote: una in cui archiviare i dati e l'altra in cui archiviare i modelli sottoposti a training. La tabella **iris_models** viene usata per l'archiviazione di modelli serializzati generati in altri esercizi.

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
    > Se non si ha familiarità con T-SQL, vale la pena di memorizzare l'istruzione `DROP...IF`. Quando si cerca di creare una tabella e ne esiste già una, SQL Server restituisce un errore: "Nel database esiste già un oggetto con il nome 'iris_data'". Un modo per evitare errori di questo tipo consiste nell'eliminare eventuali tabelle o altri oggetti esistenti come parte del codice.

4. Eseguire il codice seguente per creare la tabella da usare per archiviare il modello sottoposto a training. Per salvare i modelli Python (o R) in SQL Server, è necessario serializzarli e archiviarli in una colonna di tipo **varbinary (max)** . 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Oltre al contenuto del modello, in genere è possibile aggiungere colonne per altri metadati utili, come il nome del modello, la data di training, l'algoritmo di origine e i parametri, i dati di origine e così via. Per semplicità, per il momento si userà solo il nome del modello.

## <a name="populate-the-table"></a>Popolare la tabella

È possibile ottenere dati Iris incorporati sia da R che da Python. È possibile usare Python o R per caricare i dati in un frame di dati e quindi inserirli in una tabella del database. Lo spostamento dei dati di training da una sessione esterna in una tabella di SQL Server è un processo in più passaggi:

+ Progettare una stored procedure che ottenga i dati desiderati.
+ Eseguire la stored procedure per ottenere effettivamente i dati.
+ Creare un'istruzione INSERT per specificare la posizione in cui salvare i dati recuperati.

1. Nei sistemi in cui è integrato Python creare la stored procedure seguente che usa codice Python per caricare i dati.

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

    Quando si esegue questo codice, dovrebbe essere visualizzato il messaggio "I comandi sono stati completati". Significa che la stored procedure è stata creata in base alle specifiche.

2. In alternativa, nei sistemi in cui è integrato R creare una stored procedure che usa R.

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

3. Per popolare effettivamente la tabella, eseguire la stored procedure e specificare la tabella in cui devono essere scritti i dati. Quando viene eseguita, la stored procedure esegue il codice Python o R, che carica il set di dati Iris incorporato e quindi inserisce i dati nella tabella **iris_data**.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Se non si ha familiarità con T-SQL, tenere presente che l'istruzione INSERT aggiunge semplicemente nuovi dati, non verifica la presenza di dati esistenti né elimina e ricompila la tabella. Per evitare di ottenere più copie degli stessi dati in una tabella, è possibile eseguire prima questa istruzione: `TRUNCATE TABLE iris_data`. L'istruzione T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) elimina i dati esistenti, ma mantiene intatta la struttura della tabella.

    > [!TIP]
    > Per modificare la stored procedure in un secondo momento, non è necessario eliminarla e ricrearla. Usare l'istruzione [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql). 


## <a name="query-the-data"></a>Eseguire una query sui dati

Come passaggio di convalida, eseguire una query per confermare che i dati sono stati caricati.

1. In Esplora oggetti fare clic con il pulsante destro del mouse sul database **irissql** in Database e avviare una nuova query.

2. Eseguire alcune query semplici:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>Passaggi successivi

Nella guida di avvio rapido successiva si creerà un modello di Machine Learning e lo si salverà in una tabella, quindi si userà il modello per generare risultati stimati.

+ [Avvio rapido: Creare, eseguire il training e assegnare i punteggi a un modello predittivo in Python con Machine Learning Services per SQL Server](quickstart-python-train-score-in-tsql.md)
