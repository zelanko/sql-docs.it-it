---
title: 'Esercitazione per Python: Ski Rental (regressione lineare)'
description: In questa esercitazione si userà Python e la regressione lineare in SQL Server Machine Learning Services per prevedere il numero di noleggi di sci.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 718487ba55b2b8db8f16b59df5785cf78ff501f1
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242509"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Esercitazione per Python: Prevedere il noleggio di sci con regressione lineare in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa serie di esercitazioni in quattro parti si useranno Python e la regressione lineare in [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) per prevedere il numero di noleggi di sci. L'esercitazione usa un [notebook Python in Azure Data Studio](../../azure-data-studio/sql-notebooks.md), ma è anche possibile usare il proprio Integrated Development Environment Python (IDE).

Si supponga di essere proprietari di un'azienda di noleggio Ski e di voler prevedere il numero di affitti che saranno disponibili in una data futura. Queste informazioni consentiranno di preparare le scorte, il personale e le strutture.

Nella prima parte di questa serie verranno configurati i prerequisiti. Nelle parti due e tre verranno sviluppati alcuni script Python in un notebook di Jupyter per preparare i dati ed eseguire il training di un modello di machine learning. Quindi, nella terza parte, verranno eseguiti gli script Python all'interno SQL Server usando le stored procedure T-SQL.

L'articolo spiega come:

> [!div class="checklist"]
> * Importare un database di esempio in SQL Server 

Nella [seconda parte](python-ski-rental-linear-regression-prepare-data.md)verrà illustrato come caricare i dati da SQL Server in un frame di dati Python e preparare i dati in Python.

Nella [terza parte](python-ski-rental-linear-regression-train-model.md)verrà illustrato come eseguire il training di un modello di regressione lineare in Python.

Nella [quarta parte](python-ski-rental-linear-regression-deploy-model.md), si apprenderà come archiviare il modello in SQL Server, quindi creare stored procedure dagli script Python sviluppati in parti due e tre. Le stored procedure vengono eseguite in SQL Server per eseguire stime basate sui nuovi dati.

## <a name="prerequisites"></a>Prerequisiti

* SQL Server Machine Learning Services: per informazioni su come installare Machine Learning Services, vedere la Guida all'installazione di [Windows](../install/sql-machine-learning-services-windows-install.md) o la Guida all' [installazione di Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json).

* IDE Python: questa esercitazione usa un notebook Python in [Azure Data Studio](../../azure-data-studio/what-is.md). Per ulteriori informazioni, vedere [come utilizzare i notebook in Azure Data Studio](../../azure-data-studio/sql-notebooks.md). 

    È anche possibile usare l'IDE di Python, ad esempio un notebook Jupyter o [Visual Studio Code](https://code.visualstudio.com/docs) con l' [estensione Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) e l' [estensione MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

* pacchetto [revoscalepy](../python/ref-py-revoscalepy.md) : il pacchetto **revoscalepy** è incluso in SQL Server Machine Learning Services. Per usare il pacchetto in un computer client, vedere [configurare un client Data Science per lo sviluppo Python](../python/setup-python-client-tools-sql.md) per le opzioni per l'installazione locale del pacchetto.

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
    pip install pandas
    pip install sklearn
    pip install pickle
    ```

## <a name="restore-the-sample-database"></a>Ripristinare il database di esempio

Il set di dati di esempio usato in questa esercitazione è stato salvato in un file di backup del database con **estensione bak** che è possibile scaricare e usare.

1. Scaricare il file [TutorialDB. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak).

1. Seguire le istruzioni riportate in [ripristinare un database da un file di backup](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) in Azure Data Studio, usando i dettagli seguenti:

   * Importa dal file **TutorialDB. bak** scaricato
   * Assegnare al database di destinazione il nome "TutorialDB"

1. È possibile verificare che il set di dati esista dopo il ripristino del database eseguendo una query sulla tabella **dbo. rental_data** :

    ```sql
    USE TutorialDB;
    SELECT * FROM [dbo].[rental_data];
    ```

## <a name="next-steps"></a>Passaggi successivi

Nella prima parte di questa serie di esercitazioni sono stati completati i passaggi seguenti:

* Prerequisiti installati
* Importare un database di esempio in un SQL Server

Per preparare i dati dal database TutorialDB, seguire la seconda parte di questa serie di esercitazioni:

> [!div class="nextstepaction"]
> [Esercitazione per Python: Preparare i dati per il training di un modello di regressione lineare](python-ski-rental-linear-regression-prepare-data.md)