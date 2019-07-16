---
title: Esercitazione per data Scientist usando il linguaggio R - SQL Server Machine Learning
description: Esercitazione che illustra come creare una soluzione R end-to-end per analitica nel database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 45d587b4d62c33e944b15c6b951fa1323620c50e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961706"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>Esercitazione: Sviluppo di SQL Data Scientist possono dati R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questa esercitazione per data Scientist, imparare a compilare la soluzione end-to-end per la modellazione predittiva basata sul supporto delle funzionalità di R in SQL Server 2016 o SQL Server 2017. Questa esercitazione Usa un' [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) database in SQL Server. 

Si utilizza una combinazione di codice R, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati e funzioni SQL personalizzate per compilare un modello di classificazione che indica la probabilità che il driver potrebbe riceverà una Mancia in una determinata corsa. È inoltre distribuire il modello R in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usare i dati del server per generare punteggi basati sul modello.

In questo esempio può essere esteso a tutti i tipi di problemi reali, ad esempio alla previsione delle risposte dei clienti alle campagne di vendita o alla previsione di spesa o partecipazione agli eventi. Poiché il modello può essere richiamato da una stored procedure, è possibile incorporarlo facilmente in un'applicazione.

Poiché la procedura dettagliata è progettata per illustrare agli sviluppatori R [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R viene usato laddove possibile. Tuttavia, ciò non significa che R sia necessariamente lo strumento migliore per ogni attività. In molti casi, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe offrire prestazioni migliori, in particolare in attività quali l'aggregazione dei dati e la progettazione delle funzionalità.  Tali attività possono trarre vantaggio dalle nuove funzionalità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ad esempio gli indici columnstore con ottimizzazione per la memoria. Cerchiamo di evidenziare le ottimizzazioni possibili lungo il percorso.

## <a name="prerequisites"></a>Prerequisiti

+ [SQL Server 2017 Machine Learning Services con integrazione di R](../install/sql-machine-learning-services-windows-install.md#verify-installation) o [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

+ [Autorizzazioni database](../security/user-permission.md) e un account di accesso di SQL Server database utente

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [Database di esempio dei Taxi di NYC](demo-data-nyctaxi-in-sql.md)

+ Un IDE R come RStudio o lo strumento RGUI predefinito incluso in R

È consigliabile eseguire questa procedura dettagliata in una workstation client. È necessario essere in grado di connettersi, nella stessa rete, a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computer con SQL Server e il linguaggio R abilitata. Per istruzioni sulla configurazione della workstation, vedere [configurare un client di analisi scientifica dei dati per lo sviluppo R](../r/set-up-a-data-science-client.md).

In alternativa, è possibile eseguire la procedura dettagliata in un computer che abbia sia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e un ambiente di sviluppo R, ma è sconsigliato questa configurazione per un ambiente di produzione. Se è necessario includere client e server nello stesso computer, assicurarsi di installare un secondo set di librerie di Microsoft R per l'invio di script R da un client "remoto". Non usare le librerie R che vengono installate nei file di programma dell'istanza di SQL Server. In particolare, se si usa un computer, è necessario della libreria RevoScaleR in entrambe le posizioni per supportare le operazioni client e server.

+ C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>Pacchetti R aggiuntivi

Questa procedura dettagliata richiede alcune librerie R che non sono installate per impostazione predefinita come parte di [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. È necessario installare tali pacchetti sia sul client in cui si sviluppa la soluzione e sul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computer in cui si distribuisce la soluzione.

### <a name="on-a-client-workstation"></a>In una workstation client

Nell'ambiente R, copiare le righe seguenti ed eseguire il codice nella finestra della Console (Rgui o un IDE). Alcuni pacchetti installati anche i pacchetti necessari. In tutti, circa 32 pacchetti vengono installati. È necessario disporre di una connessione internet per completare questo passaggio.
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>Nel server

Sono disponibili diverse opzioni per l'installazione dei pacchetti in SQL Server. Ad esempio, SQL Server offre [gestione dei pacchetti R](../r/install-additional-r-packages-on-sql-server.md) funzionalità che consente agli amministratori di database, creare un repository di pacchetti e assegnare utenti i diritti per installare i propri pacchetti. Tuttavia, se sei un amministratore nel computer, è possibile installare nuovi pacchetti R, usando fino a quando si installa per la libreria corretta.

> [!NOTE]
> Nel server **non li** installare in una libreria utente, anche se viene richiesto. Se si installa una libreria utente, l'istanza di SQL Server non è possibile trovare o eseguire i pacchetti. Per altre informazioni, vedere [installazione di nuovi pacchetti R in SQL Server](../r/install-additional-r-packages-on-sql-server.md).

1. Nel computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aprire RGui.exe **come amministratore**.  Se è stato installato utilizzando le impostazioni predefinite di SQL Server R Services, Rgui.exe è reperibile in C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\bin\x64).

2. Al prompt di R, eseguire i comandi R seguenti:
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  Questo esempio Usa la funzione grep di R per cercare il vettore di percorsi disponibili e trovare il percorso che include "Program Files". Per altre informazioni, vedere [ https://www.rdocumentation.org/packages/base/functions/grep ](https://www.rdocumentation.org/packages/base/functions/grep).

  Se si ritiene che i pacchetti già installati, controllare l'elenco dei pacchetti installati eseguendo `installed.packages()`.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esplorare e riepilogare i dati](walkthrough-view-and-summarize-data-using-r.md)