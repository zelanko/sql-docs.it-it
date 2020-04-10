---
title: 'Guida introduttiva: Eseguire il training di un modello in R'
description: In questo argomento di avvio rapido si creerà ed eseguirà il training di un modello predittivo con T. Il modello verrà salvato in una tabella nell'istanza di SQL Server in uso, quindi si userà il modello per stimare i valori dei nuovi dati tramite Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b6be97041912027cf284ff34c2c826a37edabe93
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116144"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>Guida introduttiva: Creare un modello predittivo e assegnare punteggi in R con Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo argomento di avvio rapido si creerà ed eseguirà il training di un modello predittivo con T. Il modello verrà salvato in una tabella nell'istanza di SQL Server in uso, quindi si userà il modello per stimare i valori dei nuovi dati tramite [Machine Learning Services per SQL Server](../what-is-sql-server-machine-learning.md).

Si creeranno due stored procedure che verranno eseguite in SQL. La prima usa il set di dati **mtcars** incluso in R e genera un modello lineare generalizzato (GLM, Generalized Linear Model) semplice che stima la probabilità che un veicolo sia dotato di trasmissione manuale. La seconda stored procedure, per l'assegnazione dei punteggi, chiama il modello generato nella prima stored procedure per restituire un set di stime basate sui nuovi dati. Inserendo il codice R in una stored procedure SQL, le operazioni sono contenute in SQL, sono riutilizzabili e possono essere chiamate da altre stored procedure e applicazioni client.

> [!TIP]
> Se è necessario rivedere le informazioni sui modelli lineari, vedere questa esercitazione che descrive il processo di adattamento di un modello tramite rxLinMod:  [Fitting Linear Models](/machine-learning-server/r/how-to-revoscaler-linear-model) (Adattamento di modelli lineari)

Completando questo argomento di avvio rapido si apprenderà:

> [!div class="checklist"]
> - Come incorporare codice R in una stored procedure
> - Come passare input al codice tramite input nella stored procedure
> - Come usare le stored procedure per rendere operativi i modelli

## <a name="prerequisites"></a>Prerequisiti

