---
title: Guida introduttiva che mostra funzioni R-SQL Server Machine Learning
description: Questa Guida introduttiva illustra come scrivere una funzione R per un calcolo statistico avanzato.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: f43709f563d1dc5838cdd6636bcac4dc5664a6da
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469275"
---
# <a name="quickstart-using-r-functions"></a>Avvio rapido: Uso delle funzioni R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Se sono state completate le guide introduttive precedenti, si ha familiarità con le operazioni di base e si è pronti per qualcosa di più complesso, ad esempio per le funzioni statistiche. Le funzioni statistiche avanzate complesse da implementare in T-SQL possono essere eseguite in R con una sola riga di codice.

In questa Guida introduttiva verranno incorporate le funzioni matematiche e di utilità R in una stored procedure SQL Server.

## <a name="prerequisites"></a>Prerequisiti

Una guida introduttiva precedente, [Verify R exists in SQL Server](quickstart-r-verify.md), fornisce informazioni e collegamenti per la configurazione dell'ambiente R necessario per questa Guida introduttiva.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Creare una stored procedure per generare numeri casuali

Per semplicità, usare il pacchetto r `stats` , che viene installato e caricato per impostazione predefinita quando si installa il supporto della funzionalità r in SQL Server. Il pacchetto contiene centinaia di funzioni per le attività statistiche comuni, tra cui la funzione `rnorm`, che genera una quantità specificata di numeri casuali usando la distribuzione normale, in base a una deviazione e a una media standard.

Ad esempio, questo codice R restituisce 100 numeri, in una media di 50, in base alla deviazione standard 3.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

Per chiamare questa riga di codice R da T-SQL, eseguire sp_execute_external_script e aggiungere la funzione R nel parametro di script R, in questo modo:

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

Si vuole semplificare la generazione di un set diverso di numeri casuali?

Questa operazione è facile quando viene combinata con SQL Server: definire una stored procedure che ottenga gli argomenti dall'utente. Passare quindi gli argomenti nello script R come variabili.

```sql
CREATE PROCEDURE MyRNorm (@param1 int, @param2 int, @param3 int)
AS
    EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
    WITH RESULT SETS (([Density] float NOT NULL));
```

+ La prima riga definisce ognuno dei parametri di input SQL necessari quando viene eseguita la stored procedure.

+ La riga che inizia con `@params` definisce tutte le variabili usate dal codice R e i tipi di dati SQL corrispondenti.

+ Le righe immediatamente successive eseguono il mapping dei nomi dei parametri SQL ai nomi delle variabili R corrispondenti.

Dopo aver eseguito il wrapping della funzione R in una stored procedure, è possibile chiamare facilmente la funzione e passare valori diversi, in questo modo:

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>Usare funzioni di utilità R per la risoluzione dei problemi

Per impostazione predefinita, un'installazione di R include `utils` il pacchetto, che fornisce un'ampia gamma di funzioni di utilità per l'analisi dell'ambiente R corrente. Questo può essere utile se si riscontrano discrepanze nel modo in cui il codice R viene eseguito in SQL Server e in ambienti esterni.

Ad esempio, è possibile usare la funzione R `memory.limit()` per ottenere memoria per l'ambiente R corrente. Poiché il pacchetto `utils` viene installato, ma non viene caricato per impostazione predefinita, prima di tutto è necessario usare la funzione `library()` per caricarlo.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        mymemory <- memory.limit();
        OutputDataSet <- as.data.frame(mymemory);'
    , @input_data_1 = N' ;'
WITH RESULT SETS (([Col1] int not null));
```

Molti utenti vogliono usare le funzioni di temporizzazione del sistema in R, `system.time` ad `proc.time`esempio e, per acquisire il tempo usato dai processi r e analizzare i problemi di prestazioni.

Per un esempio, vedere questa esercitazione: [Creare funzionalità di dati](../tutorials/walkthrough-create-data-features.md). In questa procedura dettagliata le funzioni di temporizzazione R sono incorporate nella soluzione per confrontare le prestazioni di due metodi per la creazione di funzionalità dai dati: Confronto tra funzioni R e e funzioni T-SQL.

## <a name="next-steps"></a>Passaggi successivi

Il passaggio successivo consiste nella creazione di un modello predittivo tramite R in SQL Server.

> [!div class="nextstepaction"]
> [Avvio rapido: Creazione di un modello predittivo](quickstart-r-create-predictive-model.md)
