---
title: "Guida introduttiva per un'esecuzione di codice \"Hello World\" base R in T-SQL: SQL Server Machine Learning"
description: Guida introduttiva per lo script R in SQL Server. Informazioni di base della chiamata al metodo di script R usando la stored procedure sp_execute_external_script in un esercizio hello-world.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1ec9580a533e51b7e99ea0ac34c1d322a27da452
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042280"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>Avvio rapido: Script R di "Hello world" in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questa Guida introduttiva illustra i concetti chiave eseguendo una "Hello World" R script inT-SQL, un'introduzione al **sp_execute_external_script** stored procedure di sistema. 

## <a name="prerequisites"></a>Prerequisiti

Una Guida introduttiva precedente [R verificare esiste nel Server SQL](quickstart-r-verify.md), vengono fornite informazioni e collegamenti per configurare l'ambiente R necessario per questa Guida introduttiva.

## <a name="basic-r-interaction"></a>Interazione di base R

Esistono due modi, è possibile eseguire codice R nel Database SQL:

+ Aggiungere lo script R come argomento delle stored procedure di sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).
+ Da un [client R remoto](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client), connettersi al database SQL ed eseguire codice che usa il Database SQL come contesto di calcolo.

L'esercizio seguente è incentrata sul modello di interazione prima: come passare il codice R a una stored procedure.

1. Eseguire uno script semplice per vedere come viene eseguito uno script R nel database SQL.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))'
    '
    ```

2. Supponendo che si dispone di tutto configurare correttamente la correttezza del risultato viene calcolato e di R `print` funzione restituisce il risultato per il **messaggi** finestra.

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Durante il recupero **stdout** messaggi è utile quando il test del codice, più spesso è necessario restituire i risultati in formato tabulare, in modo che è possibile usarlo in un'applicazione o scriverlo in una tabella. Vedere [Guida introduttiva: Handle di input e output usano R in SQL Server](rtsql-working-with-inputs-and-outputs.md) per altre informazioni.

Tenere presente che tutti gli elementi all'interno di `@script` argomento deve essere un codice R valido.

## <a name="run-a-hello-world-script"></a>Eseguire uno script Hello World

L'esercizio seguente viene eseguito un altro script R semplici.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

Gli input per questa stored procedure includono:

+ *@language* parametro definisce l'estensione del linguaggio da chiamare, in questo caso R.
+ *@script* parametro definisce i comandi passati al runtime di R. L'intero script R deve essere incluso in questo argomento come testo Unicode. È anche possibile aggiungere il testo a una variabile di tipo **nvarchar** e quindi chiamare la variabile.
+ *@input_data_1* i dati vengono restituiti dalla query, passata al runtime di R, che restituisce i dati in SQL Server come un frame di dati.
+ SET di risultati di clausola definisce lo schema della tabella dati restituita per SQL Server, aggiunta di "Hello World" come nome della colonna **int** per il tipo di dati.

**Risultati**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Passaggi successivi

Ora che è stato eseguito un paio di script R semplici, esaminiamo più da vicino strutturazione di input e output.

> [!div class="nextstepaction"]
> [Avvio rapido: Gestire input e output](quickstart-r-inputs-and-outputs.md)
