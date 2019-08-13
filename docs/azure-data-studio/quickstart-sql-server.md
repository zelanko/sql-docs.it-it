---
title: 'Avvio rapido: Connettersi ed eseguire query in SQL Server'
titleSuffix: Azure Data Studio
description: Questo argomento di avvio rapido illustra come usare Azure Data Studio per connettersi a SQL Server ed eseguire una query
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.openlocfilehash: 4117d8c16e96252f792e14d282d285527008874f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959399"
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>Avvio rapido: Connettersi ed eseguire query in SQL Server con [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Questo argomento di avvio rapido illustra come usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per connettersi a SQL Server e come usare istruzioni Transact-SQL (T-SQL) per creare il database *TutorialDB* usato nelle esercitazioni di [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="prerequisites"></a>Prerequisites

Per completare questo argomento di avvio rapido è necessario [!INCLUDE[name-sos](../includes/name-sos-short.md)] e l'accesso a SQL Server.

- [Installare [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md).

Se non si ha accesso a SQL Server, selezionare la piattaforma dai collegamenti seguenti. Assicurarsi di conoscere l'account di accesso e la password SQL:
- [Windows - Scaricare SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)
- [macOS - Scaricare SQL Server 2017 in Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)
- [Linux - Scaricare SQL Server 2017 Developer Edition](https://docs.microsoft.com/sql/linux/sql-server-linux-overview#install): è sufficiente seguire la procedura per *Creare ed eseguire query sui dati*.


## <a name="connect-to-a-sql-server"></a>Connettersi a SQL Server

   
1. Avviare **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** .
1. La prima volta che si esegue [!INCLUDE[name-sos](../includes/name-sos-short.md)] viene visualizzata la pagina di **introduzione**. Se la pagina di **introduzione** non viene visualizzata, selezionare **Help** > **Introduzione**. Selezionare **Nuova connessione** per aprire il riquadro **Connessione**:
   
   ![Icona Nuova connessione](media/quickstart-sql-server/new-connection-icon.png)

1. Questo articolo usa l'account di *accesso SQL*, ma è supportata anche l'*autenticazione di Windows*. Compilare i campi come indicato di seguito:
 
    - **Nome server:** localhost
    - **Tipo di autenticazione:** Account di accesso SQL  
    - **Nome utente:** Nome utente di SQL Server  
    - **Password:** Password di SQL Server  
    - **Nome database:** lasciare vuoto questo campo 
    - **Gruppo di server:** \<Valore predefinito\>  

   ![Nuova schermata di connessione](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>Creazione di un database

Questa procedura consente di creare un database denominato **TutorialDB**:

1. Fare clic con il pulsante destro del mouse sul server, **localhost**, e selezionare **Nuova query**.
1. Incollare il frammento di codice seguente nella finestra di query: 

   ```sql
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
      CREATE DATABASE [TutorialDB];
   GO
   IF SERVERPROPERTY('ProductVersion') > '12'
       ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON;
   GO
   ```
1. Fare clic su **Esegui** per eseguire la query.

Dopo il completamento della query, nell'elenco di database viene incluso anche il nuovo database **TutorialDB**. Se il database non è visualizzato, fare clic con il pulsante destro del mouse sul nodo **Database** e selezionare **Aggiorna**.


## <a name="create-a-table"></a>Creare una tabella

Si vuole creare una tabella nel database *TutorialDB*, ma l'editor di query è ancora connesso al database *master*. 

1. Modificare il contesto di connessione in **TutorialDB**:

   ![Modifica del contesto](media/quickstart-sql-server/change-context.png)



1. Incollare il frammento di codice seguente nella finestra di query e fare clic su **Esegui**:

   > [!NOTE]
   > È possibile aggiungerlo alla query esistente nell'editor oppure sovrascriverla. Facendo clic su **Esegui** viene eseguita solo la query evidenziata. Se nessuna query risulta selezionata, facendo clic su **Esegui** vengono eseguite tutte le query nell'editor.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
      DROP TABLE dbo.Customers;
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
       CustomerId  int NOT NULL PRIMARY KEY, -- primary key column
       Name        nvarchar(50) NOT NULL,
       Location    nvarchar(50) NOT NULL,
       Email       nvarchar(50) NOT NULL
   );
   GO
   ```

Dopo il completamento della query, nell'elenco di tabelle viene inclusa anche la nuova tabella **Clienti**. Potrebbe essere necessario fare clic con il pulsante destro del mouse sul nodo **TutorialDB > Tabelle** e selezionare **Aggiorna**.

## <a name="insert-rows"></a>Inserire righe

- Incollare il frammento di codice seguente nella finestra di query e fare clic su **Esegui**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId], [Name], [Location], [Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```



## <a name="view-the-data-returned-by-a-query"></a>Visualizzare i dati restituiti da una query
1. Incollare il frammento di codice seguente nella finestra di query e fare clic su **Esegui**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Vengono visualizzati i risultati della query:

   ![Selezione dei risultati](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>Passaggi successivi
Ora che è stata effettuata la connessione a SQL Server ed è stata eseguita una query, effettuare l'[esercitazione sull'editor di codice](tutorial-sql-editor.md).


