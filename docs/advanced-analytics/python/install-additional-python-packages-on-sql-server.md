---
title: Installare nuovi pacchetti di linguaggio Python
description: Aggiungere nuovi pacchetti Python a SQL Server 2017 Machine Learning Services (in-database) e Machine Learning Server (standalone).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/16/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0e305f778ee132c06e9a2b08c8cec64f0535846a
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345520"
---
# <a name="install-new-python-packages-on-sql-server"></a>Installare nuovi pacchetti Python in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive come installare nuovi pacchetti Python in un'istanza di SQL Server 2017 Machine Learning Services. In generale, il processo di installazione di nuovi pacchetti è simile a quello in un ambiente Python standard. Tuttavia, se il server non dispone di una connessione Internet, sono necessari alcuni passaggi aggiuntivi.

Per ulteriori informazioni sul percorso del pacchetto e i percorsi di installazione, vedere [ottenere informazioni sul pacchetto R o Python](../package-management/installed-package-information.md).

## <a name="prerequisites"></a>Prerequisiti

+ [SQL Server 2017 Machine Learning Services (in-database)](../install/sql-machine-learning-services-windows-install.md) con l'opzione del linguaggio Python. 

+ I pacchetti devono essere conformi a Python 3,5 ed essere eseguiti in Windows. 

+ Per installare i pacchetti è necessario l'accesso amministrativo al server.

## <a name="considerations"></a>Considerazioni

Prima di aggiungere i pacchetti, valutare se il pacchetto è adatto per l'ambiente SQL Server. Un server di database è in genere un asset condiviso che ospita più carichi di lavoro. Se si aggiungono pacchetti che inseriscono una quantità eccessiva di pressione di calcolo sul server, le prestazioni risulteranno ridotte. 

Inoltre, alcuni dei pacchetti Python più diffusi, ad esempio Flask, eseguono attività, ad esempio lo sviluppo Web, più adatti per un ambiente autonomo. Si consiglia di usare Python nel database per le attività che traggono vantaggio da una stretta integrazione con il motore di database, ad esempio Machine Learning, anziché attività che eseguono semplicemente query sul database.

I server di database sono spesso bloccati. In molti casi, l'accesso a Internet è completamente bloccato. Per i pacchetti con un lungo elenco di dipendenze, è necessario identificare tali dipendenze in anticipo ed essere disposti a installarle manualmente.

## <a name="add-a-new-python-package"></a>Aggiungere un nuovo pacchetto python

Per questo esempio, si presuppone che si desideri installare un nuovo pacchetto direttamente nel computer SQL Server.

L'installazione del pacchetto è per istanza. Se si dispone di più istanze di Machine Learning Services, è necessario aggiungere il pacchetto a ciascuna di esse.

