---
title: Guida introduttiva per la stima dal modello usando R - SQL Server Machine Learning
description: In questa Guida introduttiva, informazioni sull'assegnazione del punteggio utilizzando un modello predefinito nei dati di R e SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 00fdcb0c8c9c535645268a0212e52eef6f7c88f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961991"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>Avvio rapido: Stima dal modello usando R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa Guida introduttiva, usare il modello creato nella precedente Guida introduttiva per assegnare un punteggio stime basate su dati aggiornati. Per eseguire _assegnazione di punteggi_ usando nuovi dati, ottenere uno dei modelli con training dalla tabella e quindi chiamare un nuovo set di dati su cui basare le stime. Assegnazione dei punteggi è un termine usato talvolta in analisi scientifica dei dati per indicare la generazione di stime, le probabilità o altri valori in base a nuovi dati inseriti in un modello con training.

## <a name="prerequisites"></a>Prerequisiti

Questa Guida introduttiva è un'estensione della [creare un modello predittivo](quickstart-r-create-predictive-model.md).

## <a name="create-the-table-of-new-data"></a>Creare la tabella di nuovi dati

In primo luogo, creare una tabella con i nuovi dati. 

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

## <a name="predict-manual-transmission"></a>Stimare la trasmissione manuale

A questo punto il `dbo.GLM_models` tabella potrebbe contenere più modelli R, tutti compilati usando parametri o algoritmi, diversi o sottoposti a training su subset diversi di dati.

Per ottenere stime basate su un modello specifico, è necessario scrivere uno script SQL che esegue le operazioni seguenti:

1. Ottiene il modello desiderato
2. Ottiene i nuovi dati di input
3. Chiama una funzione di stima R compatibile con tale modello

In questo esempio, si userà il modello denominato `default model`.

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

+ Nell'esempio di `str` (funzione) viene aggiunto durante la fase di test per verificare lo schema dei dati restituiti da R. È possibile rimuovere l'istruzione in un secondo momento.

+ I nomi delle colonne usate nello script R non vengono necessariamente passati all'output della stored procedure. È qui abbiamo utilizzato la clausola WITH RESULTS per definire alcuni nuovi nomi di colonna.

**Risultati**

![Set di risultati per stimare properbility della trasmissione manuale](./media/r-predict-am-resultset.png)

È anche possibile usare la [PREDICT in Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) per generare un valore stimato o un punteggio in base a un modello archiviato.

## <a name="next-steps"></a>Passaggi successivi

L'integrazione di R con SQL Server rende più semplice distribuire soluzioni R su larga scala, sfruttando le funzionalità migliori di R e dei database relazionali, per una gestione dei dati a prestazioni elevate e un'analisi R più rapida. 

Altre informazioni sulle soluzioni R con SQL Server tramite scenari end-to-end creati dai team di sviluppo Microsoft Data Science e R Services.

> [!div class="nextstepaction"]
> [Esercitazioni di SQL Server R](sql-server-r-tutorials.md)
