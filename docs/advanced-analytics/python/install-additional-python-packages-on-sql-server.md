---
title: Installare nuovi pacchetti di linguaggio Python - SQL Server Machine Learning
description: Aggiungere nuovi pacchetti Python per SQL Server 2017 Machine Learning Services (In-Database) e Machine Learning Server (Standalone).
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: fc038f94fc24b8c0f795efc18c62acc1656877a7
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432314"
---
# <a name="install-new-python-packages-on-sql-server"></a>Installare nuovi pacchetti di Python in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive come installare nuovi pacchetti di Python in un'istanza di SQL Server 2017 Machine Learning Services. In generale, il processo per l'installazione di nuovi pacchetti è simile a quella in un ambiente di Python standard. Tuttavia, alcuni passaggi aggiuntivi sono necessari se il server non ha una connessione a internet.

Per altre informazioni sui percorsi di installazione e posizione del pacchetto, vedere [ottenere R o Python informazioni sul pacchetto](../r/determine-which-packages-are-installed-on-sql-server.md).

## <a name="prerequisites"></a>Prerequisiti

+ [SQL Server 2017 Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md) con l'opzione di linguaggio Python. 

+ I pacchetti devono essere Python 3.5 conforme ed eseguiti su Windows. 

+ Accesso amministrativo al server è necessario installare i pacchetti.

## <a name="considerations"></a>Considerazioni

Prima di aggiungere i pacchetti, valutare se il pacchetto è una scelta ideale per l'ambiente di SQL Server. In genere un server di database è una risorsa condivisa da tenere conto di più carichi di lavoro. Se si aggiungono pacchetti di inserire una quantità eccessiva utilizzo computazionale elevato sul server, le prestazioni ne risentiranno. 

Inoltre, alcuni pacchetti Python più diffusi (ad esempio Flask) eseguono le attività, ad esempio lo sviluppo web, che sono più adatte per un ambiente autonomo. È consigliabile usare Python nel database per le attività che traggono vantaggio da una stretta integrazione con il motore di database, ad esempio di apprendimento automatico, piuttosto che le attività che è sufficiente eseguire query sul database.

I server di database sono bloccati di frequente. In molti casi, l'accesso a Internet è bloccato interamente. Per i pacchetti con un lungo elenco di dipendenze, è necessario identificare in anticipo queste dipendenze ed essere disposti a installare manualmente ognuno di essi.

## <a name="add-a-new-python-package"></a>Aggiungere un nuovo pacchetto di Python

In questo esempio si presuppone che si desidera installare un nuovo pacchetto direttamente nel computer SQL Server.

Installazione dei pacchetti avviene per ogni istanza. Se si dispone di più istanze di servizi di Machine Learning, è necessario aggiungere il pacchetto da ciascuno di essi.

