---
title: RevoScaleR funzione esercitazione approfondita a SQL Server Machine Learning
description: Questa esercitazione descrive come chiamare le funzioni RevoScaleR mediante l'integrazione di R di SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 48d65bfe54890c5ea0d8bfdca9c76fa0978a917d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511728"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Esercitazione: Usare funzioni RevoScaleR R con dati di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) è un pacchetto di Microsoft R offrendo distribuita e l'elaborazione parallela per data science e machine learning i carichi di lavoro. Per lo sviluppo di R in SQL Server **RevoScaleR** è uno dei principali pacchetti predefiniti, con le funzioni per la creazione di oggetti origine dati, l'impostazione di un contesto di calcolo, la gestione dei pacchetti, cosa più importante: utilizzo di dati end-to-end, dall'importazione per analisi e visualizzazione. Algoritmi di Machine Learning in SQL Server attiva una dipendenza **RevoScaleR** origini dati. Data l'importanza delle **RevoScaleR**, sapere quando e come chiamare le funzioni è una competenza essenziale. 

In questa esercitazione in più parti, viene presentato numerose **RevoScaleR** funzioni per le attività associate di analisi scientifica dei dati. Nel processo, si apprenderà come creare un contesto di calcolo remoto, spostare dati tra contesti di calcolo locali e remoti e di eseguire codice R in un Server SQL remoto. Verrà anche illustrato come analizzare e tracciare i dati in locale e nel server remoto e come creare e distribuire modelli.

## <a name="prerequisites"></a>Prerequisiti

+ [Machine Learning Services di SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) con la funzionalità di R o [SQL Server 2016 R Services (in-Database)](../install/sql-r-services-windows-install.md)
  
+ [Autorizzazioni database](../security/user-permission.md) e un account di accesso di SQL Server database utente

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ Un IDE come RStudio o lo strumento RGUI predefinito incluso in R

Per spostarsi avanti e indietro tra contesti di calcolo locali e remoti, è necessario disporre di due sistemi. Locale è in genere una workstation di sviluppo con la potenza di sufficienti per carichi di lavoro di analisi scientifica dei dati. Remote in questo caso è SQL Server 2017 o SQL Server 2016 con abilitata la funzionalità di R. 

Il passaggio di contesti di calcolo viene affermato su aventi la stessa versione **RevoScaleR** nei sistemi locali e remoti. In una workstation locale, è possibile ottenere il **RevoScaleR** pacchetti e provider correlati tramite l'installazione di Microsoft R Client.

Se è necessario includere client e server nello stesso computer, assicurarsi di installare un secondo set di librerie di Microsoft R per l'invio di script R da un client "remoto". Non usare le librerie R che vengono installate nei file di programma dell'istanza di SQL Server. In particolare, se si usa un computer, è necessario il **RevoScaleR** libreria in entrambe le posizioni per supportare le operazioni client e server.

+ C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR

Per istruzioni sulla configurazione del client, vedere [configurare un client di analisi scientifica dei dati per lo sviluppo R](../r/set-up-a-data-science-client.md).


## <a name="r-development-tools"></a>Strumenti di sviluppo R

Gli sviluppatori di R in genere usano gli IDE per la scrittura e debug del codice R. Di seguito sono riportati alcuni suggerimenti:

- **R Tools per Visual Studio** (RTVS) è disponibile gratuitamente come plug-in che offre Intellisense, debug e il supporto per Microsoft R. È possibile usarlo con R Server e SQL Server Machine Learning Services. Per scaricarlo, vedere [R Tools per Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- **RStudio** è uno degli ambienti più diffusi per lo sviluppo di R. Per altre informazioni, vedere [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/).

- Strumenti R di base (R.exe, RTerm.exe, RScripts.exe) inoltre vengono installati per impostazione predefinita quando si installa R in SQL Server o Client R. Se non si desidera installare un IDE, è possibile utilizzare gli strumenti predefiniti di R per eseguire il codice in questa esercitazione.

È importante ricordare che **RevoScaleR** è necessario che nei computer locali e remoti. È possibile completare questa esercitazione usando un'installazione generica di RStudio o un altro ambiente in cui Manca le librerie di Microsoft R. Per altre informazioni, vedere [Configurare un client per l'analisi scientifica dei dati](../r/set-up-a-data-science-client.md).

## <a name="summary-of-tasks"></a>Riepilogo delle attività

+ I dati vengono inizialmente ottenuti dai file CSV o XDF. Importare i dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando le funzioni di **RevoScaleR** pacchetto.
+ Modello di training e di assegnazione dei punteggi viene eseguito utilizzando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contesto di calcolo. 
+ Uso **RevoScaleR** funzioni per creare nuovi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle per salvare i risultati della valutazione.
+ Creare tracciati sia nel server e contesto di calcolo locale.
+ Eseguire il training sui dati in un modello [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database, esecuzione di R nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza.
+ Estrarre un subset di dati e salvarlo come file XDF per usarlo nell'analisi nella workstation locale.
+ Ottenere i nuovi dati per la classificazione, aprendo una connessione ODBC per la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database. Assegnazione dei punteggi viene eseguito nella workstation locale.
+ Creare una funzione R personalizzata ed eseguirlo nel server di contesto di calcolo per eseguire una simulazione.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Lezione 1: Creare database e autorizzazioni](deepdive-work-with-sql-server-data-using-r.md)