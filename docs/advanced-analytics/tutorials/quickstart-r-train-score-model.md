---
title: Creare e assegnare un punteggio a un modello predittivo in R
titleSuffix: SQL Server Machine Learning Services
description: Creare un modello predittivo semplice in R usando SQL Server Machine Learning Services, quindi stimare un risultato usando nuovi dati.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fc968c9364f23826b366721590f72ac1b0af0391
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005974"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>Avvio rapido: Creare e assegnare un punteggio a un modello predittivo in R con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa Guida introduttiva si creerà e si eseguirà il training di un modello predittivo usando R, si salverà il modello in una tabella nell'istanza di SQL Server, quindi si userà il modello per stimare i valori dei nuovi dati usando [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

Il modello che verrà usato in questa Guida introduttiva è un semplice modello lineare generalizzato (GLM) che consente di stimare la probabilità che un veicolo sia stato dotato di una trasmissione manuale. Si userà il set di dati **mtcars** incluso in R.

> [!TIP]
> Se è necessario un aggiornamento sui modelli lineari, provare questa esercitazione che descrive il processo di adattamento di un modello usando rxLinMod:  [Fitting Linear Models](/machine-learning-server/r/how-to-revoscaler-linear-model) (Adattamento di modelli lineari)

## <a name="prerequisites"></a>Prerequisiti

- Questa Guida introduttiva richiede l'accesso a un'istanza di SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con il linguaggio R installato.

  L'istanza di SQL Server può trovarsi in una macchina virtuale di Azure o in locale. È sufficiente tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, pertanto potrebbe essere necessario abilitare l'esecuzione di [script esterni](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che **launchpad di SQL Server servizio** sia in esecuzione prima di iniziare.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script R. È possibile eseguire questi script utilizzando qualsiasi strumento di gestione del database o query, purché sia possibile connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o stored procedure. Questa Guida introduttiva usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-the-model"></a>Creare il modello

Per creare il modello, è necessario creare dati di origine per il training, creare il modello e eseguirne il training usando i dati, quindi archiviare il modello in un database SQL in cui può essere usato per generare stime con nuovi dati.

### <a name="create-the-source-data"></a>Creare i dati di origine

1. Aprire **SQL Server Management Studio** e connettersi all'istanza di SQL Server.

1. Creare una tabella per salvare i dati di training.

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
   > Nel runtime R sono inclusi diversi set di dati di piccole e grandi dimensioni. Per ottenere un elenco dei set di impostazioni installati con R, digitare `library(help="datasets")` da un prompt dei comandi di R.

### <a name="create-and-train-the-model"></a>Creare ed eseguire il training del modello

I dati relativi alla velocità dell'auto contengono due colonne, sia numeric: potenza (`hp`) che Weight (`wt`). Da questi dati verrà creato un modello lineare generalizzato (GLM) che stima la probabilità che un veicolo sia stato dotato di una trasmissione manuale.

Per compilare il modello, è necessario definire la formula all'interno del codice R e passare i dati come parametro di input.

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

- Il primo argomento per `glm` è il parametro della *Formula* , che definisce `am` come dipendente da `hp + wt`.
- I dati di input vengono archiviati nella variabile `MTCarsData`, popolata dalla query SQL. Se non si assegna un nome specifico ai dati di input, il nome predefinito della variabile sarà _InputDataSet_.

### <a name="store-the-model-in-the-sql-database"></a>Archiviare il modello nel database SQL

Successivamente, archiviare il modello in un database SQL per poterlo utilizzare per la stima o ripetere il training. 

1. Creare una tabella per archiviare il modello.

   L'output di un pacchetto R che crea un modello è in genere un oggetto binario. La tabella in cui è archiviato il modello deve pertanto fornire una colonna di tipo **varbinary (max)** .

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. Eseguire l'istruzione Transact-SQL seguente per chiamare il stored procedure, generare il modello e salvarlo nella tabella creata.

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > Se si esegue questo codice una seconda volta, si ottiene questo errore: "Violazione del vincolo PRIMARY KEY... Impossibile inserire la chiave duplicata nell'oggetto dbo. stopping_distance_models ". Un modo per evitare questo errore consiste nell'aggiornare il nome di ogni nuovo modello. È ad esempio possibile sostituire il nome con uno più descrittivo e includere il tipo di modello, il giorno della creazione e così via.

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>Assegnare punteggi ai nuovi dati usando il modello sottoposto a training

Il *Punteggio* è un termine usato nella Data Science per indicare la generazione di stime, probabilità o altri valori in base ai nuovi dati inseriti in un modello sottoposto a training. Si userà il modello creato nella sezione precedente per assegnare punteggi alle stime rispetto ai nuovi dati.

### <a name="create-a-table-of-new-data"></a>Creare una tabella di nuovi dati

Per prima cosa, creare una tabella con nuovi dati.

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

### <a name="predict-manual-transmission"></a>Prevedere la trasmissione manuale

Per ottenere stime basate sul modello, scrivere uno script SQL che esegue le operazioni seguenti:

1. Ottiene il modello desiderato
1. Ottiene i nuovi dati di input
1. Chiama una funzione di stima R compatibile con tale modello

Nel corso del tempo, la tabella potrebbe contenere più modelli R, tutti compilati con parametri o algoritmi diversi o sottoposti a training su subset diversi di dati. In questo esempio si userà il modello denominato `default model`.

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

- Usare un'istruzione SELECT per ottenere un singolo modello dalla tabella e passarlo come parametro di input.

- Dopo avere recuperato il modello dalla tabella, chiamare la funzione `unserialize` nel modello.

- Applicare la funzione `predict` con gli argomenti appropriati al modello e fornire i nuovi dati di input.

> [!NOTE]
> Nell'esempio, la funzione `str` viene aggiunta durante la fase di test, per verificare lo schema dei dati restituiti da R. È possibile rimuovere l'istruzione in un secondo momento.
>
> I nomi di colonna usati nello script R non vengono necessariamente passati all'output del stored procedure. Qui viene utilizzata la clausola WITH RESULTs per definire nuovi nomi di colonna.

**Risultati**

![Set di risultati per la stima di properbility di trasmissione manuale](./media/r-predict-am-resultset.png)

È anche possibile usare l'istruzione [Predict (Transact-SQL)](../../t-sql/queries/predict-transact-sql.md) per generare un valore o un punteggio stimato in base a un modello archiviato.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su SQL Server Machine Learning Services, vedere:

- [Che cos'è SQL Server Machine Learning Services (Python e R)?](../what-is-sql-server-machine-learning.md)