- Questo argomento di avvio rapido richiede l'accesso a un'istanza di SQL Server con [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) con il linguaggio R installato.

  L'istanza di SQL Server può essere in una macchina virtuale di Azure o in locale. Tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, quindi potrebbe essere necessario [abilitare lo scripting esterno](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che il **servizio Launchpad di SQL Server** sia in esecuzione prima di iniziare.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script R. È possibile eseguire questi script usando qualsiasi strumento di gestione del database o di query, purché possa connettersi a un'istanza di SQL Server, nonché eseguire una query T-SQL o una stored procedure. In questo argomento di avvio rapido viene usato [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-the-model"></a>Creare il modello

Per creare il modello, è necessario creare i dati di origine per il training, creare il modello ed eseguirne il training usando i dati e quindi archiviare il modello in un database SQL in cui può essere usato per generare stime con nuovi dati.

### <a name="create-the-source-data"></a>Creare i dati di origine

1. Aprire SSMS, connettersi all'istanza di SQL Server e aprire una nuova finestra di query.

1. Creare una tabella in cui salvare i dati di training.

   ```sql
   CREATE TABLE dbo.MTCars(
       mpg decimal(10, 1) NOT NULL,
       cyl int NOT NULL,
       disp decimal(10, 1) NOT NULL,
       hp int NOT NULL,
       drat decimal(10, 2) NOT NULL,
       wt decimal(10, 3) NOT NULL,
       qsec decimal(10, 2) NOT NULL,
       vs int NOT NULL,
       am int NOT NULL,
       gear int NOT NULL,
       carb int NOT NULL
   );
   ```

1. Inserire i dati dal set di dati predefinito `mtcars`.

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > Molti set di dati di piccole e grandi dimensioni sono inclusi con il runtime di R. Per ottenere un elenco dei set di dati installati con R, digitare `library(help="datasets")` da un prompt dei comandi R.

### <a name="create-and-train-the-model"></a>Creare il modello ed eseguirne il training

I dati sulla velocità delle auto contengono due colonne, entrambe numeriche, relative a cavalli vapore (`hp`) e peso (`wt`). Da questi dati si creerà un modello lineare generalizzato (GLM, Generalized Linear Model) che stima la probabilità che un veicolo sia dotato di trasmissione manuale.

Per creare il modello, si definisce la formula nel codice R e si passano i dati come parametro di input.

```sql
DROP PROCEDURE IF EXISTS generate_GLM;
GO
CREATE PROCEDURE generate_GLM
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'carsModel <- glm(formula = am ~ hp + wt, data = MTCarsData, family = binomial);
        trained_model <- data.frame(payload = as.raw(serialize(carsModel, connection=NULL)));'
    , @input_data_1 = N'SELECT hp, wt, am FROM MTCars'
    , @input_data_1_name = N'MTCarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model VARBINARY(max)));
END;
GO
```

- Il primo argomento di `glm` è il parametro *formula*, che definisce `am` come dipendente da `hp + wt`.
- I dati di input vengono archiviati nella variabile `MTCarsData`, che viene popolata dalla query SQL. Se non si assegna un nome specifico ai dati di input, il nome predefinito della variabile è _InputDataSet_.

### <a name="store-the-model-in-the-sql-database"></a>Archiviare il modello nel database SQL

Archiviare quindi il modello in un database SQL per poterlo usare per la stima o poter eseguire di nuovo il training. 

1. Creare una tabella per archiviare il modello.

   L'output di un pacchetto R che crea un modello è in genere un oggetto binario. La tabella in cui si archivia il modello deve quindi contenere una colonna di tipo **varbinary(max)** .

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. Eseguire l'istruzione Transact-SQL seguente per chiamare la stored procedure, generare il modello e salvarlo nella tabella creata.

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > Se si esegue questo codice una seconda volta, si otterrà questo errore: "Violazione del vincolo PRIMARY KEY...Impossibile inserire la chiave duplicata nell'oggetto dbo.stopping_distance_models". Un modo per evitare questo errore consiste nell'aggiornare il nome per ogni nuovo modello. Ad esempio, si può modificare il nome scegliendone uno più descrittivo e includere il tipo di modello, il giorno di creazione e così via.

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>Assegnare punteggi ai nuovi dati usando il modello sottoposto a training

L'*assegnazione dei punteggi* è un concetto di data science che indica la generazione di stime, probabilità o altri valori in base ai nuovi dati inseriti in un modello sottoposto a training. Si userà il modello creato nella sezione precedente per assegnare punteggi alle stime in base ai nuovi dati.

### <a name="create-a-table-of-new-data"></a>Creare una tabella di nuovi dati

Creare prima di tutto una tabella con nuovi dati.

```sql
CREATE TABLE dbo.NewMTCars(
    hp INT NOT NULL
    , wt DECIMAL(10,3) NOT NULL
    , am INT NULL
)
GO

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (110, 2.634)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (72, 3.435)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (220, 5.220)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (120, 2.800)
GO
```

### <a name="predict-manual-transmission"></a>Stimare la trasmissione manuale

Per ottenere stime basate su un modello specifico, scrivere uno script SQL che esegue le operazioni seguenti:

1. Ottiene il modello desiderato
1. Ottiene i nuovi dati di input
1. Chiama una funzione di stima R compatibile con tale modello

Col tempo, la tabella potrebbe contenere più modelli R, tutti creati usando parametri o algoritmi diversi o sottoposti a training su subset di dati diversi. In questo esempio viene usato il modello denominato `default model`.

```sql
DECLARE @glmmodel varbinary(max) = 
    (SELECT model FROM dbo.GLM_models WHERE model_name = 'default model');

EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(glmmodel));
            new <- data.frame(NewMTCars);
            predicted.am <- predict(current_model, new, type = "response");
            str(predicted.am);
            OutputDataSet <- cbind(new, predicted.am);
            '
    , @input_data_1 = N'SELECT hp, wt FROM dbo.NewMTCars'
    , @input_data_1_name = N'NewMTCars'
    , @params = N'@glmmodel varbinary(max)'
    , @glmmodel = @glmmodel
WITH RESULT SETS ((new_hp INT, new_wt DECIMAL(10,3), predicted_am DECIMAL(10,3)));
```

Lo script precedente esegue i passaggi seguenti:

- Usa un'istruzione SELECT per ottenere un singolo modello dalla tabella e passarlo come parametro di input.

- Dopo aver recuperato il modello dalla tabella, chiama la funzione `unserialize` sul modello.

- Applica la funzione `predict` con gli argomenti appropriati al modello e fornisce i nuovi dati di input.

> [!NOTE]
> Nell'esempio la funzione `str` viene aggiunta durante la fase di test per controllare lo schema di dati restituito da R. È sempre possibile rimuovere l'istruzione in un secondo momento.
>
> I nomi di colonna usati nello script R non vengono necessariamente passati all'output della stored procedure. Qui viene usata la clausola WITH RESULTS per definire alcuni nuovi nomi di colonna.

**Risultati**

![Set di risultati per la stima della probabilità della trasmissione manuale](./media/r-predict-am-resultset.png)

È anche possibile usare l'istruzione [PREDICT (Transact-SQL)](../../t-sql/queries/predict-transact-sql.md) per generare un punteggio o un valore stimato in base a un modello archiviato.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su Machine Learning Services per SQL Server, vedere:

- [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
