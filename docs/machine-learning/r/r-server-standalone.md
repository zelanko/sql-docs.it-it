---
title: Informazioni su Machine Learning Server o R Server autonomo
description: Informazioni sulle differenze tra R Server autonomo e Machine Learning Server nella configurazione di SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/13/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 67cdc278387de1faef999aa67543ec73c021bc41
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489741"
---
# <a name="what-are-standalone-machine-learning-server-or-r-server-in-sql-server"></a>Informazioni su Machine Learning Server o R Server autonomo in SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

SQL Server fornisce il supporto dell'installazione per un'istanza di R Server o Machine Learning Server autonomo eseguito indipendentemente da SQL Server. A seconda della versione di SQL Server, un server autonomo si basa su R open source ed eventualmente su Python, a cui si sovrappongono librerie a prestazioni elevate di Microsoft che aggiungono caratteristiche di analisi statistica e predittiva su larga scala. Le librerie abilitano anche le attività di Machine Learning con script R o Python. 

In SQL Server 2016 questa funzionalità è denominata **R Server (Standalone)** ed è solo R. In SQL Server 2017 questa funzionalità è denominata **Machine Learning Server (Standalone)** e include sia R che Python.  

> [!Note]
> Essendo installato dal programma di installazione di SQL Server, un server autonomo è equivalente, dal punto di vista funzionale, alle versioni non SQL di [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server) e supporta gli stessi scenari utente, tra cui esecuzione remota, operazionalizzazione e servizi Web, e la raccolta completa di librerie R e Python.

## <a name="components"></a>Componenti

SQL Server 2016 è solo R. SQL Server 2017 supporta R e Python. La tabella seguente descrive le caratteristiche di ogni versione.

| Componente | Descrizione |
|-----------|-------------|
| Pacchetti R | [**RevoScaleR**](ref-r-revoscaler.md) è la libreria primaria per R scalabile con funzioni per la manipolazione, la trasformazione, la visualizzazione e l'analisi dei dati.  <br/>[**MicrosoftML**](ref-r-microsoftml.md) aggiunge algoritmi di Machine Learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi del sentiment. <br/>[**sqlRUtils**](ref-r-sqlrutils.md) fornisce funzioni helper per inserire gli script R in una stored procedure T-SQL, registrare una stored procedure con un database ed eseguirla da un ambiente di sviluppo R.<br/>[**olapR**](ref-r-olapr.md) server a specificare le query MDX in R.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) è la distribuzione di R open source di Microsoft. Il pacchetto e l'interprete sono inclusi. Usare sempre la versione di MRO aggregata nel programma di installazione. |
| Strumenti R | I prompt dei comandi e le finestre della console R sono strumenti standard in una distribuzione R. Sono disponibili in \Programmi\Microsoft SQL Server\140\R_SERVER\bin\x64. |
| Esempi e script R |  Poiché i pacchetti R e RevoScaleR open source includono set di dati predefiniti, è possibile creare ed eseguire lo script usando i dati preinstallati. Sono disponibili in \Programmi\Microsoft SQL Server\140\R_SERVER\library\datasets e \library\RevoScaleR. |
| Pacchetti Python | [**revoscalepy**](../python/ref-py-revoscalepy.md) è la libreria primaria per Python scalabile con funzioni per la manipolazione, la trasformazione, la visualizzazione e l'analisi dei dati. <br/>[**microsoftml**](../python/ref-py-microsoftml.md) aggiunge algoritmi di Machine Learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi del sentiment.  |
| Strumenti Python | Lo strumento da riga di comando Python predefinito è utile per test e attività ad hoc. Lo strumento è disponibile in \Programmi\Microsoft SQL Server\140\PYTHON_SERVER\python.exe. |
| Anaconda | Anaconda è una distribuzione open source di Python e di pacchetti essenziali. |
| Esempi e script Python | Come R, Python include set di dati e script predefiniti. I dati di revoscalepy sono disponibili in \Programmi\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelli con training preliminare in R e Python | I modelli con training preliminare vengono creati per casi d'uso specifici e gestiti dal team di tecnici di data science di Microsoft. È possibile usare i modelli con training preliminare così some sono per valutare con un punteggio il sentiment positivo-negativo nel testo o rilevare le caratteristiche nelle immagini, usando i nuovi input di dati forniti. I modelli con training preliminare sono supportati e utilizzabili in un server autonomo, ma non è possibile installarli tramite il programma di installazione di SQL Server. Per altre informazioni, vedere [Installare modelli di Machine Learning con training preliminare in SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-a-standalone-server"></a>Uso di un server autonomo

