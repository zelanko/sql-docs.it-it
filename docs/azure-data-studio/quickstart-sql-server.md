---
title: 'Guida introduttiva: Connettersi ed eseguire query di SQL Server'
titleSuffix: Azure Data Studio
description: Questa Guida introduttiva illustra come usare Azure Data Studio per connettersi a SQL Server ed eseguire una query
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 9e25008836b72ac8860953c5a1f98c13d7540d92
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143451"
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>Guida introduttiva: Connettersi ed eseguire query usando SQL Server [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Con questa guida introduttiva viene illustrato come utilizzare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per connettersi a SQL Server e quindi utilizzare istruzioni Transact-SQL (T-SQL) per creare il *TutorialDB* utilizzato [!INCLUDE[name-sos](../includes/name-sos-short.md)] esercitazioni.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa guida rapida, è necessario [!INCLUDE[name-sos](../includes/name-sos-short.md)] e un accesso a SQL Server.

- [Installare [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Se non si dispone di alcun SQL Server, selezionare la piattaforma usata dai collegamenti seguenti (assicurarsi di usare l'account di accesso SQL e la password corretti):
- [Windows - Scaricare SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)
- [macOS - Scaricare SQL Server 2017 in Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)
- [Linux - scaricare SQL Server 2017 Developer Edition](https://docs.microsoft.com/sql/linux/sql-server-linux-overview#install) -è sufficiente seguire i passaggi fino a *creare ed eseguire query sui dati*.


## <a name="connect-to-a-sql-server"></a>Connettersi a SQL Server

   
1. Avviare **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**.
1. Alla prima esecuzione di  *[!INCLUDE[name-sos](../includes/name-sos-short.md)]* verrà mostrata la finestra di dialogo **Connessione**.  Se essa non appare, fare clic sull'icona **Nuova connessione** nella pagina **SERVER**:
   
   ![Icona "Nuova connessione"](media/quickstart-sql-server/new-connection-icon.png)

1. Questo articolo usa *Account di accesso SQL*, ma l'accesso tramite *Autenticazione di Windows* è comunque supportato. Compilare i campi come indicato di seguito:
 
    - **Nome del server:** localhost
    - **Tipo di autenticazione:** Account di accesso SQL  
    - **Nome utente:** Nome utente per SQL Server  
    - **Password:** Password per SQL Server  
    - **Nome del database:** lasciare vuoto questo campo 
    - **Gruppo di server:** \<Default\>  

   ![Schermata "Nuova connessione"](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>Creazione di un database

La procedura seguente crea un database denominato **TutorialDB**:

1. Fare clic con il pulsante destro sul server, **localhost**e selezionare **nuova Query.**
1. Nella finestra query, incollare il frammento seguente: 

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

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```
1. Per eseguire la query, fare clic su **Esegui** .

Dopo il completamento della query, il nuovo **TutorialDB** viene visualizzato nell'elenco dei database.  Se non è presente, fare doppio clic sul nodo **Database** e selezionare **Aggiorna**.


## <a name="create-a-table"></a>Creare una tabella

L'editor di query è ancora connesso al *master* database, ma si vuole creare una tabella sul database *TutorialDB*. 

1. Impostare il contesto di connessione su **TutorialDB**:

   ![Modifica del contesto](media/quickstart-sql-server/change-context.png)



1. Incollare il frammento di codice seguente nella finestra query, quindi fare clic su **Esegui**:

   > [!NOTE]
   > È possibile aggiungere lo script o sovrascrivere la query precedente nell'editor. Si noti che il clic su **Esegui** esegue solo la query selezionata. Se nulla è selezionato, tutte le query presenti nel foglio vengono eseguite. Se nulla è selezionato, tutte le query presenti nel foglio vengono eseguite. 

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

Dopo il completamento della query, la nuova tabella **dbo.Customers** è visualizzata nell'elenco di tabelle.  Potrebbe tuttavia essere necessario fare clic con il pulsante destro del mouse sul nodo **TutorialDB > Tabelle** e selezionare **Aggiorna**.

## <a name="insert-rows"></a>Inserire righe

- Incollare il frammento di codice seguente nella finestra query, quindi fare clic su **Esegui**:

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



## <a name="view-the-data-returned-by-a-query"></a>Visualizzare i dati restituiti da una query
1. Incollare il frammento di codice seguente nella finestra query, quindi fare clic su **Esegui**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Vengono visualizzati i risultati della query:

   ![Selezionare i risultati](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>Passaggi successivi
Ora che si è connessi con SQL Server e si sono eseguite query, provare l'[esercitazione editor di codice](tutorial-sql-editor.md).


