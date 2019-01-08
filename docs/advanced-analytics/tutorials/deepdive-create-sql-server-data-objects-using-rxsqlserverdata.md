---
title: Creare oggetti dati SQL Server usando RevoScaleR RxSqlServerData - SQL Server Machine Learning
description: Procedura dettagliata su come creare oggetti dati usando il linguaggio R in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cbd6f8bb9fd44be44132fd71e7e8eca3c9625b43
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596392"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>Creare oggetti dati SQL Server usando RxSqlServerData (esercitazione di RevoScaleR e SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa lezione fa parte il [esercitazione RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) su come usare [funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Lezione 2 è una continuazione della creazione del database: aggiunta di tabelle e il caricamento dei dati. Se un amministratore di database della creazione del database e account di accesso nel [lezione uno](deepdive-work-with-sql-server-data-using-r.md), è possibile aggiungere tabelle con un IDE R come RStudio o, ad esempio uno strumento incorporato **Rgui**.

Da R, connettersi a SQL Server e usare **RevoScaleR** funzioni per eseguire le attività seguenti:

> [!div class="checklist"]
> * Creare tabelle per i dati di training e previsioni
> * Caricare dati nelle tabelle da un file CSV locale

Dati di esempio sono i dati di frode simulato carta di credito (ccFraud set di dati), suddiviso in set di training e set di dati di assegnazione dei punteggi. Il file di dati è inclusa nella **RevoScaleR**.

Usare un IDE R oppure **Rgui** questi ogni chiamata richiede il completamento. Assicurarsi di usare i file eseguibili R disponibili in questa posizione: C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\bin\x64 (entrambi Rgui.exe se si usa tale strumento, o un IDE R che puntano a c:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER). Presenza di un' [workstation client R](../r/set-up-a-data-science-client.md) con questi file eseguibili sono considerato un prerequisito di questa esercitazione.

## <a name="create-the-training-data-table"></a>Creare la tabella di dati di training

1. Store la stringa di connessione di database in una variabile R. Di seguito sono riportati due esempi di stringhe di connessione ODBC valide per SQL Server: uno con un account di accesso SQL e uno per l'autenticazione integrata di Windows. 

   Assicurarsi di modificare il nome del server, nome utente e password in modo appropriato.

    **Account di accesso SQL**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>; Database=RevoDeepDive;Uid=<user_name>;Pwd=<password>"
    ```

    **Autenticazione di Windows**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>;Database=RevoDeepDive;Trusted_Connection=True"
    ```

2. Specificare il nome della tabella che si vuole creare e salvarlo in una variabile R.
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    Poiché l'istanza del server e il nome del database sono già specificati come parte della stringa di connessione, quando si combinano le due variabili, il *completi* nome della nuova tabella diventa  *ccfraudsmall*.
  
3.  Facoltativamente, specificare *rowsPerRead* per controllare il numero di righe di dati viene lette in ogni batch.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Anche se questo parametro è facoltativo, impostandola può comportare i calcoli più efficienti. La maggior parte delle funzioni analitiche avanzate in **RevoScaleR** e **MicrosoftML** elaborare i dati in blocchi. Il *rowsPerRead* parametro determina il numero di righe in ogni blocco.
  
    Potrebbe essere necessario provare a usare questa impostazione per trovare il giusto equilibrio. Se il valore è troppo grande, l'accesso ai dati potrebbe essere lenta se non vi è memoria sufficiente per elaborare i dati in blocchi di tale dimensione. Viceversa, in alcuni sistemi, se il valore di *rowsPerRead* è troppo piccolo, delle prestazioni possono anche rallentare.
  
    Come valore iniziale, utilizzare la dimensione predefinita del processo batch definita dall'istanza del motore di database per controllare il numero di righe in ogni blocco (5.000 righe). Salvare tale valore nella variabile *sqlRowsPerRead*.
  
4.  Definire una variabile per il nuovo oggetto origine dati e passare gli argomenti definiti in precedenza per il **RxSqlServerData** costruttore. Si noti che l'oggetto viene creato ma non popolato. Il caricamento dei dati è un passaggio separato.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>Creare la tabella di dati di assegnazione dei punteggi

Usando la stessa procedura, creare la tabella che contiene i dati dei punteggi usando lo stesso processo.

1. Creare una nuova variabile R, *sqlScoreTable*, per archiviare il nome della tabella usata per l'assegnazione dei punteggi.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Inserire la variabile come argomento nella funzione **RxSqlServerData** per definire un secondo oggetto origine dati, *sqlScoreDS*.
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Poiché la stringa di connessione e altri parametri sono già definiti come variabili nell'area di lavoro R, è possibile riutilizzarlo per nuove origini dati che rappresentano diverse tabelle, viste o query.

