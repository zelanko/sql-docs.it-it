---
title: Guida introduttiva a oggetti e tipi di dati R e SQL
description: Questa Guida introduttiva illustra come usare i tipi di dati e gli oggetti dati in R e SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 686ba69425dc9bc6554b369be3d5fadd24b5a234
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469392"
---
# <a name="quickstart-handle-data-types-and-objects-using-r-in-sql-server"></a>Avvio rapido: Gestire i tipi di dati e gli oggetti usando R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa Guida introduttiva viene illustrata un'introduzione pratica ai problemi comuni che si verificano quando si trasferiscono i dati tra R e SQL Server. L'esperienza acquisita in questo esercizio fornisce uno sfondo essenziale quando si lavora con i dati nel proprio script.

Di seguito sono riportati i problemi comuni da tenere presente:

+ Talvolta i tipi di dati non corrispondono
+ Le conversioni implicite potrebbero avere luogo
+ In alcuni casi sono necessarie operazioni cast e convert
+ R e SQL usano oggetti dati differenti

## <a name="prerequisites"></a>Prerequisiti

Una guida introduttiva precedente, [Verify R exists in SQL Server](quickstart-r-verify.md), fornisce informazioni e collegamenti per la configurazione dell'ambiente R necessario per questa Guida introduttiva.

## <a name="always-return-a-data-frame"></a>Restituire sempre un frame di dati

Quando lo script restituisce risultati da R a SQL Server, i dati devono essere restituiti come **data.frame**. Qualsiasi altro tipo di oggetto generato nello script, indipendentemente dal fatto che si tratti di un elenco, un fattore, un vettore o dati binari, deve essere convertito in un frame di dati se si desidera restituirlo come parte dei risultati del stored procedure. A questo scopo, sono disponibili più funzioni R per il supporto della modifica di altri oggetti in un frame di dati. È anche possibile serializzare un modello binario e restituirlo in un frame di dati. Entrambe le operazioni verranno eseguite più avanti in questa esercitazione.

Per prima cosa, è possibile provare con alcuni oggetti r Basic, vettori, matrici ed elenchi, per vedere in che modo la conversione in un frame di dati modifica l'output passato a SQL Server.

Confrontare questi due script "Hello World" in R. Gli script sembrano quasi identici, ma la prima restituisce una singola colonna di tre valori, mentre la seconda restituisce tre colonne con un singolo valore.

**Esempio 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**Esempio 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identify-schema-and-data-types"></a>Identificare lo schema e i tipi di dati

Perché i risultati sono così diversi? 

La risposta può essere trovata usando il comando `str()` di R. Aggiungere la funzione `str(object_name)` in qualsiasi punto dello script R per fare in modo che lo schema dati dell'oggetto R specificato venga restituito come messaggio informativo. Per visualizzare i messaggi, vedere il riquadro **Messaggi** di Visual Studio Code o la scheda **Messaggi** in SSMS.

Per capire come mai l'Esempio 1 e l'Esempio 2 producano risultati così diversi, inserire la riga `str(OutputDataSet)` alla fine della definizione di variabile _@script_ in ogni istruzione, come riportato di seguito:

**Esempio 1 con la funzione Str aggiunta**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**Esempio 2 con la funzione Str aggiunta**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

A questo punto, riesaminare il testo in **Messaggi** per capire perché l'output è differente.

**Risultati - Esempio 1**

```sql
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**Risultati - Esempio 2**

```sql
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

