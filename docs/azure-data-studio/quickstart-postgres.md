---
title: 'Avvio rapido: Connettersi ed eseguire query con PostgreSQL'
titleSuffix: Azure Data Studio
description: Questa Guida introduttiva illustra come usare Azure Data Studio per connettersi a PostgreSQL ed eseguire una query
ms.custom: seodec18
ms.date: 03/19/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
manager: craigg
ms.openlocfilehash: dbf7b427c8c978538370a576aa50c35dd15417cf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63252944"
---
# <a name="quickstart-connect-and-query-postgresql-using-includename-sosincludesname-sos-shortmd"></a>Avvio rapido: Connettersi ed eseguire query con PostgreSQL [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Questa Guida introduttiva illustra come usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per connettersi a Postgres e quindi usare istruzioni SQL per creare il database *tutorialdb* ed eseguire una query.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa Guida introduttiva, è necessario [!INCLUDE[name-sos](../includes/name-sos-short.md)], l'estensione di PostgreSQL per [! INCLUDERE[nome-sos](../includes/name-sos-short.md)e l'accesso a un server PostgreSQL.

- [Installare [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).
- [Installare le estensioni di PostgreSQL per Azure Data Studio](postgres-extension.md).
- [Installare PostgreSQL](https://www.postgresql.org/download/). (In alternativa, è possibile creare un database Postgres nel cloud usando [az postgres backup](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli)). 

## <a name="connect-to-postgresql"></a>Connettersi a PostgreSQL

1. Avviare **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**.

2. La prima volta che avvia [!INCLUDE[name-sos](../includes/name-sos-short.md)] il **connessione** verrà visualizzata la finestra di dialogo. Se il **connessione** finestra di dialogo non si apre, fare clic sui **nuova connessione** icona nel **server** pagina:

   ![Icona "Nuova connessione"](media/quickstart-postgresql/new-connection-icon.png)

3. Nel modulo che viene visualizzata, passare a **tipo di connessione** e selezionare **PostgreSQL** dall'elenco a discesa.


4. Compilare i campi rimanenti usando il nome del server, nome utente e password per il server PostgreSQL. 

   ![Schermata "Nuova connessione"](media/quickstart-postgresql/new-connection-screen.png)  

   | Impostazione       | Valore di esempio | Descrizione |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome server** | localhost | Nome completo del server |
   | **Nome utente** | Postgres | Il nome utente desiderato con cui accedere. |
   | **Password (account di accesso SQL)** | *password* | La password per l'account che con cui si esegue l'accesso. |
   | **Password** | *Controlla* | Selezionare questa casella se non si vuole immettere la password ogni volta che si connette. |
   | **Nome database** | \<Default\> | Se si desidera che la connessione per specificare un database, riempire l'oggetto. |
   | **Gruppo di server** | \<Default\> | Questa opzione consente di assegnare questa connessione a un gruppo di server specifico che è creare. | 
   | **Nome (facoltativo)** | *Lasciare vuoto* | Questa opzione consente di specificare un nome descrittivo per il server. | 

5. Selezionare **Connetti**. 

Dopo aver stabilito la connessione, il server viene aperto nel **server** nella barra laterale.


## <a name="create-a-database"></a>Creazione di un database

La procedura seguente crea un database denominato **tutorialdb**:

1. Fare clic su server PostgreSQL nel **i server** nella barra laterale e selezionare **nuova Query**.

2. Incollare l'istruzione SQL nell'editor di query che si apre.

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. Nella barra degli strumenti selezionare **eseguiti** per eseguire la query. Le notifiche risultano visibili nel **messaggi** riquadro per visualizzare lo stato di avanzamento di query.

>[!TIP]
> È possibile usare **F5** sulla tastiera per eseguire l'istruzione invece di usare **eseguire**.

Al termine dell'esecuzione della query, fare doppio clic su **database** e selezionare **aggiornare** per visualizzare **tutorialdb** nell'elenco sotto il **database** nodo .


## <a name="create-a-table"></a>Creare una tabella

 La procedura seguente crea una tabella di **tutorialdb**:

1. Modificare il contesto di connessione al **tutorialdb** usando l'elenco a discesa nell'editor di query. 

   ![Modifica del contesto](media/quickstart-postgresql/change-context.png)

2. Incollare l'istruzione SQL nell'editor di query e fare clic su **eseguiti**. 

   > [!NOTE]
   > È possibile aggiungere questo o sovrascrivere la query esistente nell'editor. Facendo clic **eseguire** esegue solo le query che è evidenziata. Se non viene evidenziato, fare clic su **eseguire** esegue tutte le query nell'editor.

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

Incollare il frammento di codice seguente nella finestra query, quindi fare clic su **Esegui**:

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

## <a name="query-the-data"></a>Eseguire query sui dati

1. Incollare il seguente frammento di codice nell'editor di query, quindi fare clic su **Esegui**:
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. Vengono visualizzati i risultati della query:

   ![Visualizzare i risultati](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>Passaggi successivi

Scopri le [scenari disponibili per Postgres in Azure Data Studio](postgres-extension.md). 