> [!NOTE]
> La funzione Usa argomenti diversi per la definizione di un'origine dati basata su un'intera tabella rispetto per un'origine dati basata su una query. Questo avviene perché il motore di database di SQL Server è necessario preparare le query in modo diverso. Più avanti in questa esercitazione descrive come creare un oggetto origine dati basato su una query SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Caricamento dei dati nelle tabelle SQL con R

Ora che sono state create le tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è possibile caricare dati nelle tabelle usando la funzione **Rx** appropriata.

Il **RevoScaleR** pacchetto contiene le funzioni specifiche per i tipi di origine dati. Per i dati di testo, usare [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) per generare l'oggetto origine dati. Sono disponibili funzioni aggiuntive per la creazione di oggetti origine dati da dati Hadoop, dati ODBC e così via.

> [!NOTE]
> In questa sezione è necessario disporre **Esegui DDL** autorizzazioni sul database.

### <a name="load-data-into-the-training-table"></a>Caricare i dati nella tabella di training

1. Creare una variabile R *ccFraudCsv*e assegnare alla variabile il percorso del file CSV che contiene i dati di esempio. Questo set di dati è disponibile nel **RevoScaleR**. "sampleDataDir" è una parola chiave nel **rxGetOption** (funzione).
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Si noti che la chiamata a **rxGetOption**, che è associato con il metodo GET [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) nelle **RevoScaleR**. Utilizzare questa utilità per impostare ed elencate le opzioni relative a contesti di calcolo locali e remoti, ad esempio la directory condivisa predefinita o il numero di processori (Core) da utilizzare nei calcoli.
    
    Questa particolare chiamata recupera gli esempi dalla libreria corretta, indipendentemente dal quale viene eseguito il codice. Ad esempio, provare a eseguire la funzione in SQL Server e nel computer di sviluppo e osservare i percorsi diversi.
  
2. Definire una variabile per archiviare i nuovi dati e usare la funzione **RxTextData** per specificare l'origine dati di testo.
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    L'argomento *colClasses* è importante. Usarlo per indicare il tipo di dati da assegnare a ogni colonna di dati caricati dal file di testo. In questo esempio, tutte le colonne vengono gestite come testo, tranne le colonne denominate, che vengono gestite come valori interi.
  
3. A questo punto, è possibile sospendere un momento e visualizzare il database in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Aggiornare l'elenco delle tabelle del database.
  
    È possibile vedere che, anche se gli oggetti di dati R sono stati creati nell'area di lavoro locale, le tabelle non sono state create nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database. Inoltre, nessun dato è stato caricato dal file di testo nella variabile R.
  
4. Inserire i dati, chiamando la funzione [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) (funzione).
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    Supponendo che non si verifichino problemi con la stringa di connessione, dopo una breve pausa, verranno visualizzati risultati simili ai seguenti:
  
    *Totale righe scritte: 10000, totale tempo: 0.466* *righe lette: 10000, totale righe elaborate: 10000, tempo di blocco totale: 0.577 secondi*
  
5. Aggiornare l'elenco delle tabelle. Per verificare che ogni variabile abbia i tipi di dati corretti e sia stata importata correttamente, è anche possibile fare doppio clic nella tabella in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e selezionare **seleziona le prime 1000 righe**.

### <a name="load-data-into-the-scoring-table"></a>Caricare dati nella tabella di assegnazione dei punteggi

1. Ripetere i passaggi per caricare il set di dati utilizzato per l'assegnazione dei punteggi nel database.
  
    Iniziare indicando il percorso del file di origine.
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. Usare la funzione **RxTextData** per ottenere i dati e salvarli nella variabile *inTextData*.
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  Chiamare la funzione **rxDataStep** per sovrascrivere la tabella corrente con il nuovo schema e i nuovi dati.
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - L'argomento *inData* definisce l'origine dati da usare.
  
    - L'argomento *outFile* specifica la tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui verranno salvati i dati.
  
    - Se la tabella esiste già e non si usa la *sovrascrivere* opzione, i risultati vengono inseriti senza troncamenti.
  
Anche in questo caso, se la connessione ha avuto esito positivo, verrà visualizzato un messaggio che indica il completamento e il tempo necessario per scrivere i dati nella tabella:

*Totale righe scritte: 10000, totale tempo: 0.384*
*righe lette: 10000, totale righe elaborate: 10000, tempo di blocco totale: 0.456 secondi*

## <a name="more-about-rxdatastep"></a>Altre informazioni su rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) è una funzione potente che può eseguire più trasformazioni su un frame di dati R. È anche possibile usare rxDataStep per convertire i dati nella rappresentazione richiesta dalla destinazione: in questo caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Facoltativamente, è possibile specificare trasformazioni sui dati usando funzioni R negli argomenti di **rxDataStep**. Esempi di queste operazioni sono disponibili più avanti in questa esercitazione.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Eseguire query e modificare i dati SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)