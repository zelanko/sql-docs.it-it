---
title: Usare l'utilità sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL statements, executing
- command prompt utilities [SQL Server], sqlcmd
- statements [SQL Server], executing
- sqlcmd utility, about sqlcmd utility
ms.assetid: 3ec89119-7314-43ef-9e91-12e72bb63d62
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19c13fba697477174f671344304a9cd4befba53e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063642"
---
# <a name="use-the-sqlcmd-utility"></a>Utilizzo dell'utilità sqlcmd
  L'utilità `sqlcmd` è un'utilità della riga di comando per l'esecuzione interattiva ad hoc di istruzioni e script [!INCLUDE[tsql](../../includes/tsql-md.md)], nonché per l'automazione di attività di scripting [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per utilizzare `sqlcmd` in modo interattivo o per compilare file script da eseguire tramite `sqlcmd`, è necessario conoscano [!INCLUDE[tsql](../../includes/tsql-md.md)]. L'utilità `sqlcmd` viene in genere utilizzata nei modi seguenti:  
  
-   Gli utenti immettono interattivamente istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] in modo analogo all'utilizzo del prompt dei comandi. I risultati vengono visualizzati al prompt dei comandi. Per aprire una finestra del prompt dei comandi, fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Accessori**e quindi su **Prompt dei comandi**. Al prompt dei comandi digitare `sqlcmd` seguito da un elenco delle opzioni desiderate. Per un elenco completo delle opzioni supportate da `sqlcmd`, vedere [utilità sqlcmd](../../tools/sqlcmd-utility.md).  
  
-   Gli utenti inviano un processo `sqlcmd` specificando una singola istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] da eseguire o facendo in modo che l'utilità punti a un file di testo contenente istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] da eseguire. L'output viene in genere indirizzato a un file di testo, ma può essere anche visualizzato al prompt dei comandi.  
  
-   [Modalità SQLCMD](edit-sqlcmd-scripts-with-query-editor.md) nell'editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
-   Oggetti SMO (SQL Server Management Objects)  
  
-   Processi CmdExec di SQL Server Agent.  
  
## <a name="typically-used-sqlcmd-options"></a>Opzioni di sqlcmd utilizzate di frequente  
 Le opzioni seguenti sono quelle utilizzate più di frequente:  
  
-   L'opzione server ( **-S**) che identifica l'istanza del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui `sqlcmd` si connette.  
  
-   Le opzioni di autenticazione ( **-E**, **- U**, e **-P**) che specificano le credenziali che `sqlcmd` utilizza per connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  Opzione **-E** che è l'opzione predefinita e non è necessario specificarla.  
  
-   Opzioni di input ( **-Q**, **- q**, e **-i**) che identificano la posizione dell'input `sqlcmd`.  
  
-   L'opzione di output ( **-o**) che specifica il file in cui `sqlcmd` consiste nell'inserire il proprio output.  
  
## <a name="connecting-to-the-sqlcmd-utility"></a>Connessione all'utilità sqlcmd  
 Vengono di seguito riportati alcuni utilizzi comuni dell'utilità `sqlcmd`:  
  
-   Connessione a un'istanza predefinita utilizzando l'autenticazione di Windows per eseguire in modo interattivo le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    sqlcmd -S <ComputerName>  
    ```  
  
    > [!NOTE]  
    >  Nell'esempio precedente, **-E** non è specificata perché è l'opzione predefinita e `sqlcmd` si connette all'istanza predefinita usando l'autenticazione di Windows.  
  
-   Connessione a un'istanza denominata utilizzando l'autenticazione di Windows per eseguire in modo interattivo istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName>  
    ```  
  
     o Gestione configurazione  
  
    ```  
    sqlcmd -S .\<InstanceName>  
    ```  
  
