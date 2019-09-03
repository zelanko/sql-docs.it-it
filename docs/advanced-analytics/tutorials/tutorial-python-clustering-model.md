---
title: 'Esercitazione: Eseguire il clustering in Python'
description: In questa serie di esercitazioni in quattro parti verrà eseguito il clustering dei clienti in un database SQL tramite Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: abcd13b5db24f7ffd44a21b4690f14d97645cdd5
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211925"
---
# <a name="tutorial-perform-clustering-in-python-with-sql-server-machine-learning-services"></a>Esercitazione: Eseguire il clustering in Python con SQL Server Machine Learning Services

In questa serie di esercitazioni in quattro parti verrà usato Python per sviluppare e distribuire un modello di clustering K-means in [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) per il clustering dei dati del cliente.

Nella prima parte di questa serie verranno configurati i prerequisiti per l'esercitazione e quindi si importerà un set di dati di esempio in un database SQL. Più avanti in questa serie questi dati verranno usati per eseguire il training e la distribuzione di un modello di clustering in Python con SQL Server Machine Learning Services.

Nelle parti due e tre di questa serie si svilupperanno alcuni script Python in un notebook di Azure Data Studio per analizzare e preparare i dati ed eseguire il training di un modello di machine learning. Quindi, nella quarta parte, verranno eseguiti gli script Python all'interno di un database SQL usando le stored procedure.

Il clustering può essere illustrato come organizzare i dati in gruppi in cui i membri di un gruppo sono in qualche modo simili. Per questa serie di esercitazioni, si supponga di disporre di un'azienda di vendita al dettaglio. Si utilizzerà l'algoritmo **K-means** per eseguire il clustering dei clienti in un set di dati di acquisti del prodotto e viene restituito. Con il clustering dei clienti, è possibile concentrare in modo più efficace le attività di marketing selezionando gruppi specifici.
Il clustering K-means è un algoritmo di *apprendimento* non supervisionato che cerca modelli nei dati in base a analogie.

L'articolo spiega come:

> [!div class="checklist"]
> * Importare un database di esempio in un'istanza di SQL Server

Nella [seconda parte](tutorial-python-clustering-model-prepare-data.md)verrà illustrato come preparare i dati da un database SQL per eseguire il clustering.

Nella [terza parte](tutorial-python-clustering-model-build.md)verrà illustrato come creare ed eseguire il training di un modello di clustering K-means in Python.

Nella [quarta parte](tutorial-python-clustering-model-deploy.md)verrà illustrato come creare un stored procedure in un database SQL in grado di eseguire il clustering in Python in base ai nuovi dati.

## <a name="prerequisites"></a>Prerequisiti

* [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) con l'opzione del linguaggio Python-seguire le istruzioni di installazione nella [Guida](../install/sql-machine-learning-services-windows-install.md) all'installazione di Windows o nella Guida all' [installazione di Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15).

* IDE Python: questa esercitazione usa un notebook Python in [Azure Data Studio](../../azure-data-studio/what-is.md). Per ulteriori informazioni, vedere [come utilizzare i notebook in Azure Data Studio](../../azure-data-studio/sql-notebooks.md). È anche possibile usare l'IDE di Python, ad esempio un notebook Jupyter o [Visual Studio Code](https://code.visualstudio.com/docs) con l' [estensione Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) e l' [estensione MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).

* pacchetto [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) : il pacchetto **revoscalepy** è incluso in SQL Server Machine Learning Services. Per usare il pacchetto in un computer client, vedere [configurare un client Data Science per lo sviluppo Python](../python/setup-python-client-tools-sql.md) per le opzioni per l'installazione locale del pacchetto.

  Se si usa un notebook Python in Azure Data Studio, seguire questa procedura aggiuntiva per usare **revoscalepy**:

  1. Apri Azure Data Studio
  1. Dal menu **file** selezionare **Preferenze** e quindi **Impostazioni** .
  1. Espandi **estensioni** e seleziona **configurazione notebook**
  1. In **percorso Python**immettere il percorso in cui sono state installate le librerie, ad esempio `C:\path-to-python-for-mls`.
  1. Assicurarsi che l'opzione **USA Python esistente** sia selezionata
  1. Riavvia Azure Data Studio

  Se si usa un IDE di Python diverso, seguire una procedura simile per l'IDE.

* Strumento di query SQL: in questa esercitazione si presuppone che si stia usando [Azure Data Studio](../../azure-data-studio/what-is.md). È anche possibile usare [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS).

* Pacchetti Python aggiuntivi: gli esempi in questa serie di esercitazioni usano pacchetti Python che potrebbero essere installati o meno. Usare i comandi **PIP** seguenti per installare questi pacchetti, se necessario.

  ```console
  pip install matplotlib
  pip install scipy
  pip install sklearn
  ```

## <a name="import-the-sample-database"></a>Importazione del database di esempio

Il set di dati di esempio usato in questa esercitazione è stato salvato in un file di backup del database con **estensione bak** che è possibile scaricare e usare. Questo set di dati è derivato dal set di dati [tpcx-BB](http://www.tpc.org/tpcx-bb/default.asp) fornito da [Transaction Processing Performance Council (TPC)](http://www.tpc.org/default.asp).

1. Scaricare il file [tpcxbb_1gb. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) nella cartella SQL Server backup. Per l'istanza di database predefinita, la cartella è:

   `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\`

1. Aprire Azure Data Studio, connettersi all'istanza di SQL Server e aprire una nuova finestra query.

1. Eseguire i comandi seguenti per ripristinare il database.

   ```sql
   USE master;
   GO

   RESTORE DATABASE tpcxbb_1gb
   FROM DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\tpcxbb_1gb.bak'
   WITH MOVE 'tpcxbb_1gb' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\tpcxbb_1gb.mdf'
      , MOVE 'tpcxbb_1gb_log' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\tpcxbb_1gb.ldf';
   GO
   ```

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si intende continuare con questa esercitazione, eliminare il database tpcxbb_1gb da SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Nella prima parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Importare un database di esempio in un'istanza di SQL Server

Per preparare i dati per il modello di Machine Learning, seguire la seconda parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione: Preparare i dati per eseguire il clustering in Python con SQL Server Machine Learning Services](tutorial-python-clustering-model-prepare-data.md)
