---
title: Come usare le funzioni RevoScaleR per trovare o installare pacchetti R
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: dafbe12c6304866dc36dde6fffec44da441e582f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344830"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>Come usare le funzioni RevoScaleR per trovare o installare pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 9.0.1 e versioni successive includono funzioni per la gestione dei pacchetti R a SQL Server contesto di calcolo. Queste funzioni possono essere utilizzate da computer non amministratori remoti per installare i pacchetti in SQL Server senza accesso diretto al server.

SQL Server 2017 Machine Learning Services include già una versione più recente di RevoScaleR. SQL Server 2016 R Services i clienti devono eseguire un [aggiornamento del componente](../install/upgrade-r-and-python.md) per ottenere le funzioni di gestione dei pacchetti RevoScaleR. Per istruzioni su come recuperare la versione e il contenuto del pacchetto, vedere [ottenere informazioni sul pacchetto](../package-management/installed-package-information.md).

## <a name="revoscaler-functions-for-package-management"></a>Funzioni RevoScaleR per la gestione dei pacchetti

La tabella seguente descrive le funzioni usate per l'installazione e la gestione dei pacchetti R.

| Funzione | Descrizione |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | Determinare il percorso della libreria di istanze nel SQL Server remoto. |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | Ottiene il percorso per uno o più pacchetti nella SQL Server remota. |
| [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | Chiamare questa funzione da un client R remoto per installare i pacchetti in un SQL Server contesto di calcolo, da un repository specificato o leggendo i pacchetti compressi memorizzati localmente. Questa funzione controlla la presenza di dipendenze e garantisce che tutti i pacchetti correlati possano essere installati SQL Server, proprio come l'installazione di pacchetti R nel contesto di calcolo locale. Per utilizzare questa opzione, è necessario abilitare la gestione dei pacchetti nel server e nel database. Gli ambienti client e server devono avere la stessa versione di RevoScaleR. |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | Ottiene un elenco di pacchetti installati nel contesto di calcolo specificato. |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | Copia le informazioni relative a una libreria di pacchetti tra il file system e il database, per il contesto di calcolo specificato. |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | Rimuove i pacchetti da un contesto di calcolo specificato. Calcola inoltre le dipendenze e garantisce che i pacchetti che non vengono più usati da altri pacchetti in SQL Server vengano rimossi per liberare risorse. |

## <a name="prerequisites"></a>Prerequisiti

+ [Abilitare la gestione dei pacchetti R remota in SQL Server](r-package-how-to-enable-or-disable.md)

+ Le versioni di RevoScaleR devono essere le stesse negli ambienti client e server. Per ulteriori informazioni, vedere [ottenere informazioni sul pacchetto](../package-management/installed-package-information.md).

+ Autorizzazione per la connessione al server e a un database e per l'esecuzione di comandi R. È necessario essere un membro di un ruolo del database che consente di installare i pacchetti nell'istanza e nel database specificati.

+ I`rpkgs-shared` pacchetti nell' **ambito condiviso** possono essere installati dagli utenti appartenenti al ruolo in un database specifico. Tutti gli utenti in questo ruolo possono disinstallare i pacchetti condivisi.

+ I pacchetti nell' **ambito privato** possono essere installati da qualsiasi utente appartenente `rpkgs-private` al ruolo in un database. Tuttavia, gli utenti possono visualizzare e disinstallare solo i propri pacchetti.

+ I proprietari del database possono utilizzare pacchetti condivisi o privati.

## <a name="client-connections"></a>Connessioni client

Una workstation client può essere [Microsoft R client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows) o una [Microsoft Machine Learning server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (i data scientist usano spesso la versione gratuita Developer Edition) nella stessa rete.

Quando si chiamano le funzioni di gestione dei pacchetti da un client R remoto, è necessario creare prima un oggetto contesto di calcolo usando la funzione [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) . Successivamente, per ogni funzione di gestione dei pacchetti utilizzata, passare il contesto di calcolo come argomento.

L'identità utente viene in genere specificata durante l'impostazione del contesto di calcolo. Se non si specifica un nome utente e una password quando si crea il contesto di calcolo, viene usata l'identità dell'utente che esegue il codice R.

1. Da una riga di comando di R, definire una stringa di connessione per l'istanza e il database.
2. Usare il costruttore [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) per definire un contesto di calcolo SQL Server, usando la stringa di connessione.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. Creare un elenco dei pacchetti che si desidera installare e salvare l'elenco in una variabile di stringa.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. Chiamare [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) e passare il contesto di calcolo e la variabile di stringa contenente i nomi dei pacchetti.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Se sono necessari pacchetti dipendenti, vengono installati anche se nel client è disponibile una connessione Internet.
    
    I pacchetti vengono installati usando le credenziali dell'utente che effettua la connessione, nell'ambito predefinito per tale utente.

## <a name="call-package-management-functions-in-stored-procedures"></a>Chiamare le funzioni di gestione dei pacchetti nelle stored procedure

È possibile eseguire le funzioni di gestione `sp_execute_external_script`dei pacchetti all'interno di. Quando si esegue questa operazione, la funzione viene eseguita utilizzando il contesto di sicurezza del chiamante del stored procedure.

## <a name="examples"></a>Esempi

In questa sezione vengono forniti esempi di utilizzo di queste funzioni da un client remoto per la connessione a un'istanza o a un database di SQL Server come contesto di calcolo.

Per tutti gli esempi, è necessario specificare una stringa di connessione o un contesto di calcolo, che richiede una stringa di connessione. Questo esempio fornisce un modo per creare un contesto di calcolo per SQL Server:

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

A seconda della posizione in cui si trova il server e del modello di sicurezza, potrebbe essere necessario fornire una specifica di dominio e subnet nella stringa di connessione oppure utilizzare un account di accesso SQL. Ad esempio:

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Ottenere il percorso del pacchetto in un contesto di calcolo di SQL Server remoto

Questo esempio Mostra come ottenere il percorso del pacchetto **RevoScaleR** nel contesto `sqlcc`di calcolo.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**Risultati**

"C:/Program Files/Microsoft SQL Server/MSSQL14. MSSQLSERVER/R_SERVICES/Library/RevoScaleR "

> [!TIP]
> Se è stata abilitata l'opzione per visualizzare l'output della console SQL, è possibile che vengano visualizzati messaggi di stato dalla `print` funzione che precede l'istruzione. Al termine del test del codice, impostare `consoleOutput` su false nel costruttore del contesto di calcolo per eliminare i messaggi.

### <a name="get-locations-for-multiple-packages"></a>Ottenere i percorsi per più pacchetti

Nell'esempio seguente vengono ottenuti i percorsi per i pacchetti **RevoScaleR** e **lattice** nel contesto `sqlcc`di calcolo. Per ottenere informazioni su più pacchetti, passare un vettore di stringa contenente i nomi dei pacchetti.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>Ottenere le versioni del pacchetto in un contesto di calcolo remoto

Eseguire questo comando da una console R per ottenere il numero di build e i numeri di versione per i pacchetti installati nel contesto di calcolo, *sqlServer*.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**Risultati**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>Installare un pacchetto in SQL Server

Questo esempio Mostra come installare il pacchetto di **previsione** e le relative dipendenze nel contesto di calcolo.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>Rimuovere un pacchetto da SQL Server

Questo esempio Mostra come rimuovere il pacchetto di **previsione** e le relative dipendenze dal contesto di calcolo.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>Sincronizzare i pacchetti tra database e file system

Nell'esempio seguente viene controllato il **TestDB**del database e viene determinato se tutti i pacchetti sono installati nel file System. Se alcuni pacchetti risultano mancanti, vengono installati nel file system.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

La sincronizzazione del pacchetto funziona in base al database e ai singoli utenti. Per ulteriori informazioni, vedere [sincronizzazione dei pacchetti R per SQL Server](../r/package-install-uninstall-and-sync.md).

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>Usare un stored procedure per elencare i pacchetti in SQL Server

Eseguire questo comando da Management Studio o da un altro strumento che supporta T-SQL per ottenere un elenco dei pacchetti installati nell'istanza corrente, usando `rxInstalledPackages` in un stored procedure.

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

La `rxSqlLibPaths` funzione può essere utilizzata per determinare la libreria attiva utilizzata da SQL Server Machine Learning Services. Questo script può restituire solo il percorso di libreria per il server corrente. 

```sql
declare @instance_name nvarchar(100) = @@SERVERNAME, @database_name nvarchar(128) = db_name();
exec sp_execute_external_script 
  @language = N'R',
  @script = N'
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    .libPaths(rxSqlLibPaths(connStr));
    print(.libPaths());
  ', 
  @input_data_1 = N'', 
  @params = N'@instance_name nvarchar(100), @database_name nvarchar(128)',
  @instance_name = @instance_name, 
  @database_name = @database_name;
```

## <a name="see-also"></a>Vedere anche

+ [Abilitare la gestione remota dei pacchetti R](r-package-how-to-enable-or-disable.md)
+ [Sincronizzare i pacchetti R](package-install-uninstall-and-sync.md)
+ [Suggerimenti per l'installazione di pacchetti R](packages-installed-in-user-libraries.md)
+ [Pacchetti predefiniti](../package-management/default-packages.md)