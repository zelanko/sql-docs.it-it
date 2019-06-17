---
title: Eseguire il backup e ripristinare un database
titleSuffix: Azure Data Studio
description: Informazioni su come eseguire il backup e ripristinare un database tramite Data Studio di Azure
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 93f38f8e703aabc765d3badc91393eb130081c99
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797966"
---
# <a name="backup-and-restore-databases-using-includename-sosincludesname-sos-shortmd"></a>Backup e ripristino di database usando [!INCLUDE[name-sos](../includes/name-sos-short.md)]

In questa esercitazione imparerete a usare [!INCLUDE[name-sos](../includes/name-sos-short.md)] per:
> [!div class="checklist"]
> * Effettuare il backup di un database 
> * Visualizzare lo stato del backup
> * Generare lo script utilizzato per eseguire il backup
> * Ripristinare un database
> * Visualizzare lo stato dell'attività di ripristino

## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione richiede il database *TutorialDB* su SQL Server. Per crearlo, completare la guida rapida seguente:

- [Connettersi ed eseguire query su SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)

Questa esercitazione richiede la connessione a un database di SQL Server. Database SQL di Azure con i backup automatici in modo che Data Studio di Azure non eseguire il backup di Database SQL di Azure e il ripristino. Per informazioni dettagliate, vedere [informazioni sui backup automatici del Database SQL](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

## <a name="backup-a-database"></a>Effettuare il backup di un database

1. Aprire la dashboard del database TutorialDB (aprire la barra laterale **SERVER** con **CTRL+G**, espandere **Database**, fare clic con il pulsante destro del mouse su **TutorialDB** e selezionare **Gestisci**).

2. Aprire la finestra di dialogo **Backup database** (fare clic su **Backup** sul widget **Attività**).

   ![Widget attività](./media/tutorial-backup-restore-sql-server/tasks.png)

3. In questa esercitazione utilizzeremo le opzioni predefinite per il backup. Fare clic su **Backup**.
   ![finestra di dialogo backup](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

Dopo aver fatto clic su **Backup**, la finestra di dialogo **Backup database** si chiude e inizia il processo di backup.

## <a name="view-the-backup-status-and-view-the-backup-script"></a>Visualizzare lo stato del backup e lo script di backup

1. Aprire **Cronologia attività** tramite l'icona ad orologio nella *barra delle azioni* o premere **CTRL+T**.

   ![Cronologia attività](./media/tutorial-backup-restore-sql-server/task-history.png)

2. Per visualizzare lo script di backup nell'editor, premere il tasto destro su **Backup del database effettuato con successo** e selezionare **Script**.

   ![script di backup](./media/tutorial-backup-restore-sql-server/task-script.png) 

## <a name="restore-a-database-from-a-backup-file"></a>Ripristinare un database da un file di backup


1. Aprire la barra laterale **SERVER** (**CTRL+G**), premere il tasto destro sul vostro server e scegliere **Gestisci**. 

2. Aprire la finestra di dialogo **Ripristina database** (fare clic su **Ripristino** sul widget **attività**).

2. Selezionare **file di Backup** nel campo **ripristina da**. 

3. Fare clic sui puntini di sospensione (...) nel **percorso del file di Backup** e selezionare il file di backup più recente per *TutorialDB*.

3. Scrivere ora **TutorialDB_Restored** nel campo **database di destinazione** nell'area **destinazione** per ripristinare il file di backup in un nuovo database.

   ![ripristino](./media/tutorial-backup-restore-sql-server/restore.png)

4. Fare clic su **Ripristina**

5. Per visualizzare lo stato dell'operazione di ripristino, premere **CTRL + T** per aprire il **Cronologia attività** nella barra laterale.

   ![ripristino](./media/tutorial-backup-restore-sql-server/task-history-restore.png)


In questa esercitazione si è appreso come:
> [!div class="checklist"]
> * Effettuare il backup di un database 
> * Visualizzare lo stato del backup
> * Generare lo script utilizzato per eseguire il backup
> * Ripristinare un database
> * Visualizzare lo stato dell'attività di ripristino

