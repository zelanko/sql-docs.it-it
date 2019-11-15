---
title: Installare nuovi pacchetti R
description: Informazioni su come usare sqlmlutils per installare nuovi pacchetti R in un'istanza di Machine Learning Services per SQL Server o R Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 827e83a0d1b363d3b91477b9ae85fec156ee4fc9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727493"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>Installare nuovi pacchetti R con sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come usare le funzioni incluse in [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) per installare nuovi pacchetti R in un'istanza di Machine Learning Services per SQL Server o R Services per SQL Server. I pacchetti installati possono essere usati negli script R in esecuzione nel database usando l'istruzione T-SQL [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

> [!NOTE]
> Per aggiungere pacchetti R in SQL Server non è consigliabile usare il comando `install.packages` standard di R. In alternativa, usare **sqlmlutils**, come descritto in questo articolo.

## <a name="prerequisites"></a>Prerequisites

- Installare [R](https://www.r-project.org) e [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) nel computer client usato per connettersi a SQL Server. È possibile usare qualsiasi IDE di R per l'esecuzione di script, ma in questo articolo si presuppone che venga usato RStudio.

- Installare [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) nel computer client usato per connettersi a SQL Server. È possibile usare altri strumenti di query o gestione di database, ma in questo articolo si presuppone che venga usato Azure Data Studio o SSMS.

### <a name="other-considerations"></a>Altre considerazioni

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

1. Scaricare la versione più recente del file ZIP di **sqlmlutils** da https://github.com/Microsoft/sqlmlutils/tree/master/R/dist nel computer client. Non decomprimere il file.

1. Aprire un **prompt dei comandi** ed eseguire i comandi seguenti per installare i pacchetti **sqlmlutils** e **RODBCext**. Sostituire il percorso completo del file ZIP di **sqlmlutils** scaricato. In questo esempio si presuppone che il file si trovi nella cartella Documents. Il pacchetto **RODBCext** viene trovato online e installato.

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>Installare sqlmlutils offline

Se il computer client non dispone di una connessione Internet, è necessario scaricare i pacchetti **sqlmlutils** e **RODBCext** in anticipo usando un computer con accesso a Internet. È quindi possibile copiare i file in una cartella del computer client e installare i pacchetti offline.

Il pacchetto **RODBCext** dispone di una serie di pacchetti dipendenti e quindi l'identificazione di tutte le dipendenze per un pacchetto diventa complicata. È consigliabile usare [**miniCRAN**](https://andrie.github.io/miniCRAN/) in modo da creare per il pacchetto una cartella di repository locale che includa tutti i pacchetti dipendenti.
Per altre informazioni, vedere [Creare un repository di pacchetti R locale usando miniCRAN](create-a-local-package-repository-using-minicran.md).

Il pacchetto **sqlmlutils** è costituito da un singolo file ZIP che è possibile copiare nel computer client e installare.

In un computer con accesso a Internet:

1. Installare **miniCRAN**. Per informazioni dettagliate, vedere [Installare miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran).

1. In RStudio eseguire lo script R seguente per creare un repository locale del pacchetto **RODBCext**. Questo esempio crea il repository nella cartella `c:\downloads\rodbcext`.

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
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

1. Scaricare la versione più recente del file ZIP di **sqlmlutils** da https://github.com/Microsoft/sqlmlutils/tree/master/R/dist. Non decomprimere il file ZIP. Ad esempio, scaricare il file in `c:\downloads\sqlmlutils_0.7.1.zip`.

1. Copiare l'intera cartella del repository di **RODBCext** (`c:\downloads\rodbcext`) e il file ZIP di **sqlmlutils** (`c:\downloads\sqlmlutils_0.7.1.zip`) nel computer client. Ad esempio, copiarli nella cartella `c:\temp\packages` del computer client.

Nel computer client usato per connettersi a SQL Server, aprire un prompt dei comandi ed eseguire i comandi seguenti per installare **RODBCext** e quindi **sqlmlutils**.

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>Aggiungere un pacchetto R in SQL Server

Nell'esempio seguente si aggiungerà il pacchetto [**glue**](https://cran.r-project.org/web/packages/glue/) in SQL Server.

### <a name="add-the-package-online"></a>Aggiungere il pacchetto online

Se il computer client usato per connettersi a SQL Server dispone di accesso a Internet, è possibile usare **sqlmlutils** per trovare il pacchetto **glue** e le eventuali dipendenze su Internet, quindi installare il pacchetto in un'istanza di SQL Server in modalità remota.

1. Nel computer client aprire RStudio e creare un nuovo file di **script R**.

1. Usare lo script R seguente per installare il pacchetto **glue** usando **sqlmlutils**. Usare le proprie informazioni di connessione al database di SQL Server. Se non si usa l'autenticazione di Windows, aggiungere i parametri `uid` e `pwd`.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > Il valore di **scope** per la definizione dell'ambito può essere **PUBLIC** o **PRIVATE**. L'ambito pubblico è utile all'amministratore del database per installare i pacchetti che possono essere usati da tutti gli utenti. L'ambito privato consente di limitare la disponibilità del pacchetto all'utente che lo ha installato. Se non si specifica l'ambito, il valore predefinito è **PRIVATE**.

### <a name="add-the-package-offline"></a>Aggiungere il pacchetto offline

Se il computer client non dispone di una connessione Internet, è possibile usare **miniCRAN** per scaricare il pacchetto **glue** usando un computer con accesso a Internet. Copiare quindi il pacchetto nel computer client in cui è possibile installare il pacchetto offline.
Per informazioni sull'installazione di **miniCRAN**, vedere [Installare miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran).

In un computer con accesso a Internet:

1. Eseguire lo script R seguente per creare un repository locale per **glue**. Questo esempio crea la cartella del repository in `c:\downloads\glue`.

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

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
   > Il valore di **scope** per la definizione dell'ambito può essere **PUBLIC** o **PRIVATE**. L'ambito pubblico è utile all'amministratore del database per installare i pacchetti che possono essere usati da tutti gli utenti. L'ambito privato consente di limitare la disponibilità del pacchetto all'utente che lo ha installato. Se non si specifica l'ambito, il valore predefinito è **PRIVATE**.

## <a name="use-the-package"></a>Usare il pacchetto

Dopo aver installato il pacchetto **glue**, è possibile usarlo in uno script R in SQL Server con il comando T-SQL **sp_execute_external_script**.

1. Aprire Azure Data Studio o SSMS e connettersi al database di SQL Server.

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
- Per altre informazioni su Machine Learning Services per SQL Server, vedere [Che cos'è Machine Learning Services per SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
