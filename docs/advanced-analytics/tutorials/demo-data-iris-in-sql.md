---
title: Set di dati demo Iris per le esercitazioni su Python e R
Description: Creare un database contenente il set di dati Iris e una tabella per archiviare i modelli. Questo set di dati viene usato in esercizi che illustrano come eseguire il wrapping del linguaggio R o del codice Python in un SQL Server stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5050fc0d0fcbb6c70b7aabea1b67d75cc686b96b
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345230"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>Dati demo di Iris per le esercitazioni su Python e R in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questo esercizio viene creato un database di SQL Server per archiviare i dati dal [set di dati del fiore Iris](https://en.wikipedia.org/wiki/Iris_flower_data_set) e i modelli basati sugli stessi dati. I dati Iris sono inclusi nelle distribuzioni R e Python installate da SQL Server e vengono usati nelle esercitazioni di machine learning per SQL Server. 

Per completare questo esercizio, è necessario disporre di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) o un altro strumento in grado di eseguire query T-SQL.

Le esercitazioni e le guide introduttive che usano questo set di dati includono quanto segue:

+  [Avvio rapido: Creare, eseguire il training e usare un modello Python con stored procedure in SQL Server](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>Creare il database

1. Avviare SQL Server Management Studio e aprire una nuova finestra **query** .  

2. Creare un nuovo database per questo progetto e modificare il contesto della finestra di **query** in modo da utilizzare il nuovo database.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > Se non si ha familiarità con SQL Server o si sta lavorando a un server di cui si è proprietari, un errore comune è quello di eseguire l'accesso e iniziare a lavorare senza accorgersi che ci si trova nel database **Master** . Per assicurarsi di utilizzare il database corretto, specificare sempre il contesto utilizzando l' `USE <database name>` istruzione (ad esempio, `use irissql`).

3. Aggiungere alcune tabelle vuote: una per archiviare i dati e l'altra per archiviare i modelli sottoposti a training. La tabella **iris_models** viene utilizzata per archiviare i modelli serializzati generati in altri esercizi.

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
    > Se non si ha familiarità con T-SQL, si paga per memorizzare `DROP...IF` l'istruzione. Quando si tenta di creare una tabella e ne esiste già una, SQL Server restituisce un errore: "Esiste già un oggetto denominato" iris_data "nel database". Un modo per evitare tali errori consiste nell'eliminare tutte le tabelle esistenti o altri oggetti come parte del codice.

4. Eseguire il codice seguente per creare la tabella utilizzata per archiviare il modello sottoposto a training. Per salvare i modelli Python (o R) in SQL Server, è necessario serializzarli e archiviarli in una colonna di tipo **varbinary (max)** . 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Oltre al contenuto del modello, in genere è possibile aggiungere colonne per altri metadati utili, ad esempio il nome del modello, la data di training, l'algoritmo di origine e i parametri, i dati di origine e così via. Per il momento si manterrà semplice e si userà solo il nome del modello.

## <a name="populate-the-table"></a>Popolare la tabella

È possibile ottenere dati Iris incorporati da R o Python. È possibile usare Python o R per caricare i dati in un frame di dati e quindi inserirli in una tabella del database. Lo stato di trasferimento dei dati di training da una sessione esterna in una tabella SQL Server è un processo in più passaggi:

+ Progettare un stored procedure che ottenga i dati desiderati.
+ Eseguire l'stored procedure per ottenere effettivamente i dati.
+ Costruire un'istruzione INSERT per specificare dove salvare i dati recuperati.

1. Nei sistemi con integrazione con Python creare i stored procedure seguenti che usano il codice Python per caricare i dati.

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

    Quando si esegue questo codice, viene ricevuto il messaggio "i comandi sono stati completati". Ciò significa che il stored procedure è stato creato in base alle specifiche.

2. In alternativa, nei sistemi con integrazione R creare una procedura che usi R.

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

3. Per popolare effettivamente la tabella, eseguire il stored procedure e specificare la tabella in cui devono essere scritti i dati. Quando viene eseguito, il stored procedure esegue il codice Python o R, che carica il set di dati Iris incorporato, quindi inserisce i dati nella tabella **iris_data** .

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Se non si ha familiarità con T-SQL, tenere presente che l'istruzione INSERT aggiunge solo nuovi dati; non verifica la presenza di dati esistenti o Elimina e ricompila la tabella. Per evitare di ottenere più copie degli stessi dati in una tabella, è possibile eseguire prima questa istruzione: `TRUNCATE TABLE iris_data`. L'istruzione T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) Elimina i dati esistenti ma mantiene intatta la struttura della tabella.

    > [!TIP]
    > Per modificare il stored procedure in un secondo momento, non è necessario eliminarlo e ricrearlo. Utilizzare l'istruzione [alter procedure](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) . 


## <a name="query-the-data"></a>Eseguire query sui dati

Come passaggio di convalida, eseguire una query per confermare che i dati sono stati caricati.

1. In Esplora oggetti, in database, fare clic con il pulsante destro del mouse sul database **irissql** e avviare una nuova query.

2. Eseguire alcune query semplici:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>Passaggi successivi

Nella Guida introduttiva seguente si creerà un modello di apprendimento automatico e lo si salverà in una tabella, quindi si userà il modello per generare risultati stimati.

+ [Avvio rapido: Creare, eseguire il training e usare un modello Python con stored procedure in SQL Server](quickstart-python-train-score-in-tsql.md)