-   Connessione a un'istanza denominata utilizzando l'autenticazione di Windows e specificando i file di input e di output:  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName> -i <MyScript.sql> -o <MyOutput.rpt>  
    ```  
  
-   Connessione all'istanza predefinita nel computer locale utilizzando l'autenticazione di Windows, esecuzione di una query e impostazione di `sqlcmd` in modo che rimanga in esecuzione al termine dell'esecuzione della query:  
  
    ```  
    sqlcmd -q "SELECT * FROM AdventureWorks2012.Person.Person"  
    ```  
  
-   Connessione all'istanza predefinita nel computer locale utilizzando l'autenticazione di Windows, esecuzione di una query, indirizzamento dell'output a un file e impostazione di `sqlcmd` in modo che venga chiuso al termine dell'esecuzione della query:  
  
    ```  
    sqlcmd -Q "SELECT * FROM AdventureWorks2012.Person.Person" -o MyOutput.txt  
    ```  
  
-   Connessione a un'istanza denominata utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire in modo interattivo istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] con richiesta di password da parte di `sqlcmd`:  
  
    ```  
    sqlcmd -U MyLogin -S <ComputerName>\<InstanceName>  
    ```  
  
    > [!NOTE]  
    >  Per un elenco delle opzioni supportate dall'utilità `sqlcmd`, eseguire: `sqlcmd -?`.  
  
## <a name="running-transact-sql-statements-interactively-by-using-sqlcmd"></a>Esecuzione interattiva di istruzioni Transact-SQL utilizzando sqlcmd  
 È possibile utilizzare l'utilità `sqlcmd` in modo interattivo per eseguire istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] in una finestra del prompt dei comandi. Per eseguire in modo interattivo [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzioni utilizzando `sqlcmd`, eseguire l'utilità senza utilizzare il **-Q**, **- q**, **-Z**, o **- i** le opzioni per specificare eventuali file di input o query. Ad esempio:  
  
 `sqlcmd -S <ComputerName>\<InstanceName>`  
  
 Quando il comando viene eseguito senza file di input o query, `sqlcmd` si connette all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi visualizza una nuova riga con il valore `1>` seguito da un carattere di sottolineatura intermittente denominato prompt di `sqlcmd`. Il valore `1` indica che si tratta della prima riga di un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)], mentre il prompt di `sqlcmd` è il punto in cui inizia l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] quando la si digita.  
  
 Al prompt di `sqlcmd` è possibile digitare istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] e comandi di `sqlcmd`, ad esempio `GO` e `EXIT`. Ogni istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] viene inserita in un buffer denominato cache dell'istruzione. Dopo aver digitato il comando `GO` e premuto di INVIO, queste istruzioni vengono inviate a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per uscire `sqlcmd`, digitare `EXIT` o `QUIT` all'inizio di una nuova riga.  
  
 Per cancellare il contenuto della cache delle istruzioni, digitare `:RESET`. Tipizzazione `^C` provoca `sqlcmd` per uscire. È inoltre possibile utilizzare `^C` per arrestare l'esecuzione della cache delle istruzioni dopo l'esecuzione di un comando `GO`.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] le istruzioni immesse in una sessione interattiva possono essere modificate immettendo il **: ED** comandi e `sqlcmd` prompt dei comandi. Verrà aperto l'editor. Dopo aver modificato l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] e chiuso l'editor, l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] modificata verrà visualizzata nella finestra di comando. Immettere `GO` per eseguire therevised [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione.  
  
## <a name="quoted-strings"></a>Stringhe tra virgolette  
 I caratteri racchiusi tra virgolette vengono utilizzati senza alcuna pre-elaborazione aggiuntiva, fatta eccezione per il fatto che è possibile inserire virgolette in una stringa immettendo due virgolette consecutive. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tratta questa sequenza di caratteri come virgoletta. La traduzione avviene tuttavia nel server. Le variabili di scripting non vengono espanse se sono incluse all'interno di una stringa.  
  
 Ad esempio:  
  
 `sqlcmd`  
  
 `PRINT "Length: 5"" 7'";`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Length: 5" 7'`  
  
