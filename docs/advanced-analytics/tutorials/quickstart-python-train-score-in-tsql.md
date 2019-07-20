---
title: Guida introduttiva ai modelli Python per il training e le stime mediante stored procedure
description: Incorporare il codice Python in SQL Server stored procedure per creare, eseguire il training e usare un modello Python con il set di dati Iris classico. Salvare un modello sottoposto a training in SQL Server, quindi utilizzarlo per generare risultati stimati.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c2c36c5aa81da098064885fd5b006d78494cd962
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345768"
---
# <a name="quickstart-create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>Avvio rapido: Creare, eseguire il training e usare un modello Python con stored procedure in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa Guida introduttiva con Python si creeranno ed eseguiranno due stored procedure. Il primo usa il set di dati del fiore Iris classico e genera un modello Naive Bayes per stimare una specie di Iris in base alle caratteristiche floreali. La seconda procedura riguarda l'assegnazione dei punteggi. Chiama il modello generato nella prima procedura per restituire un set di stime. Inserendo il codice in un stored procedure, le operazioni sono contenute, riutilizzabili e richiamabili da altre stored procedure e applicazioni client. 

Completando questa Guida introduttiva, si apprenderà:

> [!div class="checklist"]
> * Come incorporare il codice Python in un stored procedure
> * Come passare input al codice tramite input nel stored procedure
> * Modalità di utilizzo delle stored procedure per rendere operativo i modelli

## <a name="prerequisites"></a>Prerequisiti

Una guida introduttiva precedente, [Verify Python exists in SQL Server](quickstart-python-verify.md), fornisce informazioni e collegamenti per la configurazione dell'ambiente Python necessario per questa Guida introduttiva.

I dati di esempio usati in questo esercizio sono il database [**irissql**](demo-data-iris-in-sql.md) .

## <a name="create-a-stored-procedure-that-generates-models"></a>Creazione di un stored procedure che genera modelli

Un modello comune nello sviluppo SQL Server consiste nell'organizzare operazioni programmabili in stored procedure distinte. In questo passaggio verrà creato un stored procedure che genera un modello per la stima dei risultati. 

1. Aprire una nuova finestra di query in Management Studio, connessa al database **irissql** . 

    ```sql
    USE irissql
    GO
    ```

2. Copiare il codice seguente per creare una nuova stored procedure. 

   Quando viene eseguita, questa procedura chiama [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) per avviare una sessione di Python. 
   
   Gli input necessari per il codice Python vengono passati come parametri di input in questa stored procedure. L'output sarà un modello sottoposto a training, basato sulla libreria Python **Scikit-learn** per l'algoritmo di machine learning. 

   Questo codice usa [**Pickle**](https://docs.python.org/2/library/pickle.html) per serializzare il modello. Verrà eseguito il training del modello utilizzando i dati dalle colonne da 0 a 4 della tabella **iris_data** . 
   
   I parametri visualizzati nella seconda parte della procedura articolano gli input e gli output dei modelli. Per quanto possibile, si vuole che il codice Python in esecuzione in un stored procedure disponga di input e output chiaramente definiti che eseguono il mapping a stored procedure input e output passati in fase di esecuzione. 

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]].values.ravel()))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

3. Verificare che il stored procedure esista. 

   Se lo script T-SQL del passaggio precedente è stato eseguito senza errori, viene creato un nuovo stored procedure denominato **generate_iris_model** che viene aggiunto al database **irissql** . È possibile trovare stored procedure nel **Esplora oggetti**di Management Studio, in **programmabilità**.

## <a name="execute-the-procedure-to-create-and-train-models"></a>Eseguire la procedura per creare ed eseguire il training dei modelli

In questo passaggio, eseguire la procedura per eseguire il codice incorporato, creando un modello sottoposto a training e serializzato come output. I modelli archiviati per il riutilizzo in SQL Server vengono serializzati come flusso di byte e archiviati in una colonna VARBINARY (MAX) in una tabella di database. Una volta che il modello viene creato, sottoposto a training, serializzato e salvato in un database, può essere chiamato da altre procedure o dalla funzione di [stima T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) nei carichi di lavoro di assegnazione dei punteggi.

1. Copiare il codice seguente per eseguire la procedura. L'istruzione specifica per l'esecuzione di un stored procedure `EXEC` è nella quinta riga.

   Questo particolare script Elimina un modello esistente con lo stesso nome ("Naive Bayes") per creare spazio per i nuovi creati rieseguendo la stessa procedura. Senza l'eliminazione del modello, si verifica un errore che indica che l'oggetto esiste già. Il modello viene archiviato in una tabella denominata **iris_models**, sottoposta a provisioning al momento della creazione del database **irissql** .

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. Verificare che il modello sia stato inserito in un altro modo per restituire un elenco di modelli

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **Risultati**

    | model_name  | model |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>Creazione ed esecuzione di un stored procedure per la generazione di stime

