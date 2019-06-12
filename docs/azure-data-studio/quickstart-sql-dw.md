---
title: 'Avvio rapido: Connettersi ed eseguire query su Azure SQL Data Warehouse'
titleSuffix: Azure Data Studio
description: Questa Guida introduttiva illustra come usare Azure Data Studio per connettersi a un Azure SQL Data Warehouse ed eseguire una query
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: f98f6be4502254910b5c144f08a95181ccf1b2a7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800271"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>Avvio rapido: Usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per connettersi ed eseguire query sui dati in Azure SQL Data Warehouse

Con questa guida introduttiva viene illustrato come utilizzare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per connettersi a un Azure SQL Data Warehouse e quindi utilizzare istruzioni Transact-SQL per creare, inserire e selezionare i dati. 

## <a name="prerequisites"></a>Prerequisiti
Per completare questa guida rapida, è necessario [!INCLUDE[name-sos](../includes/name-sos-short.md)] e un'istanza di Azure SQL Data Warehouse.

- [Installare [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Se non si dispone già di un'istanza di SQL Data Warehouse, vedere [Creare un'istanza di SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Ricorda il nome del server e le credenziali di accesso.


## <a name="connect-to-your-data-warehouse"></a>Connettersi al data warehouse

Usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per stabilire una connessione al server Azure SQL Data Warehouse.

1. Alla prima esecuzione di [!INCLUDE[name-sos](../includes/name-sos-short.md)] verrà mostrata la pagina **Connessione**. Se essa non appare, fare clic sull'icona **Nuova connessione** nella barra laterale **SERVER**:
   
   ![Nuova connessione](media/quickstart-sql-dw/new-connection-icon.png)

2. Questo articolo usa *Account di accesso SQL*, ma l'accesso tramite *Autenticazione di Windows* è comunque supportato. Compilare i campi come indicato di seguito, specificando il nome del server, il nome utente e la password per il server Azure SQL usato:

   | Impostazione       | Valore suggerito | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome server** | Nome completo del server | Il nome deve essere simile al seguente: **sqldwsample.database.windows.net** |
   | **Autenticazione** | Account di accesso SQL| In questa esercitazione viene utilizzata l'autenticazione di SQL. |
   | **Nome utente** | Account amministratore del server | Si tratta dell'account specificato al momento della creazione del server. |
   | **Password (account di accesso SQL)** | Password per l'account amministratore del server | Si tratta della password specificata al momento della creazione del server. |
   | **Salvare la password?** | Sì o No | Selezionare Sì se non si vuole immettere la password ogni volta. |
   | **Nome database** | *Lasciare vuoto* | Il nome del database a cui si effettua la connessione. |
   | **Gruppo di server** | Selezionare <Default> | Se è stato creato un gruppo di server, è possibile impostare per un gruppo di server specifico. | 

   ![Icona "Nuova connessione"](media/quickstart-sql-dw/new-connection-screen.png) 

3. Se il server non dispone di una regola firewall che consenta di Studio dei dati di Azure per la connessione, il **Crea nuova regola del firewall** viene aperto. Completare il modulo per creare una nuova regola firewall. Per informazioni dettagliate, vedere [Regole del firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nuova regola del firewall](media/quickstart-sql-dw/firewall.png)  

4. Dopo avere stabilito la connessione al server, quest'ultimo appare nella barra laterale *Server*.

## <a name="create-the-tutorial-data-warehouse"></a>Creare il data warehouse per l'esercitazione
1. Fare clic con il pulsante destro sul server, in Esplora oggetti e selezionare **nuova Query.**

1. Incollare il seguente frammento di codice nell'editor di query, quindi fare clic su **Esegui**:

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

L'editor di query è ancora connesso al *master* database, ma si vuole creare una tabella sul database *TutorialDB*. 

1. Impostare il contesto di connessione su **TutorialDB**:

   ![Modifica del contesto](media/quickstart-sql-database/change-context.png)


1. Incollare il seguente frammento di codice nell'editor di query, quindi fare clic su **Esegui**:

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
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>Inserire righe

1. Incollare il seguente frammento di codice nell'editor di query, quindi fare clic su **Esegui**:

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
1. Incollare il seguente frammento di codice nell'editor di query, quindi fare clic su **Esegui**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Vengono visualizzati i risultati della query:

   ![Selezionare i risultati](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>Pulire le risorse

Altri articoli in questa raccolta si basano su questa guida rapida. Se si prevede di continuare con le esercitazioni successive, non pulire le risorse create in questa guida rapida. Se non si prevede di continuare, utilizzare la procedura seguente per eliminare le risorse create nel portale di Azure.
Pulire le risorse eliminando i gruppi di risorse che non sono più necessari. Per informazioni dettagliate, vedere [Pulire le risorse](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Passaggi successivi

Ora che si è connessi correttamente a un data warehouse Azure SQL e si sono eseguite query, provare l'[Esercitazione editor di codice](tutorial-sql-editor.md).
