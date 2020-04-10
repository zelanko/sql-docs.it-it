---
title: 'Esercitazione su Python: Noleggi di sci'
description: Nella terza parte di questa serie di esercitazioni in quattro parti si compilerà un modello di regressione lineare in Python per stimare il noleggio di sci con Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8f07c056e903f1036bfba15398f7cf54a1985f2d
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116414"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Esercitazione su Python: Stimare il noleggio di sci con la regressione lineare in Machine Learning Services per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa serie di esercitazioni in quattro parti si useranno Python e la regressione lineare in [Machine Learning Services per SQL Server](../what-is-sql-server-machine-learning.md) per stimare il numero di noleggi di sci. In questa esercitazione viene usato un [notebook Python in Azure Data Studio](../../azure-data-studio/sql-notebooks.md), ma è possibile usare anche un ambiente IDE (Integrated Development Environment) Python integrato.

Si supponga di essere i proprietari di un'agenzia di noleggio di sci e di voler stimare il numero di noleggi richiesti in una data futura. Queste informazioni consentiranno di preparare correttamente le scorte, il personale e le strutture.

Nella prima parte di questa serie verranno configurati i prerequisiti. Nelle seconda e nella terza parte si svilupperanno alcuni script Python in un notebook Jupyter per preparare i dati ed eseguire il training di un modello di Machine Learning. Nella quarta parte verranno quindi eseguiti gli script Python in SQL Server mediante stored procedure T-SQL.

In questo articolo si apprenderà come:

> [!div class="checklist"]
> * Importare un database di esempio in SQL Server 

Nella [seconda parte](python-ski-rental-linear-regression-prepare-data.md) si apprenderà come caricare i dati da SQL Server in un frame di dati Python e come preparare i dati in Python.

Nella [terza parte](python-ski-rental-linear-regression-train-model.md) si apprenderà come eseguire il training di un modello di regressione lineare in Python.

Nella [quarta parte](python-ski-rental-linear-regression-deploy-model.md) si apprenderà come archiviare il modello in SQL Server e creare stored procedure dagli script Python sviluppati nella seconda e nella terza parte. Le stored procedure verranno quindi eseguite in SQL Server per eseguire stime basate sui nuovi dati.

## <a name="prerequisites"></a>Prerequisiti

* Machine Learning Services per SQL Server: per informazioni su come installare Machine Learning Services, vedere la [guida all'installazione di Windows](../install/sql-machine-learning-services-windows-install.md) o la [guida all'installazione di Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json).

* IDE Python: questa esercitazione usa un notebook Python in [Azure Data Studio](../../azure-data-studio/what-is.md). Per altre informazioni, vedere [Come usare i notebook in Azure Data Studio](../../azure-data-studio/sql-notebooks.md). 

    È anche possibile usare il proprio ambiente di sviluppo integrato di Python, ad esempio un notebook Jupyter o [Visual Studio Code](https://code.visualstudio.com/docs) con l'[estensione Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) e l'[estensione mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

* Strumento di query SQL: questa esercitazione presuppone che si usi [Azure Data Studio](../../azure-data-studio/what-is.md). È possibile usare anche [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS).

* Pacchetti Python aggiuntivi: gli esempi in questa serie di esercitazioni usano i seguenti pacchetti Python, che potrebbero essere installati o meno per impostazione predefinita:

  * pandas
  * pyodbc
  * sklearn

  Per installare questi pacchetti:
  1. In Azure Data Studio selezionare **Gestisci pacchetti**.
  2. Nel riquadro **Gestisci pacchetti** selezionare la scheda **Aggiungi nuovo**.
  3. Per ognuno dei seguenti pacchetti immettere il nome del pacchetto, fare clic su **Cerca**, quindi fare clic su **Installa**.

  In alternativa è possibile aprire un **prompt dei comandi**, passare al percorso di installazione della versione di Python usata in Azure Data Studio (ad esempio `cd %LocalAppData%\Programs\Python\Python37-32`), quindi eseguire `pip install` per ogni pacchetto.

## <a name="restore-the-sample-database"></a>Ripristinare il database di esempio

Il database di esempio usato in questa esercitazione è stato salvato in un file di backup del database con estensione **bak** che è possibile scaricare e usare.

1. Scaricare il file [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak).

1. Seguire le istruzioni in [Ripristinare un database da un file di backup](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) in Azure Data Studio usando i dettagli seguenti:

   * Importare i dati dal file **TutorialDB.bak** scaricato
   * Assegnare al database di destinazione il nome "TutorialDB"

1. È possibile verificare che il database ripristinato esista eseguendo una query sulla tabella **dbo.rental_data**:

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```

Abilitare gli script esterni eseguendo i comandi SQL seguenti:

  ```sql
  sp_configure 'external scripts enabled', 1;
  RECONFIGURE WITH override;
  ```

## <a name="next-steps"></a>Passaggi successivi

Nella prima parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Sono stati installati i prerequisiti
* È stato importato un database di esempio in SQL Server

Per preparare i dati dal database TutorialDB, seguire la seconda parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione su Python: Preparare i dati per eseguire il training di un modello di regressione lineare](python-ski-rental-linear-regression-prepare-data.md)