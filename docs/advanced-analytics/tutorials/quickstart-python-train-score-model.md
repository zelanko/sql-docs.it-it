---
title: Creare e assegnare punteggi a un modello predittivo in Python
titleSuffix: SQL Server Machine Learning Services
description: Creare un modello predittivo semplice in Python usando SQL Server Machine Learning Services, quindi stimare un risultato usando nuovi dati.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/14/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cb564d7dc8564b31a90a09f53aedaba953519f76
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313664"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-python-with-sql-server-machine-learning-services"></a>Avvio rapido: Creare e assegnare un punteggio a un modello predittivo in Python con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa Guida introduttiva si creerà e si eseguirà il training di un modello predittivo usando Python, si salverà il modello in una tabella nell'istanza di SQL Server, quindi si userà il modello per stimare i valori dei nuovi dati usando [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

Verranno create ed eseguite due stored procedure in esecuzione in SQL. Il primo usa il set di dati del fiore Iris classico e genera un modello Naive Bayes per stimare una specie di Iris in base alle caratteristiche floreali. La seconda procedura riguarda l'assegnazione dei punteggi: chiama il modello generato nella prima procedura per restituire un set di stime in base ai nuovi dati. Inserendo il codice in un stored procedure, le operazioni sono contenute, riutilizzabili e richiamabili da altre stored procedure e applicazioni client.

Completando questa Guida introduttiva, si apprenderà:

> [!div class="checklist"]
> - Come incorporare il codice Python in un stored procedure
> - Come passare input al codice tramite input nel stored procedure
> - Modalità di utilizzo delle stored procedure per rendere operativo i modelli

## <a name="prerequisites"></a>Prerequisiti

- Questa Guida introduttiva richiede l'accesso a un'istanza di SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con il linguaggio Python installato.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script Python. È possibile eseguire questi script utilizzando qualsiasi strumento di gestione del database o query, purché sia possibile connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o stored procedure. Questa Guida introduttiva usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

- I dati di esempio usati in questo esercizio sono i dati di esempio Iris. Seguire le istruzioni in [Iris Demo Data](demo-data-iris-in-sql.md) per creare il database di esempio **irissql**.

## <a name="create-a-stored-procedure-that-generates-models"></a>Creazione di un stored procedure che genera modelli

In questo passaggio verrà creato un stored procedure che genera un modello per la stima dei risultati.

1. Aprire una nuova finestra di query in SSMS connessa al database **irissql** . 

    ```sql
    USE irissql
    GO
    ```

1. Copiare il codice seguente per creare una nuova stored procedure.

   Quando viene eseguita, questa procedura chiama [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) per avviare una sessione di Python. 
   
   Gli input necessari per il codice Python vengono passati come parametri di input in questa stored procedure. L'output sarà un modello sottoposto a training, basato sulla libreria Python **Scikit-learn** per l'algoritmo di machine learning. 

   Questo codice usa [**Pickle**](https://docs.python.org/2/library/pickle.html) per serializzare il modello. Verrà eseguito il training del modello utilizzando i dati dalle colonne da 0 a 4 della tabella **iris_data** . 
   
   I parametri visualizzati nella seconda parte della procedura articolano gli input e gli output dei modelli. Per quanto possibile, si vuole che il codice Python in esecuzione in un stored procedure disponga di input e output chiaramente definiti che eseguono il mapping a stored procedure input e output passati in fase di esecuzione.

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model VARBINARY(max) OUTPUT)
    AS
    BEGIN
        EXECUTE sp_execute_external_script @language = N'Python'
            , @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]], iris_data[["SpeciesId"]].values.ravel()))
    '
            , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
            , @input_data_1_name = N'iris_data'
            , @params = N'@trained_model varbinary(max) OUTPUT'
            , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

1. Verificare che il stored procedure esista. 

   Se lo script T-SQL del passaggio precedente è stato eseguito senza errori, viene creato un nuovo stored procedure denominato **generate_iris_model** che viene aggiunto al database **irissql** . È possibile trovare stored procedure nel **Esplora oggetti**di SSMS, in **programmabilità**.

## <a name="execute-the-procedure-to-create-and-train-models"></a>Eseguire la procedura per creare ed eseguire il training dei modelli

In questo passaggio viene eseguita la procedura per eseguire il codice incorporato, creando un modello sottoposto a training e serializzato come output. 

I modelli archiviati per il riutilizzo in SQL Server vengono serializzati come flusso di byte e archiviati in una colonna VARBINARY (MAX) in una tabella di database. Una volta che il modello viene creato, sottoposto a training, serializzato e salvato in un database, può essere chiamato da altre procedure o dalla funzione di [stima T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) nei carichi di lavoro di assegnazione dei punteggi.

1. Eseguire lo script seguente per eseguire la procedura. L'istruzione specifica per l'esecuzione di un stored procedure è `EXECUTE` nella quarta riga.

   Questo particolare script Elimina un modello esistente con lo stesso nome ("Naive Bayes") per creare spazio per i nuovi creati rieseguendo la stessa procedura. Senza l'eliminazione del modello, si verifica un errore che indica che l'oggetto esiste già. Il modello viene archiviato in una tabella denominata **iris_models**, sottoposta a provisioning al momento della creazione del database **irissql** .

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXECUTE generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

