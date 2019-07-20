---
title: R Server autonomo o installazione Machine Learning Server
description: Panoramica introduttiva a R Server autonomo e Machine Learning Server nella configurazione SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: dphansen
ms.author: davidph
ms.openlocfilehash: f50049b1b93068748da84342d68ab6cb319c5d98
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344894"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server (autonomo) e Machine Learning Server (autonomo) in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server fornisce il supporto per l'installazione di un R Server autonomo o Machine Learning Server eseguito in modo indipendente da SQL Server. A seconda della versione SQL Server, un server autonomo ha una base di R Open Source e possibilmente Python, sovrapposto a librerie ad alte prestazioni di Microsoft che aggiungono analisi statistiche e predittive su larga scala. Le librerie abilitano anche le attività di Machine Learning scritte in R o Python. 

In SQL Server 2016 questa funzionalità è denominata **R Server (standalone)** ed è solo R. In SQL Server 2017, viene chiamato **Machine Learning Server (standalone)** e include sia R che Python.  

> [!Note]
> Come installato dal programma di installazione SQL Server, un server autonomo è funzionalmente equivalente alle versioni non SQL di [Microsoft Machine Learning server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), che supportano gli stessi scenari utente, tra cui l'esecuzione remota, la messa in funzione e il Web Servizi e la raccolta completa di librerie R e Python.

## <a name="components"></a>Componenti

SQL Server 2016 è solo R. SQL Server 2017 supporta R e Python. Nella tabella seguente vengono descritte le funzionalità di ciascuna versione.

