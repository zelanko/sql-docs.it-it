---
title: "Guida introduttiva per un Python di base di \"Hello World\" di codice l'esecuzione in T-SQL: SQL Server Machine Learning"
description: Guida introduttiva per script di Python in SQL Server. Informazioni di base della chiamata al metodo di script Python usando la stored procedure sp_execute_external_script in un esercizio hello-world.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/10/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6d8da3ce90e915344f2380d4cd5cc866db6715ef
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59476636"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>Avvio rapido: Script di Python "Hello world" in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questa Guida introduttiva illustra i concetti chiave eseguendo un "Hello World" Python script inT-SQL, un'introduzione al **sp_execute_external_script** stored procedure di sistema. 

## <a name="prerequisites"></a>Prerequisiti

Una Guida introduttiva precedente [Python verificare esiste nel Server SQL](quickstart-python-verify.md), vengono fornite informazioni e collegamenti per la configurazione dell'ambiente di Python necessario per questa Guida introduttiva.

## <a name="basic-python-interaction"></a>Interazione di Python di base

Esistono due modi per eseguire il codice Python in SQL Server:

+ Aggiungere uno script di Python come argomento delle stored procedure di sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Da un [client Python remoto](../python/setup-python-client-tools-sql.md), connettersi a SQL Server ed eseguire codice che Usa SQL Server come contesto di calcolo. Questa operazione richiede [revoscalepy](../python/ref-py-revoscalepy.md).

L'esercizio seguente è incentrata sul modello di interazione prima: come passare il codice Python a una stored procedure.

1. Eseguire codice semplice per vedere come i dati vengono passati avanti e indietro tra SQL Server e Python.

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

2. Supponendo che si dispone di tutto è configurato correttamente e Python e SQL Server comunichino tra loro, viene calcolato il risultato corretto e di Python `print` funzione restituisce il risultato per il **messaggi** windows.

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Durante il recupero **stdout** messaggi risulta utile quando il test del codice, più spesso è necessario restituire i risultati in formato tabulare, in modo che è possibile usarlo in un'applicazione o scriverlo in una tabella.

Per il momento, tenere presenti queste regole:

+ Tutti gli elementi all'interno di `@script` argomento deve essere il codice Python valido. 
+ Il codice deve seguire tutte le regole di Python riguardanti il rientro, i nomi delle variabili e così via. Quando si verifica un errore, verificare di spazi vuoti e maiuscole e minuscole.
+ Tra i linguaggi di programmazione Python è uno dei più flessibile per quanto riguarda le virgolette singole e virgolette doppie. si tratta sostanzialmente intercambiabili. Tuttavia, T-SQL vengono utilizzate le virgolette solo determinati aspetti e il `@script` argomento vengono utilizzate le virgolette per racchiudere il codice Python come una stringa Unicode. Pertanto, si potrebbe essere necessario esaminare il codice Python e cambiare alcuni tra virgolette singole in virgolette doppie.
+ Se si usa le eventuali librerie che non vengono caricate per impostazione predefinita, è necessario utilizzare un'istruzione import all'inizio dello script per caricarli. SQL Server aggiunge diverse librerie specifici del prodotto. Per altre informazioni, vedere [librerie Python](../python/python-libraries-and-data-types.md).
+ Se la libreria non è già installata, interrompere e installare il pacchetto di Python all'esterno di SQL Server, come descritto di seguito: [Installare nuovi pacchetti Python in SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>Eseguire uno script Hello World

L'esercizio seguente viene eseguito un altro script Python semplice.

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

Gli input per questa stored procedure includono:

+ *@language* parametro definisce l'estensione del linguaggio da chiamare, in questo caso, Python.
+ *@script* parametro definisce i comandi passati al runtime di Python. L'intero script Python deve essere incluso in questo argomento, come testo Unicode. È anche possibile aggiungere il testo a una variabile di tipo **nvarchar** e quindi chiamare la variabile.
+ *@input_data_1* i dati vengono restituiti dalla query, passata al runtime di Python, che restituisce i dati in SQL Server come un frame di dati.
+ SET di risultati di clausola definisce lo schema della tabella dati restituita per SQL Server, aggiunta di "Hello World" come nome della colonna **int** per il tipo di dati.

**Risultati**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Passaggi successivi

Ora che è stato eseguito un paio di semplici script di Python, esaminiamo più da vicino strutturazione di input e output.

> [!div class="nextstepaction"]
> [Guida introduttiva: Gestire gli input e output](quickstart-python-inputs-and-outputs.md)
