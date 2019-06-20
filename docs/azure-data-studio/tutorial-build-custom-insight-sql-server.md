---
title: 'Esercitazione: Compilare un widget insight personalizzato'
titleSuffix: Azure Data Studio
description: Questa esercitazione illustra come compilare widget insight personalizzato e aggiungerli ai dashboard di server e database in Azure Data Studio.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 20b8bb332f2b8910d533407e79799dab162ac217
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797983"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>Esercitazione: Compilare un widget insight personalizzato

Con questa esercitazione viene mostrato come costruire un widget di informazioni dettagliate personalizzato sfruttando le query di informazioni dettagliate.

Durante questa esercitazione si apprenderà come:
> [!div class="checklist"]
> * Eseguire una query e visualizzarla in un grafico
> * Compilare un widget di informazioni personalizzato dal grafico
> * Aggiungere il grafico a un dashboard di server o database
> * Aggiungere i dettagli per il widget di informazioni personalizzato

## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione richiede *TutorialDB*, un database su SQL Server o Database SQL di Azure. Per crearlo, completare una delle guide rapide seguenti:

- [Connettersi ed eseguire query su SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Connettersi ed eseguire query su Azure SQL Database tramite[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>Eseguire una query e visualizzare il risultato in un grafico
In questo passaggio, eseguiremo uno script sql per ottenere la lista delle sessioni attive.

1. Per aprire un nuovo editor, premere **Ctrl + N**. 

2. Modificare il contesto di connessione su **TutorialDB**.

3. Incollare la query seguente nell'editor di query:

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. Salvare la query in un \*file con estensione `.sql`. Per questa esercitazione, salvare lo script come *activeSession.sql*.

5. Per eseguire la query, premere **F5**.

6. Dopo che vengono visualizzati i risultati della query, fare clic su **Visualizzazione grafico** nella barra laterale a destra dei risultati, quindi fare clic sulla scheda **Visualizzatore grafico**.

7. Change **tipo di grafico** al **conteggio**. Queste impostazioni di eseguire il rendering di un grafico di conteggio.

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>Aggiungere le informazioni dettagliate personalizzate alla dashboard del database

1. Per aprire la configurazione del widget di informazioni dettagliate, fare clic su **creare informazioni dettagliate** nel *Visualizzatore grafico*:

   ![configurazione](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. Copiare la configurazione proposta (il JSON). 

3. Premere **Ctrl+virgola** per aprire le *impostazioni utente*.

4. Scrivere *dashboard* in *Cerca impostazioni*.

5. Fare clic su **Edit** per *dashboard.database.widgets*.

   ![impostazioni del dashboard](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. Incollare il frammento di JSON in *dashboard.database.widgets*. Le impostazioni della dashboard del database dovrebbero essere simili al seguente listato:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql"
                }
            }
        }
    ]
   ```

7. Salvare le *impostazioni utente* e aprire la dashboard del database *TutorialDB* per visualizzare il widget con le sessioni attive:

   ![insight activesession](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>Aggiungere i dettagli al widget personalizzato

1. Per aprire un nuovo editor, premere **Ctrl + N**.

2. Modificare il contesto di connessione su **TutorialDB**.

3. Incollare la query seguente nell'editor di query:

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. Salvare la query in un \*file con estensione `.sql`. Per questa esercitazione, salvare lo script come *activeSessionDetail.sql*.

5. Premere **Ctrl+virgola** per aprire le *impostazioni utente*.

6. Modificare il nodo *dashboard.database.widgets* nel file di impostazioni:

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql",
                    "details": {
                        "queryFile": "{your file folder}/activeSessionDetail.sql",
                        "label": "SID",
                        "value": "Login Name"
                    }
                }
            }
        }
    ]
   ```

7. Salvare le *impostazioni utente* e aprire la dashboard di *TutorialDB*. Fare clic sul pulsante con i puntini di sospensione (...) accanto a *My Widget* per visualizzare i dettagli:

    ![insight activesession](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione si è appreso come:
> [!div class="checklist"]
> * Eseguire una query e visualizzarla in un grafico
> * Compilare un widget di informazioni personalizzato dal grafico
> * Aggiungere il grafico a un dashboard di server o database
> * Aggiungere i dettagli per il widget di informazioni personalizzato

Per informazioni su come eseguire backup e ripristino di database, completare l'esercitazione successiva:

> [!div class="nextstepaction"]
> [Eseguire backup e ripristino di database](tutorial-backup-restore-sql-server.md).
