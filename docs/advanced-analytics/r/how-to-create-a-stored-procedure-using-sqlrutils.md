---
title: Come creare una stored procedure usando sqlrutils
description: Usare il pacchetto R sqlrutils in SQL Server per aggregare il codice del linguaggio R in una singola funzione che può essere passata come argomento a una stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0713a126a237f20b2de4e3b16225bb9e5ae26307
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345575"
---
# <a name="create-a-stored-pprocedure-using-sqlrutils"></a>Creare un pProcedure archiviato usando sqlrutils
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive i passaggi per la conversione del codice R per l'esecuzione come stored procedure T-SQL. Per ottenere i migliori risultati possibili, può essere necessario modificare il codice per garantire che tutti gli input possano essere parametrizzati.

## <a name="bkmk_rewrite"></a>Passaggio 1. Riscrivere lo script R

Per ottenere risultati ottimali, è necessario riscrivere il codice R per incapsularlo come una singola funzione.

Tutte le variabili usate dalla funzione devono essere definite all'interno della funzione o devono essere definite come parametri di input. Vedere il [codice di esempio](#samples) in questo articolo.

Inoltre, poiché i parametri di input per la funzione R diventeranno i parametri di input del stored procedure SQL, è necessario assicurarsi che gli input e gli output siano conformi ai requisiti di tipo seguenti:

### <a name="inputs"></a>Input

Tra i parametri di input può esistere al massimo un frame di dati.

Gli oggetti nel frame di dati e altri parametri di input della funzione devono essere dei tipi di dati R seguenti:
- POSIXct
- numeric
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

## <a name="step-2-generate-required-objects"></a>Passaggio 2. Genera oggetti necessari

Dopo che il codice R è stato pulito e può essere chiamato come una singola funzione, si useranno le funzioni nel pacchetto **sqlrutils** per preparare gli input e gli output in un modulo che può essere passato al costruttore che compila effettivamente il stored procedure.

**sqlrutils** fornisce funzioni che definiscono lo schema e il tipo di dati di input e definiscono lo schema e il tipo di dati di output. Include anche funzioni che possono convertire gli oggetti R nel tipo di output richiesto. È possibile eseguire più chiamate di funzione per creare gli oggetti necessari, a seconda dei tipi di dati usati dal codice.

### <a name="inputs"></a>Input

Se la funzione accetta input per ogni input, chiamare le funzioni seguenti:

- `setInputData`Se l'input è un frame di dati
- `setInputParameter`per tutti gli altri tipi di input

Quando si esegue ogni chiamata di funzione, viene creato un oggetto R che verrà passato successivamente come argomento a `StoredProcedure`, per creare il stored procedure completo.

### <a name="outputs"></a>Output

**sqlrutils** offre più funzioni per la conversione di oggetti R, ad esempio elenchi, per i dati. frame necessari per SQL Server.
Se la funzione restituisce un frame di dati direttamente, senza prima eseguirne il wrapping in un elenco, è possibile ignorare questo passaggio.
È anche possibile ignorare la conversione di questo passaggio se la funzione restituisce NULL.

Quando si converte un elenco o si recupera un particolare elemento da un elenco, scegliere una delle seguenti funzioni:

- `setOutputData`Se la variabile da ottenere dall'elenco è un frame di dati
- `setOutputParameter`per tutti gli altri membri dell'elenco

Quando si esegue ogni chiamata di funzione, viene creato un oggetto R che verrà passato successivamente come argomento a `StoredProcedure`, per creare il stored procedure completo.

## <a name="step-3-generate-the-stored-procedure"></a>Passaggio 3. Genera la stored procedure

Quando tutti i parametri di input e output sono pronti, effettuare una chiamata `StoredProcedure` al costruttore.

**Utilizzo**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

Per illustrare, si supponga di voler creare un stored procedure denominato **sp_rsample** con questi parametri:

