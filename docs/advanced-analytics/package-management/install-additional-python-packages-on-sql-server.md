---
title: Installare pacchetti Python con sqlmlutils
description: Informazioni su come usare lo strumento pip di Python per installare nuovi pacchetti Python in un'istanza di Machine Learning Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/30/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9d759921ac82f34156856b587161f44c64269ea0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76929893"
---
# <a name="install-python-packages-with-sqlmlutils"></a>Installare pacchetti Python con sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come usare le funzioni incluse in [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) per installare nuovi pacchetti Python in un'istanza di Machine Learning Services per SQL Server. I pacchetti installati possono essere usati negli script Python in esecuzione nel database usando l'istruzione T-SQL [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

Per altre informazioni sulla posizione dei pacchetti e sui percorsi di installazione, vedere [Ottenere informazioni sui pacchetti Python](../package-management/python-package-information.md).

> [!NOTE]
> Per aggiungere pacchetti Python in SQL Server 2019 non è consigliabile usare il comando `pip install` standard di Python. In alternativa, usare **sqlmlutils**, come descritto in questo articolo.

## <a name="prerequisites"></a>Prerequisites

+ È necessario che sia installato [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) con l'opzione relativa al linguaggio Python.

+ Installare [python](https://www.python.org/) nel computer client usato per connettersi a SQL Server. Può anche essere necessario un ambiente di sviluppo per Python, ad esempio [Visual Studio Code](https://code.visualstudio.com/download) con l'[estensione per Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python). 

+ Installare [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) nel computer client usato per connettersi a SQL Server. È possibile usare altri strumenti di query o gestione di database, ma in questo articolo si presuppone che venga usato Azure Data Studio o SSMS.

### <a name="other-considerations"></a>Altre considerazioni

+ I pacchetti devono essere conformi a Python 3.5 ed essere eseguiti in Windows.

+ La libreria di pacchetti Python si trova nella cartella Programmi dell'istanza di SQL Server e, per impostazione predefinita, è necessario disporre delle autorizzazioni di amministratore per eseguire installazioni in questa cartella. Per altre informazioni, vedere [Percorso della libreria dei pacchetti](../package-management/python-package-information.md#default-python-library-location).

+ L'installazione di un pacchetto viene eseguita a livello di istanza. Se si hanno più istanze di Machine Learning Services, è necessario aggiungere il pacchetto a ciascuna di esse.

+ Prima di aggiungere un pacchetto, valutare se è adatto all'ambiente di SQL Server.

  + È consigliabile usare Python all'interno nel database per le attività che traggono vantaggio da una stretta integrazione con il motore di database, ad esempio Machine Learning, piuttosto che per le attività che eseguono semplicemente query sul database.

  + Se si aggiungono pacchetti che richiedono un utilizzo elevato delle risorse di calcolo del server, possono verificarsi problemi di prestazioni.

  + In un ambiente di SQL Server con protezione avanzata, è consigliabile evitare i tipi di pacchetti seguenti:
    + Pacchetti che richiedono l'accesso alla rete
    + Pacchetti che richiedono l'accesso al file system con privilegi elevati
    + Pacchetti usati per lo sviluppo Web o altre attività che non traggono vantaggio dall'esecuzione all'interno di SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Installare sqlmlutils nel computer client

Prima di usare **sqlmlutils**, è necessario installarlo nel computer client usato per connettersi a SQL Server. Assicurarsi di aver `pip` installato. Vedere [Installazione di pip](https://pip.pypa.io/en/stable/installing/) per altre informazioni.

1. Scaricare la versione più recente del file ZIP di **sqlmlutils** da https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist nel computer client. Non decomprimere il file.

1. Aprire un **prompt dei comandi** ed eseguire i comandi seguenti per installare il pacchetto **sqlmlutils**. Sostituire il percorso completo del file ZIP di **sqlmlutils** scaricato. In questo esempio si presuppone che il file scaricato sia `c:\temp\sqlmlutils_0.7.2.zip`.

   ```console
   pip install "pymssql<3.0"
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils_0.7.2.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>Aggiungere un pacchetto Python in SQL Server

Nell'esempio seguente si aggiungerà il pacchetto [text-tools](https://pypi.org/project/text-tools/) in SQL Server.

### <a name="add-the-package-online"></a>Aggiungere il pacchetto online

Se il computer client usato per connettersi a SQL Server dispone di accesso a Internet, è possibile usare **sqlmlutils** per trovare il pacchetto **text-tools** e le eventuali dipendenze su Internet, quindi installare il pacchetto in un'istanza di SQL Server in modalità remota.

1. Nel computer client aprire **Python** o un ambiente per Python.

1. Usare i comandi seguenti per installare il pacchetto **text-tools**. Usare le proprie informazioni di connessione al database di SQL Server. Se non si usa l'autenticazione di Windows, aggiungere i parametri `uid` e `pwd`.

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>Aggiungere il pacchetto offline

Se il computer client usato per connettersi a SQL Server non dispone di accesso a Internet, è possibile usare **pip** in un computer con accesso a Internet per scaricare il pacchetto e gli eventuali pacchetti dipendenti in una cartella locale. Copiare quindi la cartella nel computer client in cui è possibile installare il pacchetto offline.

#### <a name="on-a-computer-with-internet-access"></a>In un computer con accesso a Internet

1. Aprire un **prompt dei comandi** ed eseguire il comando seguente per creare una cartella locale contenente il pacchetto **text-tools**. Questo esempio crea la cartella `c:\temp\text-tools`.

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. Copiare la cartella `text-tools` nel computer client. Nell'esempio seguente si presuppone che sia stata copiata in `c:\temp\packages\text-tools`.

#### <a name="on-the-client-computer"></a>Nel computer client

Usare **sqlmlutils** per installare ogni pacchetto (file WHL) presente nella cartella locale creata da **pip**. L'ordine di installazione dei pacchetti non è importante.

In questo esempio, **text-tools** non ha dipendenze e pertanto nella cartella `text-tools` è presente un solo file da installare. Al contrario, un pacchetto come **scikit-plot** ha 11 dipendenze e quindi nella cartella si troveranno 12 file da installare singolarmente, ovvero il pacchetto **scikit-plot** e gli 11 pacchetti dipendenti.

Eseguire lo script Python seguente. Usare il percorso e il nome effettivi del pacchetto e le proprie informazioni di connessione al database di SQL Server. Se non si usa l'autenticazione di Windows, aggiungere i parametri `uid` e `pwd`. Ripetere l'istruzione `sqlmlutils.SQLPackageManager` per ogni file di pacchetto nella cartella.

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase")
sqlmlutils.SQLPackageManager(connection).install("c:/temp/packages/text-tools/text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package-in-sql-server"></a>Usare il pacchetto in SQL Server

È ora possibile usare il pacchetto in uno script Python in SQL Server. Ad esempio:

```python
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
from text_tools.finders import find_best_string
corpus = "Lorem Ipsum text"
query = "Ipsum"
first_match = find_best_string(query, corpus)
print(first_match)
  '
```

## <a name="remove-the-package-from-sql-server"></a>Rimuovere il pacchetto da SQL Server

Se si vuole rimuovere il pacchetto **text-tools**, usare il comando Python seguente nel computer client, con la stessa variabile di connessione definita in precedenza.

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="see-also"></a>Vedere anche

+ Per visualizzare le informazioni sui pacchetti Python installati in Machine Learning Services per SQL Server, vedere [Ottenere informazioni sui pacchetti Python](../package-management/python-package-information.md).

+ Per informazioni sull'installazione dei pacchetti R in Machine Learning Services per SQL Server, vedere [Installare nuovi pacchetti R in SQL Server](../r/install-additional-r-packages-on-sql-server.md).
