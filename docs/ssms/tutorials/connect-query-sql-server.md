---
title: Connettersi a un'istanza di SQL Server ed eseguire query
description: Esercitazione per la connessione a un'istanza di SQL Server tramite SQL Server Management Studio e l'esecuzione di query T-SQL di base.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: markingmyname
ms.author: maghan
ms.reviewer: sstein; maghan
ms.topic: tutorial
ms.prod_service: sql-tools
ms.prod: sql
ms.technology: ssms
ms.custom: seo-lt-2019
ms.date: 03/13/2018
ms.openlocfilehash: ac805437d716bbc7e8fdf95f491c64331ddb4658
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286265"
---
# <a name="tutorial-connect-to-and-query-a-sql-server-instance-by-using-sql-server-management-studio-ssms"></a>Esercitazione: Connettersi a un'istanza di SQL Server ed eseguire query con SQL Server Management Studio (SSMS)

Questa esercitazione illustra come usare SQL Server Management Studio (SSMS) per connettersi all'istanza di SQL Server ed eseguire alcuni comandi Transact-SQL (T-SQL) di base. Questo articolo illustra come seguire i passaggi seguenti:

> [!div class="checklist"]
> * Connessione a un'istanza di SQL Server
> * Creare un database ("TutorialDB")
> * Creare una tabella ("Customers") nel nuovo database
> * Inserire righe nella nuova tabella
> * Eseguire query nella tabella e visualizzare i risultati
> * Usare la tabella della finestra di query per verificare le proprietà di connessione
> * Modificare il server al quale è connessa la finestra di query

## <a name="prerequisites"></a>Prerequisiti

Per completare questa esercitazione è necessario avere SQL Server Management Studio e l'accesso a un'istanza di SQL Server. 