## <a name="strings-that-span-multiple-lines"></a>Stringhe che si estendono su più righe  
 `sqlcmd` supporta script con stringhe che si estendono su più righe. Ad esempio, l'istruzione `SELECT` seguente si estende su più righe ma rappresenta una stringa singola eseguita quando si preme INVIO dopo aver digitato `GO`.  
  
 `SELECT First line`  
  
 `FROM Second line`  
  
 `WHERE Third line;`  
  
 `GO`  
  
## <a name="interactive-sqlcmd-example"></a>Esempio di esecuzione interattiva dell'utilità sqlcmd  
 Nell'esempio seguente viene illustrato il contenuto della finestra del prompt dei comandi quando si esegue `sqlcmd` in modo interattivo.  
  
 Quando si apre la finestra del prompt dei comandi, è presente una riga simile alla seguente:  
  
 `C:\> _`  
  
 Questo significa che la cartella `C:\` è la cartella corrente. Se si specifica un nome di file, Windows cercherà il file in tale cartella.  
  
 Digitare `sqlcmd` per connettersi all'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer locale. Il contenuto della finestra del prompt dei comandi sarà il seguente:  
  
 `C:\>sqlcmd`  
  
 `1> _`  
  
 Questo significa che è stata eseguita la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e `sqlcmd` è ora pronto ad accettare istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] e comandi `sqlcmd` . Il carattere di sottolineatura intermittente dopo il valore `1>` è il prompt di `sqlcmd` che contrassegna la posizione in cui verranno visualizzati le istruzioni e i comandi digitati. A questo punto, digitare `USE AdventureWorks2012` e premere INVIO e quindi digitare `GO` e premere INVIO. Il contenuto della finestra del prompt dei comandi sarà il seguente:  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `1> _`  
  
 La pressione di INVIO dopo aver immesso `USE AdventureWorks2012` segnala all'utilità `sqlcmd` di iniziare una nuova riga. Premendo INVIO, dopo avere digitato `GO,` viene segnalato a `sqlcmd` di inviare l'istruzione `USE AdventureWorks2012` all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. `sqlcmd` restituisce quindi un messaggio per indicare che l'istruzione `USE` è stata completata correttamente e visualizza un nuovo prompt di `1>` per indicare che è possibile immettere un nuovo comando o istruzione.  
  
 Nell'esempio seguente viene illustrato il contenuto della finestra del prompt dei comandi quando si digita un'istruzione `SELECT` , un comando `GO` per eseguire l'istruzione `SELECT`e un comando `EXIT` per uscire da `sqlcmd`:  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `BusinessEntityID   FirstName                 LastName`  
  
 `----------- -------------------------------- -----------`  
  
 `1           Syed                             Abbas`  
  
 `2           Catherine                        Abel`  
  
 `3           Kim                              Abercrombie`  
  
 `(3 rows affected)`  
  
 `1> EXIT`  
  
 `C:\>`  
  
 Le righe successive alla riga `3> GO` costituiscono l'output di un'istruzione `SELECT` . Dopo la generazione dell'output, `sqlcmd` reimposta il prompt di `sqlcmd` e visualizza `1>`. Dopo aver immesso `EXIT` nella riga `1>`, nella finestra del prompt dei comandi viene visualizzata la stessa riga presente alla prima apertura di tale finestra. Ciò indica che la sessione di `sqlcmd` è terminata. È ora possibile chiudere la finestra del prompt dei comandi digitando un altro comando `EXIT` .  
  
## <a name="running-transact-sql-script-files-by-using-sqlcmd"></a>Esecuzione di file script Transact-SQL utilizzando sqlcmd  
 È possibile utilizzare `sqlcmd` per eseguire file script del database. I file di script sono file di testo che contengono una combinazione di [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzioni `sqlcmd` comandi e variabili di scripting. Per altre informazioni sullo scripting di variabili, vedere [Utilizzo di sqlcmd con variabili di scripting](sqlcmd-use-with-scripting-variables.md). Il funzionamento di `sqlcmd` con le istruzioni, i comandi e le variabili di scripting presenti in un file script è analogo al funzionamento con le istruzioni e i comandi immessi in modo interattivo. La principale differenza sta nel fatto che `sqlcmd` legge il file di input senza pause anziché attendere l'immissione di istruzioni, comandi e variabili di scripting da parte dell'utente.  
  
 I file script di database possono essere creati nei modi seguenti:  
  
-   È possibile compilare ed eseguire il debug di un set di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] in modo interattivo in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi salvare il contenuto della finestra Query come file script.  
  
-   È possibile creare un file di testo contenente istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzando un editor di testo, ad esempio Blocco note.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-running-a-script-by-using-sqlcmd"></a>A. Esecuzione di uno script utilizzando sqlcmd  
 Avviare Blocco note e digitare le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti:  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 Creare una cartella denominata `MyFolder` e quindi salvare lo script come file `MyScript.sql` nella cartella `C:\MyFolder`. Al prompt dei comandi immettere quanto segue per eseguire lo script e inserire l'output nel file `MyOutput.txt` della cartella `MyFolder`:  
  
 `sqlcmd -i C:\MyFolder\MyScript.sql -o C:\MyFolder\MyOutput.txt`  
  
 Il contenuto di `MyOutput.txt` visualizzato in Blocco note sarà il seguente:  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `BusinessEntityID FirstName   LastName`  
  
 `---------------- ----------- -----------`  
  
 `1                Syed        Abbas`  
  
 `2                Catherine   Abel`  
  
 `3                Kim         Abercrombie`  
  
 `(3 rows affected)`  
  
### <a name="b-using-sqlcmd-with-a-dedicated-administrative-connection"></a>B. Utilizzo di sqlcmd con una connessione amministrativa dedicata  
 Nell'esempio seguente `sqlcmd` viene utilizzato per connettersi a un server in cui si è verificato un problema di blocco utilizzando la connessione amministrativa dedicata (DAC, Dedicated Administration Connection).  
  
 `C:\>sqlcmd -S ServerName -A`  
  
 `1> SELECT blocked FROM sys.dm_exec_requests WHERE blocked <> 0;`  
  
 `2> GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `spid   blocked`  
  
 `------ -------`  
  
 `62       64`  
  
 `(1 rows affected)`  
  
 Utilizzare `sqlcmd` per terminare il processo di blocco.  
  
 `1> KILL 64;`  
  
 `2> GO`  
  
