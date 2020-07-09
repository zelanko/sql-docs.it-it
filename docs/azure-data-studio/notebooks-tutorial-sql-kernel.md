---
title: Notebook con kernel SQL in Azure Data Studio
description: Questa esercitazione illustra come è possibile creare ed eseguire un notebook di SQL Server.
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray, alayu
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 64e5bcfa188707e784d33a6504b120c4ce0ea553
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735325"
---
# <a name="create-and-run-a-sql-server-notebook"></a>Creare ed eseguire un notebook di SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questa esercitazione illustra come creare ed eseguire un notebook in Azure Data Studio con SQL Server.

## <a name="prerequisites"></a>Prerequisiti

- [Azure Data Studio installato](download-azure-data-studio.md)
- SQL Server installato
  - [Windows](../database-engine/install-windows/install-sql-server.md)
  - [Linux](../linux/sql-server-linux-setup.md)

## <a name="new-notebook"></a>Nuovo notebook

Questa procedura illustra come creare un file di notebook in Azure Data Studio:

1. In Azure Data Studio connettersi all'istanza di SQL Server.

2. Selezionare la connessione in **Connessioni** nella finestra **Server**. Selezionare quindi **Nuovo notebook**.

   ![Apri notebook](media/notebook-tutorial/azure-data-studio-open-notebook.png)

3. Attendere che il **kernel** e il contesto di destinazione **(Connetti a**) siano popolati. Verificare che **Kernel** sia impostato su **SQL** e impostare **Collega a** per l'istanza di SQL Server (in questo caso *localhost*).

   ![Imposta Kernel e Connetti a](media/notebook-tutorial/set-kernel-and-attach-to.png)

## <a name="run-a-notebook-cell"></a>Eseguire una cella del notebook

È possibile eseguire ogni cella del notebook premendo il pulsante di riproduzione a sinistra della cella. I risultati verranno visualizzati nel notebook al termine dell'esecuzione della cella.

### <a name="code"></a>Codice

Aggiungere una nuova cella di codice selezionando il comando **+Codice** sulla barra degli strumenti.

![Barra degli strumenti del notebook](media/notebooks-guidance/notebook-toolbar.png)

In questo esempio viene creato un nuovo database.

```sql
USE master
GO

   -- Drop the database if it already exists
IF  EXISTS (
        SELECT name
        FROM sys.databases
        WHERE name = N'TestNotebookDB'
   )
DROP DATABASE TestNotebookDB
GO

-- Create the database
CREATE DATABASE TestNotebookDB
GO
```

   ![Eseguire la cella del notebook](media/notebook-tutorial/run-notebook-cell.png)

Se si esegue uno script che restituisce un risultato, è possibile salvare il risultato in formati diversi.

- Salva in formato CSV
- Salva in formato Excel
- Salva in formato JSON
- Salva in formato XML

In questo caso, viene restituito il risultato di [PI](../t-sql/functions/pi-transact-sql.md).

```sql
SELECT PI() AS PI;
GO
```

![Eseguire la cella del notebook](media/notebook-tutorial/run-notebook-cell-2.png)

### <a name="text"></a>Text

Aggiungere una nuova cella di testo selezionando il comando **+Testo** sulla barra degli strumenti.

![Barra degli strumenti del notebook](media/notebooks-guidance/notebook-toolbar.png)

La cella passa alla modalità di modifica ed è quindi possibile digitare la sintassi markdown e, nello stesso tempo, visualizzare l'anteprima

![Cella di markdown](media/notebooks-guidance/notebook-markdown-cell.png)

Se si fa clic all'esterno della cella di testo, viene visualizzato il testo markdown.

![Testo markdown](media/notebooks-guidance/notebook-markdown-preview.png)

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sui notebook:

- [Come usare i notebook con SQL Server](notebooks-guidance.md)

- [Come gestire i notebook in Azure Data Studio](notebooks-manage-sql-server.md)

- [Eseguire un notebook di esempio con Spark](../big-data-cluster/notebooks-tutorial-spark.md)