Viene installato in questo esempio il pacchetto [CNTK](https://docs.microsoft.com/cognitive-toolkit/), un framework per l'apprendimento avanzato da Microsoft che supporta la personalizzazione, training e la condivisione di tipi diversi di reti neurali.

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>Passaggio 1. Scaricare la versione di Windows del pacchetto Python

+ Se si siano installando i pacchetti Python in un server senza accesso a internet, è necessario scaricare il file con estensione WHL in un computer diverso e quindi copiarlo nel server.

    In un computer separato, ad esempio, è possibile scaricare il file con estensione WHL da questo sito [ https://cntk.ai/PythonWheel/CPU-Only ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl), quindi copiare il file `cntk-2.1-cp35-cp35m-win_amd64.whl` in una cartella locale nel computer SQL Server.

+ SQL Server 2017 Usa Python 3.5. 

> [!IMPORTANT]
> Assicurarsi di ottenere la versione di Windows del pacchetto. Se il file termina con GZ, probabilmente non è la versione corretta.

Questa pagina contiene download per più piattaforme e per più versioni di Python: [Configurare CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>Passaggio 2. Aprire un prompt dei comandi di Python

Individuare il percorso di libreria Python predefinito utilizzato da SQL Server. Se è stato installato più istanze, individuare la cartella PYTHON_SERVICE per l'istanza in cui si desidera aggiungere il pacchetto.

Ad esempio, se è stato installato Machine Learning Services utilizzando le impostazioni predefinite e apprendimento automatico è abilitato nell'istanza predefinita, il percorso sarà come segue:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Aprire il prompt dei comandi di Python associato all'istanza.

> [!TIP]
> Per il futuro, debug e test, è possibile configurare un ambiente Python specifico per la libreria di istanza.

### <a name="step-3-install-the-package-using-pip"></a>Passaggio 3. Installare il pacchetto tramite pip

+ Se sei abituato a usare la riga di comando di Python, usare PIP.exe per installare nuovi pacchetti. È possibile trovare il **pip** programma di installazione nel `Scripts` sottocartella. 

  Il programma di installazione di SQL Server non aggiunge gli script nel percorso di sistema. Se si verifica un errore che `pip` non è riconosciuto come comando interno o esterno, è possibile aggiungere la cartella degli script per la variabile di percorso in Windows.

  Il percorso completo del **script** cartella in un'installazione predefinita è il seguente:

    C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

+ Se si usa Visual Studio 2017 o Visual Studio 2015 con le estensioni di Python, è possibile eseguire `pip install` dal **ambienti Python** finestra. Fare clic su **pacchetti**e nella casella di testo, specificare il nome o il percorso del pacchetto da installare. Non è necessario digitare `pip install`; viene inserito automaticamente automaticamente. 

    - Se il computer abbia accesso a Internet, fornire il nome del pacchetto o l'URL di un pacchetto specifico e una versione. 
    
    Ad esempio, per installare la versione di CNTK supportato per Windows e Python 3.5, specificare l'URL di download: `https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - Se il computer non ha accesso a internet, è necessario scaricare il file con estensione WHL prima di iniziare l'installazione. Quindi, specificare il percorso file locale e il nome. Ad esempio, incollare il percorso e il file per installare il file con estensione WHL scaricato dal sito seguente: `"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

Potrebbe essere richiesto di elevare le autorizzazioni per completare l'installazione.

Durante l'installazione, è possibile visualizzare i messaggi di stato nella finestra del prompt dei comandi:

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>Passaggio 4. Caricare il pacchetto o le sue funzioni come parte dello script

Durante l'installazione è stata completata, è possibile immediatamente iniziare usando il pacchetto come descritto nel passaggio successivo.

Per esempi di apprendimento avanzato con CNTK, vedere queste esercitazioni: [API Python per CNTK](https://cntk.ai/pythondocs/tutorials.html)

Per usare le funzioni dal pacchetto nello script, inserire lo standard `import <package_name>` istruzione nelle righe iniziale dello script:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>Elenca i pacchetti installati tramite conda

Esistono diversi modi in cui è possibile ottenere un elenco dei pacchetti installati. Ad esempio, è possibile visualizzare i pacchetti installati nel **ambienti Python** windows di Visual Studio.

Se si usa la riga di comando di Python, è possibile usare **Pip** o nella **conda** Gestione pacchetti, inclusi con l'ambiente Anaconda Python aggiunto dal programma di installazione di SQL Server.

1. Passare a C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. Fare doppio clic su **conda.exe** > **Esegui come amministratore**, quindi immettere `conda list` per restituire un elenco dei pacchetti installati nell'ambiente corrente.

1. Analogamente, fare doppio clic su **pip.exe** > **Esegui come amministratore**, quindi immettere `pip list` per restituire le stesse informazioni. 

Per altre informazioni sulle **conda** e come è possibile usarlo per creare e gestire più ambienti Python, vedere [gestione degli ambienti con conda](https://conda.io/docs/user-guide/tasks/manage-environments.html).

> [!Note]
> Il programma di installazione di SQL Server non aggiunge Pip o Conda per il percorso di sistema e in un'istanza di SQL Server di produzione, mantenendo i file eseguibili non essenziali fuori del percorso è una procedura consigliata. Tuttavia, per gli ambienti di sviluppo e test, è possibile aggiungere la cartella degli script alla variabile di ambiente PATH di sistema per eseguire Pip e Conda sul comando da qualsiasi posizione.
