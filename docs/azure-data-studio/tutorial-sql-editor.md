---
title: "Esercitazione: Usare l'editor Transact-SQL per creare oggetti di database"
titleSuffix: Azure Data Studio
description: Questa esercitazione illustra le funzionalità principali in Azure Data Studio che semplificano l'uso con T-SQL.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 2a158ecd0223f7483494e4b28068c4634874e11d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797940"
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>Esercitazione: Usare l'editor Transact-SQL per creare oggetti di database- [!INCLUDE[name-sos](../includes/name-sos-short.md)]

La creazione e l'esecuzione di query, stored procedure, script, e così via sono le attività principali dei professionisti che operano su database. Questa esercitazione illustra le funzionalità chiave nell'editor T-SQL per creare oggetti database.

In questa esercitazione imparerete a usare [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] per:
> [!div class="checklist"]
> * Ricercare oggetti database
> * Modificare i dati della tabella 
> * Usare frammenti di codice per scrivere rapidamente T-SQL
> * Visualizzare i dettagli dell'oggetto database con *Visualizza definizione* e *Vai a definizione*


## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione richiede *TutorialDB*, un database su SQL Server o Database SQL di Azure. Per crearlo, completare una delle guide rapide seguenti:

- [Connettersi ed eseguire query su SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Connettersi ed eseguire query su Azure SQL Database tramite [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>Individuare rapidamente un oggetto database ed eseguire un'attività comune

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] fornisce un widget di ricerca per trovare rapidamente gli oggetti database. L'elenco dei risultati fornisce un menu di scelta rapida per le attività comuni relative all'oggetto selezionato, ad esempio *modifica dati* per una tabella.

1. Aprire la barra laterale server (**Ctrl + G**), espandere **database**e selezionare **TutorialDB**. 

1. Aprire la *Dashboard TutorialDB* selezionando **TutorialDB** e successivamente **Gestisci** dal menu di scelta rapida:

   ![menu di scelta rapida - gestione](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. Nella dashboard, fare doppio clic su **dbo.Customers** (nel widget di ricerca) e selezionare **modifica dati**.
   
   > [!TIP]
   > Per i database con molti oggetti, usare il widget di ricerca per individuare rapidamente ciò che si sta cercando, come tabelle, viste, e così via.

   ![widget di ricerca rapida](./media/tutorial-sql-editor/quick-search-widget.png)

1. Modificare la colonna **Email** nella prima riga, scrivendo *orlando0@adventure-works.comorlando0@adventure-works.com* . Premere **invio** per salvare le modifiche.

   ![Modificare i dati](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>Usare frammenti di codice T-SQL per creare le stored procedure

[!INCLUDE[name-sos](../includes/name-sos-short.md)] fornisce molti frammenti di codice T-SQL incorporati per la creazione rapida di istruzioni.


1. Aprire un nuovo editor di query premendo **Ctrl+N**.

2. Scrivere **sql** nell'editor, selezionare con la freccia verso il basso la voce **sqlCreateStoredProcedure** e premere il *tab* (o *invio*) per espandere il frammento relativo alle stored procedure.

   ![snippet-list](./media/tutorial-sql-editor/snippet-list.png)

3. Il frammento creato include due campi per la modifica rapida, *StoredProcedureName* e *SchemaName*. Selezionare *StoredProcedureName* e premere il pulsante destro del mouse. Selezionare quindi **Modifica tutte le occorrenze**. A questo punto digitare *getCustomer* e tutte le voci *StoredProcedureName* verranno sostituite da *getCustomer*.

   ![snippet](./media/tutorial-sql-editor/snippet.png)

5. Sostituire allo stesso modo tutte le occorrenze di *SchemaName* con *dbo*. 
6. Il frammento contiene segnaposto per parametri e testo da aggiornare nel corpo. Il comando *EXECUTE* contiene inoltre il segnaposto come commento, poiché non si sa a priori il numero di parametri che avrà la procedura. er questa esercitazione il frammento di codice di aggiornamento risulterà simile al codice seguente:

    ```sql
    -- Create a new stored procedure called 'getCustomer' in schema 'dbo'
    -- Drop the stored procedure if it already exists
    IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.ROUTINES
    WHERE SPECIFIC_SCHEMA = N'dbo'
    AND SPECIFIC_NAME = N'getCustomer'
    )
    DROP PROCEDURE dbo.getCustomer
    GO
    -- Create the stored procedure in the specified schema
    CREATE PROCEDURE dbo.getCustomer
    @ID int
    -- add more stored procedure parameters here
    AS
    -- body of the stored procedure
    SELECT  c.CustomerId, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerId = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. Per creare la stored procedure e testarne l'esecuzione, premere **F5**.

A questo punto viene creata la stored procedure e il riquadro **RISULTATI** mostra il record restituito in formato JSON. Per visualizzare il JSON formattato, fare clic sul record. 


## <a name="use-peek-definition"></a>Utilizzare Visualizza definizione 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] offre la possibilità di visualizzare una definizione di oggetti usando la funzionalità di anteprima della definizione. In questa sezione viene creata una seconda stored procedure e tramite Visualizza definizione vengono mostrate le colonne di una tabella per creare rapidamente il corpo della stored procedure che la consuma.

1. Aprire un nuovo editor premendo **Ctrl+N**. 

2. Scrivere *sql* nell'editor, selezionare con la freccia verso il basso la voce *sqlCreateStoredProcedure* e premere il *tab* (o *invio*) per espandere il frammento relativo alle stored procedure.
3. Digitare *setCustomer* per *StoredProcedureName* e *dbo* per *SchemaName*

3. Sostituire @param con la definizione di parametro seguente:

   ```sql
   @json_val nvarchar(max)
   ```

4. Sostituire il corpo della stored procedure con il codice seguente:
   ```sql
   INSERT INTO dbo.Customers
   ```

5. Nella *INSERT* appena aggiunta premere il tasto destro sulla tabella **dbo.Customers** e selezionare **Visualizza definizione**.

   ![Visualizza definizione](./media/tutorial-sql-editor/peek-definition.png)

6. La definizione della tabella viene mostrata in modo rapido ed è possibile visualizzare le colonne presenti nella tabella. Fare riferimento all'elenco delle colonne per completare facilmente le istruzioni per la stored procedure. Completare la creazione dell'istruzione INSERT e il corpo della stored procedure. Infine, chiudere la finestra di definizione:

   ```sql
   INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
    )
   ```
7. Eliminare (o impostare come commento) i comandi *EXECUTE* nella parte inferiore della query.
8. L'intera istruzione dovrebbe essere simile al seguente:

   ```sql
   -- Create a new stored procedure called 'setCustomer' in schema 'dbo'
   -- Drop the stored procedure if it already exists
   IF EXISTS (
   SELECT *
       FROM INFORMATION_SCHEMA.ROUTINES
       WHERE SPECIFIC_SCHEMA = N'dbo'
       AND SPECIFIC_NAME = N'setCustomer'
   )
   DROP PROCEDURE dbo.setCustomer
   GO
   -- Create the stored procedure in the specified schema
   CREATE PROCEDURE dbo.setCustomer
       @json_val nvarchar(max) 
   AS
       -- body of the stored procedure
       INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. Per creare la stored procedure *setCustomer*, premere **F5**.

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>Utilizzare il salvataggio dei risultati come JSON per testare la procedura setCustomer

La stored procedure *setCustomer* creata nella sezione precedente richiede i dati JSON passati nel parametro *@json_val* . In questa sezione viene illustrato come ottenere un JSON formattato correttamente per poi passarlo al parametro, in modo da testare la stored procedure.

1. Nella barra laterale **SERVER** premere il tasto destro del mouse su *dbo.Customers* e fare clic su **Seleziona le prime 1000 righe**.

2. Selezionare la prima riga nella visualizzazione dei risultati, assicurarsi che sia selezionata l'intera riga (il numero 1 nella colonna più a sinistra fare clic) e selezionare **Salva con nome JSON**.  
3. Cambiare la cartella in un percorso da ricordare al fine di eliminare il file in un secondo momento (sul desktop, ad esempio) e fare clic su **Salva**. Il file in formato JSON si aprirà.

   ![Salva come JSON](./media/tutorial-sql-editor/save-as-json.png)

4. Selezionare i dati JSON nell'editor e copiarlo.
5. Aprire un nuovo editor premendo **Ctrl+N**.
6. Nei passaggi precedenti viene illustrato come è possibile ottenere facilmente i dati formattati correttamente per completare la chiamata alla procedura *setCustomer*. Il codice seguente usa lo stesso formato JSON con nuovi dettagli in modo da poter testare la procedura *setCustomer*. L'istruzione include la sintassi per dichiarare il parametro ed eseguire le procedure di get e set. È possibile incollare i dati copiati dalla sezione precedente e modificarli o semplicemente incollare l'istruzione seguente nell'editor di query.

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerId": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. Eseguire premendo **F5**. Lo script inserisce un nuovo cliente e restituisce le nuove informazioni su di esso in formato JSON. Fare clic sul risultato per aprire una visualizzazione formattata.

   ![risultato del test](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione si è appreso come:
> [!div class="checklist"]
> * Ricercare oggetti database
> * Modificare i dati della tabella 
> * Scrivere lo script T-SQL utilizzando i frammenti di codice
> * Visualizzare i dettagli dell'oggetto database con Visualizza definizione e Vai a definizione


Per informazioni su come abilitare il widget delle **cinque query più lente**, completare l'esercitazione successiva:

> [!div class="nextstepaction"]
> [Abilitare il widget sulle query lente](tutorial-qds-sql-server.md)
