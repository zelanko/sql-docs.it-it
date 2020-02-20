---
title: Creare oggetti RxSqlServerData
description: 'Esercitazione di RevoScaleR 2: Come creare oggetti dati usando il linguaggio R in SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7869fc3fc67cb24542223c2300cd7b6ebcf1eb41
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76922568"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>Creare oggetti dati di SQL Server usando RxSqlServerData (esercitazione di SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa è l'esercitazione 2 della [serie di esercitazioni per RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) dedicate all'uso delle [funzioni di RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Questa esercitazione è una continuazione di quella sulla creazione del database: aggiunta di tabelle e caricamento dei dati. Se un amministratore di database ha creato il database e l'account di accesso nell'[esercitazione 2](deepdive-work-with-sql-server-data-using-r.md), è possibile aggiungere tabelle usando un IDE R come RStudio o uno strumento integrato come **Rgui**.

Da R, connettersi a SQL Server e usare le funzioni di **RevoScaleR** per eseguire le attività seguenti:

> [!div class="checklist"]
> * Creare tabelle per i dati di training e le stime
> * Caricare i dati di un file CSV locale nelle tabelle

I dati di esempio sono dati di frodi con carta di credito simulate (set di dati ccFraud), partizionati in set di dati di training e di assegnazione dei punteggi. Il file di dati è incluso in **RevoScaleR**.

Usare un IDE R o **Rgui** per completare queste attività. Assicurarsi di usare i file eseguibili R disponibili in questo percorso: C:\Programmi\Microsoft\R Client\R_SERVER\bin\x64 (Rgui.exe se si usa lo strumento corrispondente o un IDE R che punta a C:\Programmi\Microsoft\R Client\R_SERVER). La presenza di una [workstation client R](../r/set-up-a-data-science-client.md) con questi eseguibili è un prerequisito di questa esercitazione.

## <a name="create-the-training-data-table"></a>Creare la tabella dei dati di training

1. Archiviare la stringa di connessione del database in una variabile R. Di seguito sono riportati due esempi di stringhe di connessione ODBC per SQL Server valide: una per un account di accesso SQL e una per l'autenticazione integrata di Windows. 

   Assicurarsi di modificare il nome del server, il nome utente e la password nel modo appropriato.

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
  
    Poiché l'istanza del server e il nome del database sono già specificati come parte della stringa di connessione, quando si combinano le due variabili il nome *completo* della nuova tabella diventa *instance.database.schema.ccFraudSmall*.
  
3.  Facoltativamente, specificare il parametro *rowsPerRead* per controllare il numero di righe di dati lette in ogni batch.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Anche se questo parametro è facoltativo, la sua impostazione può migliorare l'efficienza dei calcoli. La maggior parte delle funzioni di analisi avanzate in **RevoScaleR** e **MicrosoftML** elabora i dati in blocchi. Il parametro *rowsPerRead* determina il numero di righe in ogni blocco.
  
    Potrebbe essere necessario fare esperimenti con questa impostazione per trovare il giusto equilibrio. Se il valore è troppo grande, l'accesso ai dati potrebbe essere lento se non è disponibile memoria sufficiente per elaborare i dati in blocchi di quelle dimensioni. Viceversa, in alcuni sistemi, se il valore di *rowsPerRead* è troppo piccolo, le prestazioni possono risentirne.
  
    Come valore iniziale, usare le dimensioni predefinite del processo batch definite dall'istanza del motore di database per controllare il numero di righe in ogni blocco (5.000 righe). Salvare il valore nella variabile *sqlRowsPerRead*.
  
4.  Definire una variabile per il nuovo oggetto di origine dati e passare gli argomenti definiti in precedenza al costruttore **RxSqlServerData**. Si noti che l'oggetto viene creato ma non popolato. Il caricamento dei dati è un passaggio separato.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>Creare la tabella dei dati dei punteggi

Usando gli stessi passaggi, creare la tabella che contiene i dati dei punteggi mediante lo stesso processo.

1. Creare una nuova variabile R, *sqlScoreTable*, per archiviare il nome della tabella usata per l'assegnazione dei punteggi.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Inserire la variabile come argomento nella funzione **RxSqlServerData** per definire un secondo oggetto origine dati, *sqlScoreDS*.
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Poiché la stringa di connessione e altri parametri sono già stati definiti come variabili nell'area di lavoro di R, è possibile riutilizzarli per nuove origini dati che rappresentano tabelle, viste o query diverse.

