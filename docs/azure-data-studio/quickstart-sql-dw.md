---
title: Connettersi a un data warehouse SQL di Azure ed eseguire query
description: Questo argomento di avvio rapido illustra come usare Azure Data Studio per connettersi ad Azure SQL Data Warehouse ed eseguire una query
ms.prod: azure-data-studio
ms.technology: ''
ms.reviewer: alayu, maghan, sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: f9a8213dacb3a7f221d3a3c3e51f0ed94bb6990a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728015"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>Avvio rapido: Usare Azure Data Studio per connettersi a un data warehouse SQL di Azure ed eseguire query sui dati

Questo avvio rapido illustra come usare Azure Data Studio per connettersi a un data warehouse SQL di Azure e quindi usare istruzioni Transact-SQL per creare, inserire e selezionare dati. 

## <a name="prerequisites"></a>Prerequisiti
Per completare questo avvio rapido, è necessario Azure Data Studio e un data warehouse SQL di Azure.

- [Installare Azure Data Studio](download.md).

Se Azure Data Studio non è ancora stato installato, vedere [Creare un data warehouse SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Annotare il nome del server e le credenziali di accesso.


## <a name="connect-to-your-data-warehouse"></a>Connettersi al data warehouse

Usare Azure Data Studio per stabilire una connessione al server del data warehouse SQL di Azure.

1. La prima volta che si esegue Azure Data Studio viene visualizzata la pagina **Connessione**. Se la pagina **Connessione** non viene visualizzata, fare clic su **Aggiungi connessione** o sull'icona **Nuova connessione** nella barra laterale **SERVER**:
   
   ![Icona Nuova connessione](media/quickstart-sql-dw/new-connection-icon.png)

2. Questo articolo usa l'account di *accesso SQL*, ma è supportata anche l'*autenticazione di Windows*. Compilare i campi seguenti usando il nome server, il nome utente e la password relativi al *server SQL di Azure*:

   | Impostazione       | Valore consigliato | Descrizione |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome server** | Nome completo del server | Il nome deve essere simile a: **sqldwsample.database.windows.net** |
   | **autenticazione** | Account di accesso SQL| In questa esercitazione viene usata l'autenticazione SQL. |
   | **Nome utente** | Account amministratore del server | Si tratta dell'account specificato al momento della creazione del server. |
   | **Password (account di accesso SQL)** | Password per l'account amministratore del server | Si tratta della password specificata al momento della creazione del server. |
   | **Salvare la password?** | Sì o No | Se non si vuole immettere la password ogni volta, selezionare Sì. |
   | **Nome database** | *lasciare vuoto* | Il nome del database a cui si effettua la connessione. |
   | **Gruppo di server** | Selezionare <Default> | È possibile impostare questo campo su uno specifico gruppo di server precedentemente creato. | 

   ![Icona Nuova connessione](media/quickstart-sql-dw/new-connection-screen.png) 

3. Se nel server non è presente una regola del firewall che consente la connessione di Azure Data Studio, viene visualizzato il modulo **Crea nuova regola del firewall**. Completare il modulo per creare una nuova regola del firewall. Per informazioni dettagliate, vedere [Regole del firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nuova regola del firewall](media/quickstart-sql-dw/firewall.png)  

4. Dopo il completamento della connessione, il server si apre nella barra laterale *Server*.

## <a name="create-the-tutorial-data-warehouse"></a>Creare il data warehouse dell'esercitazione
1. Fare clic con il pulsante destro del mouse in Esplora oggetti del server e scegliere **Nuova query**.

1. Incollare il frammento di codice seguente nell'editor di query e fare clic su **Esegui**:

   ```sql
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB] (EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
    GO  
    
    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
   ```


## <a name="create-a-table"></a>Creare una tabella

Si vuole creare una tabella nel database *TutorialDB*, ma l'editor di query è ancora connesso al database *master*. 

1. Modificare il contesto di connessione in **TutorialDB**:

   ![Modifica del contesto](media/quickstart-sql-database/change-context.png)


1. Incollare il frammento di codice seguente nell'editor di query e fare clic su **Esegui**:

   > [!NOTE]
   > È possibile aggiungerlo alla query esistente nell'editor oppure sovrascriverla. Facendo clic su **Esegui** viene eseguita solo la query evidenziata. Se nessuna query risulta selezionata, facendo clic su **Esegui** vengono eseguite tutte le query nell'editor.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>Inserire righe

1. Incollare il frammento di codice seguente nell'editor di query e fare clic su **Esegui**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```


## <a name="view-the-result"></a>Visualizzare il risultato
1. Incollare il frammento di codice seguente nell'editor di query e fare clic su **Esegui**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Vengono visualizzati i risultati della query:

   ![Selezione dei risultati](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>Pulire le risorse

Altri articoli contenuti in questa raccolta si basano su questo argomento di avvio rapido. Se si prevede di svolgere anche gli argomenti di avvio rapido successivi, non eliminare le risorse create in questo argomento. In caso contrario, attenersi alla procedura seguente per eliminare le risorse create da questo argomento di avvio rapido nel portale di Azure.
Per pulire le risorse, eliminare i gruppi di risorse non più necessari. Per informazioni dettagliate, vedere [Pulire le risorse](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Passaggi successivi

Ora che è stata effettuata la connessione ad Azure SQL Data Warehouse ed è stata eseguita una query, effettuare l'[esercitazione sull'editor di codice](tutorial-sql-editor.md).
