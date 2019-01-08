---
title: Ottenere informazioni sul pacchetto R e Python - servizi di SQL Server Machine Learning
description: Determinare la versione del pacchetto R e Python, è possibile verificarla e ottenere un elenco dei pacchetti installati in SQL Server R Services o servizi di Machine Learning.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 47badb15b5f5a2d0eabc63b8fd1be3e83a0caffb
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645370"
---
#  <a name="get-r-and-python-package-information"></a>Ottenere informazioni sul pacchetto R e Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In alcuni casi quando si lavora con più ambienti o le installazioni di R o Python, è necessario verificare che il codice che è in esecuzione stia utilizzando l'ambiente previsto per l'area di lavoro corretta o Python per R. Ad esempio, se è stato eseguito l'aggiornamento di machine learning tramite i componenti [associazione](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md), potrebbe essere il percorso della libreria R in una cartella diversa da quella predefinita. Inoltre, se si installa R Client o un'istanza del server autonoma, potrebbe essere più librerie R nel computer.

Esempi di script R e Python in questo articolo mostrano come ottenere il percorso e la versione dei pacchetti utilizzato da SQL Server.

## <a name="get-the-r-library-location"></a>Ottenere il percorso della libreria R

Per qualsiasi versione di SQL Server, eseguire l'istruzione seguente per verificare i [libreria di pacchetti R predefinita](installing-and-managing-r-packages.md) per l'istanza corrente:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Facoltativamente, è possibile usare [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) nelle versioni più recenti di RevoScaleR in Machine Learning Services di SQL Server 2017 o [R Services aggiornata almeno R per RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). Questa stored procedure restituisce il percorso della libreria di istanza e la versione di RevoScaleR usate da SQL Server:

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> Il [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) funzione può essere eseguita solo nel computer locale. La funzione non può restituire i percorsi di libreria per le connessioni remote.

**Risultati**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>Ottenere il percorso di libreria di Python

Per la **Python** in SQL Server 2017, eseguire l'istruzione seguente per verificare la libreria predefinita per l'istanza corrente. Questo esempio viene restituito l'elenco delle cartelle incluse in Python `sys.path` variabile. L'elenco include la directory corrente e il percorso della libreria standard.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**Risultati**

```text
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

Per altre informazioni sulla variabile `sys.path` e come viene usato per impostare il percorso di ricerca dell'interprete per i moduli, vedere il [documentazione di Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>Elencare tutti i pacchetti

Esistono diversi modi che è possibile ottenere un elenco completo dei pacchetti attualmente installati. Uno dei vantaggi dell'esecuzione di comandi dell'elenco di pacchetti da sp_execute_external_script è che si ricevano sempre i pacchetti installati nella libreria di istanza.

### <a name="r"></a>R

Nell'esempio seguente viene utilizzata la funzione R `installed.packages()` in un [!INCLUDE[tsql](../../includes/tsql-md.md)] stored procedure per ottenere una matrice di pacchetti che sono stati installati nella libreria R_SERVICES per l'istanza corrente. Questo script restituisce i campi nome e la versione del pacchetto nel file di descrizione, viene restituito solo il nome.

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Per altre informazioni su facoltativo e campi predefiniti per il campo della descrizione del pacchetto R, vedere [ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

### <a name="python"></a>Python

Il `pip` modulo viene installato per impostazione predefinita e supporta molte operazioni per i pacchetti installato listato, oltre a quelli supportati per Python standard. È possibile eseguire `pip` da Python prompt dei comandi, naturalmente, ma è anche possibile chiamare alcune funzioni pip da `sp_execute_external_script`.

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
  import pip
  import pandas as pd
  installed_packages = pip.get_installed_distributions()
  installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
  df = pd.DataFrame(installed_packages_list)
  OutputDataSet = df'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

Quando si esegue `pip` dalla riga di comando, sono disponibili molte altre utili funzioni: `pip list` Ottiene tutti i pacchetti installati, mentre `pip freeze` Elenca i pacchetti installati da `pip`e non vengono elencati i pacchetti pip se stesso dipende. È anche possibile usare `pip freeze` per generare un file di dipendenza.

## <a name="find-a-single-package"></a>Trovare un singolo pacchetto

Se è stato installato un pacchetto e si desidera assicurarsi che sia disponibile per una particolare istanza di SQL Server, è possibile eseguire la chiamata di stored procedure seguente per caricare il pacchetto e restituire solo i messaggi.

### <a name="r"></a>R

In questo esempio cerca e carica la libreria RevoScaleR, se disponibile.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ Se il pacchetto viene trovato, viene restituito un messaggio: "Comandi completati".

+ Se il pacchetto non può essere disponibile o non caricato, viene visualizzato un errore che contiene il testo: "non c'è nessun pacchetto denominato 'MissingPackageName'"

### <a name="python"></a>Python

Il controllo equivalente per Python può essere eseguito da Python della shell, usando `conda` o `pip` comandi. In alternativa, è possibile eseguire questa istruzione in una stored procedure:

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
  import pip
  import pkg_resources
  pckg_name = "revoscalepy"
  pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
  installed_pckg = pckgs.query(''key == @pckg_name'')
  print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")'
```

<a name="get-package-vers"></a>

## <a name="get-package-version"></a>Ottenere la versione del pacchetto

È possibile ottenere R e Python tramite Management Studio le informazioni sulla versione del pacchetto.

### <a name="r-package-version"></a>Versione del pacchetto R

Questa istruzione restituisce la versione del pacchetto RevoScaleR e la versione di R di base.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Versione del pacchetto Python

Questa istruzione restituisce la versione del pacchetto revoscalepy e la versione di Python.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import revoscalepy
import sys
print(revoscalepy.__version__)
print(sys.version)
'
```

## <a name="next-steps"></a>Passaggi successivi

+ [Installare nuovi pacchetti R](install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)