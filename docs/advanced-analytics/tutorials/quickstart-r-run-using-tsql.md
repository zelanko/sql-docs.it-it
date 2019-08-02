---
title: Guida introduttiva per un'esecuzione di codice R di base "Hello World" in T-SQL
description: Guida introduttiva per script R in SQL Server. Informazioni di base sulla chiamata di script R con il sistema sp_execute_external_script stored procedure in un esercizio Hello-World.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ac9537e3e13313e6ca0094a75b0e72c7c8ee80c2
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714749"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>Avvio rapido: Script R "Hello World" in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa Guida introduttiva illustra i concetti chiave eseguendo uno script R "Hello World" inT-SQL, con un'introduzione al stored procedure di sistema **sp_execute_external_script** . 

## <a name="prerequisites"></a>Prerequisiti

Una guida introduttiva precedente, [Verify R exists in SQL Server](quickstart-r-verify.md), fornisce informazioni e collegamenti per la configurazione dell'ambiente R necessario per questa Guida introduttiva.

## <a name="basic-r-interaction"></a>Interazione R di base

Esistono due modi per eseguire il codice R nel database SQL:

+ Aggiungere uno script R come argomento del stored procedure di sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).
+ Da un [client R remoto](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client)connettersi al database SQL ed eseguire il codice usando il database SQL come contesto di calcolo.

Il seguente esercizio è incentrato sul primo modello di interazione: come passare il codice R a un stored procedure.

1. Eseguire uno script semplice per vedere come viene eseguito uno script R nel database SQL.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

2. Supponendo che tutti gli elementi impostati correttamente siano corretti, viene calcolato il risultato corretto e `print` la funzione R restituisce il risultato nella finestra **messaggi** .

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Il recupero dei messaggi **stdout** è utile quando si esegue il test del codice, più spesso è necessario restituire i risultati in formato tabulare, in modo che sia possibile utilizzarlo in un'applicazione o scriverlo in una tabella. Vedere [Avvio rapido: Per ulteriori informazioni, gestire input e output](rtsql-working-with-inputs-and-outputs.md) usando R in SQL Server.

Tenere presente che tutto ciò `@script` che si trova all'interno dell'argomento deve essere un codice R valido.

## <a name="run-a-hello-world-script"></a>Eseguire uno script di Hello World

L'esercizio seguente esegue un altro semplice script R.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

Gli input per questo stored procedure includono:

+ *@language* il parametro definisce l'estensione del linguaggio da chiamare, in questo caso R.
+ *@script* il parametro definisce i comandi passati al runtime di R. L'intero script R deve essere incluso in questo argomento come testo Unicode. È anche possibile aggiungere il testo a una variabile di tipo **nvarchar** e quindi chiamare la variabile.
+ *@input_data_1* i dati vengono restituiti dalla query, passati al runtime di R, che restituisce i dati da SQL Server come frame di dati.
+ CON la clausola set di risultati viene definito lo schema della tabella dati restituita per SQL Server, aggiungendo "Hello World" come nome di colonna, **int** per il tipo di dati.

**Risultati**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Passaggi successivi

Ora che sono stati eseguiti due semplici script R, è possibile esaminare in modo più approfondito la strutturazione di input e output.

> [!div class="nextstepaction"]
> [Avvio rapido: Gestire input e output](quickstart-r-inputs-and-outputs.md)
