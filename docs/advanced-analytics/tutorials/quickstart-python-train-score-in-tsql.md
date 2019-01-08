---
title: Guida introduttiva per i modelli di Python per il training e le stime utilizzando stored procedure - SQL Server Machine Learning
description: Incorporare il codice Python in stored procedure SQL Server per creare, eseguire il training e usare un modello Python con il set di dati Iris classico. Salvare un modello con training per SQL Server e quindi usarlo per generare i risultati stimati.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e8bacc383eba1148c1b357c344bc483e824df99b
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046911"
---
# <a name="quickstart-create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>Guida introduttiva: Creare, eseguire il training e usare un modello Python con le stored procedure in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa Guida introduttiva tramite Python, si crea e due stored procedure. Il primo Usa il set di dati dei fiori Iris classico e genera un modello Naïve Bayes per prevedere una specie di Iris in base alle caratteristiche del fiore. La seconda procedura sia per l'assegnazione dei punteggi. Chiama il modello generato nella prima procedura per un set di stime di output. Inserire codice in una stored procedure, le operazioni sono indipendenti, riutilizzabili e richiamabile da altre stored procedure e le applicazioni client. 

Completando questa Guida introduttiva, si apprenderà:

> [!div class="checklist"]
> * Come incorporare codice Python in una stored procedure
> * Come passare gli input per il codice tramite gli input nella stored procedure
> * Come vengono usate stored procedure per rendere operativi i modelli

## <a name="prerequisites"></a>Prerequisiti

Una Guida introduttiva precedente [Python verificare esiste nel Server SQL](quickstart-python-verify.md), vengono fornite informazioni e collegamenti per la configurazione dell'ambiente di Python necessario per questa Guida introduttiva.

I dati di esempio usati in questo esercizio sono il [ **irissql** ](demo-data-iris-in-sql.md) database.

## <a name="create-a-stored-procedure-that-generates-models"></a>Creare una stored procedure che genera i modelli

Un modello comune nello sviluppo di SQL Server consiste nell'organizzare operazioni programmabile in stored procedure distinte. In questo passaggio si creerà una stored procedure che genera un modello per la stima dei risultati. 

1. Aprire una nuova finestra query in Management Studio connesso per il **irissql** database. 

    ```sql
    USE irissql
    GO
    ```