### <a name="c-using-sqlcmd-to-execute-a-stored-procedure"></a>C. Utilizzo di sqlcmd per eseguire una stored procedure  
 Nell'esempio seguente viene illustrata la modalità di esecuzione di una stored procedure mediante `sqlcmd`. Creare la stored procedure seguente.  
  
 `USE AdventureWorks2012;`  
  
 `IF OBJECT_ID ( ' dbo.ContactEmailAddress, 'P' ) IS NOT NULL`  
  
 `DROP PROCEDURE dbo.ContactEmailAddress;`  
  
 `GO`  
  
 `CREATE PROCEDURE dbo.ContactEmailAddress`  
  
 `(`  
  
 `@FirstName nvarchar(50)`  
  
 `,@LastName nvarchar(50)`  
  
 `)`  
  
 `AS`  
  
 `SET NOCOUNT ON`  
  
 `SELECT EmailAddress`  
  
 `FROM Person.Person`  
  
 `WHERE FirstName = @FirstName`  
  
 `AND LastName = @LastName;`  
  
 `SET NOCOUNT OFF`  
  
 Al prompt di `sqlcmd` digitare il comando seguente:  
  
 `C:\sqlcmd`  
  
 `1> :Setvar FirstName Gustavo`  
  
 `1> :Setvar LastName Achong`  
  
 `1> EXEC dbo.ContactEmailAddress $(Gustavo),$(Achong)`  
  
 `2> GO`  
  
 `EmailAddress`  
  
 `-----------------------------`  
  
 `gustavo0@adventure-works.com`  
  
