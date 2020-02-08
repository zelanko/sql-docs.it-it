---
title: 'Avvio rapido: Connettersi ed eseguire query in PostgreSQL'
titleSuffix: Azure Data Studio
description: Questo argomento di avvio rapido illustra come usare Azure Data Studio per connettersi a PostgreSQL ed eseguire una query
ms.custom: seodec18
ms.date: 09/18/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
ms.openlocfilehash: ac4d1a3ae93310475c284661e1b8dff1d9a9f523
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71127246"
---
# <a name="quickstart-connect-and-query-postgresql-using-includename-sosincludesname-sos-shortmd"></a>Avvio rapido: Connettersi ed eseguire query in PostgreSQL con [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Questo argomento di avvio rapido illustra come usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per connettersi a Postgres e come usare istruzioni SQL per creare il database *tutorialdb* ed eseguire query su di esso.

## <a name="prerequisites"></a>Prerequisites

Per completare questo argomento di avvio rapido sono necessari [!INCLUDE[name-sos](../includes/name-sos-short.md)], l'estensione PostgreSQL per [!INCLUDE[name-sos](../includes/name-sos-short.md)] e l'accesso a un server PostgreSQL.

- [Installare [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md).
- [Installare l'estensione PostgreSQL per Azure Data Studio](postgres-extension.md).
- [Installare PostgreSQL](https://www.postgresql.org/download/). In alternativa, è possibile creare un database Postgres nel cloud con il comando [az postgres up](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli). 

## <a name="connect-to-postgresql"></a>Connettersi a PostgreSQL

1. Avviare **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** .

2. La prima volta che si avvia [!INCLUDE[name-sos](../includes/name-sos-short.md)], viene visualizzata la finestra di dialogo **Connessione**. Se la finestra di dialogo **Connessione** non si apre, fare clic sull'icona **Nuova connessione** nella pagina **SERVER**:

   ![Icona Nuova connessione](media/quickstart-postgresql/new-connection-icon.png)

3. Nel modulo che viene visualizzato, passare a **Tipo di connessione** e scegliere **PostgreSQL** nell'elenco a discesa.


4. Compilare i campi rimanenti usando il nome server, il nome utente e la password relativi al server PostgreSQL. 

   ![Nuova schermata di connessione](media/quickstart-postgresql/new-connection-screen.png)  

   | Impostazione       | Valore di esempio | Descrizione |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome server** | localhost | Nome completo del server |
   | **Nome utente** | postgres | Nome utente con cui si desidera eseguire l'accesso. |
   | **Password (account di accesso SQL)** | *password* | Password dell'account con cui si esegue l'accesso. |
   | **Password** | *Controllo* | Selezionare questa casella se non si vuole immettere la password ogni volta che ci si connette. |
   | **Nome database** | \<Default\> | Compilare questo campo se si vuole che nella connessione sia specificato un database. |
   | **Gruppo di server** | \<Default\> | Questa opzione consente di assegnare la connessione a uno specifico gruppo di server precedentemente creato. | 
   | **Nome (facoltativo)** | *lasciare vuoto* | Questa opzione consente di specificare un nome descrittivo per il server. | 

5. Selezionare **Connetti**. 

Dopo il completamento della connessione, il server si apre nella barra laterale **SERVER**.


## <a name="create-a-database"></a>Creazione di un database

Questa procedura consente di creare un database denominato **tutorialdb**:

1. Fare clic con il pulsante destro del mouse sul server PostgreSQL nella barra laterale **SERVER** e scegliere **Nuova query**.

2. Incollare questa istruzione SQL nell'editor di query visualizzato.

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. Sulla barra degli strumenti selezionare **Esegui** per eseguire la query. Nel riquadro **MESSAGGI** vengono visualizzate alcune notifiche che informano l'utente sullo stato di avanzamento della query.

>[!TIP]
> Per eseguire l'istruzione è possibile premere **F5** sulla tastiera anziché usare l'opzione **Esegui**.

Dopo il completamento della query, fare clic con il pulsante destro del mouse su **Database** e scegliere **Aggiorna** per visualizzare la voce **tutorialdb** nell'elenco presente sotto il nodo **Database**.


## <a name="create-a-table"></a>Creare una tabella

 Questa procedura consente di creare una tabella in **tutorialdb**:

1. Modificare il contesto di connessione in **tutorialdb** usando l'elenco a discesa disponibile nell'editor di query. 

   ![Modifica del contesto](media/quickstart-postgresql/change-context.png)

2. Incollare l'istruzione SQL seguente nell'editor di query e fare clic su **Esegui**. 

   > [!NOTE]
   > È possibile aggiungerla o sovrascrivere la query esistente nell'editor. Facendo clic su **Esegui** viene eseguita solo la query evidenziata. Se nessuna query risulta evidenziata, facendo clic su **Esegui** vengono eseguite tutte le query nell'editor.

   ```sql
   -- Drop the table if it already exists
   DROP TABLE IF EXISTS customers;
   -- Create a new table called 'customers'
   CREATE TABLE customers(
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR (50) NOT NULL,
       location VARCHAR (50) NOT NULL,
       email VARCHAR (50) NOT NULL
   );
   ```

## <a name="insert-rows"></a>Inserire righe

Incollare il frammento di codice seguente nella finestra di query e fare clic su **Esegui**:

   ```sql
   -- Insert rows into table 'customers'
   INSERT INTO customers
       (customer_id, name, location, email)
    VALUES
      ( 1, 'Orlando', 'Australia', ''),
      ( 2, 'Keith', 'India', 'keith0@adventure-works.com'),
      ( 3, 'Donna', 'Germany', 'donna0@adventure-works.com'),
      ( 4, 'Janet', 'United States','janet1@adventure-works.com');
   ```

## <a name="query-the-data"></a>Eseguire una query sui dati

1. Incollare il frammento di codice seguente nell'editor di query e fare clic su **Esegui**:
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. Vengono visualizzati i risultati della query:

   ![Visualizzazione dei risultati](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>Passaggi successivi

Informazioni sugli [scenari disponibili per Postgres in Azure Data Studio](postgres-extension.md). 