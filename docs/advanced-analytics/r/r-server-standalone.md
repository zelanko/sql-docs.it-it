---
title: Installazione Standalone R Server o Machine Learning Server - servizi di SQL Server Machine Learning
description: Panoramica introduttiva alla versione autonoma di R Server e Machine Learning Server nel programma di installazione di SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 47edd434445d57c5ca25373b5dc15fa328f94019
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642592"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server (Standalone) e Machine Learning Server (Standalone) in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server fornisce il supporto di installazione per un Server R autonomo o Machine Learning Server che viene eseguito indipendentemente da SQL Server. A seconda della versione di SQL Server, un server autonomo è una base di R open source e, possibilmente, Python, da sovrapporre con librerie ad alte prestazioni da Microsoft che aggiungono analitica predittiva e statistiche su larga scala. Librerie consentono anche le attività di apprendimento automatico con script in R o Python. 

In SQL Server 2016, questa funzionalità è detta **R Server (Standalone)** ed è solo R. In SQL Server 2017, bensì **Machine Learning Server (Standalone)** e include R e Python.  

> [!Note]
> Installato dal programma di installazione di SQL Server, è funzionalmente equivalente alle versioni non SQL personalizzata di un server autonomo [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), che supportano gli stessi scenari utente, tra cui l'esecuzione remota, servizi web e l'operazionalizzazione e la raccolta completa di librerie di R e Python.

## <a name="components"></a>Componenti

SQL Server 2016 è solo R. SQL Server 2017 supporta R e Python. La tabella seguente descrive le funzionalità di ogni versione.

| Componente | Descrizione |
|-----------|-------------|
| Pacchetti R | [**RevoScaleR** ](ref-r-revoscaler.md) è la libreria primaria per R scalabili con le funzioni per la manipolazione dei dati, trasformazione, visualizzazione e analisi.  <br/>[**MicrosoftML** ](ref-r-microsoftml.md) aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del sentiment, analisi delle immagini e analisi del testo. <br/>[**sqlRUtils** ](ref-r-sqlrutils.md) fornisce funzioni helper per l'inserimento di script R in una stored procedure T-SQL archiviate, la registrazione di una stored procedure con un database e l'esecuzione della stored procedure da un ambiente di sviluppo R.<br/>[**mrsdeploy** ](operationalization-with-mrsdeploy.md) offerte web distribuzione del servizio (in SQL Server 2017 solo). <br/>[**olapR** ](ref-r-olapr.md) di specificare le query MDX in R.|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) è distribuzione open source di Microsoft di R. Sono inclusi il pacchetto e dell'interprete. Usare sempre la versione di MRO in bundle nel programma di installazione. |
| Strumenti R | Prompt dei comandi e le finestre della console R sono gli strumenti standard in una distribuzione di R. Trovare in \Programmi\Microsoft SQL Server\140\R_SERVER\bin\x64. |
| Esempi di R e gli script |  Pacchetti open source di R e RevoScaleR includono set di dati incorporato in modo che è possibile creare ed eseguire lo script usando i dati pre-installati. La ricerca di essi in \Programmi\Microsoft SQL Server\140\R_SERVER\library\datasets e \library\RevoScaleR. |
| Pacchetti Python | [**revoscalepy** ](../python/ref-py-revoscalepy.md) è la libreria primaria per Python scalabile con funzioni di manipolazione dei dati, trasformazione, visualizzazione e analisi. <br/>[**microsoftml** ](../python/ref-py-microsoftml.md) aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del sentiment, analisi delle immagini e analisi del testo.  |
| Strumenti Python | Lo strumento da riga di comando di Python predefinito è utile per test ad hoc e attività. Trovare lo strumento in \Programmi\Microsoft SQL Server\140\PYTHON_SERVER\python.exe. |
| Anaconda | Anaconda è una distribuzione open source di Python e i pacchetti essenziali. |
| Gli script ed esempi di Python | Come con R, Python include set di dati incorporato e gli script. Trovare i dati revoscalepy \Programmi\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelli con training preliminare in R e Python | I modelli con training preliminare vengono creati per casi d'uso specifici e gestiti per il team di progettazione di analisi scientifica dei dati in Microsoft. È possibile usare i modelli con training preliminare come-consiste nell'assegnare un punteggio del sentiment negativo positivo in testo o funzionalità vengono rilevati in immagini usando nuovi input di dati fornito. I modelli con training preliminare sono supportati e utilizzabile in un server autonomo, ma non è possibile installarli tramite l'installazione di SQL Server. Per altre informazioni, vedere [Install pretrained modelli di machine learning in SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-a-standalone-server"></a>Uso di un server autonomo

