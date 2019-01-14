---
title: Usare l'estensione mssql Visual Studio Code per SQL Server in Linux | Microsoft Docs
description: Usare l'estensione mssql per Visual Studio Code per modificare ed eseguire script Transact-SQL per SQL Server in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: sql-linux
ms.openlocfilehash: 583c7ac13b49370b333e80568c4b52885b58dcf3
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100566"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-on-linux"></a>Usare Visual Studio Code per creare ed eseguire script Transact-SQL in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come usare il *mssql* estensione per Visual Studio Code sviluppare i database di SQL Server in Linux.

## <a name="install-and-start-visual-studio-code"></a>Installare e avviare Visual Studio Code

Visual Studio Code è un editor grafico di codice per Linux, macOS e Windows che supporta le estensioni. 

1. [Scaricare e installare Visual Studio Code] nel computer.
   
1. Avviare Visual Studio Code.
   
   >[!NOTE]
   >Se Visual Studio Code non viene avviato quando si è connessi tramite una sessione di desktop remoto di xrdp, vedere [Visual Studio Code non funziona in Ubuntu quando si è connessi tramite XRDP](https://github.com/Microsoft/vscode/issues/3451).

## <a name="install-the-mssql-extension"></a>Installare l'estensione mssql

Il [estensione mssql per Visual Studio Code] consente di connettersi a SQL Server, eseguire una query con Transact-SQL (T-SQL) e visualizzare i risultati.

1. In Visual Studio Code, selezionare **View** > **comandi**, oppure premere **Ctrl**+**MAIUSC** + **P**, oppure premere **F1** per aprire il **comandi**. 
   
1. Nel **riquadro comandi**, selezionare **estensioni: Installare le estensioni** dall'elenco a discesa. 
   
1. Nel **Extensions** riquadro, digitare *mssql*.
   
1. Selezionare il **SQL Server (mssql)** estensione e quindi selezionare **installare**. 
   
   ![Installare l'estensione mssql](./media/sql-server-linux-develop-use-vscode/vscode-extension.png)   
   
1. Al termine dell'installazione, selezionare **Ricarica** per abilitare l'estensione. 

## <a name="create-or-open-a-sql-file"></a>Creare o aprire un file SQL

L'estensione mssql Abilita i comandi mssql e T-SQL IntelliSense nell'editor del codice quando la modalità di linguaggio è impostata su **SQL**.

1. Selezionare **File** > **nuovo File** oppure premere **Ctrl**+**N**. Per impostazione predefinita, Visual Studio Code apre un nuovo file di testo normale. 

1. Selezionare **testo normale** sulla barra di stato inferiore oppure premere **Ctrl**+**K** > **M**, selezionare **SQL** dall'elenco a discesa di lingue. 
   
   ![Modalità linguaggio SQL](./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png)   
   
Se si apre un file esistente con un *con estensione SQL* estensione di file, la modalità di linguaggio viene impostata automaticamente su SQL.  

## <a name="connect-to-sql-server"></a>Connessione a SQL Server

Seguire questi passaggi per creare un profilo di connessione e connettersi a SQL Server.

> [!TIP] 
> È anche possibile creare e modificare i profili di connessione nel file di impostazioni utente (*Settings. JSON*). Per aprire il file di impostazioni, selezionare **File** > **preferenze** > **impostazioni**. Per altre informazioni, vedere [gestire i profili di connessione].
   
1. Premere **Ctrl**+**MAIUSC**+**P** oppure **F1** per aprire la **comandi**. 
   
1. Tipo di *sql* per visualizzare il servizio mssql comandi o tipo *sqlcon*, quindi selezionare **MS SQL: Connettere** dall'elenco a discesa.
   
   ![comandi MSSQL](./media/sql-server-linux-develop-use-vscode/vscode-commands.png)   
   
   >[!NOTE]
   >Un file SQL, ad esempio il file SQL vuoto che è stato creato, deve avere lo stato attivo nell'editor del codice prima di poter eseguire i comandi mssql. 

1. Selezionare **Creazione guidata profilo connessione** per creare un nuovo profilo di connessione per il Server SQL.
   
1. Seguire le istruzioni per specificare le proprietà per il nuovo profilo di connessione. Dopo aver specificato ogni valore, premere **invio** per continuare. 
   
   1. **Nome del server o stringa di connessione ADO**: Specificare il nome di istanza di SQL Server. Uso *localhost* per connettersi a un'istanza di SQL Server nel computer locale. Per connettersi a un Server SQL remoto, immettere il nome della destinazione di SQL Server o il relativo indirizzo IP. Se è necessario specificare una porta, utilizzare la virgola per separarle dal nome. Ad esempio, per un server locale in esecuzione sulla porta 1401, immettere *localhost, 1401*. 
      
      >[!NOTE]
      >È anche possibile immettere la stringa di connessione di ADO per il database in questo caso, premere **invio**e, facoltativamente, nome del profilo di connessione e premere **invio** nuovamente a connettersi e creare il profilo. 
      
   1. **Nome del database** (facoltativo): Il database che si desidera utilizzare. Per creare un nuovo database, non specificare un database, nome e premere **invio** per continuare. 
      
   1. **Tipo di autenticazione**: Premere **invio** per selezionare **account di accesso SQL**. 
      
   1. **Nome utente**: Immettere il nome di un utente con accesso a un database nel server.
      
   1. **Password**: Immettere la password per l'utente specificato.
      
   1. **Salva Password**: Premere **invio** per selezionare **Yes** e salvare la password. Selezionare **No** venga richiesta la password ogni volta che viene usato il profilo di connessione. 
      
   1. **Nome profilo** (facoltativo): Digitare un nome per il profilo di connessione, ad esempio *localhost profilo*. 
   
   Dopo aver selezionato **invio**, Visual Studio Code crea il profilo di connessione e si connette a SQL Server. 
   
   > [!TIP]
   > Se la connessione non riesce, provare a isolare il problema dal messaggio di errore nel **Output** pannello in Visual Studio Code. Per aprire la **Output** Pannello di selezione **View** > **Output**. Vedere anche il [connessione indicazioni risoluzione].
   
1. Verificare la connessione nella barra di stato inferiore.
   
  ![Stato della connessione](./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png)   
   
## <a name="create-a-sql-database"></a>Creare un database SQL

1. Nel nuovo file SQL che è stato avviato in precedenza, digitare *sql* per visualizzare un elenco di frammenti di codice modificabile. 

  ![Frammenti di codice SQL](./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png)   
   
1. Selezionare **sqlCreateDatabase**.
   
1. Nel frammento di codice, sostituire `DatabaseName` con `TutorialDB`:
   
   ```sql
   -- Create a new database called 'TutorialDB'
   -- Connect to the 'master' database to run this snippet
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```
   
1. Premere **Ctrl**+**MAIUSC**+**elettronica** per eseguire i comandi Transact-SQL. Visualizzare i risultati nella finestra di query.
   
  ![Creare i messaggi di database](./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png)   
   
> [!TIP]
> È possibile personalizzare i tasti di scelta rapida per i comandi mssql. Visualizzare [personalizzare i tasti di scelta rapida].

## <a name="create-a-table"></a>Creare una tabella

1. Eliminare il contenuto della finestra dell'editor di codice.
   
1. Premere **Ctrl**+**MAIUSC**+**P** oppure **F1** per aprire la **comandi**. 
   
1. Tipo *sql* per visualizzare il servizio mssql comandi o tipo *sqluse*, quindi selezionare il **MS SQL: Use Database** comando.
   
1. Selezionare nuovo **TutorialDB** database. 
   
   ![Usare il database](./media/sql-server-linux-develop-use-vscode/vscode-use-database.png)   
   
1. Nell'editor del codice, digitare *sql* per visualizzare i frammenti di codice, selezionare **sqlCreateTable**, quindi premere **invio**.
   
1. Nel frammento di codice, digitare *dipendenti* per il nome della tabella e *dbo* per il nome dello schema.
   
1. Creare le colonne come illustrato nel codice seguente:
   
   ```sql
   -- Create a new table called 'Employees' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Employees', 'U') IS NOT NULL
   DROP TABLE dbo.Employees
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Employees
   (
      EmployeesId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location   [NVARCHAR](50)  NOT NULL
   );
   GO
   ```
   
1. Premere **Ctrl**+**MAIUSC**+**elettronica** per creare la tabella.

## <a name="insert-and-query"></a>Inserimento e query

1. Aggiungere le istruzioni seguenti per inserire quattro righe nella **dipendenti** tabella. 

   ```sql
   -- Insert rows into table 'Employees'
   INSERT INTO Employees
      ([EmployeesId],[Name],[Location])
   VALUES
      ( 1, N'Jared', N'Australia'),
      ( 2, N'Nikita', N'India'),
      ( 3, N'Tom', N'Germany'),
      ( 4, N'Jake', N'United States')   
   GO   
   -- Query the total count of employees
   SELECT COUNT(*) as EmployeeCount FROM dbo.Employees;
   -- Query all employee information
   SELECT e.EmployeesId, e.Name, e.Location 
   FROM dbo.Employees as e
   GO
   ```
   
   > [!TIP]
   > Durante la digitazione, usare T-SQL IntelliSense per completare le istruzioni.
   >![T-SQL IntelliSense](./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png)   
   
1. Premere **Ctrl**+**MAIUSC**+**elettronica** per eseguire i comandi. I due comportare la visualizzazione di set nel **risultati** finestra. 
   
   ![Risultati](./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png)   

## <a name="view-and-save-the-result"></a>Visualizzare e salvare il risultato
   
1. Selezionare **View** > **Editor Layout** > **Capovolgi Layout** per passare a un layout di divisione verticale o orizzontale.
   
1. Selezionare il **risultati** e **messaggi** pannello intestazioni per comprimere ed espandere i pannelli.
   
   ![Attiva/disattiva intestazioni](./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png)   
   
   > [!TIP]
   > È possibile personalizzare il comportamento predefinito dell'estensione mssql. Visualizzare [personalizzare le opzioni dell'estensione].
   
1. Selezionare l'icona di griglia di ingrandimento alla seconda griglia di risultati per ingrandire i risultati.
   
   ![Ottimizzare la griglia](./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png)   
   
   > [!NOTE]
   > Quando lo script T-SQL produce due o più le griglie dei risultati, viene visualizzata l'icona di ingrandimento.
   
1. Aprire il menu di scelta rapida della griglia facendo clic sulla griglia. 
   
   ![Menu di scelta rapida](./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png)   
   
1. Selezionare **Seleziona tutto**.
   
1. Aprire di nuovo il menu di scelta rapida della griglia e selezionare **Salva con nome JSON** per salvare i risultati in un *JSON* file.
   
1. Specificare un nome per il file JSON. 
   
1. Verificare che il file JSON vengono salvate e viene aperto in Visual Studio Code.
   
   ![Salva come JSON](./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png)   

Se è necessario salvare ed eseguire gli script SQL in un secondo momento, per amministrazione o un progetto di sviluppo più grande, salvare gli script con un *con estensione SQL* estensione.

## <a name="next-steps"></a>Passaggi successivi

Se si ha familiarità con T-SQL, vedere [esercitazione: Scrivere istruzioni Transact-SQL] e il [Riferimento Transact-SQL (motore di Database)].

Per altre informazioni sull'utilizzo o aggiunta come contributo all'estensione mssql, vedere la [wiki di progetto di estensione mssql].

Per altre informazioni sull'uso di Visual Studio Code, vedere la [documentazione di Visual Studio Code](https://code.visualstudio.com/docs).

[estensione MSSQL per Visual Studio Code]:https://aka.ms/mssql-marketplace
[Scaricare e installare Visual Studio Code]:https://code.visualstudio.com/Download
[.Net Core instructions]:https://www.microsoft.com/net/core
[gestire i profili di connessione]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[connessione indicazioni risoluzione]:./sql-server-linux-troubleshooting-guide.md#connection
[personalizzare i tasti di scelta rapida]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[Esercitazione: Scrivere istruzioni Transact-SQL]:https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements
[Riferimento Transact-SQL (motore di Database)]:https://docs.microsoft.com/sql/t-sql/language-reference
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[Windows 10 Universal C Runtime]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[personalizzare le opzioni dell'estensione]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[wiki di progetto di estensione MSSQL]: https://github.com/Microsoft/vscode-mssql/wiki