* Installare [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Se non si dispone dell'accesso a un'istanza di SQL Server, selezionare la piattaforma in uso tra i collegamenti seguenti. Se si sceglie Autenticazione SQL, usare le credenziali di accesso di SQL Server.

* **Windows**: [Scaricare SQL Server 2017 Developer](https://www.microsoft.com/sql-server/sql-server-downloads).
* **macOS**: [Scaricare SQL Server 2017 in Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

## <a name="connect-to-a-sql-server-instance"></a>Connessione a un'istanza di SQL Server

1. Avviare SQL Server Management Studio. Quando si esegue SSMS per la prima volta viene visualizzata la finestra di dialogo **Connetti al server**. Se la finestra non si apre è possibile aprirla manualmente selezionando **Esplora oggetti** > **Connetti** > **Motore di database**.

    ![Collegamento Connetti in Esplora oggetti](media/connect-query-sql-server/connectobjexp.png)

2. Nella finestra **Connetti al server** seguire l'elenco seguente:

    * In **Tipo di server** selezionare **Motore di database** (in genere l'opzione predefinita).
    * In **Nome server** immettere il nome dell'istanza di SQL Server in uso. In questo articolo viene usato il nome istanza SQL2016ST sul nome host NODE5 [NODE5\SQL2016ST]. Se non si sa come determinare il nome dell'istanza di SQL Server, vedere [Suggerimenti e consigli per l'uso di SSMS](ssms-tricks.md#determine-sql-server-name).

    * In **Autenticazione** selezionare **Autenticazione di Windows**. In questo articolo viene usata l'autenticazione di Windows, ma è supportato anche l'accesso di SQL Server. Se si seleziona **Account di accesso SQL** viene richiesto di specificare un nome utente e una password. Per altre informazioni sui tipi di autenticazione, vedere [Connetti al server (motore di database)](https://docs.microsoft.com/sql/ssms/f1-help/connect-to-server-database-engine).

    ![Campo "Nome server" con l'opzione per l'uso dell'istanza di SQL Server](media/connect-query-sql-server/connection2.png)

    È anche possibile modificare altre opzioni di connessione selezionando **Opzioni**. Sono esempi di opzioni di connessione il database al quale ci si connette, il valore di timeout della connessione e il protocollo di rete. In questo articolo vengono usati i valori predefiniti per tutte le opzioni.

3. Dopo aver completato tutti i campi selezionare **Connetti**.

### <a name="examples-of-successful-connections"></a>Esempi di connessioni riuscite

Per verificare se la connessione a SQL Server è stata eseguita correttamente, espandere ed esplorare gli oggetti in **Esplora oggetti**. Questi oggetti sono diversi a seconda del tipo di server al quale si sceglie di connettersi. 

* Connessione a un server SQL Server locale, in questo caso NODE5\SQL2016ST: ![Connessione a un server locale](media/connect-query-sql-server/connect-on-prem.png)

* Connessione a un database SQL di Azure, in questo caso msftestserver.database.windows.net: ![Connessione a un database SQL di Azure](media/connect-query-sql-server/connect-sql-azure.png)

  >[!NOTE]
  > In questa esercitazione è stata usata l'*autenticazione di Windows* per connettersi al server SQL Server locale, ma questo metodo non è supportato per il database SQL di Azure. Pertanto la figura seguente illustra l'uso dell'autenticazione SQL per la connessione al database SQL di Azure. Per altre informazioni, vedere [Autenticazione per SQL locale](../../relational-databases/security/choose-an-authentication-mode.md) e [Autenticazione per SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview#access-management). 

## <a name="create-a-database"></a>Creazione di un database

Creare un database denominato TutorialDB seguendo questa procedura:

1. Fare clic con il pulsante destro del mouse in Esplora oggetti e scegliere **Nuova query**:

   ![Collegamento Nuova query](media/connect-query-sql-server/newquery.png)

2. Nella finestra di query incollare il frammento di codice T-SQL seguente: 

   ```sql
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```

3. Per eseguire la query fare clic su **Esegui** o premere F5 sulla tastiera.

   ![Comando Esegui](media/connect-query-sql-server/execute.png)
  
    Al termine della query il nuovo database TutorialDB viene visualizzato nell'elenco dei database in Esplora oggetti. Se il database non viene visualizzato, fare clic con il pulsante destro del mouse sul nodo **Database** e selezionare **Aggiorna**.  

## <a name="create-a-table-in-the-new-database"></a>Creare una tabella nel nuovo database

In questa sezione si crea una tabella nel database TutorialDB appena creato. L'editor di query è ancora nel contesto del database *master*. Cambiare il contesto e impostare la connessione al database *TutorialDB* seguendo questa procedura:

1. Nella casella di riepilogo a discesa dei database selezionare il database desiderato, come indicato di seguito: 

   ![Modificare il database](media/connect-query-sql-server/changedb.png)

2. Incollare il frammento di codice T-SQL seguente nella finestra di query, selezionarlo e fare clic su **Esegui** o premere F5 sulla tastiera.  
   È possibile sostituire il testo esistente nella finestra di query o aggiungerlo alla fine. Per eseguire l'intero testo nella finestra di query, selezionare **Esegui**. Se il testo è stato aggiunto, è opportuno eseguire solo la parte del testo. Evidenziare quindi la parte e selezionare **Esegui**.  
  
   ```sql
   USE [TutorialDB]
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

Al termine della query la nuova tabella Customers viene visualizzata nell'elenco delle tabelle in Esplora oggetti. Se la tabella non viene visualizzata, fare clic con il pulsante destro del mouse sul nodo **TutorialDB** > **Tabelle** in Esplora oggetti e scegliere **Aggiorna**.

## <a name="insert-rows-into-the-new-table"></a>Inserire righe nella nuova tabella

Ora si inseriranno alcune righe nella tabella Customers creata in precedenza. Incollare il frammento di codice T-SQL seguente nella finestra di query e selezionare **Esegui**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="query-the-table-and-view-the-results"></a>Eseguire query nella tabella e visualizzare i risultati

I risultati di una query vengono visualizzati sotto la finestra di testo della query. Per eseguire una query sulla tabella Customers e visualizzare le righe inserite in precedenza, seguire questa procedura:

1. Incollare il frammento di codice T-SQL seguente nella finestra di query e selezionare **Esegui**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

    I risultati della query vengono visualizzati al di sotto dell'area in cui è stato immesso il testo: 

   ![Elenco Risultati](media/connect-query-sql-server/queryresults.png)

2. Modificare il formato di visualizzazione dei risultati selezionando una delle opzioni seguenti:

     ![Tre opzioni per la visualizzazione dei risultati della query](media/connect-query-sql-server/results.png)

    * Il pulsante centrale visualizza i risultati in **Visualizzazione griglia**, l'opzione predefinita. 
    * Il primo pulsante visualizza i risultati in **Visualizzazione testo**, come illustrato nell'immagine della sezione successiva.
    * Il terzo pulsante consente di salvare i risultati in un file che per impostazione predefinita ha l'estensione rpt.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>Verificare le proprietà di connessione usando la tabella della finestra di query

È possibile trovare informazioni sulle proprietà di connessione tra i risultati della query. Dopo aver eseguito la query specificata nel passaggio precedente, esaminare le proprietà di connessione nella parte inferiore della finestra di query.

* È possibile determinare il server e il database ai quali si è connessi e il nome utente usato.
* È anche possibile visualizzare la durata della query e il numero di righe restituite dalla query eseguita in precedenza.

    ![Proprietà di connessione](media/connect-query-sql-server/connectionproperties.png)

    > [!Note]
    > Nell'immagine i risultati sono visualizzati in **Visualizzazione testo**.

## <a name="change-the-server-based-on-the-query-window"></a>Modificare il server in base alla finestra di query

È possibile modificare il server al quale è connessa la finestra di query corrente seguendo questa procedura:

1. Fare clic con il pulsante destro del mouse nella finestra di query e selezionare **Connessione** > **Cambia connessione**. Viene visualizzata di nuovo la finestra **Connetti al server**.

2. Modificare il server usato dalla query.

   ![Comando Cambia connessione](media/connect-query-sql-server/changeconnection.png)

    > [!NOTE]
    > Questa azione modifica solo il server al quale è connessa la finestra di query e non il server usato da Esplora oggetti.

## <a name="azure-data-studio"></a>Azure Data Studio

È anche possibile connettersi ed eseguire query di [SQL Server](../../azure-data-studio/quickstart-sql-server.md), di un [database SQL di Azure](../../azure-data-studio/quickstart-sql-database.md) e di [Azure SQL Data Warehouse](../../azure-data-studio/quickstart-sql-dw.md) usando Azure Data Studio.

## <a name="next-steps"></a>Passaggi successivi

Il modo migliore per acquisire familiarità con SSMS è la pratica diretta. Questi articoli illustrano le varie funzionalità disponibili in SSMS. Questi articoli illustrano come gestire i componenti di SSMS e individuare le funzionalità usate regolarmente.

* [Scripting](scripting-ssms.md)
* [Uso di modelli in SSMS](../template/templates-ssms.md)
* [Configurazione di SSMS](ssms-configuration.md)
* [Suggerimenti e consigli per l'uso di SSMS](ssms-tricks.md)
* [Azure Data Studio](../../azure-data-studio/download.md)