### <a name="d-using-sqlcmd-for-database-maintenance"></a>D. Utilizzo di sqlcmd per la manutenzione del database  
 Nell'esempio seguente viene illustrato l'utilizzo di `sqlcmd` per un'attività di manutenzione del database. Creare `C:\BackupTemplate.sql` con il codice seguente.  
  
 `USE master;`  
  
 `BACKUP DATABASE [$(db)] TO DISK='$(bakfile)';`  
  
 Al prompt di `sqlcmd` digitare il comando seguente:  
  
 `C:\ >sqlcmd`  
  
 `1> :connect <server>`  
  
 `Sqlcmd: Successfully connected to server <server>.`  
  
 `1> :setvar db msdb`  
  
 `1> :setvar bakfile c:\msdb.bak`  
  
 `1> :r c:\BackupTemplate.sql`  
  
 `2> GO`  
  
 `Changed database context to 'master'.`  
  
 `Processed 688 pages for database 'msdb', file 'MSDBData' on file 2.`  
  
 `Processed 5 pages for database 'msdb', file 'MSDBLog' on file 2.`  
  
 `BACKUP DATABASE successfully processed 693 pages in 0.725 seconds (7.830 MB/sec)`  
  
### <a name="e-using-sqlcmd-to-execute-code-on-multiple-instances"></a>E. Utilizzo di sqlcmd per eseguire codice su più istanze  
 Il codice seguente in un file rappresenta un esempio di script che si connette a due istanze. Si noti il comando `GO` prima della connessione alla seconda istanza.  
  
 `:CONNECT <server>\,<instance1>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
 `:CONNECT <server>\,<instance2>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
### <a name="e-returning-xml-output"></a>E. Restituzione di output XML  
 Nell'esempio seguente viene illustrato come l'output XML venga restituito non formattato in un flusso continuo.  
  
 `C:\>sqlcmd -d AdventureWorks2012`  
  
 `1> :XML ON`  
  
 `1> SELECT TOP 3 FirstName + ' ' + LastName + ', '`  
  
 `2> FROM Person.Person`  
  
 `3> GO`  
  
 `Syed Abbas, Catherine Abel, Kim Abercrombie,`  
  
### <a name="f-using-sqlcmd-in-a-windows-script-file"></a>F. Utilizzo di sqlcmd in un file script di Windows  
 Oggetto `sqlcmd`comando, ad esempio `sqlcmd -i C:\InputFile.txt -o C:\OutputFile.txt,` possono essere eseguiti in un file con estensione bat insieme a VBScript. In questo caso, non utilizzare opzioni interattive. Nel computer che esegue il file con estensione bat deve essere installato `sqlcmd`.  
  
 Creare innanzitutto i quattro file seguenti:  
  
-   C:\badscript.sql  
  
    ```  
    SELECT batch_1_this_is_an_error  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\goodscript.sql  
  
    ```  
    SELECT 'batch #1'  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\returnvalue.sql  
  
    ```  
    :exit(select 100)  
    @echo off  
    C:\windowsscript.bat  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
-   C:\windowsscript.bat  
  
    ```  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
 Quindi, al prompt dei comandi eseguire `C:\windowsscript.bat`:  
  
 `C:\>windowsscript.bat`  
  
 `Running badscript.sql`  
  
 `== An error occurred`  
  
 `Running goodscript.sql`  
  
 `Running returnvalue.sql`  
  
 `SQLCMD returned 100 to the command shell`  
  
