---
title: Installare nuovi pacchetti R con sqlmlutils
description: Informazioni su come usare sqlmlutils per installare nuovi pacchetti R in un'istanza di SQL Server Machine Learning Services o R Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 579f4c4e236fcc9ee22067522c47a8286b869d51
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000782"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>Installare nuovi pacchetti R con sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come usare le funzioni nel pacchetto [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) per installare nuovi pacchetti R in un'istanza di SQL Server Machine Learning Services o R Services per SQL Server. I pacchetti installati possono essere usati negli script R eseguiti nel database usando l'istruzione T-SQL [SP-Execute-External-script-Transact-SQL](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) .

> [!NOTE]
> Il comando r `install.packages` standard non è consigliato per l'aggiunta di pacchetti R in SQL Server. Usare invece **sqlmlutils** come descritto in questo articolo.

## <a name="prerequisites"></a>Prerequisiti

- Installare [R](https://www.r-project.org) e [rstudio desktop](https://www.rstudio.com/products/rstudio/download/) nel computer client usato per connettersi a SQL Server. È possibile usare qualsiasi IDE R per l'esecuzione di script, ma in questo articolo si presuppone RStudio.

- Installare [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) nel computer client usato per connettersi al SQL Server. È possibile usare altri strumenti di gestione o query di database, ma in questo articolo si presuppone Azure Data Studio o SSMS.

### <a name="other-considerations"></a>Altre considerazioni

- Lo script R in esecuzione in SQL Server può utilizzare solo i pacchetti installati nella libreria di istanze predefinita. SQL Server non è in grado di caricare pacchetti da librerie esterne, anche se tale libreria si trova nello stesso computer. Sono incluse le librerie R installate con altri prodotti Microsoft.

- In un ambiente di SQL Server con protezione avanzata, è consigliabile evitare quanto segue:
  - Pacchetti per i quali è richiesto l'accesso alla rete
  - Pacchetti per i quali è richiesto l'accesso file system elevato
  - Pacchetti usati per lo sviluppo Web o altre attività che non traggono vantaggio dall'esecuzione all'interno SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Installare sqlmlutils nel computer client

Per usare **sqlmlutils**, è prima di tutto necessario installarlo nel computer client usato per connettersi a SQL Server.

Il pacchetto **sqlmlutils** dipende dal pacchetto **RODBCext** e **RODBCext** dipende da una serie di altri pacchetti. Le procedure seguenti installano tutti questi pacchetti nell'ordine corretto.

### <a name="install-sqlmlutils-online"></a>Installare sqlmlutils online

Se il computer client dispone di accesso a Internet, è possibile scaricare e installare **sqlmlutils** e i pacchetti dipendenti in linea.

1. Scaricare il file zip di **sqlmlutils** più https://github.com/Microsoft/sqlmlutils/tree/master/R/dist recente da al computer client. Non decomprimere il file.

1. Aprire un **prompt** dei comandi ed eseguire i comandi seguenti per installare i pacchetti **sqlmlutils** e **RODBCext**. Sostituire il percorso completo del file zip **sqlmlutils** scaricato. in questo esempio si presuppone che il file si trovi nella cartella documenti. Il pacchetto **RODBCext** è disponibile online e installato.

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>Installare sqlmlutils offline

Se il computer client non dispone di una connessione Internet, è necessario scaricare i pacchetti **sqlmlutils** e **RODBCext** in anticipo utilizzando un computer che dispone di accesso a Internet. È quindi possibile copiare i file in una cartella nel computer client e installare i pacchetti offline.

Il pacchetto **RODBCext** include una serie di pacchetti dipendenti e l'identificazione di tutte le dipendenze per un pacchetto diventa complicata. Si consiglia di utilizzare [**miniCRAN**](https://andrie.github.io/miniCRAN/) per creare una cartella del repository locale per il pacchetto che include tutti i pacchetti dipendenti.
Per altre informazioni, vedere [creare un repository di pacchetti R locale usando miniCRAN](../r/create-a-local-package-repository-using-minicran.md).

Il pacchetto **sqlmlutils** è costituito da un singolo file zip che è possibile copiare nel computer client e installare.

In un computer con accesso a Internet:

1. Installare **miniCRAN**. Per informazioni dettagliate, vedere [Install miniCRAN](../r/create-a-local-package-repository-using-minicran.md#install-minicran) .

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

   Per il `Rversion` valore, usare la versione di R installata in SQL Server. Per verificare la versione installata, usare il comando T-SQL seguente.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Scaricare la versione più recente del file https://github.com/Microsoft/sqlmlutils/tree/master/R/dist zip di sqlmlutils da (non decomprimere il file). Ad esempio, scaricare il file in `c:\downloads\sqlmlutils_0.7.1.zip`.

1. Copiare l'intera cartella del repository RODBCext`c:\downloads\rodbcext`() e il file zip di`c:\downloads\sqlmlutils_0.7.1.zip`sqlmlutils () nel computer client. Ad esempio, copiarli nella cartella `c:\temp\packages` nel computer client.

Nel computer client usato per connettersi a SQL Server, aprire un prompt dei comandi ed eseguire i comandi seguenti per installare **RODBCext** e quindi **sqlmlutils**.

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>Aggiungere un pacchetto R in SQL Server

Nell'esempio seguente si aggiungerà il pacchetto [**Glue**](https://cran.r-project.org/web/packages/glue/) a SQL Server.

### <a name="add-the-package-online"></a>Aggiungere il pacchetto online

Se il computer client usato per connettersi a SQL Server dispone di accesso a Internet, è possibile usare **sqlmlutils** per trovare il pacchetto **Glue** e tutte le dipendenze su Internet, quindi installare il pacchetto in un'istanza di SQL Server in modalità remota.

1. Nel computer client aprire RStudio e creare un nuovo file di **script R** .

1. Usare il seguente script R per installare il pacchetto **Glue** usando **sqlmlutils**. Sostituire le informazioni di connessione del database SQL Server.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase",
     uid = "yoursqluser",
     pwd = "yoursqlpassword")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > L' **ambito** può essere **pubblico** o **privato**. L'ambito pubblico è utile all'amministratore del database per installare i pacchetti che tutti gli utenti possono usare. Ambito privato rende disponibile il pacchetto solo per l'utente che lo installa. Se non si specifica l'ambito, l'ambito predefinito è **privato**.

### <a name="add-the-package-offline"></a>Aggiungere il pacchetto offline

Se il computer client non dispone di una connessione Internet, è possibile usare **miniCRAN** per scaricare il pacchetto **Glue** usando un computer che dispone di accesso a Internet. Il pacchetto viene quindi copiato nel computer client in cui è possibile installare il pacchetto offline.
Vedere [Install miniCRAN](../r/create-a-local-package-repository-using-minicran.md#install-minicran) per informazioni sull'installazione di **miniCRAN**.

In un computer con accesso a Internet:

1. Eseguire lo script R seguente per creare un repository locale per l' **associazione**. Questo esempio crea la cartella del repository `c:\downloads\glue`in.

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


   Per il `Rversion` valore, usare la versione di R installata in SQL Server. Per verificare la versione installata, usare il comando T-SQL seguente.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Copiare l'intera cartella del repository di`c:\downloads\glue`Glue () nel computer client. Ad esempio, copiarlo nella cartella `c:\temp\packages\glue`.

Sul computer client:

1. Aprire RStudio e creare un nuovo file di **script R** .

1. Usare il seguente script R per installare il pacchetto **Glue** usando **sqlmlutils**. Sostituire le informazioni di connessione del database SQL Server.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase",
     uid = "yoursqluser",
     pwd = "yoursqlpassword")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > L' **ambito** può essere **pubblico** o **privato**. L'ambito pubblico è utile all'amministratore del database per installare i pacchetti che tutti gli utenti possono usare. Ambito privato rende disponibile il pacchetto solo per l'utente che lo installa. Se non si specifica l'ambito, l'ambito predefinito è **privato**.

## <a name="use-the-package"></a>Usare il pacchetto

Una volta installato il pacchetto **Glue** , è possibile usarlo in uno script R SQL Server con il comando T-SQL **sp_execute_external_script** .

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

Se si vuole rimuovere il pacchetto **Glue** , eseguire il seguente script R. Usare la stessa variabile di **connessione** definita in precedenza.

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni sui pacchetti R installati, vedere [ottenere informazioni sui pacchetti r](r-package-information.md)
- Per informazioni sull'uso dei pacchetti R, vedere [Suggerimenti per l'uso di pacchetti r](../r/packages-installed-in-user-libraries.md)
- Per informazioni sull'installazione dei pacchetti Python, vedere [Install Python Packages with PIP](install-additional-python-packages-on-sql-server.md)
- Per ulteriori informazioni su SQL Server Machine Learning Services, vedere [che cos'è SQL Server Machine Learning Services (Python e R)?](../what-is-sql-server-machine-learning.md)
