---
title: Scrivere funzioni R avanzate
titleSuffix: SQL Server Machine Learning Services
description: Questa Guida introduttiva illustra come scrivere una funzione R per un calcolo statistico avanzato con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/03/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 55849cec8b3362b3a5f2786e007f08f0c376b8a5
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71951858"
---
# <a name="quickstart-write-advanced-r-functions-with-sql-server-machine-learning-services"></a>Avvio rapido: Scrivere funzioni R avanzate con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa Guida introduttiva descrive come incorporare funzioni matematiche e di utilità R in un stored procedure SQL con SQL Server Machine Learning Services. Le funzioni statistiche avanzate complesse da implementare in T-SQL possono essere eseguite in R con una sola riga di codice.

## <a name="prerequisites"></a>Prerequisiti

- Questa Guida introduttiva richiede l'accesso a un'istanza di SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con il linguaggio R installato.

  L'istanza di SQL Server può trovarsi in una macchina virtuale di Azure o in locale. È sufficiente tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, pertanto potrebbe essere necessario abilitare l'esecuzione di [script esterni](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che **launchpad di SQL Server servizio** sia in esecuzione prima di iniziare.

- È anche necessario uno strumento per l'esecuzione di query SQL che contengono script R. È possibile eseguire questi script utilizzando qualsiasi strumento di gestione del database o query, purché sia possibile connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o stored procedure. Questa Guida introduttiva usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Creare una stored procedure per generare numeri casuali

Per semplicità, usare il pacchetto r `stats` , installato e caricato per impostazione predefinita in SQL Server Machine Learning Services con R installato. Il pacchetto contiene centinaia di funzioni per le attività statistiche comuni, tra cui la funzione `rnorm`, che genera una quantità specificata di numeri casuali usando la distribuzione normale, in base a una deviazione e a una media standard.

Ad esempio, il codice R seguente restituisce 100 numeri su una media di 50, data una deviazione standard di 3.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

Per chiamare questa riga di r da T-SQL, aggiungere la funzione r nel parametro di script r di `sp_execute_external_script`, come segue:

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

Si vuole semplificare la generazione di un set diverso di numeri casuali?

Questa operazione è facile se combinata con SQL Server. Definire un stored procedure che ottiene gli argomenti dall'utente, quindi passarli nello script R come variabili.

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

Il pacchetto **utils** , installato per impostazione predefinita, offre un'ampia gamma di funzioni di utilità per l'analisi dell'ambiente R corrente. Queste funzioni possono essere utili se si individuano discrepanze nel modo in cui il codice R viene eseguito in SQL Server e in ambienti esterni.

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
> Molti utenti vogliono usare le funzioni di temporizzazione del sistema in R, `system.time` ad `proc.time`esempio e, per acquisire il tempo usato dai processi r e analizzare i problemi di prestazioni. Per un esempio, vedere l'esercitazione [creare funzionalità di dati](../tutorials/walkthrough-create-data-features.md) in cui le funzioni temporali R sono incorporate nella soluzione.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su SQL Server Machine Learning Services, vedere:

- [Che cos'è SQL Server Machine Learning Services (Python e R)?](../what-is-sql-server-machine-learning.md)
