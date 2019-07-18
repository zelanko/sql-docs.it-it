---
title: Sviluppare e distribuire SQL Server di database per Linux | Microsoft Docs
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.openlocfilehash: b98980837f6dce2ebd9f39be142b816f37f16cd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077398"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Usare Visual Studio per creare i database di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT) Trasforma Visual Studio in un ambiente avanzato per lo sviluppo e il database lifecycle management (DLM) for SQL Server in Linux. È possibile sviluppare, compilare, testare e pubblicare il database da un progetto di controllo del codice sorgente, esattamente come si sviluppa il codice dell'applicazione.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Installare Visual Studio e SQL Server Data Tools

1. Se non si è già installato Visual Studio nel computer Windows [scaricare e installare Visual Studio]. Se non hai una licenza di Visual Studio, Visual Studio Community edition è un IDE gratuito con funzionalità complete per studenti, sviluppatori singoli e open source.

2. Durante l'installazione di Visual Studio, selezionare **Custom** per il **scegliere il tipo di installazione** opzione. Scegliere **Avanti**

3. Selezionare **Microsoft SQL Server Data Tools**, **Git per Windows**, e **estensione GitHub per Visual Studio** dall'elenco di selezione funzionalità.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. Continuare e completare l'installazione di Visual Studio. Può richiedere alcuni minuti.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>Aggiornare SQL Server Data Tools versione di SSDT 17.0 RC

SQL Server in Linux è supportato da SSDT versione 17.0 RC o versione successiva.

* [Scaricare e installare SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939).

## <a name="create-a-new-database-project-in-source-control"></a>Creare un nuovo progetto di database nel controllo del codice sorgente

1. Avviare Visual Studio.

2. Selezionare **Team Explorer** nel **visualizzazione** menu. 

3. Fare clic su **New** nelle **Git Repository locale** sezione la **Connect** pagina.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. Fare clic su **Crea**. Dopo aver creato il repository Git locale, fare doppio clic su **SSDTRepo**.

4. Fare clic su **New** nel **soluzioni** sezione. Selezionare **SQL Server** sotto **Other Languages** nodo nel **nuovo progetto** finestra di dialogo.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. Digitare **TutorialDB** per il nome e fare clic su **OK** per creare un nuovo progetto di database.

## <a name="create-a-new-table-in-the-database-project"></a>Creare una nuova tabella nel progetto di database

1. Selezionare **Esplora soluzioni** nel **visualizzazione** menu.

2. Aprire il menu progetto facendo clic su **TutorialDB** in Esplora soluzioni.

3. Selezionare **tabella** sotto **aggiungere**.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. Tramite Progettazione tabelle, aggiungere due colonne, nome `nvarchar(50)` e il percorso `nvarchar(50)`, come illustrato nell'immagine. SSDT genera il `CREATE TABLE` script man mano che si aggiungono le colonne nella finestra di progettazione.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. Salvare il **Table1.sql** file.

## <a name="build-and-validate-the-database"></a>Creare e convalidare il database

1. Aprire il menu di progetto di database sul **TutorialDB** e selezionare **compilazione**. SSDT viene compilato con file di codice sorgente nel progetto e compila un file di pacchetto (con estensione dacpac) dell'applicazione livello dati. Ciò consente di pubblicare un database all'istanza di SQL Server in Linux. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. Archiviare il messaggio di conferma di compilazione **Output** finestra in Visual Studio. 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>Pubblicare il database all'istanza di SQL Server in Linux

1. Aprire il menu di progetto di database sul **TutorialDB** e selezionare **Publish**.

2. Fare clic su **modifica** per selezionare l'istanza di SQL Server in Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. Nella finestra di dialogo connessione, immettere il nome host o indirizzo IP dell'istanza di SQL Server su Linux, nome utente e password.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. Scegliere il **pubblica** pulsante sulla finestra di dialogo pubblica.

5. Controllare lo stato di pubblicazione nel **operazioni degli strumenti dati** finestra.

6. Fare clic su **visualizzare i risultati** oppure **Visualizza Script** per visualizzare i dettagli del database di pubblicare i risultati in SQL Server in Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Avere creato un nuovo database nell'istanza di SQL Server in Linux e appreso le nozioni di base dello sviluppo di un database con un progetto di database di controllo del codice sorgente.

## <a name="next-steps"></a>Passaggi successivi

Se si ha familiarità con T-SQL, vedere [Esercitazione: Scrittura di istruzioni Transact-SQL] e il [Riferimento Transact-SQL (motore di Database)].

Per altre informazioni sullo sviluppo di un database con SQL Data Tools, vedere [documenti MSDN di SSDT]

[Scaricare e installare Visual Studio]: https://www.visualstudio.com/downloads/
[Download and Install SSDT]:https://aka.ms/ssdt-download
[Documenti MSDN di SSDT]: https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx
[Esercitazione: Scrittura di istruzioni Transact-SQL]: https://msdn.microsoft.com/library/ms365303.aspx
[Riferimento Transact-SQL (motore di Database)]: https://msdn.microsoft.com/library/bb510741.aspx
