---
title: Installare nuovi pacchetti R
description: Informazioni su come usare sqlmlutils per installare nuovi pacchetti R in un'istanza di Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/04/2020
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 4e467fb50ae2b2c76deea885990b160745c691eb
ms.sourcegitcommit: 9be0047805ff14e26710cfbc6e10d6d6809e8b2c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042521"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>Installare nuovi pacchetti R con sqlmlutils

[!INCLUDE [SQL Server 2019 SQL MI](../../includes/applies-to-version/sqlserver2019-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Questo articolo descrive come usare le funzioni del pacchetto [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) per installare nuovi pacchetti R in un'istanza di [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md) e in [cluster Big Data](../../big-data-cluster/machine-learning-services.md). I pacchetti installati possono essere usati negli script R in esecuzione nel database usando l'istruzione T-SQL [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

> [!NOTE]
> Il pacchetto **sqlmlutils** descritto in questo articolo viene usato per aggiungere pacchetti R a SQL Server 2019 o versione successiva. Per SQL Server 2017 e versioni precedenti, vedere [Installare i pacchetti con gli strumenti R](https://docs.microsoft.com/sql/machine-learning/package-management/install-r-packages-standard-tools?view=sql-server-2017).
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Questo articolo descrive come usare le funzioni del pacchetto [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) per installare nuovi pacchetti R in un'istanza di [Machine Learning Services per Istanza gestita di SQL di Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview). I pacchetti installati possono essere usati negli script R in esecuzione nel database usando l'istruzione T-SQL [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).
::: moniker-end

## <a name="prerequisites"></a>Prerequisiti

- Installare [R](https://www.r-project.org) e [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) nel computer client usato per connettersi a SQL Server. È possibile usare qualsiasi IDE di R per l'esecuzione di script, ma in questo articolo si presuppone che venga usato RStudio.

- Installare [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) nel computer client usato per connettersi a SQL Server. È possibile usare altri strumenti di query o gestione di database, ma in questo articolo si presuppone che venga usato Azure Data Studio.

### <a name="other-considerations"></a>Altre considerazioni

- L'installazione del pacchetto è specifica dell'istanza di SQL, del database e dell'utente indicati nelle informazioni di connessione specificate per **sqlmlutils**. Per usare il pacchetto in più istanze o database SQL oppure per utenti diversi, è necessario installare il pacchetto per ognuno di essi. L'eccezione è che se il pacchetto viene installato da un membro di `dbo`, il pacchetto è *pubblico* ed è condiviso con tutti gli utenti. Se un utente installa una versione più recente di un pacchetto pubblico, tale pacchetto non sarà interessato, ma l'utente avrà accesso alla versione più recente.

- Lo script R eseguito in SQL Server può usare solo i pacchetti installati nella libreria dell'istanza predefinita. SQL Server non è in grado di caricare pacchetti da librerie esterne, anche se si trovano nello stesso computer, incluse le librerie R installate con altri prodotti Microsoft.

- In un ambiente di SQL Server con protezione avanzata, è consigliabile evitare i tipi di pacchetti seguenti:
  - Pacchetti che richiedono l'accesso alla rete
  - Pacchetti che richiedono l'accesso al file system con privilegi elevati
  - Pacchetti usati per lo sviluppo Web o altre attività che non traggono vantaggio dall'esecuzione all'interno di SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Installare sqlmlutils nel computer client

Prima di usare **sqlmlutils**, è necessario installarlo nel computer client usato per connettersi a SQL Server.

Il pacchetto **sqlmlutils** dipende dal pacchetto **RODBCext** e **RODBCext** dipende da una serie di altri pacchetti. Le procedure seguenti installano tutti questi pacchetti nell'ordine corretto.

### <a name="install-sqlmlutils-online"></a>Installare sqlmlutils online

Se il computer client dispone di accesso a Internet, è possibile scaricare e installare **sqlmlutils** e i relativi pacchetti dipendenti online.

1. Scaricare la versione più recente del file **sqlmlutils** (`.zip` per Windows, `.tar.gz` per Linux) da https://github.com/Microsoft/sqlmlutils/tree/master/R/dist al computer client. Non espandere il file.

1. Aprire un **prompt dei comandi** ed eseguire i comandi seguenti per installare i pacchetti **RODBCext** e **sqlmlutils**. Sostituire il percorso del file **sqlmlutils** scaricato. Il pacchetto **RODBCext** viene trovato online e installato.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='https://mran.microsoft.com/snapshot/2019-02-01/')"
   R CMD INSTALL sqlmlutils_0.7.1.zip
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='https://mran.microsoft.com/snapshot/2019-02-01/')"
   R CMD INSTALL sqlmlutils_0.7.1.tar.gz
   ```
   ::: moniker-end

### <a name="install-sqlmlutils-offline"></a>Installare sqlmlutils offline

Se il computer client non dispone di una connessione Internet, è necessario scaricare i pacchetti **RODBCext** e **sqlmlutils** in anticipo usando un computer con accesso a Internet. È quindi possibile copiare i file in una cartella del computer client e installare i pacchetti offline.

Il pacchetto **RODBCext** dispone di una serie di pacchetti dipendenti e quindi l'identificazione di tutte le dipendenze per un pacchetto diventa complicata. È consigliabile usare [**miniCRAN**](https://andrie.github.io/miniCRAN/) in modo da creare per il pacchetto una cartella di repository locale che includa tutti i pacchetti dipendenti.
Per altre informazioni, vedere [Creare un repository di pacchetti R locale usando miniCRAN](create-a-local-package-repository-using-minicran.md).

Il pacchetto **sqlmlutils** è costituito da un singolo file che è possibile copiare nel computer client e installare.

In un computer con accesso a Internet:

1. Installare **miniCRAN**. Per informazioni dettagliate, vedere [Installare miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran).

1. In RStudio eseguire lo script R seguente per creare un repository locale del pacchetto **RODBCext**. In questo esempio si presuppone che il repository venga creato nella cartella `rodbcext`.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2019-02-01/")
   local_repo <- "rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2019-02-01/")
   local_repo <- "rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```
   ::: moniker-end

   Per il valore di `Rversion`, usare la versione di R installata in SQL Server. Per verificare la versione installata, usare il comando T-SQL seguente.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Scaricare la versione più recente del file **sqlmlutils** (`.zip` per Windows, `.tar.gz` per Linux) da [https://github.com/Microsoft/sqlmlutils/tree/master/R/dist](https://github.com/Microsoft/sqlmlutils/tree/master/R/dist). Non espandere il file.

1. Copiare l'intera cartella del repository di **RODBCext** e il file **sqlmlutils** nel computer client.

Nel computer client usato per connettersi a SQL Server:

1. Aprire un prompt dei comandi.

1. Eseguire i comandi seguenti per installare **RODBCext** e quindi **sqlmlutils**. Sostituire i percorsi completi della cartella del repository **RODBCext** e del file **sqlmlutils** copiati nel computer.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='rodbcext')"
   R CMD INSTALL sqlmlutils_0.7.1.zip
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```console
   R -e "install.packages('RODBCext', repos='rodbcext')"
   R CMD INSTALL sqlmlutils_0.7.1.tar.gz
   ```
   ::: moniker-end

## <a name="add-an-r-package-on-sql-server"></a>Aggiungere un pacchetto R in SQL Server

Nell'esempio seguente si aggiungerà il pacchetto [**glue**](https://cran.r-project.org/web/packages/glue/) in SQL Server.

### <a name="add-the-package-online"></a>Aggiungere il pacchetto online

Se il computer client usato per connettersi a SQL Server dispone di accesso a Internet, è possibile usare **sqlmlutils** per trovare il pacchetto **glue** e le eventuali dipendenze su Internet, quindi installare il pacchetto in un'istanza di SQL Server in modalità remota.

1. Nel computer client aprire RStudio e creare un nuovo file di **script R**.

1. Usare lo script R seguente per installare il pacchetto **glue** usando **sqlmlutils**. Sostituire le informazioni di connessione del database di SQL Server personalizzate.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server   = "server",
     database = "database",
     uid      = "username",
     pwd      = "password")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > L'ambito (**scope**) può essere **PUBLIC** o **PRIVATE**. L'ambito pubblico è utile all'amministratore del database per installare i pacchetti che possono essere usati da tutti gli utenti. L'ambito privato consente di limitare la disponibilità del pacchetto all'utente che lo ha installato. Se non si specifica l'ambito, il valore predefinito è **PRIVATE**.

### <a name="add-the-package-offline"></a>Aggiungere il pacchetto offline

Se il computer client non dispone di una connessione Internet, è possibile usare **miniCRAN** per scaricare il pacchetto **glue** usando un computer con accesso a Internet. Copiare quindi il pacchetto nel computer client in cui è possibile installare il pacchetto offline.
Per informazioni sull'installazione di **miniCRAN**, vedere [Installare miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran).

In un computer con accesso a Internet:

1. Eseguire lo script R seguente per creare un repository locale per **glue**. Questo esempio crea la cartella del repository in `c:\downloads\glue`.

   ::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```
   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```
   ::: moniker-end

   Per il valore di `Rversion`, usare la versione di R installata in SQL Server. Per verificare la versione installata, usare il comando T-SQL seguente.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Copiare l'intera cartella del repository di **glue** (`c:\downloads\glue`) nel computer client. Ad esempio, copiarla nella cartella `c:\temp\packages\glue`.

Nel computer client:

1. Aprire RStudio e creare un nuovo file di **script R**.

1. Usare lo script R seguente per installare il pacchetto **glue** usando **sqlmlutils**. Usare le proprie informazioni di connessione al database di SQL Server. Se non si usa l'autenticazione di Windows, aggiungere i parametri `uid` e `pwd`.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > L'ambito (**scope**) può essere **PUBLIC** o **PRIVATE**. L'ambito pubblico è utile all'amministratore del database per installare i pacchetti che possono essere usati da tutti gli utenti. L'ambito privato consente di limitare la disponibilità del pacchetto all'utente che lo ha installato. Se non si specifica l'ambito, il valore predefinito è **PRIVATE**.

## <a name="use-the-package"></a>Usare il pacchetto

Dopo aver installato il pacchetto **glue**, è possibile usarlo in uno script R in SQL Server con il comando T-SQL **sp_execute_external_script**.

1. Aprire Azure Data Studio e connettersi al database di SQL Server.

1. Eseguire il comando seguente:

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
       , @script = N'
   library(glue)

   name <- "Fred"
   birthday <- as.Date("2020-06-14")
   text <- glue(''My name is {name} '',
   ''and my birthday is {format(birthday, "%A, %B %d, %Y")}.'')

   print(text)
         ';
   ```

    **Risultati**

    ```text
    My name is Fred and my birthday is Sunday, June 14, 2020.
    ```

## <a name="remove-the-package"></a>Rimuovere il pacchetto

Se si vuole rimuovere il pacchetto **glue**, eseguire lo script R seguente. Usare la stessa variabile **connection** definita in precedenza.

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni sui pacchetti R installati, vedere [Ottenere informazioni sui pacchetti R](r-package-information.md)
- Per informazioni sull'uso di pacchetti R, vedere [Suggerimenti per l'uso di pacchetti R](tips-for-using-r-packages.md)
- Per informazioni sull'installazione dei pacchetti Python, vedere [Installare pacchetti Python con pip](install-additional-python-packages-on-sql-server.md)
- Per altre informazioni su Machine Learning Services per SQL Server, vedere [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../sql-server-machine-learning-services.md)
