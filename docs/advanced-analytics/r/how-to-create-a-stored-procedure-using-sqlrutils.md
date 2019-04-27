---
title: Come creare una stored procedure con sqlrutils - servizi di SQL Server Machine Learning
description: Per incorporare codice linguaggio R in una singola funzione che può essere passata come argomento a una stored procedure, utilizzare il pacchetto sqlrutils R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 014fb8344a0b2cf93dc7f375fffc717663f53a46
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641839"
---
# <a name="create-a-stored-pprocedure-using-sqlrutils"></a>Creare una stored pProcedure con sqlrutils
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive i passaggi per la conversione del codice R per l'esecuzione di una procedura T-SQL archiviate. Per ottenere i migliori risultati possibili, può essere necessario modificare il codice per garantire che tutti gli input possano essere parametrizzati.

## <a name="bkmk_rewrite"></a>Passaggio 1. Riscrivere lo Script R

Per ottenere risultati ottimali, è necessario riscrivere il codice R per è preferibile incapsularla come una singola funzione.

Tutte le variabili usate dalla funzione devono essere definite all'interno della funzione, o devono essere definite come parametri di input. Vedere le [esempi di codice](#samples) in questo articolo.

Inoltre, poiché i parametri di input per la funzione R diventerà stored procedure di parametri di input di SQL, è necessario assicurarsi che l'input e output siano conformi ai requisiti del tipo seguente:

### <a name="inputs"></a>Input

Tra i parametri di input può esistere al massimo un frame di dati.

Gli oggetti nel frame di dati e altri parametri di input della funzione devono essere dei tipi di dati R seguenti:
- POSIXct
- NUMERIC
- character
- integer
- logical
- raw

Se un tipo di input non è uno dei tipi elencati in precedenza, deve essere serializzato e passato alla funzione come *raw*. In questo caso, la funzione deve inoltre includere il codice per deserializzare l'input.

### <a name="outputs"></a>Output

La funzione può restituire uno degli elementi seguenti:

- Un frame di dati contenente i tipi di dati supportati. Tutti gli oggetti nel frame di dati devono usare uno dei tipi di dati supportati.
- Un elenco denominato contenente al massimo un frame di dati. Tutti i membri dell'elenco devono usare uno dei tipi di dati supportati.
- Un valore NULL, se la funzione non restituisce alcun risultato

## <a name="step-2-generate-required-objects"></a>Passaggio 2. Generare oggetti necessari

Dopo il codice R è stato pulito e può essere chiamato come una singola funzione, è necessario usare le funzioni nel **sqlrutils** pacchetto per preparare gli input e output in un formato che può essere passato al costruttore che crea il stored procedure.

**sqlrutils** fornisce funzioni che definiscono lo schema di dati di input e il tipo e definiscono lo schema di dati di output e tipo. Include anche le funzioni in grado di convertire gli oggetti R per il tipo di output richiesto. È possibile apportare più chiamate di funzione per creare gli oggetti necessari, a seconda dei tipi di dati che nel codice viene utilizzata.

### <a name="inputs"></a>Input

Se la funzione accetta l'input, per ogni input, chiamare le funzioni seguenti:

- `setInputData` Se l'input è un frame di dati
- `setInputParameter` per tutti gli altri tipi di input

Quando si apportano ogni funzione chiamata, viene creato un oggetto R che passerà in un secondo momento come argomento a `StoredProcedure`, per creare la stored procedure completa.

### <a name="outputs"></a>Output

**sqlrutils** offre diverse funzioni per la conversione di R oggetti, ad esempio gli elenchi per il frame di dati necessari per SQL Server.
Se la funzione restituisce un frame di dati direttamente, senza prima eseguirne il wrapping in un elenco, è possibile ignorare questo passaggio.
È anche possibile ignorare la conversione in questo passaggio se la funzione restituisce NULL.

Quando la conversione di un elenco o recupero di un particolare elemento da un elenco, scegliere tra queste funzioni:

- `setOutputData` Se la variabile per ottenere l'elenco è un frame di dati
- `setOutputParameter` per tutti gli altri membri dell'elenco

Quando si apportano ogni funzione chiamata, viene creato un oggetto R che passerà in un secondo momento come argomento a `StoredProcedure`, per creare la stored procedure completa.

## <a name="step-3-generate-the-stored-procedure"></a>Passaggio 3. Generare la Stored Procedure

Quando tutti i parametri di input e outpui sono pronti, effettuare una chiamata al `StoredProcedure` costruttore.

**Usage**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

Per illustrare questo concetto, si supponga di voler creare una stored procedure denominata **sp_rsample** con questi parametri:

- Usa una funzione esistente **foosql**. La funzione è stata basata sul codice esistente nella funzione R **foo**, ma si ha riscritto la funzione in modo conforme ai requisiti come descritto in [in questa sezione](#bkmk_rewrite)e la funzione di aggiornamento denominato  **foosql**.
- Usa il frame di dati **queryinput** come input
- Genera come output un frame di dati con il nome di variabile R **sqloutput**
- Si vuole creare il codice T-SQL come file nei `C:\Temp` cartella, in modo che sia possibile eseguire usando SQL Server Management Studio in un secondo momento

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> Poiché si sta scrivendo il file nel file System, è possibile omettere gli argomenti che definiscono la connessione al database.

L'output della funzione è una procedura T-SQL archiviate che può essere eseguita in un'istanza di SQL Server 2016 (richiede R Services) o SQL Server 2017 (richiede servizi di Machine Learning con R). 

Per altri esempi, vedere la Guida del pacchetto, chiamando `help(StoredProcedure)` da un ambiente R.

## <a name="step-4-register-and-run-the-stored-procedure"></a>Passaggio 4. Registrare ed eseguire la Stored Procedure

Esistono due modi, che è possibile eseguire la stored procedure:

- Tramite T-SQL, da qualsiasi client che supporta le connessioni all'istanza di SQL Server 2016 o SQL Server 2017
- Da un ambiente R

Entrambi i metodi richiedono che la stored procedure deve essere registrato nel database in cui si prevede di usare la stored procedure.

### <a name="register-the-stored-procedure"></a>Registrare la stored procedure

È possibile registrare la stored procedure con R, oppure è possibile eseguire l'istruzione CREATE PROCEDURE in T-SQL.

- Usando T-SQL.  Se si è più a proprio agio con T-SQL, aprire SQl Server Management Studio (o qualsiasi altro client che è possibile eseguire i comandi SQL DDL) ed eseguire l'istruzione CREATE PROCEDURE utilizzando il codice preparato dal `StoredProcedure` (funzione).
- Usando R. Mentre si è ancora nell'ambiente R, è possibile usare il `registerStoredProcedure` funzionare **sqlrutils** per registrare la stored procedure con il database.

  Ad esempio, è possibile registrare la stored procedure **sp_rsample** nell'istanza e al database definito nella *sqlConnStr*, con la chiamata R:

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> Indipendentemente dal fatto che si usa R o SQL, è necessario eseguire l'istruzione utilizzando un account che disponga delle autorizzazioni per creare nuovi oggetti di database.

### <a name="run-using-sql"></a>Esecuzione con SQL

Dopo aver creata la stored procedure, aprire una connessione al database SQL usando qualsiasi client che supporta T-SQL e passare i valori per i parametri richiesti dalla stored procedure.

### <a name="run-using-r"></a>Esegui con R

Alcune attività di preparazione aggiuntivi è necessaria se si desidera eseguire la stored procedure dal codice R, piuttosto che da SQL Server. Ad esempio, se la stored procedure richiede i valori di input, è necessario impostare i parametri di input prima che la funzione può essere eseguita e quindi passa tali oggetti per la stored procedure nel codice R.

Il processo complessivo di chiamata preparata stored procedure SQL è come segue:

1. Chiamare `getInputParameters` per ottenere un elenco di oggetti parametro di input.
2. Definire `$query` o impostare `$value` per ogni parametro di input.
3. Usare `executeStoredProcedure` per eseguire la stored procedure dall'ambiente di sviluppo R, passando l'elenco di oggetti parametro di input impostato.

## <a name = "samples"></a>Esempio

Questo esempio mostra la prima e dopo le versioni di uno script R che ottiene dati da un database di SQL Server, esegue alcune trasformazioni sui dati e lo salva in un database diverso.

Questo semplice esempio viene usato solo per illustrare come è possibile riordinare il codice R per renderne più semplice convertire in una stored procedure.

### <a name="before-code-preparation"></a>Prima della preparazione di codice


```R
sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineSrc;Trusted_Connection=Yes;"
  
sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineTest;Trusted_Connection=Yes;"
  
sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"
  
dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
xFunc <- function(data) {
    data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
    return(data)
    }
  
xVars <- c("CRSDepTime")
  
sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
rxOpen(dsSqlFrom)
rxOpen(dsSqlTo)
  
if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo))   {
    rxSqlServerDropTable("cleanData")}
  
rxDataStep(inData = dsSqlFrom, 
     outFile = dsSqlTo,
     transformFunc = xFunc,
     transformVars = xVars,
     overwrite = TRUE)
```

> [!NOTE]
> 
> Quando si usa una connessione ODBC anziché richiamare il *RxSqlServerData* funzione, è necessario aprire la connessione usando *rxOpen* prima di poter eseguire le operazioni nel database.


### <a name="after-code-preparation"></a>Dopo la preparazione del codice

Nella versione aggiornata, la prima riga definisce il nome della funzione. Tutto l'altro codice dalla soluzione R originale diventa parte di tale funzione.

```R
myetl1function <- function() { 
   sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=Airline01;Trusted_Connection=Yes;"
   sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer02;Database=Airline02;Trusted_Connection=Yes;"
    
   sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"

   dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
   dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
   xFunc <- function(data) {
     data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
     return(data)}
  
   xVars <- c("CRSDepTime")
  
   sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
   if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo)) {rxSqlServerDropTable("cleanData")}
  
   rxDataStep(inData = dsSqlFrom, 
        outFile = dsSqlTo,
        transformFunc = xFunc,
        transformVars = xVars,
        overwrite = TRUE)
   return(NULL)
}
```

> [!NOTE]
> 
> Anche se non è necessario aprire la connessione ODBC in modo esplicito come parte del codice, è comunque necessaria una connessione ODBC per usare **sqlrutils**.

## <a name="see-also"></a>Vedere anche

[sqlrutils (SQL)](ref-r-sqlrutils.md)


