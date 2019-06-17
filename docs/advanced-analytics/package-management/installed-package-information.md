---
title: Librerie di pacchetti R e Python - servizi di SQL Server Machine Learning predefinite
description: Pacchetti R e Python installati con SQL Server per R Services, R Server, Machine Learning Services (In-Database) e Machine Learning Server (Standalone)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3126872e3333383d0cea53f38b3cfd06be86b704
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141400"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Pacchetti predefiniti R e Python in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo elenca i pacchetti R e Python installati con SQL Server e dove trovare la libreria di pacchetti.  

## <a name="r-package-list-for-sql-server"></a>Elenco dei pacchetti R per SQL Server

I pacchetti R vengono installati con [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) e [Machine Learning Services di SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) quando si seleziona la funzionalità R durante l'installazione. 

|Pacchetti         | 2016 | 2017 | Descrizione |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | Utilizzato per contesti di calcolo remoti, streaming, l'esecuzione parallela delle funzioni rx per l'importazione dei dati e trasformazione, modellazione, visualizzazione e analisi. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |Utilizzato per l'inclusione di script R nelle stored procedure. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.2 | Consente di aggiungere algoritmi di machine learning in R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9.2 | Utilizzato per la scrittura di istruzioni MDX in R. |

MicrosoftML e olapR sono disponibili per impostazione predefinita in Machine Learning Services di SQL Server 2017. In un'istanza di SQL Server 2016 R Services, è possibile aggiungere questi pacchetti tramite un [aggiornamento del componente](../install/upgrade-r-and-python.md). Un aggiornamento del componente ottiene anche le versioni più recenti dei pacchetti (ad esempio, le versioni più recenti di RevoScaleR includono funzioni per la gestione dei pacchetti in SQL Server).

## <a name="python-package-list-for-sql-server"></a>Elenco dei pacchetti Python per SQL Server

I pacchetti Python sono disponibili solo in SQL Server 2017 quando si installa [Machine Learning Services di SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) e selezionare la funzionalità di Python.

| Pacchetti         | 2017    |  Descrizione |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | Utilizzato per contesti di calcolo remoti, streaming, l'esecuzione parallela delle funzioni rx per l'importazione dei dati e trasformazione, modellazione, visualizzazione e analisi. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | Aggiunge gli algoritmi di machine learning in Python. |

## <a name="open-source-r-in-your-installation"></a>R open source nell'installazione

Supporto di R include open source sono in modo che è possibile chiamare le funzioni R di base e installare pacchetti aggiuntivi di terze parti e open source. Supporto del linguaggio R include funzionalità di base, ad esempio **base**, **stats**, **utils**e così via. Un'installazione di base di R include anche numerosi set di dati di esempio e gli strumenti R standard, ad esempio **RGui** (un semplice editor interattivo) e **RTerm** (un prompt dei comandi R). 

La distribuzione di R open source inclusi nell'installazione risulta [Microsoft R aprire (MRO)](https://mran.microsoft.com/open). MRO aggiunge valore a R di base, includendo ulteriori pacchetti open source, ad esempio la [Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library).

La tabella seguente riepiloga le versioni di R forniti da MRO usando il programma di installazione di SQL Server.

|Versione             | Versione di R       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

Si deve mai manualmente sovrascrivere la versione di R installato dal programma di installazione di SQL Server con le versioni più recenti sul web. I pacchetti R di Microsoft si basano su versioni specifiche di R. modificare l'installazione potrebbe destabilizzare il.

## <a name="open-source-python-in-your-installation"></a>Python open source nell'installazione

SQL Server 2017 aggiunge i componenti Python. Quando si seleziona l'opzione di linguaggio Python, viene installata la distribuzione Anaconda 4.2. Oltre alle librerie di codice Python, l'installazione standard include i dati di esempio, gli unit test e script di esempio. 

SQL Server 2017 Machine Learning è la prima versione di R e Python supportano.

|Versione             | Anaconda versione| Pacchetti di Microsoft    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning Services  | 4.2 su Python 3.5 | revoscalepy, microsoftml |

Si deve mai manualmente sovrascrivere la versione di Python installato dal programma di installazione di SQL Server con le versioni più recenti sul web. I pacchetti Python di Microsoft si basano su versioni specifiche di Anaconda. Modificare l'installazione potrebbe destabilizzare il.

