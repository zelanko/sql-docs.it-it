---
title: Come usare funzioni RevoScaleR per trovare o installare pacchetti R - servizi di SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0d5ba43e913f91ab93f80249cae3d0c8cf8e1740
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140404"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>Come usare funzioni RevoScaleR per trovare o installare pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 9.0.1 e versioni successive includono funzioni per la gestione dei pacchetti R un contesto di calcolo di SQL Server. Queste funzioni sono utilizzabile da remoti, a utenti non amministratori per installare i pacchetti in SQL Server senza accesso diretto al server.

Machine Learning Services di SQL Server 2017 include già una versione più recente di RevoScaleR. I clienti di SQL Server 2016 R Services è necessario eseguire un' [aggiornamento del componente](../install/upgrade-r-and-python.md) per ottenere funzioni di gestione dei pacchetti RevoScaleR. Per istruzioni su come recuperare pacchetto versione e il contenuto, vedere [ottenere informazioni sul pacchetto](../package-management/installed-package-information.md).

## <a name="revoscaler-functions-for-package-management"></a>Funzioni RevoScaleR per la gestione pacchetti

La tabella seguente descrive le funzioni utilizzate per la gestione e installazione di pacchetti R.

| Funzione | Descrizione |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | Determinare il percorso della libreria di istanza nel Server SQL remoto. |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | Ottiene il percorso di uno o più pacchetti nel Server SQL remoto. |
| [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | Chiamare questa funzione da un client remoto di R per installare i pacchetti in un contesto di calcolo di SQL Server, da un repository specificato o leggendo salvati in locale i pacchetti compressi. Questa funzione controlla le dipendenze e verifica che tutti i pacchetti correlati possono essere installati in SQL Server, come installazione di pacchetti R nel contesto di calcolo locale. Per usare questa opzione, è necessario aver abilitato gestione dei pacchetti nel server e nel database. Gli ambienti client e server devono avere la stessa versione di RevoScaleR. |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | Ottiene un elenco dei pacchetti installati nel contesto di calcolo specificato. |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | Copiare le informazioni su una libreria di pacchetti tra il file system e un database, per il contesto di calcolo specificato. |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | Rimuove i pacchetti da un contesto di calcolo specificato. Inoltre, calcola le dipendenze e assicura che i pacchetti che non vengono più utilizzati da altri pacchetti in SQL Server vengano rimossi, per liberare risorse. |

## <a name="prerequisites"></a>Prerequisiti

+ [Abilitare gestione remota dei pacchetti R in SQL Server](r-package-how-to-enable-or-disable.md)

+ Versioni di RevoScaleR devono essere gli stessi in ambienti client e server. Per altre informazioni, vedere [ottenere informazioni sul pacchetto](../package-management/installed-package-information.md).

+ Autorizzazione per connettersi al server e un database e per eseguire comandi R. È necessario essere un membro di un ruolo del database che consente di installare i pacchetti per l'istanza specificata e un database.

+ I pacchetti **ambito condiviso** possono essere installate dagli utenti che appartengono al `rpkgs-shared` ruolo in un database specificato. Tutti gli utenti in questo ruolo è possono disinstallare pacchetti condivisi.

+ I pacchetti **ambito privato** può essere installato da qualsiasi utente che appartengono al `rpkgs-private` ruolo in un database. Tuttavia, gli utenti possono vedere e disinstallare solo i propri pacchetti.

+ I proprietari del database possono utilizzare i pacchetti privati o condivisi.

## <a name="client-connections"></a>Connessioni client

Una workstation client può essere [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows) o una [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (data Scientist usano spesso l'edizione developer gratuita) nella stessa rete.

Quando si chiamano funzioni di gestione del pacchetto da un client remoto di R, è necessario creare un oggetto di contesto di calcolo in primo luogo, usando il [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) (funzione). Successivamente, per ogni funzione a Gestione pacchetti in uso, passare il contesto di calcolo come argomento.

Identità dell'utente è in genere specificato durante l'impostazione del contesto di calcolo. Se non si specifica un nome utente e una password quando si crea il contesto di calcolo, viene usata l'identità dell'utente che esegue il codice R.

1. Dalla riga di comando R, definire una stringa di connessione all'istanza e al database.
2. Usare la [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) costruttore per definire un contesto di calcolo di SQL Server, usando la stringa di connessione.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. Creare un elenco dei pacchetti che si desidera installare e salvare l'elenco in una variabile di stringa.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. Chiamare [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) e passare il contesto di calcolo e la variabile di stringa che contiene i nomi dei pacchetti.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Se sono necessari i pacchetti dipendenti, sono anche installati, supponendo che una connessione internet sia disponibile nel client.
    
    I pacchetti vengono installati utilizzando le credenziali dell'utente che effettua la connessione, nell'ambito predefinito per tale utente.

## <a name="call-package-management-functions-in-stored-procedures"></a>Chiamare le funzioni di gestione di pacchetti nelle stored procedure

Si può eseguire funzioni di gestione pacchetti all'interno di `sp_execute_external_script`. Quando si esegue questa operazione, la funzione viene eseguita utilizzando il contesto di sicurezza del chiamante stored procedure.

## <a name="examples"></a>Esempi

In questa sezione vengono forniti esempi di come usare queste funzioni da un client remoto quando ci si connette a un'istanza di SQL Server o al database come contesto di calcolo.

Per tutti gli esempi, è necessario fornire una stringa di connessione o un contesto di calcolo, che richiede una stringa di connessione. In questo esempio viene illustrato un modo per creare un contesto di calcolo di SQL Server:

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

A seconda di dove si trova il server e il modello di sicurezza, è necessario fornire un dominio e una subnet specifica nella stringa di connessione oppure usare un account di accesso SQL. Ad esempio:

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Ottenere il percorso del pacchetto in un contesto di calcolo di SQL Server remoto

Questo esempio mostra come ottenere il percorso per il **RevoScaleR** pacchetto nel contesto di calcolo, `sqlcc`.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**Risultati**

"C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> Se è stata abilitata l'opzione visualizzare l'output della console SQL, è possibile ottenere i messaggi di stato dalla funzione che precede il `print` istruzione. Dopo aver completato il test del codice, impostare `consoleOutput` su FALSE nel costruttore di contesto di calcolo per eliminare i messaggi.

### <a name="get-locations-for-multiple-packages"></a>Ottenere i percorsi per più pacchetti

L'esempio seguente ottiene i percorsi per i **RevoScaleR** e **reticolo** pacchetti, nel contesto di calcolo, `sqlcc`. Per ottenere informazioni sui pacchetti di più, passare un vettore di stringhe contenente i nomi dei pacchetti.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>Ottenere le versioni dei pacchetti in un contesto di calcolo remoto

Eseguire questo comando da una console di R per ottenere il numero di build e i numeri di versione per i pacchetti installati nel contesto di calcolo, *sqlServer*.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**Risultati**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>Installare un pacchetto in SQL Server

Questo esempio si installa il **previsione** pacchetto e le relative dipendenze nel contesto di calcolo.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>Rimuovere un pacchetto da SQL Server

Questo esempio vengono rimossi i **previsione** pacchetto e le relative dipendenze dal contesto di calcolo.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>Sincronizzare i pacchetti tra database e file system

L'esempio seguente controlla il database **TestDB**e determina se tutti i pacchetti vengono installati nel file system. Se alcuni pacchetti non sono presenti, vengono installate nel file system.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

Sincronizzazione del pacchetto funziona su una base dei singoli database e per ogni utente. Per altre informazioni, vedere [sincronizzazione tramite il pacchetto R per SQL Server](../r/package-install-uninstall-and-sync.md).

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>Usare una stored procedure per elencare i pacchetti in SQL Server

Eseguire questo comando da Management Studio o un altro strumento che supporta T-SQL, per ottenere un elenco dei pacchetti installati nell'istanza corrente, usando `rxInstalledPackages` in una stored procedure.

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

Il `rxSqlLibPaths` funzione può essere utilizzata per determinare la libreria active usata da SQL Server Machine Learning Services. Questo script può restituire solo il percorso di libreria per il server corrente. 

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