- Usa una funzione **foosql**esistente. La funzione è basata sul codice esistente nella funzione R **foo**, ma è stata riscritta la funzione per conformarsi ai requisiti descritti in [questa sezione](#bkmk_rewrite)e ha denominato la funzione aggiornata come **foosql**.
- Usa il frame di dati **queryinput** come input
- Genera come output un frame di dati con il nome della variabile  R, SQLOutput
- Si vuole creare il codice T-SQL come file nella `C:\Temp` cartella, in modo che sia possibile eseguirlo con SQL Server Management Studio in un secondo momento

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> Poiché si sta scrivendo il file nella file system, è possibile omettere gli argomenti che definiscono la connessione al database.

L'output della funzione è un stored procedure T-SQL che può essere eseguito in un'istanza di SQL Server 2016 (richiede R Services) o SQL Server 2017 (richiede Machine Learning Services con R). 

Per altri esempi, vedere la guida del pacchetto chiamando `help(StoredProcedure)` da un ambiente R.

## <a name="step-4-register-and-run-the-stored-procedure"></a>Passaggio 4. Registrare ed eseguire la stored procedure

È possibile eseguire il stored procedure in due modi:

- Utilizzando T-SQL, da qualsiasi client che supporta le connessioni all'istanza di SQL Server 2016 o SQL Server 2017
- Da un ambiente R

Per entrambi i metodi è necessario che il stored procedure sia registrato nel database in cui si intende utilizzare l'stored procedure.

### <a name="register-the-stored-procedure"></a>Registrare il stored procedure

È possibile registrare il stored procedure usando R oppure è possibile eseguire l'istruzione CREATE PROCEDURE in T-SQL.

- Uso di T-SQL.  Se si ha familiarità con T-SQL, aprire Management Studio di SQL Server (o qualsiasi altro client in grado di eseguire comandi SQL DDL) ed eseguire l'istruzione create procedure usando il codice preparato `StoredProcedure` dalla funzione.
- Uso di R. Mentre si è ancora nell'ambiente R, è possibile usare la `registerStoredProcedure` funzione in **sqlrutils** per registrare il stored procedure con il database.

  Ad esempio, è possibile registrare il stored procedure **sp_rsample** nell'istanza e nel database definiti in *sqlConnStr*, effettuando questa chiamata R:

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> Indipendentemente dal fatto che si utilizzi R o SQL, è necessario eseguire l'istruzione utilizzando un account con autorizzazioni per la creazione di nuovi oggetti di database.

### <a name="run-using-sql"></a>Esegui con SQL

Una volta creata la stored procedure, aprire una connessione al database SQL usando un client che supporta T-SQL e passare i valori per tutti i parametri richiesti dall'stored procedure.

### <a name="run-using-r"></a>Eseguire usando R

Se si vuole eseguire la stored procedure dal codice R, è necessaria una preparazione aggiuntiva piuttosto che da SQL Server. Se, ad esempio, il stored procedure richiede valori di input, è necessario impostare i parametri di input prima che la funzione possa essere eseguita, quindi passare tali oggetti al stored procedure nel codice R.

Il processo generale di chiamata del stored procedure SQL preparato è il seguente:

1. Chiamare `getInputParameters` per ottenere un elenco di oggetti parametro di input.
2. Definire `$query` o impostare `$value` per ogni parametro di input.
3. Usare `executeStoredProcedure` per eseguire la stored procedure dall'ambiente di sviluppo R, passando l'elenco di oggetti parametro di input impostato.

## <a name = "samples"></a>Esempio

Questo esempio illustra le versioni before e after di uno script R che recupera i dati da un database di SQL Server, esegue alcune trasformazioni sui dati e li salva in un altro database.

Questo semplice esempio viene usato solo per illustrare come è possibile ridisporre il codice R per semplificare la conversione in un stored procedure.

### <a name="before-code-preparation"></a>Prima della preparazione del codice


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
> Quando si utilizza una connessione ODBC anziché richiamare la funzione *RxSqlServerData* , è necessario aprire la connessione utilizzando *rxOpen* prima di poter eseguire operazioni sul database.


### <a name="after-code-preparation"></a>Dopo la preparazione del codice

Nella versione aggiornata la prima riga definisce il nome della funzione. Tutto il codice della soluzione R originale diventa parte di tale funzione.

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