## <a name="component-upgrades"></a>Aggiornamenti dei componenti

Dopo l'installazione iniziale, pacchetti R e Python sono aggiornati attraverso i service pack e gli aggiornamenti cumulativi, ma gli aggiornamenti di versione completo sono solo possibili grazie *associazione* ai criteri di supporto del ciclo di vita moderni. Associazione modifica il modello di manutenzione. Per impostazione predefinita, dopo un'installazione iniziale, i pacchetti R vengono aggiornati tramite service pack e gli aggiornamenti cumulativi. I pacchetti aggiuntivi e aggiornamenti di versione completo dei componenti di R di base sono possibili solo tramite gli aggiornamenti del prodotto (da SQL Server 2016 a SQL Server 2017) o mediante l'associazione R il supporto a Microsoft Machine Learning Server. Per altre informazioni, vedere [i componenti di eseguire l'aggiornamento di R e Python in SQL Server](../install/upgrade-r-and-python.md).

## <a name="package-library-location"></a>Percorso del pacchetto della libreria

Quando si installa l'apprendimento automatico con SQL Server, una libreria di pacchetti singolo viene creata a livello di istanza per ogni lingua da installare. In Windows, la libreria di istanza è una cartella protetta registrata con SQL Server.

Tutti i script o codice che viene eseguito nel database in SQL Server deve caricare le funzioni dalla libreria di istanza. SQL Server non è possibile accedere ai pacchetti installati in altre librerie. Questo vale per i client remoti. Quando ci si connette al server da un client remoto, qualsiasi codice R o Python che si desidera eseguire nel contesto di calcolo server può utilizzare solo i pacchetti installati nella libreria di istanza.

Per proteggere le risorse di server, la libreria di istanza predefinito può essere modificata solo da un amministratore del computer. Se non si è il proprietario del computer, è necessario ottenere l'autorizzazione dell'amministratore per installare i pacchetti in questa raccolta. 

#### <a name="file-path-for-in-database-engine-instances"></a>Percorso del file per le istanze del motore In-Database

Nella tabella seguente mostra il percorso del file di R e Python per la versione e del database le combinazioni di istanza del motore. MSSQL13 indica SQL Server 2016 ed è solo R. MSSQL14 indica SQL Server 2017 e sono presenti cartelle di R e Python. 

I percorsi dei file includono anche i nomi delle istanze. SQL Server viene installato [le istanze del motore di database](../../database-engine/configure-windows/database-engine-instances-sql-server.md) come istanza predefinita (MSSQLSERVER) o come istanza denominata definita dall'utente. Se SQL Server viene installato come istanza denominata, verrà visualizzato tale nome aggiunto come indicato di seguito: `MSSQL13.<instance_name>`.

|Versione e lingua  | Percorso predefinito|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 con R|C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 with Python |C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site-pacchetti |


#### <a name="file-path-for-standalone-server-installations"></a>Percorso del file per le installazioni di server autonomi

La tabella seguente elenca i percorsi predefiniti dei file binari quando è installato SQL Server 2016 R Server (Standalone) o un server di Machine Learning Server (Standalone) di SQL Server 2017. 

|Version| Installazione|Percorso predefinito|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning Server con R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Server, con Python |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Se si trova altre cartelle con nomi simili sottocartella e file, probabile che hanno un'installazione autonoma di Microsoft R Server o [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/). Questi prodotti server dispongono di percorsi (vale a dire, c:\Programmi\Microsoft Files\Microsoft\R Server\R_SERVER o c:\programmi\microsoft\ml SERVER\R_SERVER) e i programmi di installazione diversi. Per altre informazioni, vedere [installare Server Learning macchina per Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) oppure [installare R Server 9.1 per Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="next-steps"></a>Passaggi successivi

+ [Ottenere informazioni sui pacchetti](installed-package-information.md)
+ [Installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Abilitare la gestione remota dei pacchetti R](../r/r-package-how-to-enable-or-disable.md)
+ [Funzioni RevoScaleR per la gestione dei pacchetti R](../r/use-revoscaler-to-manage-r-packages.md)
+ [Sincronizzazione dei pacchetti R](../r/package-install-uninstall-and-sync.md)
+ [miniCRAN per il repository locale di pacchetti R](../r/create-a-local-package-repository-using-minicran.md)