Ora che è stato creato, sottoposto a training e salvato un modello, procedere con il passaggio successivo: creazione di un stored procedure che genera stime. A tale scopo, chiamare sp_execute_external_script per avviare Python, quindi passare uno script Python che carica un modello serializzato creato nell'ultimo esercizio e quindi assegna gli input di dati ai punteggi.

1. Eseguire il codice seguente per creare la stored procedure che esegue il punteggio. In fase di esecuzione, questa procedura caricherà un modello binario, utilizzerà `[1,2,3,4]` le colonne come input e specificherà le colonne `[0,5,6]` come output.

    ```sql
    CREATE PROCEDURE predict_species (@model varchar(100))
    AS
    BEGIN
    DECLARE @nb_model varbinary(max) = (SELECT model FROM iris_models WHERE model_name = @model);
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    import pickle
    irismodel = pickle.loads(nb_model)
    species_pred = irismodel.predict(iris_data[[1,2,3,4]])
    iris_data["PredictedSpecies"] = species_pred
    OutputDataSet = iris_data[[0,5,6]] 
    print(OutputDataSet)
    '
    , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@nb_model varbinary(max)'
    , @nb_model = @nb_model
    WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));
    END;
    GO
    ```

2. Eseguire il stored procedure, assegnando il nome del modello "Naive Bayes" in modo che la procedura conosca il modello da usare. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    Quando si esegue il stored procedure, viene restituito un frame di dati Python. Questa riga di T-SQL specifica lo schema per i risultati restituiti: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`. È possibile inserire i risultati in una nuova tabella o restituirli a un'applicazione.

    ![Set di risultati dall'esecuzione stored procedure](media/train-score-using-python-NB-model-results.png)

    I risultati sono stime 150 sulle specie che usano le caratteristiche floreali come input. Per la maggior parte delle osservazioni, le specie stimate corrispondono alla specie effettiva.

    Questo esempio è stato reso semplice usando il set di dati Python Iris per il training e l'assegnazione dei punteggi. Un approccio più comune consiste nell'eseguire una query SQL per ottenere i nuovi dati e passarli in Python come `InputDataSet`. 

## <a name="conclusion"></a>Conclusione

In questo esercizio si è appreso come creare stored procedure dedicate a diverse attività, in cui ogni stored procedure ha usato il sistema stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) per avviare un processo Python. Gli input per il processo Python vengono passati allo script sp_execute_external come parametri. Sia lo script Python che le variabili di dati in un database di SQL Server vengono passati come input.

In genere, è consigliabile pianificare l'uso di SSMS con codice Python lucido o codice Python semplice che restituisce output basato su riga. Come strumento, SSMS supporta linguaggi di query come T-SQL e restituisce set di righe bidimensionali. Se il codice genera un output visivo come scatterplot o istogramma, è necessario uno strumento o un'applicazione dell'utente finale in grado di eseguire il rendering dell'immagine.

Per alcuni sviluppatori Python utilizzati per la scrittura di tutti gli script inclusivi che gestiscono una serie di operazioni, l'organizzazione di attività in procedure separate potrebbe sembrare superflua. Tuttavia, il training e l'assegnazione dei punteggi hanno diversi casi d'uso. Separando tali attività, è possibile impostare le autorizzazioni per l'esecuzione di ogni attività su una pianificazione e un ambito differenti.

Analogamente, è anche possibile sfruttare le funzionalità di Resourcing di SQL Server, ad esempio l'elaborazione parallela, la governance delle risorse o la scrittura dello script per l'uso di algoritmi in [revoscalepy](../python/ref-py-revoscalepy.md) o [microsoftml](../python/ref-py-microsoftml.md) che supportano il flusso e l'esecuzione parallela. Separando il training e il punteggio, è possibile fare riferimento alle ottimizzazioni per carichi di lavoro specifici.

Un vantaggio finale è che i processi possono essere modificati usando i parametri. In questo esercizio, il codice Python che ha creato il modello (denominato "Naive Bayes" in questo esempio) è stato passato come input a un secondo stored procedure chiamare il modello in un processo di assegnazione dei punteggi. Questo esercizio usa solo un modello, ma è possibile immaginare come parametrizzazione il modello in un'attività di assegnazione dei punteggi renda lo script più utile.

## <a name="next-steps"></a>Passaggi successivi

Se si ha una nuova versione di Python per sviluppatori SQL, rivedere i passaggi e gli strumenti per usare il codice Python localmente, con la possibilità di spostare l'esecuzione da sessioni locali a un'istanza di SQL Server remota.

> [!div class="nextstepaction"]
> [Configurare una workstation client Python](../python/setup-python-client-tools-sql.md).