Gli sviluppatori R e Python scelgono in genere un server autonomo per superare i vincoli di memoria ed elaborazione di R e Python open source. Le librerie R e Python eseguite su un server autonomo possono caricare ed elaborare grandi quantità di dati in più core e aggregare i risultati in un unico output consolidato. Le funzioni a prestazioni elevate sono progettate sia per la scalabilità che per l'utilità: offrono analisi predittiva, modellazione statistica, visualizzazioni di dati e algoritmi di Machine Learning all'avanguardia in un prodotto server commerciale progettato e supportato da Microsoft.

Come server indipendente, separato da SQL Server, l'ambiente R e Python viene configurato e protetto ed è accessibile tramite il sistema operativo sottostante e gli strumenti standard disponibili nel server autonomo, non SQL Server. Non è disponibile alcun supporto predefinito per i dati relazionali di SQL Server. Per usare i dati di SQL Server, è possibile creare oggetti di origine dati e connessioni come da qualsiasi client.

A complemento di SQL Server, un server autonomo è utile anche come ambiente avanzato di sviluppo se è necessaria l'elaborazione sia locale che remota. I pacchetti R e Python in un server autonomo sono uguali a quelli forniti con un'installazione del motore di database, consentendo la portabilità del codice e il [cambio del contesto di calcolo](/machine-learning-server/r/concept-what-is-compute-context).

## <a name="how-to-get-started"></a>Attività iniziali

Iniziare con il programma di installazione, associare i file binari allo strumento di sviluppo preferito e scrivere il primo script.

### <a name="step-1-install-the-software"></a>Passaggio 1: installare il software

Installare una delle due versioni seguenti:

+ [Machine Learning Server (Standalone) per SQL Server 2017](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (Standalone) - Solo R](../install/sql-machine-learning-standalone-windows-install.md?view=sql-server-2016&preserve-view=true)

### <a name="step-2-configure-a-development-tool"></a>Passaggio 2: configurare uno strumento di sviluppo

In un server autonomo è normale lavorare in locale usando uno strumento di sviluppo installato nello stesso computer.

+ [Configurare gli strumenti R](set-up-a-data-science-client.md)
+ [Configurare gli strumenti Python](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>Passaggio 3: Scrivere il primo script

Scrivere uno script R o Python usando le funzioni di RevoScaleR, revoscalepy e gli algoritmi di Machine Learning.
  
  + [Esplorare R e RevoScaleR in 25 funzioni](/machine-learning-server/r/tutorial-r-to-revoscaler): iniziare con i comandi R di base e quindi passare alle funzioni analitiche distribuibili di RevoScaleR che offrono prestazioni e scalabilità elevate per le soluzioni R. Include versioni parallelizzabili di molti dei più diffusi pacchetti di modellazione R, tra cui clustering K-Means, alberi delle decisioni e foreste delle decisioni, nonché strumenti per la modifica dei dati.

  + [Avvio rapido: Esempio di classificazione binaria con il pacchetto microsoftml per Python](/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): creare un modello di classificazione binaria usando le funzioni di microsoftml e il noto set di dati relativo al tumore del seno.

Scegliere il linguaggio migliore per l'attività. R è ideale per i calcoli statistici che sono difficili da implementare tramite SQL. Per le operazioni sui dati basate su set, sfruttare la potenza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ottenere prestazioni ottimali. Usare il motore di database in memoria per calcoli molto veloci sulle colonne.

### <a name="step-4-operationalize-your-solution"></a>Passaggio 4: Rendere operativa la soluzione

I server autonomi possono usare le caratteristiche di [operazionalizzazione](/machine-learning-server/what-is-operationalization) di [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server) non SQL. È possibile configurare un server autonomo per l'operazionalizzazione, che offre questi vantaggi: distribuzione e hosting del codice come servizi Web, esecuzione della diagnostica, test della capacità dei servizi Web.

### <a name="step-5-maintain-your-server"></a>Passaggio 5: Gestire il server

SQL Server rilascia periodicamente aggiornamenti cumulativi. L'applicazione degli aggiornamenti cumulativi apporta miglioramenti della sicurezza e delle caratteristiche a un'installazione esistente. 

Le descrizioni delle caratteristiche nuove o modificate sono disponibili nell'articolo [Download di CAB](../install/sql-ml-cab-downloads.md) e nelle pagine Web degli [aggiornamenti cumulativi di SQL Server 2016](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) e degli [aggiornamenti cumulativi di SQL Server 2017](https://support.microsoft.com/help/4047329). 

Per altre informazioni su come applicare gli aggiornamenti a un'istanza esistente, vedere [Applicare gli aggiornamenti](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) nelle istruzioni di installazione.

## <a name="see-also"></a>Vedere anche

 [Installare R Server (Standalone) o Machine Learning Server (Standalone)](../install/sql-machine-learning-standalone-windows-install.md)
