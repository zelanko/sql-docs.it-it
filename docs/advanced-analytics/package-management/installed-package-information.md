---
title: Librerie di pacchetti R e Python predefinite
description: Pacchetti r e Python installati da SQL Server per R Services, R Server, Machine Learning Services (in-database) e Machine Learning Server (standalone)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f6cf66725ae15b2b738c020258142576ede734ec
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345076"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Pacchetti R e Python predefiniti in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo elenca i pacchetti R e Python installati con SQL Server e dove trovare la libreria di pacchetti.  

## <a name="r-package-list-for-sql-server"></a>Elenco di pacchetti R per SQL Server

I pacchetti r vengono installati con [SQL Server 2016 r Services](../install/sql-r-services-windows-install.md) e [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) quando si seleziona la funzionalità r durante l'installazione. 

|Pacchetti         | 2016 | 2017 | Descrizione |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9,2 | Usato per contesti di calcolo remoti, streaming, esecuzione parallela di funzioni RX per l'importazione e la trasformazione dei dati, la modellazione, la visualizzazione e l'analisi. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9,2 |Usato per includere script R nelle stored procedure. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9,2 | Aggiunge gli algoritmi di Machine Learning in R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9,2 | Usato per la scrittura di istruzioni MDX in R. |

MicrosoftML e olapr sono disponibili per impostazione predefinita in SQL Server 2017 Machine Learning Services. In un'istanza di SQL Server 2016 R Services è possibile aggiungere questi pacchetti tramite un [aggiornamento del componente](../install/upgrade-r-and-python.md). L'aggiornamento di un componente consente inoltre di ottenere le versioni più recenti dei pacchetti (ad esempio, le versioni più recenti di RevoScaleR includono funzioni per la gestione dei pacchetti in SQL Server).

## <a name="python-package-list-for-sql-server"></a>Elenco di pacchetti Python per SQL Server

I pacchetti Python sono disponibili solo in SQL Server 2017 quando si installa [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) e si seleziona la funzionalità Python.

| Pacchetti         | 2017    |  Descrizione |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9,2 | Usato per contesti di calcolo remoti, streaming, esecuzione parallela di funzioni RX per l'importazione e la trasformazione dei dati, la modellazione, la visualizzazione e l'analisi. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9,2 | Aggiunge algoritmi di Machine Learning in Python. |

## <a name="open-source-r-in-your-installation"></a>R Open Source nell'installazione

Il supporto r include Open Source per poter chiamare le funzioni R di base e installare altri pacchetti open source e di terze parti. Il supporto del linguaggio R include funzionalità principali, ad esempio **base**, **statistiche**, **utils**e altre. Un'installazione di base di R include anche numerosi set di impostazioni di esempio e strumenti R standard come **RGui** (un editor interattivo leggero) e **RTerm** (un prompt dei comandi di r). 