### <a name="g-using-sqlcmd-to-set-encryption-on-windows-azure-sql-database"></a>G. Utilizzo di sqlcmd per impostare la crittografia in un database SQL di Windows Azure  
 Oggetto `sqlcmd`può essere eseguito su una connessione a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] dati per specificare la crittografia e attendibilità del certificato. Due ' sqlcmd ' ' sono disponibili le opzioni:  
  
-   L'opzione -N viene utilizzata dal client per richiedere una connessione crittografata. Equivale all'opzione ADO.net `ENCRYPT = true`.  
  
-   L'opzione -C viene usata dal client per configurare l'attendibilità implicita del certificato del server senza necessità di convalida. Equivale all'opzione ADO.net `TRUSTSERVERCERTIFICATE = true`.  
  
 Il servizio [!INCLUDE[ssSDS](../../includes/sssds-md.md)] non supporta tutte le opzioni `SET` disponibili in un'istanza di SQL Server. Nelle opzioni seguenti viene generato un errore quando l'opzione `SET` corrispondente è impostata su `ON` o `OFF`:  
  
-   SET ANSI_DEFAULTS  
  
-   SET ANSI_NULLS  
  
-   SET REMOTE_PROC_TRANSACTIONS  
  
-   SET ANSI_NULL_DEFAULT  
  
 Le opzioni SET seguenti non generano eccezioni ma non possono essere utilizzate, in quanto deprecate:  
  
-   SET CONCAT_NULL_YIELDS_NULL  
  
-   SET ANSI_PADDING  
  
-   SET QUERY_GOVERNOR_COST_LIMIT  
  
#### <a name="syntax"></a>Sintassi  
 Gli esempi seguenti si riferiscono ai casi in cui le impostazioni del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client includono: `ForceProtocolEncryption = False`, `Trust Server Certificate = No`  
  
 Effettuare la connessione utilizzando le credenziali di Windows e la comunicazione crittografata:  
  
```  
SQLCMD -E -N  
  
```  
  
 Effettuare la connessione utilizzando le credenziali di Windows e un certificato server attendibile:  
  
```  
SQLCMD -E -C  
  
```  
  
 Effettuare la connessione utilizzando le credenziali di Windows, la comunicazione crittografata e un certificato server attendibile:  
  
```  
SQLCMD -E -N -C  
  
```  
  
 Gli esempi seguenti si riferiscono ai casi in cui le impostazioni del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client includono: `ForceProtocolEncryption = True`, `TrustServerCertificate = Yes`.  
  
 Effettuare la connessione utilizzando le credenziali di Windows, la comunicazione crittografata e un certificato server attendibile:  
  
```  
SQLCMD -E  
  
```  
  
 Effettuare la connessione utilizzando le credenziali di Windows, la comunicazione crittografata e un certificato server attendibile:  
  
```  
SQLCMD -E -N  
  
```  
  
 Effettuare la connessione utilizzando le credenziali di Windows, la comunicazione crittografata e un certificato server attendibile:  
  
```  
SQLCMD -E -T  
  
```  
  
 Effettuare la connessione utilizzando le credenziali di Windows, la comunicazione crittografata e un certificato server attendibile:  
  
```  
SQLCMD -E -N -C  
  
```  
  
 Se il provider specifica `ForceProtocolEncryption = True` la crittografia è abilitata anche se nella stringa di connessione è impostato `Encrypt=No`.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità sqlcmd](../../tools/sqlcmd-utility.md)   
 [Utilizzo di sqlcmd con variabili di scripting](sqlcmd-use-with-scripting-variables.md)   
 [Modifica di script SQLCMD con l'editor di query](edit-sqlcmd-scripts-with-query-editor.md)   
 [Gestire passaggi di processo](../../ssms/agent/manage-job-steps.md)   
 [Creare un passaggio di processo CmdExec](../../ssms/agent/create-a-cmdexec-job-step.md)  
  
  
