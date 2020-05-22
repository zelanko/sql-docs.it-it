---
title: Ottenere informazioni sui pacchetti Python
description: Istruzioni su come ottenere informazioni sui pacchetti Python installati in Machine Learning Services per SQL Server, inclusi i percorsi di installazione e le versioni.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/01/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fb08940a9a6c9c15d8c633f5b3c439514bc43646
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606003"
---
# <a name="get-python-package-information"></a>Ottenere informazioni sui pacchetti Python

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come ottenere informazioni sui pacchetti Python installati in Machine Learning Services per SQL Server, inclusi i percorsi di installazione e le versioni. Gli script Python di esempio mostrano come elencare le informazioni sui pacchetti, ad esempio il percorso di installazione e la versione.

## <a name="default-python-library-location"></a>Percorso della libreria Python predefinita

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Quando si installa Machine Learning con SQL Server, viene creata una singola libreria di pacchetti a livello di istanza per ogni linguaggio installato. La libreria dell'istanza è una cartella protetta registrata con SQL Server.
::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
Quando si installa Machine Learning con SQL Server, viene creata una singola libreria di pacchetti a livello di istanza per ogni linguaggio installato.
::: moniker-end

Qualsiasi script o codice eseguito nel database in SQL Server deve caricare le funzioni dalla libreria dell'istanza. SQL Server non può accedere ai pacchetti installati in altre librerie. Questo vale anche per i client remoti. Qualsiasi codice Python in esecuzione nel contesto di calcolo del server può usare solo i pacchetti installati nella libreria dell'istanza.
Per assicurare la protezione delle risorse del server, la libreria dell'istanza predefinita può essere modificata solo da un amministratore del computer.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per Python è il seguente:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

In questo esempio si presuppone che venga usata l'istanza di SQL predefinita, ovvero MSSQLSERVER. Se SQL Server è installato come istanza definita dall'utente, in alternativa viene usato il nome specificato.
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per Python è il seguente:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`

In questo esempio si presuppone che venga usata l'istanza di SQL predefinita, ovvero MSSQLSERVER. Se SQL Server è installato come istanza definita dall'utente, in alternativa viene usato il nome specificato.
::: moniker-end

Abilitare gli script esterni eseguendo i comandi SQL seguenti:

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH override;
```

Eseguire l'istruzione seguente per verificare la libreria predefinita per l'istanza corrente. Questo esempio restituisce l'elenco delle cartelle incluse nella variabile `sys.path` di Python. L'elenco include la directory corrente e il percorso della libreria standard.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

Per altre informazioni sulla variabile `sys.path` e su come viene usata per impostare il percorso di ricerca dell'interprete per i moduli, vedere [The Module Search Path](https://docs.python.org/2/tutorial/modules.html#the-module-search-path) (Percorso di ricerca dei moduli).

## <a name="default-microsoft-python-packages"></a>Pacchetti Microsoft Python predefiniti

Quando si seleziona la funzionalità Python durante l'installazione di Machine Learning Services per SQL Server, vengono installati i pacchetti Microsoft Python seguenti.

| Pacchetti | Versione |  Descrizione |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.4.7 | Usato per contesti di calcolo remoti, streaming, esecuzione parallela di funzioni rx per l'importazione e la trasformazione dei dati, modellazione, visualizzazione e analisi. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.4.7 | Aggiunge algoritmi di Machine Learning in Python. |

Per informazioni sulla versione di Python inclusa, vedere [Versioni di Python e R](../sql-server-machine-learning-services.md#versions).

### <a name="component-upgrades"></a>Aggiornamenti dei componenti

Per impostazione predefinita, i pacchetti Python vengono aggiornati tramite i Service Pack e gli aggiornamenti cumulativi. I pacchetti aggiuntivi e gli aggiornamenti completi della versione dei componenti di base di Python sono possibili solo tramite aggiornamenti del prodotto oppure tramite il binding del supporto Python con Microsoft Machine Learning Server.

Per altre informazioni, vedere [Aggiornare i componenti R e Python in SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-python-packages"></a>Pacchetti Python open source predefiniti

Quando si seleziona l'opzione relativa al linguaggio Python durante l'installazione, viene installata la distribuzione Anaconda 4.2 (su Python 3.5). Oltre alle librerie di codice Python, l'installazione standard include dati di esempio, unit test e script di esempio.

> [!IMPORTANT]
> Non si dovrebbe mai sovrascrivere manualmente la versione di Python installata dal programma di installazione di SQL Server con le versioni più recenti sul Web. I pacchetti Microsoft per Python sono basati su versioni specifiche di Anaconda. La modifica dell'installazione può rendere instabile questa distribuzione.

## <a name="list-all-installed-python-packages"></a>Elenco di tutti i pacchetti Python installati

Lo script di esempio seguente visualizza un elenco di tutti i pacchetti Python installati nell'istanza di SQL Server.

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import pkg_resources
import pandas as pd
installed_packages = pkg_resources.working_set
installed_packages_list = sorted(["%s==%s" % (i.key, i.version) for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>Trovare un singolo pacchetto Python

Se è stato installato un pacchetto Python e si vuole verificare che il pacchetto sia disponibile per una determinata istanza di SQL Server, è possibile eseguire una stored procedure per cercare il pacchetto e restituire messaggi.

Il codice seguente, ad esempio, esegue la ricerca del pacchetto `scikit-learn`.
Se il pacchetto viene trovato, il codice stampa la versione del pacchetto.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pkg_name = "pandas"
try:
    version = pkg_resources.get_distribution(pkg_name).version
    print("Package " + pkg_name + " is version " + version)
except:
    print("Package " + pkg_name + " not found")
'
```

Risultato:

```text
STDOUT message(s) from external script: Package pandas is version 0.23.4
```

Nell'esempio seguente viene stampata la versione del pacchetto `pandas`.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pkg_name = "pandas"
print(pkg_name + " package is version " + pkg_resources.get_distribution(pkg_name).version)
'
```

Nell'esempio seguente viene restituita la versione di Python.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import sys
print(sys.version)
'
```

## <a name="next-steps"></a>Passaggi successivi

::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
+ [Installare i pacchetti con gli strumenti Python](install-python-packages-standard-tools.md)
::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ [Installare nuovi pacchetti Python con sqlmlutils](install-additional-r-packages-on-sql-server.md)
::: moniker-end