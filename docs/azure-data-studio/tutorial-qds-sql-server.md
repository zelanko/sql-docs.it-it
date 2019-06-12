---
title: 'Esercitazione: Abilitare il widget di esempio le query più lente cinque'
titleSuffix: Azure Data Studio
description: Con questa esercitazione viene illustrato come abilitare il widget di esempio delle cinque query più lente nella dashboard del database.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 10795ae2e1836e018e103a51cb7bea718ec9299f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797932"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Esercitazione: Aggiungere il *cinque query più lente* widget al dashboard del database di esempio

Con questa esercitazione viene illustrato il processo di aggiunta di uno dei widget di esempio incorporati in [!INCLUDE[name-sos](../includes/name-sos-short.md)] alla *dashboard del database* al fine di visualizzare rapidamente le cinque query più lente del database. Inoltre, viene mostrato come visualizzare i dettagli delle query lente e piani di query utilizzando le funzionalità di [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Durante questa esercitazione, si apprenderà come:

> [!div class="checklist"]
> * Abilitare Archivio Query in un database
> * Aggiungere un widget integrato di informazioni dettagliate al dashboard del database
> * Visualizzare i dettagli sulle query più lente del database
> * Visualizzare piani di esecuzione per le query lente

[!INCLUDE[name-sos](../includes/name-sos-short.md)] include diversi widget integrati di informazioni dettagliate. In questa esercitazione viene illustrato come aggiungere il widget *query-data-store-db-insight*, ma i passaggi sono fondamentalmente gli stessi per l'aggiunta di altri widget.

## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione richiede *TutorialDB*, un database su SQL Server o Database SQL di Azure. Per crearlo, completare una delle guide rapide seguenti:

- [Connettersi ed eseguire query su SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Connettersi ed eseguire query su Azure SQL Database tramite [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>Attivare Archivio Query per il database

Il widget in questo esempio richiede *Query Store* deve essere abilitata.

1. Fare clic il **TutorialDB** database (nelle **server** nella barra laterale) e selezionare **nuova Query**.
2. Incollare l'istruzione Transact-SQL (T-SQL) seguente nell'editor di query e fare clic su **eseguire**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>Aggiungere il widget di query lente per il dashboard del database

Per aggiungere il *widget di query lente* al dashboard, modificare il *dashboard.database.widgets* impostazione nel *impostazioni utente* file.

1. Al fine di accedere al file delle *IMPOSTAZIONI UTENTE* premere **Ctrl+MAIUSC+P** per aprire il *riquadro comandi*.
2. Tipo di *le impostazioni* nella casella di ricerca e selezionare **preferenze: Aprire le impostazioni utente**.

   ![Comando Apri impostazioni utente](./media/tutorial-qds-sql-server/open-user-settings.png)

2. Scrivere ora *dashboard* nella ricerca impostazioni e individuare **dashboard.database.widgets**.

   ![Impostazioni di ricerca](./media/tutorial-qds-sql-server/search-settings.png)

3. Per personalizzare il **dashboard.database.widgets** impostazioni è necessario modificare il **dashboard.database.widgets** voce nella **impostazioni utente** sezione (la colonna nel lato destro). Se è presente alcun **dashboard.database.widgets** nel **delle impostazioni utente** sezione, passare il mouse sul **dashboard.database.widgets** testo nella colonna impostazioni predefinite e fare clic su l'icona a forma di matita visualizzata a sinistra del testo e fare clic su **Copia impostazioni**. Se viene visualizzato il menu a comparsa **sostituire nelle impostazioni**, senza selezionarlo. Andare alla **delle impostazioni utente** colonna a destra e individuare le **dashboard.database.widgets** sezione e andare al passaggio successivo.

4. Nel **dashboard.database.widgets** sezione, aggiungere quanto segue:

   ```json
        {
            "name": "slow queries widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "query-data-store-db-insight": null
            }
        },
    ```

1. Se si tratta di un nuovo widget, aggiunge la prima volta il **dashboard.database.widgets** sezione dovrebbe essere simile al seguente:

   ```json
   "dashboard.database.widgets": [
       {
           "name": "slow queries widget",
           "gridItemConfig": {
               "sizex": 2,
               "sizey": 1
           },
           "widget": {
               "query-data-store-db-insight": null
           }
       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }
       }
   ]
   ```

1. Premere **Ctrl+S** per salvare la modifica in **Impostazioni utente**.

6. Aprire la *Dashboard del database* selezionando **TutorialDB** nella barra laterale dei **SERVER**, premere il pulsante destro del mouse e scegliere **Gestisci**.

   ![Aprire il dashboard](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. Il widget delle informazioni dettagliate viene visualizzato nel dashboard: 

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Visualizzare il widget delle informazioni dettagliate per altri approfondimenti

1. Per visualizzare informazioni aggiuntive per un widget di informazioni dettagliate, fare clic sui puntini di sospensione ( **...** ) in alto a destra e selezionare **Mostra dettagli**.
2. Per visualizzare ulteriori dettagli di un elemento, selezionarlo dall'elenco dei **dati**.

   ![Finestra di dialogo Dettagli Insight](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Fare clic con il pulsante destro del mouse su sulla cella a destra di **query_sql_txt** in **Dettagli elemento** e fare clic su **Copia cella**.

4. Chiudere il riquadro **Informazioni dettagliate**.

## <a name="view-the-query-plan"></a>Visualizzare il piano di query 

1. Aprire un nuovo editor di query premendo **Ctrl+N**.

2. Incollare il testo della query copiato nei passaggi precedenti.

3. Fare clic su **spiegare**.

   ![Informazioni dettagliate QDS - Spiega](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. Visualizzare il piano di esecuzione della query:

   ![showplan](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>Salvare e aprire un piano di query 

1. Aprire la finestra di dialogo delle informazioni dettagliate.
2. Selezionare uno degli elementi di query.
2. Fare clic con il pusante destro del mouse sul valore **query_plan** e selezionare **Copia cella**

   ![Piano di Insights QDS](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. Premere **Ctrl+N** per aprire un nuovo editor.

4. Incollare il piano copiato nell'editor.

5. Premere **Ctrl+S** per salvare il file e modificare l'estensione del file in *.sqlplan*. *sqlplan* non è visualizzato nell'elenco a discesa estensione di file, quindi digitarlo in. Per questa esercitazione, denominare il file *slowquery.sqlplan*.

6. Il piano di query viene aperto nel visualizzatore dei piani di query in [!INCLUDE[name-sos](../includes/name-sos-short.md)]:

   ![Piano di Insights QDS](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione si è appreso come:
> [!div class="checklist"]
> * Abilitare Archivio Query in un database
> * Aggiungere un widget di informazioni dettagliate al dashboard del database
> * Visualizzare i dettagli sulle query più lente del database
> * Visualizzare piani di esecuzione per le query lente


Per informazioni su come abilitare il widget di esempio **utilizzo dello spazio delle tabelle**, completare l'esercitazione successiva:

> [!div class="nextstepaction"]
> [Abilitare il widget di esempio di informazioni dettagliate sullo spazio delle tabelle](tutorial-table-space-sql-server.md)
