---
title: Installare pacchetti Python con pip
description: Informazioni su come usare PIP Python per installare nuovi pacchetti Python in un'istanza di SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: dc5addca9c9bbf01408cea89f85676813b97506c
ms.sourcegitcommit: 52d3902e7b34b14d70362e5bad1526a3ca614147
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2019
ms.locfileid: "70109751"
---
# <a name="install-python-packages-with-sqlmlutils"></a>Installare pacchetti Python con sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come usare le funzioni nel pacchetto [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) per installare nuovi pacchetti Python in un'istanza di SQL Server Machine Learning Services. I pacchetti installati possono essere usati negli script Python eseguiti nel database usando l'istruzione T-SQL [SP-Execute-External-script-Transact-SQL](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) .

Per ulteriori informazioni sul percorso del pacchetto e i percorsi di installazione, vedere [ottenere informazioni sui pacchetti Python](../package-management/python-package-information.md).

> [!NOTE]
> Il comando Python `pip install` standard non è consigliato per l'aggiunta di pacchetti Python in SQL Server. Usare invece **sqlmlutils** come descritto in questo articolo.

## <a name="prerequisites"></a>Prerequisiti

+ È necessario avere [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) installato con l'opzione del linguaggio Python.

+ Installare [Python](https://www.python.org/) nel computer client usato per connettersi a SQL Server. È anche possibile che si desideri un ambiente di sviluppo Python, ad esempio [Visual Studio Code](https://code.visualstudio.com/download) con l' [estensione Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python). 

+ Installare [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) nel computer client usato per connettersi al SQL Server. È possibile usare altri strumenti di gestione o query di database, ma in questo articolo si presuppone Azure Data Studio o SSMS.

### <a name="other-considerations"></a>Altre considerazioni

+ I pacchetti devono essere conformi a Python 3,5 ed essere eseguiti in Windows.

+ La libreria di pacchetti Python si trova nella cartella programmi dell'istanza di SQL Server e, per impostazione predefinita, l'installazione in questa cartella richiede le autorizzazioni di amministratore. Per ulteriori informazioni, vedere [Package Library Location](../package-management/python-package-information.md#default-python-library-location).

+ L'installazione del pacchetto è per istanza. Se si dispone di più istanze di Machine Learning Services, è necessario aggiungere il pacchetto a ciascuna di esse.

+ Prima di aggiungere un pacchetto, valutare se il pacchetto è adatto per l'ambiente SQL Server.

  + Si consiglia di usare Python nel database per le attività che traggono vantaggio da una stretta integrazione con il motore di database, ad esempio Machine Learning, anziché attività che eseguono semplicemente query sul database.

  + Se si aggiungono pacchetti che inseriscono una quantità eccessiva di pressione di calcolo sul server, le prestazioni risulteranno ridotte.

  + In un ambiente di SQL Server con protezione avanzata, è consigliabile evitare quanto segue:
    + Pacchetti per i quali è richiesto l'accesso alla rete
    + Pacchetti per i quali è richiesto l'accesso file system elevato
    + Pacchetti usati per lo sviluppo Web o altre attività che non traggono vantaggio dall'esecuzione all'interno SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Installare sqlmlutils nel computer client

Per usare **sqlmlutils**, è prima di tutto necessario installarlo nel computer client usato per connettersi a SQL Server.

1. Scaricare il file zip di **sqlmlutils** più https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist recente da al computer client. Non decomprimere il file.

1. Aprire un **prompt dei comandi** ed eseguire il comando seguente per installare il pacchetto **sqlmlutils** . Sostituire il percorso completo del file zip **sqlmlutils** scaricato. in questo esempio si presuppone che il file scaricato `c:\temp\sqlmlutils_0.6.0.zip`sia.

   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils_0.6.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>Aggiungere un pacchetto python in SQL Server

Nell'esempio seguente si aggiungerà il pacchetto di [strumenti di testo](https://pypi.org/project/text-tools/) a SQL Server.

### <a name="add-the-package-online"></a>Aggiungere il pacchetto online

Se il computer client usato per connettersi a SQL Server dispone di accesso a Internet, è possibile usare **sqlmlutils** per trovare il pacchetto di **strumenti di testo** e tutte le dipendenze su Internet, quindi installare il pacchetto in un'istanza di SQL Server in modalità remota.

1. Nel computer client aprire **Python** o un ambiente Python.

1. Usare i comandi seguenti per installare il pacchetto di **strumenti di testo** . Sostituire le informazioni di connessione del database SQL Server.

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>Aggiungere il pacchetto offline

Se il computer client utilizzato per la connessione a SQL Server non dispone di una connessione Internet, è possibile utilizzare **PIP** in un computer con accesso a Internet per scaricare il pacchetto e tutti i pacchetti dipendenti in una cartella locale. Copiare quindi la cartella nel computer client in cui è possibile installare il pacchetto offline.

#### <a name="on-a-computer-with-internet-access"></a>In un computer con accesso a Internet

1. Aprire un **prompt dei comandi** ed eseguire il comando seguente per creare una cartella locale contenente il pacchetto di **strumenti di testo** . In questo esempio viene creata `c:\temp\text-tools`la cartella.

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. Copiare la `text-tools` cartella nel computer client. Nell'esempio seguente si presuppone che sia stato `c:\temp\packages\text-tools`copiato in.

#### <a name="on-the-client-computer"></a>Nel computer client

Usare **sqlmlutils** per installare ogni pacchetto (file WHL) presente nella cartella locale creata da **PIP** . Non è importante l'ordine di installazione dei pacchetti.

In questo esempio, **gli strumenti di testo** non hanno dipendenze, pertanto è presente un solo file `text-tools` dalla cartella da installare. Al contrario, un pacchetto, ad esempio **Scikit-Plot** , presenta 11 dipendenze, quindi si troveranno 12 file nella cartella (il pacchetto **Scikit-Plot** e i pacchetti dipendenti 11) e si installeranno ognuno di essi.

Eseguire lo script Python seguente. Sostituire le informazioni di connessione al database SQL Server e il percorso e il nome del file effettivo del pacchetto. Ripetere l' `sqlmlutils.SQLPackageManager` istruzione per ogni file di pacchetto nella cartella.

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
sqlmlutils.SQLPackageManager(connection).install("c:/temp/packages/text-tools/text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package-in-sql-server"></a>Usare il pacchetto in SQL Server

È ora possibile usare il pacchetto in uno script Python in SQL Server. Esempio:

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

Se si vuole rimuovere il pacchetto di **strumenti di testo** , usare il comando Python seguente nel computer client, usando la stessa variabile di connessione definita in precedenza.

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="see-also"></a>Vedere anche

+ Per visualizzare informazioni sui pacchetti Python installati in SQL Server Machine Learning Services, vedere [ottenere informazioni sul pacchetto python](../package-management/python-package-information.md).

+ Per informazioni sull'installazione dei pacchetti R in SQL Server Machine Learning Services, vedere [installare nuovi pacchetti r in SQL Server](../r/install-additional-r-packages-on-sql-server.md).