| Componente | Descrizione |
|-----------|-------------|
| Pacchetti R | [**RevoScaleR**](ref-r-revoscaler.md) è la libreria primaria per R scalabile con funzioni per la manipolazione, la trasformazione, la visualizzazione e l'analisi dei dati.  <br/>[**MicrosoftML**](ref-r-microsoftml.md) aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi dei sentimenti. <br/>[**sqlRUtils**](ref-r-sqlrutils.md) fornisce funzioni di supporto per l'inserimento di script R in un stored procedure T-SQL, la registrazione di una stored procedure con un database e l'esecuzione del stored procedure da un ambiente di sviluppo r.<br/>[**mrsdeploy**](operationalization-with-mrsdeploy.md) offre la distribuzione del servizio Web (solo in SQL Server 2017). <br/>[**olapr**](ref-r-olapr.md) è per la specifica di query MDX in R.|
| Microsoft R Open (MRO) | [**Riparazione**](https://mran.microsoft.com/open) è una distribuzione open source di Microsoft di R. Il pacchetto e l'interprete sono inclusi. Usare sempre la versione di riparazione in bundle nel programma di installazione. |
| Strumenti R | Le finestre della console R e i prompt dei comandi sono strumenti standard in una distribuzione R. Trovarli in \Programmi\microsoft SQL Server\140\R_SERVER\bin\x64. |
| Esempi e script R |  I pacchetti R e RevoScaleR Open Source includono set di dati predefiniti, in modo che sia possibile creare ed eseguire script con dati preinstallati. Per cercarli, vedere \Programmi\microsoft SQL Server\140\R_SERVER\library\datasets e \library\RevoScaleR. |
| Pacchetti Python | [**revoscalepy**](../python/ref-py-revoscalepy.md) è la libreria primaria per Python scalabile con funzioni per la manipolazione, la trasformazione, la visualizzazione e l'analisi dei dati. <br/>[**microsoftml**](../python/ref-py-microsoftml.md) aggiunge algoritmi di machine learning per creare modelli personalizzati per l'analisi del testo, l'analisi delle immagini e l'analisi dei sentimenti.  |
| Strumenti Python | Lo strumento da riga di comando Python incorporato è utile per i test e le attività ad hoc. Trovare lo strumento in \Programmi\microsoft SQL Server\140\PYTHON_SERVER\python.exe. |
| Anaconda | Anaconda è una distribuzione open source di Python e di pacchetti essenziali. |
| Esempi e script Python | Come con R, Python include set di dati e script predefiniti. Trovare i dati di revoscalepy in \Programmi\microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelli con training preliminare in R e Python | I modelli con training preliminare vengono creati per casi d'uso specifici e gestiti dal team di progettazione di data science in Microsoft. È possibile usare i modelli con training preliminare così come sono per assegnare punteggi positivi negativi nel testo o per rilevare le funzionalità nelle immagini, usando i nuovi input di dati forniti. I modelli con training preliminare sono supportati e utilizzabili in un server autonomo, ma non è possibile installarli tramite SQL Server installazione. Per altre informazioni, vedere [installare modelli di apprendimento automatico pretrainati in SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-a-standalone-server"></a>Uso di un server autonomo

Gli sviluppatori r e Python scelgono in genere un server autonomo per superare i vincoli di memoria e di elaborazione di R e Python open source. Le librerie R e Python eseguite su un server autonomo possono caricare ed elaborare grandi quantità di dati in più core e aggregare i risultati in un unico output consolidato. Le funzioni a prestazioni elevate sono progettate per la scalabilità e l'utilità: distribuzione di analisi predittive, modellazione statistica, visualizzazioni di dati e algoritmi di machine learning all'avanguardia in un prodotto server commerciale progettato e supportato da Microsoft.

Poiché un server indipendente separato da SQL Server, l'ambiente R e Python viene configurato, protetto e a cui si accede usando il sistema operativo sottostante e gli strumenti standard forniti nel server autonomo, non SQL Server. Non è disponibile alcun supporto incorporato per SQL Server dati relazionali. Se si desidera utilizzare SQL Server dati, è possibile creare oggetti origine dati e connessioni come da qualsiasi client.

In aggiunta alla SQL Server, un server autonomo è utile anche come un ambiente di sviluppo potente se è necessario l'elaborazione sia locale che remota. I pacchetti R e Python in un server autonomo sono gli stessi di quelli forniti con un'installazione del motore di database, consentendo la portabilità del codice e il [cambio del contesto di calcolo](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

## <a name="how-to-get-started"></a>Come iniziare

Iniziare con il programma di installazione, associare i file binari allo strumento di sviluppo preferito e scrivere il primo script.

### <a name="step-1-install-the-software"></a>Passaggio 1: Installare il software

Installare una delle due versioni seguenti:

+ [SQL Server 2017 Machine Learning Server (autonomo)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (autonomo)-solo R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Passaggio 2: Configurare uno strumento di sviluppo

In un server autonomo, è normale lavorare localmente usando uno sviluppo installato nello stesso computer.

+ [Configurare gli strumenti R](set-up-a-data-science-client.md)
+ [Configurare gli strumenti Python](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>Passaggio 3: Scrivere il primo script

Scrivere script R o Python usando le funzioni di RevoScaleR, revoscalepy e gli algoritmi di machine learning.
  
  + [Esplorare R e RevoScaleR in 25 funzioni](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): Inizia con i comandi R di base e quindi passa alle funzioni analitiche distribuibile RevoScaleR che offrono prestazioni elevate e scalabilità alle soluzioni R. Include versioni parallelizzabili di molti dei più diffusi pacchetti di modellazione R, tra cui clustering K-Means, alberi delle decisioni e foreste delle decisioni, nonché strumenti per la modifica dei dati.

  + [Avvio rapido: Esempio di classificazione binaria con il pacchetto](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)Python microsoftml: Creare un modello di classificazione binaria usando le funzioni di microsoftml e il set di dati del tumore del seno noto.

Scegliere la lingua migliore per l'attività. R è ideale per calcoli statistici difficili da implementare con SQL. Per le operazioni basate su set sui dati, è possibile sfruttare la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potenza di per ottenere le massime prestazioni. Usare il motore di database in memoria per calcoli molto veloci sulle colonne.

### <a name="step-4-operationalize-your-solution"></a>Passaggio 4: Rendere operativo la soluzione

I server autonomi possono usare [la funzionalità di](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) messa in funzione dei [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)non basati su SQL. È possibile configurare un server autonomo per la messa in funzione, che offre i vantaggi seguenti: distribuire e ospitare il codice come servizi Web, eseguire la diagnostica, testare la capacità del servizio Web.

### <a name="step-5-maintain-your-server"></a>Passaggio 5: Gestire il server

SQL Server rilascia periodicamente aggiornamenti cumulativi. L'applicazione degli aggiornamenti cumulativi aggiunge funzionalità di sicurezza e miglioramenti funzionali a un'installazione esistente. 

Le descrizioni delle funzionalità nuove o modificate sono disponibili nell'articolo relativo ai [Download CAB](../install/sql-ml-cab-downloads.md) e nelle pagine Web per [gli aggiornamenti cumulativi SQL Server 2016](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) e gli [aggiornamenti cumulativi di SQL Server 2017](https://support.microsoft.com/help/4047329). 

Per ulteriori informazioni su come applicare gli aggiornamenti a un'istanza esistente, vedere [applicare gli aggiornamenti](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) nelle istruzioni di installazione.

## <a name="see-also"></a>Vedere anche

 [Installa R Server (autonomo) o Machine Learning Server (autonomo)](../install/sql-machine-learning-standalone-windows-install.md)

