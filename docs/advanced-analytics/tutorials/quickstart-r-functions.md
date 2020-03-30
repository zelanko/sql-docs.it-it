---
title: 'Guida introduttiva: Funzioni R'
description: Questo argomento di avvio rapido descrive come usare funzioni matematiche e di utilità R con Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e67dcbc35bf5af88d2a7fab37f795cd5cc1d55d9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "76831770"
---
# <a name="quickstart-r-functions-with-sql-server-machine-learning-services"></a>Guida introduttiva: Funzioni R con Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo argomento di avvio rapido descrive come usare funzioni matematiche e di utilità R con Machine Learning Services per SQL Server. Le funzioni statistiche sono spesso complesse da implementare in T-SQL, ma possono essere eseguite in R con poche righe di codice.

## <a name="prerequisites"></a>Prerequisiti

- Questo argomento di avvio rapido richiede l'accesso a un'istanza di SQL Server con [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) con il linguaggio R installato.

  L'istanza di SQL Server può essere in una macchina virtuale di Azure o in locale. Tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, quindi potrebbe essere necessario [abilitare lo scripting esterno](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che il **servizio Launchpad di SQL Server** sia in esecuzione prima di iniziare.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script R. È possibile eseguire questi script usando qualsiasi strumento di gestione del database o di query, purché possa connettersi a un'istanza di SQL Server, nonché eseguire una query T-SQL o una stored procedure. In questo argomento di avvio rapido viene usato [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Creare una stored procedure per generare numeri casuali

Per semplicità, usare il pacchetto R `stats`, che viene installato e caricato per impostazione predefinita in Machine Learning Services per SQL Server con R installato. Il pacchetto contiene centinaia di funzioni per le attività statistiche comuni, tra cui la funzione `rnorm`, che genera una quantità specificata di numeri casuali usando la distribuzione normale, in base a una deviazione e a una media standard.

Ad esempio, il codice R seguente restituisce 100 numeri, in una media di 50, in base alla deviazione standard 3.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

Per chiamare questa riga di codice R da T-SQL, aggiungere la funzione R nel parametro di script R di `sp_execute_external_script`, come illustrato di seguito:

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

Si vuole semplificare la generazione di un set diverso di numeri casuali?

Questa operazione è facile se eseguita in combinazione con SQL Server. Si definisce una stored procedure che ottiene gli argomenti dall'utente e quindi si passano tali argomenti nello script R come variabili.

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- La prima riga definisce ognuno dei parametri di input SQL necessari quando viene eseguita la stored procedure.

- La riga che inizia con `@params` definisce tutte le variabili usate dal codice R e i tipi di dati SQL corrispondenti.

- Le righe immediatamente successive eseguono il mapping dei nomi dei parametri SQL ai nomi delle variabili R corrispondenti.

Dopo aver eseguito il wrapping della funzione R in una stored procedure, è possibile chiamare facilmente la funzione e passare valori diversi, in questo modo:

```sql
EXECUTE MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>Usare funzioni di utilità R per la risoluzione dei problemi

Il pacchetto **utils**, installato per impostazione predefinita, offre un'ampia gamma di funzioni di utilità per analizzare l'ambiente R corrente. Queste funzioni possono essere utili se si riscontrano discrepanze nell'esecuzione del codice R in SQL Server e in ambienti esterni.

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

> [!TIP]
> Molti utenti preferiscono usare le funzioni di calcolo del tempo di sistema in R, come `system.time` e `proc.time`, per acquisire il tempo usato dai processi R e analizzare i problemi di prestazioni. Per un esempio, vedere l'esercitazione [Creare caratteristiche dei dati](../tutorials/walkthrough-create-data-features.md) in cui le funzioni di calcolo del tempo R sono incorporate nella soluzione.

## <a name="next-steps"></a>Passaggi successivi

Per creare un modello di Machine Learning usando R in SQL Server, seguire questo argomento di avvio rapido:

> [!div class="nextstepaction"]
> [Creare un modello predittivo e assegnare punteggi in R con Machine Learning Services per SQL Server](quickstart-r-train-score-model.md)

Per altre informazioni su Machine Learning Services per SQL Server, vedere:

- [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