> [!NOTE]
> La funzione usa argomenti diversi per definire un'origine dati basata su un'intera tabella rispetto a un'origine dati basata su una query. Il motivo è che il motore di database di SQL Server deve preparare le query in modo diverso. Più avanti in questa esercitazione si apprenderà come creare un oggetto origine dati basato su una query SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Caricare i dati in tabelle SQL con R

Ora che sono state create le tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è possibile caricare dati nelle tabelle usando la funzione **Rx** appropriata.

Il pacchetto **RevoScaleR** contiene funzioni specifiche dei tipi di origine dati. Per i dati di testo, usare [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) per generare l'oggetto origine dati. Sono disponibili funzioni aggiuntive per la creazione di oggetti origine dati da dati Hadoop, dati ODBC e così via.

> [!NOTE]
> Per questa sezione, è necessario avere le autorizzazioni **Esegui DDL** per il database.

### <a name="load-data-into-the-training-table"></a>Caricare i dati nella tabella di training

1. Creare una variabile R, *ccFraudCsv*, e assegnarle il percorso del file CSV contenente i dati di esempio. Questo set di dati è disponibile in **RevoScaleR**. "sampleDataDir" è una parola chiave nella funzione **rxGetOption**.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Si noti la chiamata a **rxGetOption**, che è il metodo GET associato a [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) in **RevoScaleR**. Usare questa utilità per impostare ed elencare le opzioni relative a contesti di calcolo locali e remoti, ad esempio la directory condivisa predefinita o il numero di processori (core) da usare nei calcoli.
    
    Questa particolare chiamata recupera gli esempi dalla libreria corretta indipendentemente dalla posizione in cui viene eseguito il codice. Ad esempio, provare a eseguire la funzione in SQL Server e nel computer di sviluppo e osservare i percorsi diversi.
  
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
  
3. A questo punto, si consiglia di prendersi un momento per visualizzare il database in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Aggiornare l'elenco delle tabelle del database.
  
    Come si può notare, anche se gli oggetti di dati R sono stati creati nell'area di lavoro locale, le tabelle non sono state create nel database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Inoltre, non sono stati caricati dati dal file di testo nella variabile R.
  
4. Inserire i dati chiamando la funzione [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep).
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    Supponendo che non si verifichino problemi con la stringa di connessione, dopo una breve pausa, verranno visualizzati risultati simili ai seguenti:
  
    *Totale righe scritte: 10000 - Tempo totale: 0,466* *Righe lette: 10000 - Totale righe elaborate: 10000 - Totale tempo blocco: 0,577 secondi*
  
5. Aggiornare l'elenco delle tabelle. Per verificare che ogni variabile abbia i tipi di dati corretti e sia stata importata correttamente, è anche possibile fare clic con il pulsante destro del mouse sulla tabella in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e scegliere **Seleziona le prime 1000 righe**.

### <a name="load-data-into-the-scoring-table"></a>Caricare i dati nella tabella di assegnazione dei punteggi

1. Ripetere la stessa procedura per caricare il set di dati usato per l'assegnazione dei punteggi nel database.
  
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
  
    - Se la tabella esiste già e non si usa l'opzione *overwrite* , i risultati vengono inseriti senza troncamenti.
  
Anche in questo caso, se la connessione ha avuto esito positivo, verrà visualizzato un messaggio che indica il completamento e il tempo necessario per scrivere i dati nella tabella:

*Totale righe scritte: 10000 - Tempo totale: 0,384*
*Righe lette: 10000 - Totale righe elaborate: 10000 - Totale tempo blocco: 0,456 secondi*

## <a name="more-about-rxdatastep"></a>Altre informazioni su rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) è una potente funzione che può eseguire più trasformazioni su un frame di dati R. È possibile usare rxDataStep anche per convertire i dati nella rappresentazione richiesta dalla destinazione, in questo caso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Facoltativamente, è possibile specificare le trasformazioni sui dati usando le funzioni R negli argomenti per **rxDataStep**. Esempi di queste operazioni sono disponibili più avanti in questa esercitazione.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Eseguire query e modificare i dati SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)