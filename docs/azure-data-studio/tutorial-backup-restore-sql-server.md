---
title: Eseguire il backup e ripristinare un database
description: Seguire questa esercitazione per scoprire come eseguire il backup e il ripristino di database usando Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 8594178dc6817cc8b826268c3fd0aebce59af2ec
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88765800"
---
# <a name="backup-and-restore-databases-using-azure-data-studio"></a>Eseguire il backup e il ripristino di database con Azure Data Studio

In questa esercitazione si apprenderà come usare Azure Data Studio per:
> [!div class="checklist"]
> * Eseguire il backup del database 
> * Visualizzare lo stato dell'operazione di backup
> * Generare lo script usato per eseguire il backup
> * Ripristinare un database
> * Visualizzare lo stato dell'attività di ripristino

## <a name="prerequisites"></a>Prerequisiti

Per questa esercitazione è necessario il database *TutorialDB* di SQL Server. Per creare il database *TutorialDB*, completare uno degli argomenti di avvio rapido seguenti:

* [Connettersi ed eseguire query in SQL Server con [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)

Questa esercitazione richiede la connessione a un database di SQL Server. Azure Data Studio non esegue il backup e ripristino di database SQL di Azure poiché in essi sono già previsti backup automatici. Per informazioni dettagliate, vedere [informazioni sui backup automatici deI database SQL](/azure/sql-database/sql-database-automated-backups).

## <a name="back-up-a-database"></a>Eseguire il backup del database

1. Aprire il dashboard del database TutorialDB (aprire la barra laterale **SERVER** premendo **CTRL + G**, espandere **Database**, fare clic con il pulsante destro del mouse su **TutorialDB** e selezionare **Gestisci**).

2. Aprire la finestra di dialogo **Backup database**  (fare clic su  **Backup** nel widget **Attività**).

   ![Widget Attività](./media/tutorial-backup-restore-sql-server/tasks.png)

3. In questa esercitazione vengono usate le opzioni di backup predefinite, fare quindi clic su **Backup**.
   ![finestra di dialogo Backup](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Dopo aver fatto clic su **Backup**, la finestra di dialogo **Backup database** scompare e viene avviato il processo di backup.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Visualizzare lo stato e lo script di backup

1. Viene visualizzato il riquadro **Cronologia attività** oppure premere **CTRL + T**.

   ![Cronologia attività](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Per visualizzare lo script di backup nell'editor, fare clic con il pulsante destro del mouse su **Backup di database riuscito** e scegliere **Script**.

   ![script di backup](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>Ripristinare un database da un file di backup.

1. Aprire la barra laterale **SERVER** (**CTRL +G**), fare clic con il pulsante destro del mouse sul server e scegliere **Gestisci**.

2. Aprire la finestra di dialogo **Ripristina database**  (fare clic su  **Ripristina** nel widget **Attività**).

   ![Attività di ripristino](media/tutorial-backup-restore-sql-server/tasks-restore.png)

3. Nel campo **Ripristina da** selezionare **File di backup**.

4. Fare clic sui puntini di sospensione (...) nel campo **Percorso file di backup** e selezionare il file di backup più recente per *TutorialDB*.

5. Digitare **TutorialDB_Restored** nel campo **Database di destinazione** della sezione **Destinazione** per ripristinare il file di backup in un nuovo database. Selezionare quindi **Ripristina**.

   ![ripristinare](./media/tutorial-backup-restore-sql-server/restore.png)

6. Per visualizzare lo stato dell'operazione di ripristino, premere **CTRL + T** per aprire **Cronologia attività**.

   ![ripristinare](./media/tutorial-backup-restore-sql-server/task-history-restore.png)