Come si può notare, una leggera modifica nella sintassi di R ha un effetto notevole sullo schema dei risultati. Non verranno esaminati i motivi per cui, ma le differenze nei tipi di dati R sono descritte in dettaglio nella sezione *strutture dati* in ["Advanced R" di Hadley Wickham](http://adv-r.had.co.nz).

Per il momento, tenere semplicemente presente che è necessario verificare i risultati previsti quando si convertono oggetti R in frame di dati.

> [!TIP]
> È anche possibile usare le funzioni di identità R, `is.matrix`ad `is.vector`esempio, per restituire informazioni sulla struttura dei dati interna.

## <a name="implicit-conversion-of-data-objects"></a>Conversione implicita di oggetti dati

Ogni oggetto dati R ha regole specifiche per la gestione dei valori in combinazione con altri oggetti dati se i due oggetti dati hanno lo stesso numero di dimensioni o se un oggetto dati contiene tipi di dati eterogenei.

Si supponga, ad esempio, di eseguire l'istruzione seguente per eseguire la moltiplicazione di matrici usando R. Si moltiplica una matrice a colonna singola con i tre valori in base a una matrice con quattro valori e si aspetta una matrice 4x3 di conseguenza.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

La colonna di tre valori viene convertita automaticamente in un oggetto matrix a colonna singola. Poiché un oggetto matrix è semplicemente un caso speciale di oggetto array in R, l'oggetto array `y` viene convertito in modo implicito in un oggetto matrix a colonna singola per rendere conformi i due argomenti.

**Risultati**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

Si noti tuttavia che cosa accade quando si modifica la dimensione della matrice `y`.

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

Adesso R restituisce come risultato un valore singolo.

**Risultati**
    
|Col1|
|---|
|1542|

Per quale motivo? In questo caso, poiché i due argomenti possono essere gestiti come vettori della stessa lunghezza, R restituisce il prodotto interno come matrice.  Questo è il comportamento previsto in base alle regole dell'algebra lineare; tuttavia, potrebbe causare problemi se l'applicazione downstream prevede che lo schema di output non venga mai modificato.

> [!TIP]
> 
> Recupero degli errori Questi esempi richiedono la tabella **RTestData**. Se la tabella dati di test non è stata creata, tornare a questo argomento per creare la tabella: [Gestire input e output](../tutorials/rtsql-working-with-inputs-and-outputs.md).
> 
> Se la tabella è stata creata ma viene comunque generato un errore, assicurarsi di eseguire il stored procedure nel contesto del database che contiene la tabella e non nel database **Master** o in un altro database.
> 
> Si consiglia inoltre di evitare l'utilizzo di tabelle temporanee per questi esempi. Alcuni client R termineranno una connessione tra i batch, eliminando le tabelle temporanee.

## <a name="merge-or-multiply-columns-of-different-length"></a>Unire o moltiplicare colonne di lunghezza diversa

R offre una grande flessibilità per lavorare con vettori di dimensioni diverse e per combinare queste strutture simili a colonne in frame di dati. Gli elenchi dei vettori sono simili a una tabella, ma non seguono tutte le regole delle tabelle del database.

Ad esempio, lo script seguente definisce un oggetto array numerico di lunghezza 6 e lo archivia nella variabile R `df1`. La matrice numerica viene quindi combinata con i numeri interi della tabella RTestData, che contiene tre (3) valori, per creare un nuovo frame di `df2`dati,.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

Per riempire il frame di dati, R ripete gli elementi recuperati da RTestData per il numero di volte necessario per corrispondere al numero di elementi nell'oggetto array `df1`.

**Risultati**
    
|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

Ricordare che un frame di dati ha solo l'aspetto di una tabella, ma in realtà è un elenco di vettori.

## <a name="cast-or-convert-sql-server-data"></a>Eseguire il cast o convertire i dati di SQL Server

R e SQL Server non usano gli stessi tipi di dati, pertanto quando si esegue una query in SQL Server per ottenere i dati e quindi passarli al runtime di R, viene in genere eseguita una sorta di conversione implicita. Un'altra serie di conversioni ha luogo quando si restituiscono i dati da R a SQL Server.

- SQL Server effettua il push dei dati dalla query al processo R gestito dal servizio Launchpad e lo converte in una rappresentazione interna per una maggiore efficienza.
- Il runtime R carica i dati in una variabile data.frame ed esegue a sua volta operazioni sui dati.
- Il motore di database restituisce i dati a SQL Server usando una connessione interna protetta e presenta i dati in termini di tipi di dati di SQL Server.
- I dati vengono ottenuti tramite la connessione a SQL Server con una libreria client o di rete in grado di eseguire query SQL e di gestire set di dati tabulari. Questa applicazione client può influire sui dati in altri modi.

Per verificarne il funzionamento, eseguire una query come questa nell'data warehouse [AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) . Questa vista restituisce i dati di vendita usati per la creazione delle previsioni.

```sql
USE AdventureWorksDW
GO

SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> È possibile usare qualsiasi versione di AdventureWorks o creare una query diversa usando un database personalizzato. Il punto consiste nel tentare di gestire alcuni dati contenenti valori di tipo text, DateTime e numeric.

A questo punto, provare a incollare questa query come input per la stored procedure.

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

Se si verifica un errore, probabilmente sarà necessario apportare alcune modifiche al testo della query. Ad esempio, il predicato stringa nella clausola WHERE deve essere racchiuso tra due set di virgolette singole.

Dopo avere verificato che la query funzioni, esaminare i risultati della funzione `str` per visualizzare la modalità di gestione dei dati di input in R.

**Risultati**

```sql
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ La colonna datetime è stata elaborata usando il tipo di dati R **POSIXct**.
+ La colonna di testo "ProductSeries" è stata identificata come **fattore**, vale a dire una variabile categorica. Per impostazione predefinita, i valori stringa sono gestiti come fattori. Se si passa una stringa a R, viene convertita in un numero intero per uso interno e quindi rimappata alla stringa nell'output.

### <a name="summary"></a>Riepilogo

Da questi brevi esempi è possibile vedere la necessità di controllare gli effetti della conversione dei dati quando si passano query SQL come input. Poiché alcuni SQL Server tipi di dati non sono supportati da R, considerare questi modi per evitare errori:

+ Testare i dati in anticipo e verificare le colonne o i valori nello schema che potrebbero costituire un problema quando vengono passati al codice R.
+ Specificare le colonne nell'origine dati di input singolarmente, anziché usare `SELECT *`, per vedere in che modo verrà gestita ogni colonna.
+ Quando si preparano i dati di input, eseguire cast espliciti in base alle necessità per evitare sorprese.
+ Evitare di passare colonne di dati, ad esempio GUID o ROWGUID, che provocano errori e che non sono utili per la modellazione.

Per altre informazioni sui tipi di dati supportati e non supportati, vedere [librerie e tipi di dati di R](../r/r-libraries-and-data-types.md).

Per informazioni sull'effetto sulle prestazioni della conversione in fase di esecuzione delle stringhe in fattori numerici, vedere [R Services per SQL Server ottimizzazione delle prestazioni](../r/sql-server-r-services-performance-tuning.md).

## <a name="next-step"></a>Passaggio successivo

Nella prossima Guida introduttiva si apprenderà come applicare funzioni R ai dati SQL Server.

> [!div class="nextstepaction"]
> [Avvio rapido: Usare le funzioni R con dati di SQL Server](quickstart-r-functions.md)
