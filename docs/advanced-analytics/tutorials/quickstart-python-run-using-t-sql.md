---
title: Guida introduttiva per l'esecuzione di codice Python di base "Hello World" in T-SQL
description: Guida introduttiva per script Python in SQL Server. Informazioni di base sulla chiamata di script Python con il sistema sp_execute_external_script stored procedure in un esercizio Hello-World.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/10/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1281da6a366f7fa9d5fca20cc719a3c86825e56d
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469612"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>Avvio rapido: Script Python "Hello World" in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa Guida introduttiva illustra i concetti chiave eseguendo uno script Python "Hello World" di tipo inT-SQL, con un'introduzione al stored procedure di sistema **sp_execute_external_script** . 

## <a name="prerequisites"></a>Prerequisiti

Una guida introduttiva precedente, [Verify Python exists in SQL Server](quickstart-python-verify.md), fornisce informazioni e collegamenti per la configurazione dell'ambiente Python necessario per questa Guida introduttiva.

## <a name="basic-python-interaction"></a>Interazione Python di base

Esistono due modi per eseguire il codice Python in SQL Server:

+ Aggiungere uno script Python come argomento del stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Da un [client Python remoto](../python/setup-python-client-tools-sql.md)connettersi a SQL Server ed eseguire il codice usando il SQL Server come contesto di calcolo. Questa operazione richiede [revoscalepy](../python/ref-py-revoscalepy.md).

Il seguente esercizio è incentrato sul primo modello di interazione: come passare il codice Python a una stored procedure.

1. Eseguire un codice semplice per vedere come vengono passati i dati tra SQL Server e Python.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. Supponendo che tutti gli elementi siano configurati correttamente e che Python e SQL Server stiano comunicando tra loro, viene calcolato il risultato `print` corretto e la funzione Python restituisce il risultato alle finestre **dei messaggi** .

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Il recupero dei messaggi **stdout** è utile quando si esegue il test del codice, più spesso è necessario restituire i risultati in formato tabulare, in modo che sia possibile utilizzarlo in un'applicazione o scriverlo in una tabella.

Per il momento, tenere presenti le seguenti regole:

+ Tutti gli elementi `@script` all'interno dell'argomento devono essere codice Python valido. 
+ Il codice deve seguire tutte le regole Python relative al rientro, ai nomi delle variabili e così via. Quando viene ricevuto un errore, controllare lo spazio vuoto e la combinazione di maiuscole e minuscole.
+ Tra i linguaggi di programmazione, Python è uno dei più flessibili rispetto alle virgolette singole rispetto alle virgolette doppie; sono molto intercambiabili. Tuttavia, T-SQL usa virgolette singole solo per determinati elementi e l' `@script` argomento Usa virgolette singole per racchiudere il codice Python come stringa Unicode. Potrebbe quindi essere necessario esaminare il codice Python e modificare alcune virgolette singole con virgolette doppie.
+ Se si usano librerie che non sono caricate per impostazione predefinita, è necessario usare un'istruzione import all'inizio dello script per caricarle. SQL Server aggiunge diverse librerie specifiche del prodotto. Per altre informazioni, vedere [Python libraries](../python/python-libraries-and-data-types.md).
+ Se la libreria non è già installata, arrestare e installare il pacchetto Python all'esterno di SQL Server, come descritto di seguito: [Installare nuovi pacchetti Python in SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>Eseguire uno script di Hello World

L'esercizio seguente esegue un altro semplice script Python.

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

Gli input per questo stored procedure includono:

+ *@language* il parametro definisce l'estensione del linguaggio da chiamare, in questo caso Python.
+ *@script* il parametro definisce i comandi passati al runtime di Python. L'intero script Python deve essere racchiuso in questo argomento, come testo Unicode. È anche possibile aggiungere il testo a una variabile di tipo **nvarchar** e quindi chiamare la variabile.
+ *@input_data_1* i dati vengono restituiti dalla query, passati al runtime di Python, che restituisce i dati da SQL Server come frame di dati.
+ CON la clausola set di risultati viene definito lo schema della tabella dati restituita per SQL Server, aggiungendo "Hello World" come nome di colonna, **int** per il tipo di dati.

**Risultati**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Passaggi successivi

Ora che è stato eseguito un paio di semplici script Python, esaminare più in dettaglio la strutturazione di input e output.

> [!div class="nextstepaction"]
> [Avvio rapido: Gestire input e output](quickstart-python-inputs-and-outputs.md)
