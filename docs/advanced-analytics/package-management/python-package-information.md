---
title: Ottenere informazioni sul pacchetto python
description: Informazioni su come ottenere informazioni sui pacchetti Python installati, incluse le versioni e i percorsi di installazione, in SQL Server Machine Learning Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bccfc97fe75a718ce76ea0d1292bfc7ea6cb6564
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641178"
---
# <a name="get-python-package-information"></a>Ottenere informazioni sul pacchetto python

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come ottenere informazioni sui pacchetti Python installati, incluse le versioni e i percorsi di installazione, in SQL Server Machine Learning Services. Gli script Python di esempio illustrano come elencare le informazioni del pacchetto, ad esempio il percorso di installazione e la versione.

## <a name="default-python-library-location"></a>Percorso predefinito della libreria Python

Quando si installa Machine Learning con SQL Server, viene creata una singola libreria di pacchetti a livello di istanza per ogni lingua installata. In Windows la libreria di istanze è una cartella protetta registrata con SQL Server.

Tutti gli script o il codice eseguito nel database in SQL Server devono caricare le funzioni dalla libreria di istanze. SQL Server non è in grado di accedere ai pacchetti installati in altre librerie. Questo vale anche per i client remoti: qualsiasi codice Python in esecuzione nel contesto di calcolo del server può usare solo i pacchetti installati nella libreria di istanze.
Per proteggere le risorse del server, la libreria di istanze predefinita può essere modificata solo da un amministratore del computer.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per Python è il seguente:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
Il percorso predefinito dei file binari per Python è il seguente:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

Si presuppone che l'istanza di SQL predefinita, MSSQLSERVER. Se SQL Server viene installato come un'istanza denominata definita dall'utente, viene invece utilizzato il nome specificato.

Eseguire l'istruzione seguente per verificare la libreria predefinita per l'istanza corrente. Questo esempio restituisce l'elenco delle cartelle incluse nella variabile Python `sys.path` . L'elenco include la directory corrente e il percorso della libreria standard.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

Per ulteriori informazioni sulla variabile `sys.path` e su come viene utilizzata per impostare il percorso di ricerca dell'interprete per i moduli, vedere [il percorso di ricerca del modulo](https://docs.python.org/2/tutorial/modules.html#the-module-search-path).

## <a name="default-python-packages"></a>Pacchetti Python predefiniti

I pacchetti Python seguenti vengono installati con SQL Server Machine Learning Services quando si seleziona la funzionalità Python durante l'installazione.

| Pacchetti | Versione |  Descrizione |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9,2 | Usato per contesti di calcolo remoti, streaming, esecuzione parallela di funzioni RX per l'importazione e la trasformazione dei dati, la modellazione, la visualizzazione e l'analisi. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9,2 | Aggiunge algoritmi di Machine Learning in Python. |

### <a name="component-upgrades"></a>Aggiornamenti componenti

Per impostazione predefinita, i pacchetti Python vengono aggiornati tramite i Service Pack e gli aggiornamenti cumulativi. Pacchetti aggiuntivi e aggiornamenti completi della versione dei componenti di base di Python sono possibili solo tramite aggiornamenti del prodotto oppure associando il supporto Python a Microsoft Machine Learning Server.

Per altre informazioni, vedere [aggiornare i componenti R e Python in SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-python-packages"></a>Pacchetti Python Open Source predefiniti

Quando si seleziona l'opzione relativa al linguaggio Python durante l'installazione, viene installata la distribuzione Anaconda 4,2 (su Python 3,5). Oltre alle librerie di codice Python, l'installazione standard include dati di esempio, unit test e script di esempio.

> [!IMPORTANT]
> Non è mai necessario sovrascrivere manualmente la versione di Python installata dal programma di installazione di SQL Server con le versioni più recenti sul Web. I pacchetti Microsoft Python sono basati su versioni specifiche di Anaconda. La modifica dell'installazione potrebbe destabilizzarla.

## <a name="list-all-installed-python-packages"></a>Elencare tutti i pacchetti Python installati

Il `pip` modulo viene installato per impostazione predefinita e supporta molte operazioni per l'elenco dei pacchetti installati, oltre a quelli supportati da Python standard. È possibile eseguire `pip` da un prompt dei comandi Python, ma è anche possibile chiamare alcune funzioni PIP `sp_execute_external_script`da.

Nello script di esempio seguente viene visualizzato un elenco di pacchetti installati e delle relative versioni.

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
OutputDataSet = df
  '
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>Trovare un singolo pacchetto python

Se è stato installato un pacchetto Python e si desidera assicurarsi che sia disponibile per una particolare istanza di SQL Server, è possibile eseguire una stored procedure per caricare il pacchetto e restituire messaggi.

Il codice seguente, ad esempio, Cerca il `scikit-learn` pacchetto.
Se il pacchetto viene trovato, il codice restituisce il messaggio "Package Scikit-learn is installed".

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pip
import pkg_resources
pckg_name = "scikit-learn"
pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
  '
```

<a name="get-package-vers"></a>

Nell'esempio seguente vengono restituite le versioni del pacchetto revoscalepy e di Python.

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

+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Ottenere le informazioni sul pacchetto R](r-package-information.md)
+ [Installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md)
+ [Esercitazioni su R e Python](../tutorials/machine-learning-services-tutorials.md)