2. Copiare il codice seguente per creare una nuova stored procedure. 

   Quando viene eseguita, questa routine chiama [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) per avviare una sessione di Python. 
   
   Gli input necessari per il codice Python vengono passati come parametri di input in questa stored procedure. L'output sarà un modello con training, basato su Python **scikit-informazioni su** libreria per l'algoritmo di machine learning. 

   Questo codice viene utilizzata [ **pickle** ](https://docs.python.org/2/library/pickle.html) per serializzare il modello. Il modello verrà eseguito il training usando i dati di colonne tra 0 e 4 i **iris_data** tabella. 
   
   I parametri vedere nella seconda parte della procedura articolare dei dati di input e output dei modelli. Quanto più possibile, si desidera che il codice Python in esecuzione in una stored procedure di aver chiaramente definito gli input e output che eseguono il mapping a stored procedure input e output passato fase di esecuzione. 

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

3. Verificare che esista la stored procedure. 

   Se lo script T-SQL nel passaggio precedente è stato eseguito senza errori, una nuova stored procedure denominata **generate_iris_model** viene creato e aggiunto per il **irissql** database. È possibile trovare le stored procedure in Management Studio **Esplora oggetti**, in **programmabilità**.

## <a name="execute-the-procedure-to-create-and-train-models"></a>Eseguire la procedura per creare ed eseguire il training di modelli

In questo passaggio, eseguire la procedura per eseguire il codice incorporato, la creazione di un modello con training e serializzato come output. I modelli archiviati per il riutilizzo in SQL Server sono serializzati come un flusso di byte e archiviati in una colonna varbinary (max) in una tabella di database. Una volta il modello viene creato, sottoposto a training, serializzato e salvato in un database, può essere chiamato tramite altre procedure. exe o la [stimare T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) funzione nell'assegnazione dei punteggi dei carichi di lavoro.

1. Copiare il codice seguente per eseguire la procedura. L'istruzione specifico per l'esecuzione di una stored procedure è `EXEC` nella quinta riga.

   Questo particolare script elimina un modello esistente con lo stesso nome ("Naive Bayes") per liberare spazio per nuovi file creati eseguendo nuovamente la stessa procedura. Senza l'eliminazione del modello, si verifica un errore che indica che l'oggetto esiste già. Il modello viene archiviato in una tabella denominata **iris_models**, il provisioning di una volta creato il **irissql** database.

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. Verificare che il modello è stato inserito un altro modo per restituire un elenco dei modelli è

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **Risultati**

    | MODEL_NAME  | model |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>Creare ed eseguire una stored procedure per la generazione di stime

Ora che si hanno creati, sottoposti a training e salvato un modello, passare al passaggio successivo: creazione di una stored procedure che genera stime. Si sarà tal sp_execute_external_script chiamante per avviare Python e quindi passare nello script Python che carica un modello serializzato creato nell'esercizio precedente e quindi assegna per assegnare un punteggio dei dati di input.

1. Eseguire il codice seguente per creare la stored procedure che esegue l'assegnazione dei punteggi. In fase di esecuzione, questa procedura verrà caricato un modello binario, usare colonne `[1,2,3,4]` come input e specificare le colonne `[0,5,6]` come output.

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

2. Eseguire la stored procedure, fornendo il nome del modello "Naive Bayes" in modo che la procedura sa quale modello usare. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    Quando si esegue la stored procedure, viene restituito un frame Python. La seguente riga di T-SQL consente di specificare lo schema per i risultati restituiti: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`. È possibile inserire i risultati in una tabella nuova o restituirle a un'applicazione.

    ![Set di risultati di esecuzione di stored procedure](media/train-score-using-python-NB-model-results.png)

    I risultati sono 150 stime sui species utilizzando le caratteristiche giglio come input. Per la maggior parte delle osservazioni, specie stimato corrisponde a specie effettivo.

    In questo esempio è stato reso semplice usando il set di dati iris di Python per il training e assegnazione dei punteggi. Un approccio più tipico sarebbe prevedono l'esecuzione di una query SQL per ottenere i nuovi dati e che passare in Python come `InputDataSet`. 

## <a name="conclusion"></a>Conclusione

In questo esercizio, si è appreso come creare le stored procedure dedicate per diverse attività, utilizzare la stored procedure di sistema in cui ogni stored procedure [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) per avviare un processo di Python. Gli input al processo di Python vengono passati allo script sp_execute_external come parametri. Script di Python stesso sia le variabili di dati in un database di SQL Server vengono passate come input.

In genere, deve solo prevede di usare SQL Server Management Studio con raffinati codice Python e codice Python semplice che restituisce un output basato su righe. Come strumento di SQL Server Management Studio supporta i linguaggi di query simile a T-SQL e restituisce set di righe bidimensionali. Se il codice genera output visual, ad esempio un grafico a dispersione o istogramma, è necessaria un'applicazione strumento o degli utenti finali che eseguono il rendering dell'immagine.

Per alcuni sviluppatori di Python che sono abituati a scrivere script gratis gestisce una gamma di operazioni, organizzare le attività in procedure separate potrebbero sembrare non necessaria. Ma di training e di assegnazione dei punteggi dispone di diversi casi d'uso. Separandoli, è possibile inserire ogni attività nella pianificazione diversi e autorizzazioni per l'ambito all'operazione.

Allo stesso modo, è anche possibile sfruttare le funzionalità allocazione delle risorse di SQL Server, ad esempio l'elaborazione parallela, governance delle risorse, o scrivendo script per l'uso in algoritmi [revoscalepy](../python/ref-py-revoscalepy.md) oppure [microsoftml](../python/ref-py-microsoftml.md) che supporto per lo streaming e l'esecuzione parallela. Separando i set di training e assegnazione dei punteggi, è possibile destinare le ottimizzazioni per i carichi di lavoro specifici.

Un vantaggio finale è che i processi possono essere modificati usando i parametri. In questo esercizio, codice Python che è stato creato il modello, denominato "Naive Bayes" in questo esempio, è stato passato come input per una seconda stored procedure che chiama il modello in un processo di assegnazione dei punteggi. Questo esercizio Usa solo un modello, ma si può immaginare come definizione di parametri per il modello in un'attività di assegnazione dei punteggi renderebbe lo script più utile.

## <a name="next-steps"></a>Passaggi successivi

Se si è esperti di Python di sviluppatore SQL, esaminare i passaggi e strumenti per lavorare con il codice Python in locale, con la possibilità di spostare l'esecuzione da sessioni locali a un'istanza remota di SQL Server.

> [!div class="nextstepaction"]
> [Configurare una workstation client Python](../python/setup-python-client-tools-sql.md).

