---
title: Esercitazione per i data scientist che usano il linguaggio R
description: Esercitazione che illustra come creare una soluzione R end-to-end per l'analisi nel database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7d494329a52f73d489350792b6f43e138f3618a8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714659"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>Esercitazione: Sviluppo SQL per gli esperti di dati R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa esercitazione per i data scientist, informazioni su come creare una soluzione end-to-end per la modellazione predittiva basata sul supporto delle funzionalità R in SQL Server 2016 o SQL Server 2017. Questa esercitazione usa un database [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) in SQL Server. 

Si usa una combinazione di codice R, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati e funzioni SQL personalizzate per compilare un modello di classificazione che indica la probabilità che il driver ottenga una mancia in una particolare corsa in taxi. È anche possibile distribuire il modello R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in e usare i dati del server per generare punteggi basati sul modello.

Questo esempio può essere esteso a tutti i tipi di problemi della vita reale, ad esempio la stima delle risposte dei clienti alle campagne di vendita o la previsione di spese o presenze per gli eventi. Poiché il modello può essere richiamato da una stored procedure, è possibile incorporarlo facilmente in un'applicazione.

Poiché la procedura dettagliata è progettata per introdurre gli sviluppatori [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]r in, quando possibile viene usato r. Tuttavia, ciò non significa che R sia necessariamente lo strumento migliore per ogni attività. In molti casi, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe offrire prestazioni migliori, in particolare in attività quali l'aggregazione dei dati e la progettazione delle funzionalità.  Tali attività possono trarre vantaggio dalle nuove funzionalità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ad esempio gli indici columnstore con ottimizzazione per la memoria. Si tenta di evidenziare possibili ottimizzazioni lungo il percorso.

## <a name="prerequisites"></a>Prerequisiti

+ [SQL Server Machine Learning Services con integrazione r](../install/sql-machine-learning-services-windows-install.md#verify-installation) o [SQL Server 2016 r Services](../install/sql-r-services-windows-install.md)

+ [Autorizzazioni del database](../security/user-permission.md) e account di accesso utente del database SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [Database demo di NYC Taxi](demo-data-nyctaxi-in-sql.md)

+ Un IDE R, ad esempio RStudio o lo strumento RGUI incorporato incluso in R

Si consiglia di eseguire questa procedura dettagliata in una workstation client. È necessario essere in grado di connettersi, nella stessa rete, a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computer in cui è abilitato SQL Server e il linguaggio R. Per istruzioni sulla configurazione della workstation, vedere [configurare un client Data Science per lo sviluppo R](../r/set-up-a-data-science-client.md).

In alternativa, è possibile eseguire la procedura dettagliata in un computer che include [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia che un ambiente di sviluppo R, ma questa configurazione non è consigliata per un ambiente di produzione. Se è necessario inserire client e server nello stesso computer, assicurarsi di installare un secondo set di librerie Microsoft R per l'invio di script R da un client "remoto". Non usare le librerie R installate nei file di programma dell'istanza di SQL Server. In particolare, se si usa un solo computer, per supportare le operazioni client e server è necessaria la libreria RevoScaleR in entrambi i percorsi.

+ C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>Pacchetti R aggiuntivi

Questa procedura dettagliata richiede alcune librerie R che non sono installate per impostazione predefinita come [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]parte di. È necessario installare i pacchetti sia nel client in cui si sviluppa la soluzione sia nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computer in cui si distribuisce la soluzione.

### <a name="on-a-client-workstation"></a>In una workstation client

Nell'ambiente R copiare le righe seguenti ed eseguire il codice in una finestra della console (Rgui o IDE). Alcuni pacchetti installano anche i pacchetti necessari. In tutti i pacchetti sono installati circa 32. Per completare questo passaggio, è necessario disporre di una connessione Internet.
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>Sul server

Sono disponibili diverse opzioni per l'installazione di pacchetti in SQL Server. Ad esempio, SQL Server fornisce la funzionalità di [gestione dei pacchetti R](../r/install-additional-r-packages-on-sql-server.md) che consente agli amministratori di database di creare un repository di pacchetti e assegnare all'utente i diritti per installare i propri pacchetti. Tuttavia, se si è un amministratore del computer, è possibile installare nuovi pacchetti usando R, purché venga installato nella libreria corretta.

> [!NOTE]
> Nel server **non eseguire** l'installazione in una libreria utente anche se richiesto. Se si installa in una libreria utente, l'istanza di SQL Server non è in grado di trovare o eseguire i pacchetti. Per altre informazioni, vedere [Installing New R packages on SQL Server](../r/install-additional-r-packages-on-sql-server.md).

1. Nel computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aprire RGui.exe **come amministratore**.  Se è stato installato R Services per SQL Server utilizzando le impostazioni predefinite, Rgui. exe si trova in C:\Programmi\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\bin\x64).

2. Al prompt di R, eseguire i comandi R seguenti:
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  Questo esempio usa la funzione grep di R per cercare il vettore di percorsi disponibili e trovare il percorso che include "Program Files". Per ulteriori informazioni, vedere [https://www.rdocumentation.org/packages/base/functions/grep](https://www.rdocumentation.org/packages/base/functions/grep).

  Se si ritiene che i pacchetti siano già installati, controllare l'elenco dei pacchetti `installed.packages()`installati eseguendo.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esplorare e riepilogare i dati](walkthrough-view-and-summarize-data-using-r.md)