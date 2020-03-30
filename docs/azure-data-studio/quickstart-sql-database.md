---
title: Connettersi ed eseguire query nel database SQL di Azure
titleSuffix: Azure Data Studio
description: Questo argomento di avvio rapido illustra come usare Azure Data Studio per connettersi a un database SQL ed eseguire una query
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; maghan; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.custom: seodec18; sqlfreshmay19; seo-lt-2019
ms.date: 05/14/2019
ms.openlocfilehash: 2ed7841c3e6205ad0a6df4f232f021aeb24983cd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "74957075"
---
# <a name="quickstart-use-name-sos-to-connect-and-query-azure-sql-database"></a>Guida introduttiva: Usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per connettersi ed eseguire query nel database SQL di Azure

In questo argomento di avvio rapido si userà [!INCLUDE[name-sos](../includes/name-sos-short.md)] per connettersi a un server di database SQL di Azure. Verranno quindi eseguite istruzioni Transact-SQL (T-SQL) per creare ed eseguire query sul database TutorialDB, usato anche in altre esercitazioni di [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="prerequisites"></a>Prerequisiti

Per completare questo argomento di avvio rapido è necessario [!INCLUDE[name-sos](../includes/name-sos-short.md)] e un server di database SQL di Azure.

- [Installare [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)

Se non si ha ancora un server SQL di Azure, completare uno dei seguenti argomenti di avvio rapido sui database SQL di Azure. Ricordare il nome completo del server e le credenziali di accesso per i passaggi successivi:

- [Creare un database - Portale](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Creare un database - Interfaccia della riga di comando](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Creare un database - PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Connettersi al server di database SQL di Azure

Usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per stabilire una connessione al server di database SQL di Azure.

1. La prima volta che si esegue [!INCLUDE[name-sos](../includes/name-sos-short.md)] viene visualizzata la pagina di **introduzione**. Se la pagina di **introduzione** non viene visualizzata, selezionare **Help** > **Introduzione**. Selezionare **Nuova connessione** per aprire il riquadro **Connessione**:
   
   ![Icona Nuova connessione](media/quickstart-sql-database/new-connection-icon.png)

2. Questo articolo usa le credenziali di accesso SQL, ma supporta anche l'autenticazione di Windows. Compilare i campi seguenti usando il nome server, il nome utente e la password relativi al server SQL di Azure:

   | Impostazione       | Valore consigliato | Descrizione |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome server** | Nome completo del server | Ad esempio: **servername.database.windows.net**. |
   | **autenticazione** | Account di accesso SQL| In questa esercitazione viene usata l'autenticazione SQL. |
   | **Nome utente** | Nome utente dell'account amministratore del server | Nome utente dell'account usato per creare il server. |
   | **Password (account di accesso SQL)** | Password dell'account amministratore del server | Password dell'account usato per creare il server. |
   | **Salvare la password?** | Sì o No | Se non si vuole immettere ogni volta la password, selezionare **Sì**. |
   | **Nome database** | *lasciare vuoto* | Questa opzione consente esclusivamente di effettuare la connessione al server. |
   | **Gruppo di server** | Selezionare <Default> | È possibile impostare questo campo su uno specifico gruppo di server precedentemente creato. | 

   ![Icona Nuova connessione](media/quickstart-sql-database/new-connection-screen.png)  

3. Selezionare **Connetti**.

4. Se nel server non è presente una regola del firewall che consente la connessione di Azure Data Studio, viene visualizzato il modulo **Crea nuova regola del firewall**. Completare il modulo per creare una nuova regola del firewall. Per informazioni dettagliate, vedere [Regole del firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nuova regola del firewall](media/quickstart-sql-database/firewall.png)  

Dopo il completamento della connessione, il server si apre nella barra laterale **SERVER**.

## <a name="create-the-tutorial-database"></a>Creare il database dell'esercitazione

Nelle sezioni successive verrà creato il database TutorialDB usato anche in altre esercitazioni di [!INCLUDE[name-sos](../includes/name-sos-short.md)].

1. Fare clic con il pulsante destro del mouse sul server SQL di Azure nella barra laterale **SERVER** e scegliere **Nuova query**.

1. Incollare questo SQL nell'editor di query.

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. Sulla barra degli strumenti selezionare **Esegui**. Nel riquadro **MESSAGGI** vengono visualizzate alcune notifiche che informano l'utente sullo stato di avanzamento della query.

## <a name="create-a-table"></a>Creare una tabella

Si vuole creare una tabella nel database **TutorialDB**, ma l'editor di query è connesso al database **master**. 

1. Connettersi al database **TutorialDB**.

   ![Modifica del contesto](media/quickstart-sql-database/change-context2.png)



1. Creare una tabella `Customers`. 

   Nell'editor di query sostituire la query precedente con questa e selezionare **Esegui**.

   ```sql
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


## <a name="insert-rows-into-the-table"></a>Inserire righe nella tabella

Sostituire la query precedente con questa e selezionare **Esegui**.

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

## <a name="view-the-result"></a>Visualizzare il risultato

Sostituire la query precedente con questa e selezionare **Esegui**.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

Vengono visualizzati i risultati della query:

   ![Selezione dei risultati](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>Pulire le risorse

Gli argomenti di avvio rapido successivi si basano sulle risorse create qui. Se si prevede di svolgere anche le procedure degli articoli successivi, assicurarsi di non eliminare queste risorse. In caso contrario, nel portale di Azure eliminare le risorse non più necessarie. Per informazioni dettagliate, vedere [Pulire le risorse](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Passaggi successivi

Ora che è stata effettuata la connessione a un database SQL di Azure ed è stata eseguita una query, effettuare l'[esercitazione sull'editor di codice](tutorial-sql-editor.md).
