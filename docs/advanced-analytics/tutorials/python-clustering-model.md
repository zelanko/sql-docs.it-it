---
title: 'Esercitazione su Python: Categorizzare gli utenti'
description: In questa serie di esercitazioni in quattro parti si eseguirà il clustering dei clienti usando l'algoritmo K-Means in un database SQL usando Python con Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 245a1566bfbbf19821323d0b474669eaba1d2e6e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727079"
---
# <a name="tutorial-categorizing-customers-using-k-means-clustering-with-sql-server-machine-learning-services"></a>Esercitazione: Categorizzazione dei clienti tramite clustering K-Means con Machine Learning Services per SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa serie di esercitazioni in quattro parti si userà Python per sviluppare e distribuire un modello di clustering K-Means in [Machine Learning Services per SQL Server](../what-is-sql-server-machine-learning.md) per il clustering dei dati dei clienti.

Nella prima parte della serie verranno configurati i prerequisiti per l'esercitazione e quindi verrà ripristinato un set di dati di esempio in un database SQL. Più avanti nel corso della serie questi dati verranno usati per eseguire il training e la distribuzione di un modello di clustering in Python con Machine Learning Services per SQL Server.

Nelle seconda e nella terza parte della serie si svilupperanno alcuni script Python in un notebook di Azure Data Studio per analizzare e preparare i dati ed eseguire il training di un modello di Machine Learning. Quindi, nella quarta parte, verranno eseguiti gli script Python all'interno di un database SQL mediante stored procedure.

Per *clustering* si intende l'organizzazione dei dati in gruppi in cui i membri di ciascun gruppo sono simili per certi aspetti. Per questa serie di esercitazioni, si supponga di essere proprietari di un'azienda di vendita al dettaglio. Si userà l'algoritmo **K-Means** per eseguire il clustering dei clienti in un set di dati di acquisti e resi di prodotti. Il clustering dei clienti favorisce attività di marketing più mirate rivolte a gruppi specifici.
Il clustering K-Means è un algoritmo di *apprendimento non supervisionato* che cerca schemi nei dati in base ad analogie.

In questo articolo si apprenderà come:

> [!div class="checklist"]
> * Ripristinare un database di esempio in un'istanza di SQL Server

Nella [seconda parte](python-clustering-model-prepare-data.md) si apprenderà come preparare i dati di un database SQL per il clustering.

Nella [terza parte](python-clustering-model-build.md) si apprenderà come creare ed eseguire il training di un modello di clustering K-Means in Python.

Nella [quarta parte](python-clustering-model-deploy.md) si apprenderà come creare una stored procedure in un database SQL in grado di eseguire il clustering in Python in base ai nuovi dati.

## <a name="prerequisites"></a>Prerequisites

* [Machine Learning Services per SQL Server](../what-is-sql-server-machine-learning.md) con l'opzione del linguaggio Python: seguire le istruzioni di installazione nella [guida all'installazione di Windows](../install/sql-machine-learning-services-windows-install.md) o nella [guida all'installazione di Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15).

* IDE Python: questa esercitazione usa un notebook Python in [Azure Data Studio](../../azure-data-studio/what-is.md). Per altre informazioni, vedere [Come usare i notebook in Azure Data Studio](../../azure-data-studio/sql-notebooks.md). È anche possibile usare il proprio ambiente di sviluppo integrato di Python, ad esempio un notebook Jupyter o [Visual Studio Code](https://code.visualstudio.com/docs) con l'[estensione Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) e l'[estensione mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).

* Pacchetto [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package): il pacchetto **revoscalepy** è incluso in Machine Learning Services per SQL Server. Per usare il pacchetto in un computer client, vedere [Configurare un client di data science per lo sviluppo Python](../python/setup-python-client-tools-sql.md) per le opzioni di installazione locale del pacchetto.

  Se si usa un notebook Python in Azure Data Studio, seguire questa procedura aggiuntiva per usare **revoscalepy**:

  1. Aprire Azure Data Studio
  1. Scegliere **Preferenze** dal menu **File** e quindi selezionare **Impostazioni**
  1. Espandere **Estensioni** e selezionare **Notebook configuration** (Configurazione notebook)
  1. In **Percorso Python** immettere il percorso in cui sono state installate le librerie (ad esempio `C:\path-to-python-for-mls`)
  1. Assicurarsi che **Use Existing Python** (Usa Python esistente) sia selezionato
  1. Riavviare Azure Data Studio

  Se si usa un IDE di Python diverso, seguire una procedura simile per il proprio IDE.

* Strumento di query SQL: questa esercitazione presuppone che si usi [Azure Data Studio](../../azure-data-studio/what-is.md). È possibile usare anche [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS).

* Pacchetti Python aggiuntivi: gli esempi in questa serie di esercitazioni usano pacchetti Python che potrebbero essere installati o meno. Usare i comandi **pip** seguenti per installare questi pacchetti, se necessario.

  ```console
  pip install matplotlib
  pip install scipy
  pip install sklearn
  ```

## <a name="restore-the-sample-database"></a>Ripristinare il database di esempio

Il set di dati di esempio usato in questa esercitazione è stato salvato in un file di backup del database con estensione **bak** che è possibile scaricare e usare. Questo set di dati deriva dal set di dati [tpcx-bb](http://www.tpc.org/tpcx-bb/default.asp) fornito dal [Transaction Processing Performance Council (TPC)](http://www.tpc.org/default.asp).

1. Scaricare il file [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak).

1. Seguire le istruzioni in [Ripristinare un database da un file di backup](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) in Azure Data Studio usando i dettagli seguenti:

   * Importare i dati dal file **tpcxbb_1gb.bak** scaricato
   * Assegnare al database di destinazione il nome "tpcxbb_1gb"

1. È possibile verificare che il set di dati esista dopo il ripristino del database eseguendo una query sulla tabella **dbo.customer**:

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si intende continuare con questa esercitazione, eliminare il database tpcxbb_1gb da SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Nella prima parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Ripristinare un database di esempio in un'istanza di SQL Server

Per preparare i dati per il modello di Machine Learning, seguire la seconda parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione: Preparare i dati per eseguire il clustering in Python con Machine Learning Services per SQL Server](python-clustering-model-prepare-data.md)
