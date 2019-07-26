---
title: Guida introduttiva per eseguire stime dal modello usando R
description: Questa Guida introduttiva illustra come assegnare un punteggio usando un modello predefinito in R e SQL Server dati.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: aa3a65020f2900bc4d9e0b5c5fd5a200f3334435
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469333"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>Avvio rapido: Eseguire stime dal modello usando R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa Guida introduttiva, usare il modello creato nella Guida introduttiva precedente per assegnare punteggi alle stime rispetto ai dati aggiornati. Per eseguire il _Punteggio_ usando nuovi dati, ottenere uno dei modelli sottoposti a training dalla tabella e quindi chiamare un nuovo set di dati su cui basare le stime. Il Punteggio è un termine usato a volte in data science per indicare la generazione di stime, probabilità o altri valori in base ai nuovi dati inseriti in un modello sottoposto a training.

## <a name="prerequisites"></a>Prerequisiti

Questa Guida introduttiva è un'estensione della [creazione di un modello predittivo](quickstart-r-create-predictive-model.md).

## <a name="create-the-table-of-new-data"></a>Creare la tabella dei nuovi dati

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

## <a name="predict-manual-transmission"></a>Prevedere la trasmissione manuale

A questo punto, `dbo.GLM_models` la tabella potrebbe contenere più modelli R, tutti compilati con parametri o algoritmi diversi o sottoposti a training su subset diversi di dati.

Per ottenere stime basate su un modello specifico, è necessario scrivere uno script SQL che esegue le operazioni seguenti:

1. Ottiene il modello desiderato
2. Ottiene i nuovi dati di input
3. Chiama una funzione di stima R compatibile con tale modello

In questo esempio verrà usato il modello denominato `default model`.

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

+ Usare un'istruzione SELECT per ottenere un singolo modello dalla tabella e passarlo come parametro di input.

+ Dopo avere recuperato il modello dalla tabella, chiamare la funzione `unserialize` nel modello.

+ Applicare la funzione `predict` con gli argomenti appropriati al modello e fornire i nuovi dati di input.

+ Nell'esempio, la `str` funzione viene aggiunta durante la fase di test, per verificare lo schema dei dati restituiti da R. È possibile rimuovere l'istruzione in un secondo momento.

+ I nomi di colonna usati nello script R non vengono necessariamente passati all'output del stored procedure. In questa sezione è stata utilizzata la clausola WITH RESULTs per definire nuovi nomi di colonna.

**Risultati**

![Set di risultati per la stima di properbility di trasmissione manuale](./media/r-predict-am-resultset.png)

È anche possibile usare la [stima in Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) per generare un valore o un punteggio stimato in base a un modello archiviato.

## <a name="next-steps"></a>Passaggi successivi

L'integrazione di R con SQL Server rende più semplice distribuire soluzioni R su larga scala, sfruttando le funzionalità migliori di R e dei database relazionali, per una gestione dei dati a prestazioni elevate e un'analisi R più rapida. 

Continua a scoprire le soluzioni usando R con SQL Server attraverso scenari end-to-end creati dai team di sviluppo di Microsoft Data Science e R Services.

> [!div class="nextstepaction"]
> [Esercitazioni di SQL Server R](sql-server-r-tutorials.md)
