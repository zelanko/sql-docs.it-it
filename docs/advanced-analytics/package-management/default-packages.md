---
title: Ottenere informazioni sui pacchetti R e Python
description: Determinare la versione del pacchetto R e Python, verificare l'installazione e ottenere un elenco dei pacchetti installati in R Services per SQL Server o Machine Learning Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ff4d0839cfdf24b1b43fe9d5a371092713bc63cf
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715789"
---
#  <a name="get-r-and-python-package-information"></a>Ottenere informazioni sui pacchetti R e Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In alcuni casi, quando si lavora con più ambienti o installazioni di R o Python, è necessario verificare che il codice in esecuzione usi l'ambiente previsto per Python o l'area di lavoro corretta per R. Se ad esempio è stato [aggiornato R o Python](../install/upgrade-r-and-python.md), il percorso della libreria r potrebbe trovarsi in una cartella diversa da quella predefinita. Inoltre, se si installa R client o un'istanza del server autonomo, è possibile che nel computer siano presenti più librerie R.

Esempi di script R e Python in questo articolo illustrano come ottenere il percorso e la versione dei pacchetti usati da SQL Server.

## <a name="get-the-r-library-location"></a>Ottenere il percorso della libreria R

Per qualsiasi versione di SQL Server, eseguire l'istruzione seguente per verificare la libreria di pacchetti R predefinita per l'istanza corrente:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Facoltativamente, è possibile usare [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) nelle versioni più recenti di RevoScaleR in SQL Server Machine Learning Services o [r Services aggiornamento di r ad almeno RevoScaleR 9.0.1](../install/upgrade-r-and-python.md). Questo stored procedure restituisce il percorso della libreria di istanze e la versione di RevoScaleR usata da SQL Server:

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
> La funzione [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) può essere eseguita solo sul computer locale. La funzione non può restituire percorsi di libreria per le connessioni remote.

**Risultati**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>Ottenere il percorso della libreria Python

Per **Python**, eseguire l'istruzione seguente per verificare la libreria predefinita per l'istanza corrente. Questo esempio restituisce l'elenco delle cartelle incluse nella variabile Python `sys.path` . L'elenco include la directory corrente e il percorso della libreria standard.

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

Per ulteriori informazioni sulla variabile `sys.path` e su come viene utilizzata per impostare il percorso di ricerca dell'interprete per i moduli, vedere la documentazione di [Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path) .

## <a name="list-all-packages"></a>Elenca tutti i pacchetti

È possibile ottenere un elenco completo dei pacchetti attualmente installati in diversi modi. Uno dei vantaggi dell'esecuzione di comandi dell'elenco di pacchetti da sp_execute_external_script è la garanzia di ottenere i pacchetti installati nella libreria di istanze.

### <a name="r"></a>R

Nell'esempio seguente viene usata la funzione `installed.packages()` R in [!INCLUDE[tsql](../../includes/tsql-md.md)] una stored procedure per ottenere una matrice di pacchetti installati nella libreria R_SERVICES per l'istanza corrente. Questo script restituisce i campi relativi al nome e alla versione del pacchetto nel file di descrizione. viene restituito solo il nome.

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

Per ulteriori informazioni sui campi facoltativi e predefiniti per il campo Descrizione pacchetto R, vedere [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

### <a name="python"></a>Python

Il `pip` modulo viene installato per impostazione predefinita e supporta molte operazioni per l'elenco dei pacchetti installati, oltre a quelli supportati da Python standard. Naturalmente, è `pip` possibile eseguire da un prompt dei comandi Python, ma è anche possibile chiamare alcune funzioni PIP da `sp_execute_external_script`.

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

Quando si `pip` esegue dalla riga di comando, sono disponibili molte altre funzioni utili `pip list` : recupera tutti i pacchetti installati, mentre `pip freeze` elenca i pacchetti installati da `pip`e non elenca i pacchetti che PIP stesso dipende da. È inoltre possibile utilizzare `pip freeze` per generare un file di dipendenza.

## <a name="find-a-single-package"></a>Trova un singolo pacchetto

Se è stato installato un pacchetto e si desidera assicurarsi che sia disponibile per una particolare istanza di SQL Server, è possibile eseguire la chiamata stored procedure seguente per caricare il pacchetto e restituire solo i messaggi.

### <a name="r"></a>R

Questo esempio cerca e carica la libreria RevoScaleR, se disponibile.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ Se il pacchetto viene trovato, viene restituito un messaggio: "I comandi sono stati completati".

+ Se non è possibile trovare o caricare il pacchetto, si verifica un errore contenente il testo: "non è presente alcun pacchetto denominato ' MissingPackageName '"

### <a name="python"></a>Python

Il controllo equivalente per Python può essere eseguito dalla shell Python, usando `conda` i comandi o. `pip` In alternativa, eseguire questa istruzione in un stored procedure:

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

È possibile ottenere informazioni sulla versione del pacchetto R e Python usando Management Studio.

### <a name="r-package-version"></a>Versione del pacchetto R

Questa istruzione restituisce la versione del pacchetto RevoScaleR e la versione di base di R.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Versione del pacchetto python

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

+ [Installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)