1. Verificare che il modello sia stato inserito.

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **Risultati**

    | model_name  | model |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>Creazione ed esecuzione di un stored procedure per la generazione di stime

Ora che è stato creato, sottoposto a training e salvato un modello, procedere con il passaggio successivo: creazione di un stored procedure che genera stime. Questa operazione viene eseguita chiamando `sp_execute_external_script` per eseguire uno script Python che carica il modello serializzato e fornisce nuovi input di dati per il punteggio.

1. Eseguire il codice seguente per creare la stored procedure che esegue il punteggio. In fase di esecuzione, questa procedura caricherà un modello binario, utilizzerà le colonne `[1,2,3,4]` come input e specificherà le colonne `[0,5,6]` come output.

   ```sql
   CREATE PROCEDURE predict_species (@model VARCHAR(100))
   AS
   BEGIN
       DECLARE @nb_model VARBINARY(max) = (
               SELECT model
               FROM iris_models
               WHERE model_name = @model
               );
   
       EXECUTE sp_execute_external_script @language = N'Python'
           , @script = N'
   import pickle
   irismodel = pickle.loads(nb_model)
   species_pred = irismodel.predict(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]])
   iris_data["PredictedSpecies"] = species_pred
   OutputDataSet = iris_data[["id","SpeciesId","PredictedSpecies"]] 
   print(OutputDataSet)
   '
           , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
           , @input_data_1_name = N'iris_data'
           , @params = N'@nb_model varbinary(max)'
           , @nb_model = @nb_model
       WITH RESULT SETS((
                   "id" INT
                 , "SpeciesId" INT
                 , "SpeciesId.Predicted" INT
                   ));
   END;
   GO
   ```

2. Eseguire il stored procedure, assegnando il nome del modello "Naive Bayes" in modo che la procedura conosca il modello da usare.

   ```sql
   EXECUTE predict_species 'Naive Bayes';
   GO
   ```

   Quando si esegue il stored procedure, viene restituito un frame di dati Python. Questa riga di T-SQL specifica lo schema per i risultati restituiti: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`. È possibile inserire i risultati in una nuova tabella o restituirli a un'applicazione.

   ![Set di risultati dall'esecuzione stored procedure](media/train-score-using-python-NB-model-results.png)

   I risultati sono stime 150 sulle specie che usano le caratteristiche floreali come input. Per la maggior parte delle osservazioni, le specie stimate corrispondono alla specie effettiva.

   Questo esempio è stato reso semplice usando il set di dati Python Iris per il training e l'assegnazione dei punteggi. Un approccio più comune consiste nell'eseguire una query SQL per ottenere i nuovi dati e passarli in Python come `InputDataSet`.

## <a name="conclusion"></a>Conclusione

In questo esercizio si è appreso come creare stored procedure dedicate a diverse attività, in cui ogni stored procedure ha usato il sistema stored procedure `sp_execute_external_script` per avviare un processo Python. Gli input per il processo Python vengono passati a `sp_execute_external` come parametri. Sia lo script Python che le variabili di dati in un database di SQL Server vengono passati come input.

In genere, è consigliabile pianificare l'uso di SSMS con codice Python lucido o codice Python semplice che restituisce output basato su riga. Come strumento, SSMS supporta linguaggi di query come T-SQL e restituisce set di righe bidimensionali. Se il codice genera un output visivo come scatterplot o istogramma, è necessario uno strumento o un'applicazione dell'utente finale in grado di eseguire il rendering dell'immagine.

Per alcuni sviluppatori Python utilizzati per la scrittura di tutti gli script inclusivi che gestiscono una serie di operazioni, l'organizzazione di attività in procedure separate potrebbe sembrare superflua. Tuttavia, il training e l'assegnazione dei punteggi hanno diversi casi d'uso. Separando questi elementi, è possibile inserire ogni attività in base a una pianificazione e autorizzazioni per l'ambito diverse per ogni operazione.

Analogamente, è anche possibile sfruttare le funzionalità di Resourcing di SQL Server, ad esempio l'elaborazione parallela, la governance delle risorse o la scrittura dello script per l'uso di algoritmi in [microsoftml](../python/ref-py-microsoftml.md) che supporta l'esecuzione di flussi e paralleli. Separando il training e il punteggio, è possibile fare riferimento alle ottimizzazioni per carichi di lavoro specifici.

Un vantaggio finale è che i processi possono essere modificati usando i parametri. In questo esercizio, il codice Python che ha creato il modello (denominato "Naive Bayes" in questo esempio) è stato passato come input a un secondo stored procedure chiamare il modello in un processo di assegnazione dei punteggi. Questo esercizio usa solo un modello, ma è possibile immaginare come parametrizzazione il modello in un'attività di assegnazione dei punteggi renda lo script più utile.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su SQL Server Machine Learning Services, vedere:

- [Che cos'è SQL Server Machine Learning Services (Python e R)?](../what-is-sql-server-machine-learning.md)
