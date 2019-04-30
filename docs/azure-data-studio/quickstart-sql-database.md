---
title: 'Avvio rapido: Connettersi ed eseguire query su un database SQL di Azure'
titleSuffix: Azure Data Studio
description: Questa Guida introduttiva illustra come usare Azure Data Studio per connettersi a un database SQL ed eseguire una query
ms.custom: seodec18
ms.date: 12/21/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: d368f38589530f27db98c3c61b9cec4610818ae4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63255957"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Avvio rapido: Usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] connettersi ed eseguire query di database SQL di Azure

In questa Guida introduttiva si userà [!INCLUDE[name-sos](../includes/name-sos-short.md)] per connettersi a un server di Database SQL di Azure. Sarà quindi possibile eseguire istruzioni Transact-SQL (T-SQL) per creare ed eseguire query sul database TutorialDB, che viene usato in altri [!INCLUDE[name-sos](../includes/name-sos-short.md)] esercitazioni.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa Guida introduttiva, è necessario [!INCLUDE[name-sos](../includes/name-sos-short.md)]e un server di Database SQL di Azure.

- [Installare [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)

Se non si dispone di un server SQL di Azure, completare una delle guide introduttive seguenti Database SQL di Azure. Ricordare il nome completo del server e le credenziali per i passaggi successivi di accesso:

- [Creare un database - portale](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Creare un database - CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Creare un database: PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Connettersi al server di Database SQL di Azure

Usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per stabilire una connessione al server di Database SQL di Azure.

1. Alla prima esecuzione di [!INCLUDE[name-sos](../includes/name-sos-short.md)] verrà mostrata la pagina **Connessione**. Se non viene visualizzato il **connessione** pagina, selezionare **Aggiungi connessione**, o la **nuova connessione** icona nel **server** sidebar:
   
   ![Icona "Nuova connessione"](media/quickstart-sql-database/new-connection-icon.png)

2. Questo articolo Usa Accedi SQL, ma supporta anche l'autenticazione di Windows. Compilare i campi seguenti con il nome del server, nome utente e password per il server SQL di Azure:

   | Impostazione       | Valore suggerito | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome server** | Nome completo del server | Ad esempio: **nomeserver.database.Windows.NET**. |
   | **Autenticazione** | Account di accesso SQL| Questa esercitazione Usa l'autenticazione di SQL. |
   | **Nome utente** | Il nome utente dell'account amministratore server | Il nome utente dall'account usato per creare il server. |
   | **Password (account di accesso SQL)** | La password dell'account amministratore server | La password dall'account usato per creare il server. |
   | **Salvare la password?** | Sì o No | Selezionare **Sì** se non si vuole immettere la password ogni volta. |
   | **Nome database** | *Lasciare vuoto* | Ci si connette solo al server di seguito. |
   | **Gruppo di server** | Selezionare <Default> | È possibile impostare questo campo a un gruppo di server specifico che è stato creato. | 

   ![Icona "Nuova connessione"](media/quickstart-sql-database/new-connection-screen.png)  

3. Selezionare **Connetti**.

4. Se il server non dispone di una regola firewall che consenta di Studio dei dati di Azure per la connessione, il **Crea nuova regola del firewall** viene aperto. Completare il modulo per creare una nuova regola firewall. Per informazioni dettagliate, vedere [Regole del firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nuova regola del firewall](media/quickstart-sql-database/firewall.png)  

Dopo aver stabilito la connessione, il server viene aperto nel **server** nella barra laterale.

## <a name="create-the-tutorial-database"></a>Creare il database dell'esercitazione

Nelle sezioni successive creare il database TutorialDB usato in altri [!INCLUDE[name-sos](../includes/name-sos-short.md)] esercitazioni.

1. Fare clic sul server SQL di Azure nel **i server** nella barra laterale e selezionare **nuova Query**.

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

1. Nella barra degli strumenti, selezionare **eseguiti**. Le notifiche risultano visibili nel **messaggi** riquadro che mostra lo stato di avanzamento di query.

## <a name="create-a-table"></a>Creare una tabella

È connesso l'editor di query per il **master** database, ma si desidera creare una tabella nel **TutorialDB** database. 

1. Connettere il **TutorialDB** database.

   ![Modifica del contesto](media/quickstart-sql-database/change-context2.png)



1. Creare un `Customers` tabella. 

   Sostituire la query precedente nell'editor di query a uno e selezionare **eseguiti**.

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

Sostituire la query precedente con quella e selezionare **eseguiti**.

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

Sostituire la query precedente con quella e selezionare **eseguiti**.

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

Visualizzare i risultati della query:

   ![Selezionare i risultati](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>Pulire le risorse

Gli articoli di Guida introduttiva successiva si basano le risorse create in questo caso. Se si prevede di usare gli articoli seguenti, assicurarsi di non eliminare tali risorse. In caso contrario, nel portale di Azure, è possibile eliminare le risorse che non è più necessario. Per informazioni dettagliate, vedere [Pulire le risorse](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Passaggi successivi

Ora che è stato connesso a un database SQL di Azure ed eseguire una query, provare il [esercitazione di editor di codice](tutorial-sql-editor.md).