La distribuzione di R open source inclusa nell'installazione è [Microsoft R Open (riparazione)](https://mran.microsoft.com/open). Con l'aggiunta di un valore a R di base è possibile includere pacchetti open source aggiuntivi, ad esempio la [libreria del kernel matematico di Intel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

La tabella seguente riepiloga le versioni di R fornite da riparazione tramite SQL Server installazione.

|Versione             | Versione di R       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

Non è mai necessario sovrascrivere manualmente la versione di R installata dal programma di installazione di SQL Server con le versioni più recenti sul Web. I pacchetti Microsoft R sono basati su versioni specifiche di R. la modifica dell'installazione potrebbe destabilizzarla.

## <a name="open-source-python-in-your-installation"></a>Python Open Source nell'installazione

SQL Server 2017 aggiunge componenti Python. Quando si seleziona l'opzione relativa al linguaggio Python, è installata la distribuzione Anaconda 4,2. Oltre alle librerie di codice Python, l'installazione standard include dati di esempio, unit test e script di esempio. 

SQL Server 2017 Machine Learning è la prima versione con supporto sia per R che per Python.

|Versione             | Versione Anaconda| Pacchetti Microsoft    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning Services  | 4,2 su Python 3,5 | revoscalepy, microsoftml |

Non è mai necessario sovrascrivere manualmente la versione di Python installata dal programma di installazione di SQL Server con le versioni più recenti sul Web. I pacchetti Microsoft Python sono basati su versioni specifiche di Anaconda. La modifica dell'installazione potrebbe destabilizzarla.

## <a name="component-upgrades"></a>Aggiornamenti componenti

Dopo un'installazione iniziale, i pacchetti R e Python vengono aggiornati tramite i Service Pack e gli aggiornamenti cumulativi, ma gli aggiornamenti completi della versione sono possibili solo mediante l' *associazione* al criterio di supporto del ciclo di vita moderno. Il binding modifica il modello di manutenzione. Per impostazione predefinita, dopo un'installazione iniziale, i pacchetti R vengono aggiornati tramite i Service Pack e gli aggiornamenti cumulativi. Pacchetti aggiuntivi e aggiornamenti completi della versione dei componenti R di base sono possibili solo tramite aggiornamenti del prodotto (da SQL Server 2016 a SQL Server 2017) o mediante l'associazione del supporto R al Microsoft Machine Learning Server. Per altre informazioni, vedere [aggiornare i componenti R e Python in SQL Server](../install/upgrade-r-and-python.md).

## <a name="package-library-location"></a>Percorso libreria pacchetti

Quando si installa Machine Learning con SQL Server, viene creata una singola libreria di pacchetti a livello di istanza per ogni lingua installata. In Windows la libreria di istanze è una cartella protetta registrata con SQL Server.

Tutti gli script o il codice eseguito nel database in SQL Server devono caricare le funzioni dalla libreria di istanze. SQL Server non è in grado di accedere ai pacchetti installati in altre librerie. Questo vale anche per i client remoti. Quando ci si connette al server da un client remoto, qualsiasi codice R o Python che si vuole eseguire nel contesto di calcolo del server può usare solo i pacchetti installati nella libreria di istanze.

Per proteggere le risorse del server, la libreria di istanze predefinita può essere modificata solo da un amministratore del computer. Se non si è il proprietario del computer, potrebbe essere necessario ottenere l'autorizzazione da un amministratore per installare i pacchetti in questa libreria. 

#### <a name="file-path-for-in-database-engine-instances"></a>Percorso del file per le istanze del motore di database

La tabella seguente illustra il percorso dei file di R e Python per le combinazioni di versioni e istanze del motore di database. MSSQL13 indica SQL Server 2016 ed è solo R. MSSQL14 indica SQL Server 2017 e contiene le cartelle R e Python. 

I percorsi di file includono anche nomi di istanza. SQL Server installa le [istanze del motore di database](../../database-engine/configure-windows/database-engine-instances-sql-server.md) come istanza predefinita (MSSQLSERVER) o come istanza denominata definita dall'utente. Se SQL Server viene installato come un'istanza denominata, il nome verrà aggiunto come segue: `MSSQL13.<instance_name>`.

|Versione e lingua  | Percorso predefinito|
|----------------------|------------|
| SQL Server 2016 |C:\Programmi\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 con R|C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 con Python |C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages |


#### <a name="file-path-for-standalone-server-installations"></a>Percorso file per le installazioni di server autonomi

Nella tabella seguente sono elencati i percorsi predefiniti dei file binari quando è installato SQL Server 2016 R Server (autonomo) o SQL Server 2017 Machine Learning Server Server (standalone). 

|Version| Installazione|Percorso predefinito|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Programmi\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning Server con R |C:\Programmi\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Server con Python |C:\Programmi\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Se si trovano altre cartelle con nomi e file di sottocartelle simili, è probabile che si disponga di un'installazione autonoma di Microsoft R Server o [Machine Learning server](https://docs.microsoft.com/machine-learning-server/). Questi prodotti server dispongono di programmi di installazione e percorsi diversi (vale a dire, C:\Program Files\Microsoft\R Server\R_SERVER o C:\Program C:\programmi\microsoft\ml SERVER\R_SERVER). Per ulteriori informazioni, vedere [install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) o [Install R Server 9,1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="next-steps"></a>Passaggi successivi

+ [Ottenere informazioni sui pacchetti](installed-package-information.md)
+ [Installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Abilitare la gestione remota dei pacchetti R](../r/r-package-how-to-enable-or-disable.md)
+ [Funzioni RevoScaleR per la gestione dei pacchetti R](../r/use-revoscaler-to-manage-r-packages.md)
+ [Sincronizzazione dei pacchetti R](../r/package-install-uninstall-and-sync.md)
+ [miniCRAN per il repository locale di pacchetti R](../r/create-a-local-package-repository-using-minicran.md)