Il pacchetto installato in questo esempio è [CNTK](https://docs.microsoft.com/cognitive-toolkit/), un Framework per l'apprendimento approfondito di Microsoft che supporta la personalizzazione, il training e la condivisione di diversi tipi di reti neurali.

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>Passaggio 1. Scaricare la versione di Windows del pacchetto python

+ Se si installano pacchetti Python in un server senza accesso a Internet, è necessario scaricare il file WHL in un computer diverso e quindi copiarlo nel server.

    Ad esempio, in un computer separato è possibile scaricare il file WHL da questo sito [https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl), quindi copiare il file `cntk-2.1-cp35-cp35m-win_amd64.whl` in una cartella locale nel computer SQL Server.

+ SQL Server 2017 USA Python 3,5. 

> [!IMPORTANT]
> Assicurarsi di ottenere la versione di Windows del pacchetto. Se il file termina con. gz, probabilmente non è la versione corretta.

Questa pagina contiene i download per più piattaforme e per più versioni di Python: [Configurare CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>Passaggio 2. Aprire un prompt dei comandi Python

Individuare il percorso predefinito della libreria Python utilizzato dal SQL Server. Se sono state installate più istanze, individuare la cartella PYTHON_SERVICE per l'istanza in cui si desidera aggiungere il pacchetto.

Se ad esempio Machine Learning Services è stato installato usando le impostazioni predefinite e Machine Learning è abilitato nell'istanza predefinita, il percorso sarà il seguente:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Aprire il prompt dei comandi Python associato all'istanza.

> [!TIP]
> Per il debug e il test futuri, potrebbe essere necessario configurare un ambiente Python specifico per la libreria di istanze.

### <a name="step-3-install-the-package-using-pip"></a>Passaggio 3. Installare il pacchetto con pip

+ Se si è abituati a usare la riga di comando di Python, usare PIP. exe per installare i nuovi pacchetti. È possibile trovare il  programma di installazione PIP `Scripts` nella sottocartella. 

  SQL Server installazione non aggiunge script al percorso di sistema. Se si riceve un errore che `pip` non è riconosciuto come comando interno o esterno, è possibile aggiungere la cartella Scripts alla variabile Path in Windows.

  Il percorso completo della cartella **script** in un'installazione predefinita è il seguente:

    C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

+ Se si usa Visual Studio 2017 o Visual Studio 2015 con le estensioni di Python, è possibile eseguire `pip install` dalla finestra **ambienti Python** . Fare clic su **pacchetti**e nella casella di testo specificare il nome o il percorso del pacchetto da installare. Non è necessario digitare `pip install`, perché viene compilato automaticamente. 

    - Se il computer dispone di accesso a Internet, specificare il nome del pacchetto o l'URL di un pacchetto e di una versione specifici. 
    
    Ad esempio, per installare la versione di CNTK supportata per Windows e Python 3,5, specificare l'URL di download:`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - Se il computer non ha accesso a Internet, è necessario scaricare il file WHL prima di iniziare l'installazione. Specificare quindi il percorso e il nome del file locale. Ad esempio, incollare il percorso e il file seguenti per installare il file WHL scaricato dal sito:`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

Potrebbe essere richiesto di elevare le autorizzazioni per completare l'installazione.

Con l'avanzamento dell'installazione, è possibile visualizzare i messaggi di stato nella finestra del prompt dei comandi:

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>Passaggio 4. Caricare il pacchetto o le relative funzioni come parte dello script

Al termine dell'installazione, è possibile iniziare immediatamente a usare il pacchetto, come descritto nel passaggio successivo.

Per esempi di apprendimento approfondito con CNTK, vedere le esercitazioni seguenti: [API Python per CNTK](https://cntk.ai/pythondocs/tutorials.html)

Per usare le funzioni del pacchetto nello script, inserire l'istruzione standard `import <package_name>` nelle righe iniziali dello script:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>Elencare i pacchetti installati con conda

È possibile ottenere un elenco dei pacchetti installati in diversi modi. Ad esempio, è possibile visualizzare i pacchetti installati nelle finestre **ambienti Python** di Visual Studio.

Se si usa la riga di comando di Python, è possibile usare **PIP** o **conda** Package Manager, incluso nell'ambiente Anaconda Python aggiunto dal programma di installazione di SQL Server.

1. Passare a C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. Fare clic con il pulsante destro del mouse su **conda. exe** > **Esegui come amministratore**e immettere `conda list` per restituire un elenco di pacchetti installati nell'ambiente corrente.

1. Analogamente, fare clic con il pulsante destro del mouse su **PIP. exe** > **Esegui come amministratore**e immettere `pip list` per restituire le stesse informazioni. 

Per altre informazioni su **conda** e su come è possibile usarlo per creare e gestire più ambienti Python, vedere [gestione degli ambienti con conda](https://conda.io/docs/user-guide/tasks/manage-environments.html).

> [!Note]
> SQL Server installazione non aggiunge PIP o conda al percorso di sistema e in un'istanza di SQL Server di produzione, mantenendo i file eseguibili non essenziali fuori percorso è una procedura consigliata. Tuttavia, per gli ambienti di sviluppo e di test, è possibile aggiungere la cartella Scripts alla variabile di ambiente PATH di sistema per eseguire il comando PIP e conda da qualsiasi percorso.