In genere, gli sviluppatori di R e Python scegliere un server autonomo per spostare oltre ai vincoli di memoria e l'elaborazione dell'open source R e Python. Librerie di R e Python in esecuzione in un server autonomo possono caricare ed elaborare grandi quantità di dati su più core e aggregare i risultati in un singolo output consolidato. Le funzioni ad alte prestazioni, sono progettate per maggiore scalabilità e utilità: recapito di analitica predittiva, modellazione statistica, visualizzazioni dei dati e avanguardia algoritmi di machine learning in un prodotto commerciale server progettato e supportato da Microsoft.

Come server indipendenti disaccoppiati da SQL Server, viene configurato l'ambiente R e Python, protetto e a cui si accede usando il sistema operativo sottostante e strumenti standard forniti con il server autonomo, non SQL Server. Non vi è alcun supporto predefinito per i dati relazionali di SQL Server. Se si desidera usare dati di SQL Server, è possibile creare gli oggetti origine dati e le connessioni come si farebbe per qualsiasi client.

A complemento di SQL Server, un server autonomo è utile come un potente ambiente di sviluppo anche se è necessario computing locali e remoti. I pacchetti R e Python in un server autonomo sono identici a quelli forniti con un'installazione del motore di database, che consente la portabilità del codice e [cambio di contesto di calcolo](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

## <a name="how-to-get-started"></a>Come iniziare a usare

Iniziare con il programma di installazione, collegare i file binari dello strumento di sviluppo preferito e scrivere il primo script.

### <a name="step-1-install-the-software"></a>Passaggio 1: Installare il software

Installare una di queste versioni:

+ [Machine Learning Server (standalone) di SQL Server 2017](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (Standalone) - solo R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Passaggio 2: Configurare uno strumento di sviluppo

In un server autonomo, è comune a lavorare in locale tramite una soluzione di sviluppo installato nello stesso computer.

+ [Configurare gli strumenti R](set-up-a-data-science-client.md)
+ [Configurare gli strumenti Python](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>Passaggio 3: Scrivere il primo script

Scrivere script R o Python usando funzioni di RevoScaleR e revoscalepy di algoritmi di machine learning.
  
  + [Esplorare R e in 25 funzioni RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): Iniziare con i comandi R di base e quindi procedere con le funzioni analitiche distribuibili RevoScaleR che forniscono prestazioni elevate e scalabilità per le soluzioni R. Include versioni parallelizzabili di molti dei più diffusi pacchetti di modellazione R, tra cui clustering K-Means, alberi delle decisioni e foreste delle decisioni, nonché strumenti per la modifica dei dati.

  + [Guida introduttiva: Un esempio di classificazione binaria con il pacchetto Python microsoftml](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): Creare un modello di classificazione binaria usando le funzioni di microsoftml e il set di dati noto esempio breast cancer.

Scegliere il linguaggio migliore per l'attività. R è ideale per i calcoli statistici difficili da implementare tramite SQL. Per le operazioni sui dati basata su set sfrutta la potenza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ottenere prestazioni ottimali. Usare il motore di database in memoria per i calcoli molto veloci su colonne.

### <a name="step-4-operationalize-your-solution"></a>Passaggio 4: Rendere operative le soluzioni

Server autonomi è possono usare la [operazionalizzazione](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) funzionalità del non-SQL-marchio [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). È possibile configurare un server autonomo per l'operazionalizzazione, che offre questi vantaggi: distribuire e ospitare il codice come servizi web, Esegui la diagnostica, capacità del servizio web di test.

### <a name="step-5-maintain-your-server"></a>Passaggio 5: Gestire il server

SQL Server rilascia gli aggiornamenti cumulativi a intervalli regolari. Applicazione degli aggiornamenti cumulativi aggiunge miglioramenti funzionali e sicurezza per un'installazione esistente. 

Sono disponibili le descrizioni delle funzionalità nuove o modificate nel [download di file CAB](../install/sql-ml-cab-downloads.md) articolo e nelle pagine web per [gli aggiornamenti cumulativi di SQL Server 2016](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) e [gli aggiornamenti cumulativi di SQL Server 2017 ](https://support.microsoft.com/help/4047329). 

Per altre informazioni su come applicare gli aggiornamenti a un'istanza esistente, vedere [applicare gli aggiornamenti](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) nelle istruzioni di installazione.

## <a name="see-also"></a>Vedere anche

 [Installare R Server (Standalone) o Machine Learning Server (Standalone)](../install/sql-machine-learning-standalone-windows-install.md)

