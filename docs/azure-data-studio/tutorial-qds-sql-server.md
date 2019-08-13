---
title: 'Esercitazione: Abilitare il widget di esempio per le cinque query più lente'
titleSuffix: Azure Data Studio
description: Questa esercitazione illustra come abilitare il widget di esempio per le cinque query più lente nel dashboard del database.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 5c94d2cf8b80ad7724cc1f710dc67d3f4a13c59e
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959062"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>Esercitazione: Aggiungere il widget di esempio per le *cinque query più lente* al dashboard del database

Questa esercitazione illustra il processo di aggiunta di uno dei widget di esempio incorporati di [!INCLUDE[name-sos](../includes/name-sos-short.md)] al *dashboard del database* per visualizzare rapidamente le cinque query più lente di un database. Si apprenderà anche come visualizzare i dettagli sulle query lente e i piani di query usando le funzionalità di [!INCLUDE[name-sos](../includes/name-sos-short.md)]. In questa esercitazione verranno illustrate le procedure per:

> [!div class="checklist"]
> * Abilitare Query Store in un database
> * Aggiungere un widget di informazioni dettagliate predefinito al dashboard del database
> * Visualizzare i dettagli sulle query più lente del database
> * Visualizzare i piani di esecuzione query per le query lente

[!INCLUDE[name-sos](../includes/name-sos-short.md)] include diversi widget di informazioni dettagliate predefiniti. Questa esercitazione illustra come aggiungere il widget *query-data-store-db-insight*, ma i passaggi sono fondamentalmente gli stessi per aggiungere qualsiasi widget.

## <a name="prerequisites"></a>Prerequisites

Per questa esercitazione è necessario il database di SQL Server o il database SQL di Azure *TutorialDB*. Per creare il database *TutorialDB*, completare uno degli argomenti di avvio rapido seguenti:

- [Connettersi ed eseguire query in SQL Server con [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Connettersi ed eseguire query nel database SQL di Azure con [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>Attivare Query Store per il database

Il widget in questo esempio richiede l'abilitazione di *Query Store*.

1. Fare clic con il pulsante destro del mouse sul database **TutorialDB** nella barra laterale **SERVER** e scegliere **Nuova query**.
2. Incollare l'istruzione Transact-SQL seguente nell'editor di query e fare clic su **Esegui**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>Aggiungere il widget per le query lente al dashboard del database

Per aggiungere il *widget per le query lente* al dashboard, modificare l'impostazione *dashboard.database.widgets* nel file delle *impostazioni utente*.

1. Aprire le *impostazioni utente* premendo **CTRL+MAIUSC+P** e aprire il *riquadro comandi*.
2. Digitare *impostazioni* nella casella di ricerca e selezionare **Preferenze: Apri impostazioni utente**.

   ![Comando Apri impostazioni utente](./media/tutorial-qds-sql-server/open-user-settings.png)

2. Digitare *dashboard* nella casella di ricerca impostazioni e individuare **dashboard.database.widgets**.

   ![Ricerca impostazioni](./media/tutorial-qds-sql-server/search-settings.png)

3. Per personalizzare le impostazioni di **dashboard.database.widgets** è necessario modificare la voce **dashboard.database.widgets** nella sezione **IMPOSTAZIONI UTENTE** (la colonna sul lato destro). Se nella sezione **IMPOSTAZIONI UTENTE** non è presente la voce **dashboard.database.widgets**, posizionare il puntatore del mouse sul testo **dashboard.database.widgets** nella colonna IMPOSTAZIONI PREDEFINITE, fare clic sull'icona a forma di matita che compare a sinistra del testo e quindi fare clic su **Copia nelle impostazioni**. Se il popup indica **Sostituisci nelle impostazioni**, non fare clic su di esso. Passare alla colonna **IMPOSTAZIONI UTENTE** a destra, individuare la sezione **dashboard.database.widgets** e procedere al passaggio successivo.

4. Nella sezione **dashboard.database.widgets** aggiungere quanto segue:

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

1. Se è la prima volta che si aggiunge un nuovo widget, la sezione **dashboard.database.widgets** avrà un aspetto simile al seguente:

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

1. Premere **CTRL + S** per salvare le **Impostazioni utente** modificate.

6. Aprire il *dashboard del database* passando a **TutorialDB** nella barra laterale **SERVER**, fare clic con il pulsante destro del mouse e scegliere **Gestisci**.

   ![Apertura del dashboard](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. Il widget di informazioni dettagliate compare nel dashboard: 

   ![Widget QDS](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>Visualizzare i dettagli delle informazioni dettagliate

1. Per visualizzare informazioni aggiuntive per un widget di informazioni dettagliate, fare clic sui puntini di sospensione ( **...** ) in alto a destra e selezionare **Mostra dettagli**.
2. Per mostrare altri dettagli relativi a un elemento, selezionare un elemento nell'elenco **Dati grafico**.

   ![Finestra di dialogo dei dettagli delle informazioni dettagliate](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. Fare clic con il pulsante destro del mouse sulla cella a destra di **query_sql_txt** in **Dettagli elemento** e scegliere **Copia cella**.

4. Chiudere il riquadro **Informazioni dettagliate**.

## <a name="view-the-query-plan"></a>Visualizzare il piano di query 

1. Aprire un nuovo editor di query premendo **CTRL+N**.

2. Incollare il testo della query dai passaggi precedenti nell'editor.

3. Fare clic su **Spiega**.

   ![Spiegazione delle informazioni dettagliate QDS](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. Visualizzare il piano di esecuzione della query:

   ![showplan](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>Salvare e aprire un piano di query 

1. Aprire la finestra di dialogo dei dettagli delle informazioni dettagliate.
2. Selezionare uno degli elementi di query.
2. Fare clic con il pulsante destro del mouse sul valore **query_plan** e scegliere **Copia cella**

   ![Piano delle informazioni dettagliate QDS](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. Premere **CTRL+N** per aprire un nuovo editor.

4. Incollare il piano copiato nell'editor.

5. Premere **CTRL+S** per salvare il file e modificare l'estensione del file in *.sqlplan*. *.sqlplan* non compare nell'elenco a discesa dell'estensione di file, quindi occorre digitarlo. Per questa esercitazione, assegnare al file il nome *slowquery.sqlplan*.

6. Il piano di query si apre nel visualizzatore piano di query di [!INCLUDE[name-sos](../includes/name-sos-short.md)]:

   ![Piano delle informazioni dettagliate QDS](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione sono state illustrate le procedure per:
> [!div class="checklist"]
> * Abilitare Query Store in un database
> * Aggiungere un widget di informazioni dettagliate al dashboard del database
> * Visualizzare i dettagli sulle query più lente del database
> * Visualizzare i piani di esecuzione query per le query lente


Per informazioni su come abilitare il widget di informazioni dettagliate di esempio per lo **spazio utilizzato dalle tabelle**, completare l'esercitazione successiva:

> [!div class="nextstepaction"]
> [Abilitare il widget di informazioni dettagliate di esempio sullo spazio utilizzato dalle tabelle](tutorial-table-space-sql-server.md)
