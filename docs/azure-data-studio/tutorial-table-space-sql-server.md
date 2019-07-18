---
title: "Esercitazione: Abilitare il widget insight esempio di tabella dello spazio dell'utilizzo"
titleSuffix: Azure Data Studio
description: Questa esercitazione illustra come abilitare il widget insight tabella spazio utilizzo esempio sul dashboard del database di Studio di Azure Data.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 6ec653eac10da8c28f727277fc130722c3badef7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958981"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>Esercitazione: Abilitare la tabella dello spazio dell'utilizzo esempio insight widget usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Con questa esercitazione viene illustrato come abilitare un widget sulla dashboard del database al fine di avere una panoramica sull'utilizzo dello spazio per tutte le tabelle in un database. Durante questa esercitazione, si apprenderà come:

> [!div class="checklist"]
> * Attivare rapidamente un widget di informazioni dettagliate utilizzando un esempio incorporato
> * Visualizzare i dettagli sullo spazio utilizzato dalle tabelle
> * Filtrare i dati e visualizzare il dettaglio dell'etichetta in un grafico di informazioni dettagliate

## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione richiede *TutorialDB*, un database su SQL Server o Database SQL di Azure. Per crearlo, completare una delle guide rapide seguenti:

- [Connettersi ed eseguire query su SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Connettersi ed eseguire query sul database SQL di Azure tramite [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>Attivare un insight di gestione in [!INCLUDE[name-sos](../includes/name-sos-short.md)]del dashboard del database
[!INCLUDE[name-sos](../includes/name-sos-short.md)] offre un widget di esempio incorporato per monitorare lo spazio utilizzato dalle tabelle in un database.

1. Al fine di accedere al file delle *IMPOSTAZIONI UTENTE* premere **Ctrl+MAIUSC+P** per aprire il *riquadro comandi*.
2. Tipo di *le impostazioni* nella casella di ricerca e selezionare **preferenze: Aprire le impostazioni utente**.
2. Scrivere ora *dashboard* nella ricerca impostazioni e individuare **dashboard.database.widgets**.

3. Per personalizzare il **dashboard.database.widgets** impostazioni è necessario modificare il **dashboard.database.widgets** voce nella **impostazioni utente** sezione (la colonna nel lato destro). Se è presente alcun **dashboard.database.widgets** nel **delle impostazioni utente** sezione, passare il mouse sul **dashboard.database.widgets** testo nella colonna impostazioni predefinite e fare clic su l'icona a forma di matita visualizzata a sinistra del testo e fare clic su **Copia impostazioni**. Se viene visualizzato il menu a comparsa **sostituire nelle impostazioni**, senza selezionarlo. Andare alla **delle impostazioni utente** colonna a destra e individuare le **dashboard.database.widgets** sezione e andare al passaggio successivo.

4. Nel **dashboard.database.widgets** sezione, aggiungere quanto segue:

   ```json
        {
            "name": "Space Used by Tables",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "table-space-db-insight": null
            }
        },
    ```
Il **dashboard.database.widgets** sezione dovrebbe essere simile all'immagine seguente:

   ![Impostazioni di ricerca](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. Premere **Ctrl + S** per salvare le impostazioni.

6. Aprire la dashboard del database facendo clic con il pulsante destro del mouse su **TutorialDB**, quindi fare clic su **Gestisci**.

7. Visualizza i *spazio di tabella* widget insight, come illustrato nell'immagine seguente: 

   ![Widget](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>Utilizzo del grafico di informazioni dettagliate

Il grafico di informazioni dettagliate di [!INCLUDE[name-sos](../includes/name-sos-short.md)] fornisce filtri e dettagli al passaggio del mouse. Provare i passaggi seguenti:

1. Fare clic e attivare/disattivare la legenda *rows_count* nel grafico. [!INCLUDE[name-sos](../includes/name-sos-short.md)] mostra e nasconde le serie di dati quando si attiva o disattiva una legenda.
    
2. Passare il puntatore del mouse sul grafico. [!INCLUDE[name-sos](../includes/name-sos-short.md)]mostra ulteriori informazioni sull'etichetta della serie di dati e il relativo valore, come illustrato nella schermata seguente:

   ![legenda e attivazione/disattivazione grafico](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione si è appreso come:
> [!div class="checklist"]
> * Attivare rapidamente un widget di informazioni dettagliate utilizzando un esempio incorporato
> * Visualizzare i dettagli sullo spazio utilizzato dalle tabelle.
> * Filtrare i dati e visualizzare il dettaglio dell'etichetta in un grafico di informazioni dettagliate

Per informazioni su come costruire un widget di informazioni dettagliate personalizzato, completare l'esercitazione successiva:

> [!div class="nextstepaction"]
> [Costruire un widget di informazioni dettagliate personalizzato](tutorial-build-custom-insight-sql-server.md).
