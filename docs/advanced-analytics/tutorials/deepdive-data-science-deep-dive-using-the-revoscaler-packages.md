---
title: Esercitazione approfondita su RevoScaleR
description: In questa serie di esercitazioni si apprenderà come chiamare le funzioni RevoScaleR usando l'integrazione del linguaggio R in Machine Learning di SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fc1f427659155b5379a681787a633b6037b4bd87
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76918831"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Esercitazione: Usare le funzioni R RevoScaleR con i dati di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questa serie di esercitazione in più parti vengono presentate diverse funzioni **RevoScaleR** per le attività associate al data science. Si apprenderà come creare un contesto di calcolo remoto, spostare i dati tra contesti di calcolo locali e remoti ed eseguire il codice R in un'istanza di SQL Server remota. Viene anche illustrato come analizzare e tracciare i dati sia localmente che nel server remoto e come creare e distribuire modelli.

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) è un pacchetto Microsoft R che fornisce caratteristiche di elaborazione distribuita e parallela per i carichi di lavoro di data science e machine learning. Per lo sviluppo di R in SQL Server, **RevoScaleR** è uno dei pacchetti predefiniti principali, con funzioni per la creazione di oggetti origine dati, l'impostazione di un contesto di calcolo, la gestione dei pacchetti e, soprattutto, l'utilizzo dei dati end-to-end, dall'importazione alla visualizzazione e all'analisi. Gli algoritmi di Machine Learning in SQL Server hanno una dipendenza dalle origini dati di **RevoScaleR**. Data l'importanza di **RevoScaleR**, sapere quando e come chiamare le sue funzioni è una competenza fondamentale. 

## <a name="prerequisites"></a>Prerequisites

+ [Machine Learning Services per SQL Server](../install/sql-machine-learning-services-windows-install.md) con la caratteristica R o [R Services per SQL Server (In-Database)](../install/sql-r-services-windows-install.md)
  
+ [Autorizzazioni per il database](../security/user-permission.md) e un account di accesso per un database di SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ Un ambiente IDE come RStudio oppure lo strumento RGUI predefinito incluso con R

Per spostarsi tra i contesti di calcolo locale e remoto sono necessari due sistemi. Il sistema locale è in genere una workstation di sviluppo con potenza sufficiente per i carichi di lavoro di data science. Il sistema remoto in questo caso è SQL Server con la caratteristica R abilitata. 

Per spostarsi tra i contesti di calcolo è necessario avere la stessa versione di **RevoScaleR** sul sistema locale e su quello remoto. In una workstation locale è possibile ottenere i pacchetti **RevoScaleR** e i provider correlati installando Microsoft R Client.

Se è necessario collocare client e server nello stesso computer, assicurarsi di installare un secondo set di librerie Microsoft R per l'invio di script R da un client "remoto". Non usare le librerie R installate nella cartella Programmi dell'istanza di SQL Server. In particolare, se si usa un solo computer, per supportare le operazioni client e server è necessaria la libreria **RevoScaleR** in entrambi i percorsi.

+ C:\Programmi\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Programmi\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

Per istruzioni sulla configurazione del client, vedere [Configurare un client di data science per lo sviluppo in R](../r/set-up-a-data-science-client.md).


## <a name="r-development-tools"></a>Strumenti di sviluppo di R

Gli sviluppatori R usano in genere ambienti di sviluppo integrato per la scrittura e il debug del codice R. Di seguito sono riportati alcuni suggerimenti:

- **R Tools per Visual Studio** è un plug-in gratuito che offre Intellisense, debug e supporto per Microsoft R. È possibile usarlo sia con R Server, sia con Machine Learning Services per SQL Server. Per scaricarlo, vedere [R Tools per Visual Studio](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019).

- **RStudio** è uno degli ambienti più diffusi per lo sviluppo di R. Per altre informazioni, vedere [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/).

- Quando si installa R in SQL Server o R Client, per impostazione predefinita vengono installati anche gli strumenti R di base (R.exe, RTerm.exe, RScripts.exe). Se non si vuole installare un IDE, è possibile usare gli strumenti R predefiniti per eseguire il codice in questa esercitazione.

Tenere presente che **RevoScaleR** è necessario sia nel computer locale che in quello remoto. Non è possibile completare questa esercitazione usando un'installazione generica di RStudio o un altro ambiente in cui mancano le librerie Microsoft R. Per altre informazioni, vedere [Configurare un client per l'analisi scientifica dei dati](../r/set-up-a-data-science-client.md).

## <a name="summary-of-tasks"></a>Riepilogo delle attività

+ I dati vengono inizialmente ottenuti dai file CSV o XDF. Occorre importare i dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando le funzioni del pacchetto **RevoScaleR**.
+ Il training e l'assegnazione dei punteggi dei modelli vengono eseguiti usando il contesto di calcolo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
+ Usare le funzioni di **RevoScaleR** per creare nuove tabelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui salvare i risultati dell'assegnazione dei punteggi.
+ Creare tracciati sia nel contesto di calcolo del server che nel contesto di calcolo locale.
+ Eseguire il training di un modello sui dati nel database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eseguendo R nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
+ Estrarre un subset di dati e salvarlo come file XDF per riutilizzarlo nell'analisi nella workstation locale.
+ Ottenere nuovi dati per l'assegnazione dei punteggi aprendo una connessione ODBC al database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'assegnazione dei punteggi viene eseguita sulla workstation locale.
+ Creare una funzione R personalizzata ed eseguirla nel contesto di calcolo del server per eseguire una simulazione.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esercitazione 1: Creare il database e le autorizzazioni](deepdive-work-with-sql-server-data-using-r.md)