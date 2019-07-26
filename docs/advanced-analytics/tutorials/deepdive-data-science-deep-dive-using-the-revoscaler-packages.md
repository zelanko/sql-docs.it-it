---
title: Esercitazione approfondita sulla funzione RevoScaleR-SQL Server Machine Learning
description: In questa esercitazione si apprenderà come chiamare le funzioni RevoScaleR usando SQL Server Machine Learning integrazione R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c326d51e9b3ac4edac61f97bf5f7fa3143d8d350
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470627"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>Esercitazione: Usare le funzioni R RevoScaleR con i dati SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) è un pacchetto Microsoft R che fornisce elaborazione distribuita e parallela per i carichi di lavoro di Data Science e machine learning. Per lo sviluppo di R in SQL Server, **RevoScaleR** è uno dei pacchetti predefiniti principali, con funzioni per la creazione di oggetti origine dati, l'impostazione di un contesto di calcolo, la gestione dei pacchetti e, soprattutto, l'utilizzo dei dati end-to-end, dall'importazione in visualizzazione e analisi. Gli algoritmi di Machine Learning in SQL Server hanno una dipendenza da origini dati **RevoScaleR** . Data l'importanza di **RevoScaleR**, sapere quando e come chiamare le sue funzioni è una competenza essenziale. 

In questa esercitazione in più parti viene introdotto un intervallo di funzioni **RevoScaleR** per le attività associate a Data Science. Nel processo si apprenderà come creare un contesto di calcolo remoto, spostare i dati tra contesti di calcolo locali e remoti ed eseguire il codice R in un SQL Server remoto. Viene inoltre illustrato come analizzare e tracciare i dati sia localmente che nel server remoto e come creare e distribuire i modelli.

## <a name="prerequisites"></a>Prerequisiti

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con la funzionalità r o [2016 SQL Server r Services (in-database)](../install/sql-r-services-windows-install.md)
  
+ [Autorizzazioni del database](../security/user-permission.md) e account di accesso utente del database SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ Un IDE, ad esempio RStudio o lo strumento RGUI incorporato incluso in R

Per spostarsi avanti e indietro tra i contesti di calcolo locali e remoti, sono necessari due sistemi. Local è in genere una workstation di sviluppo con potenza sufficienti per carichi di lavoro data science. Remote in questo caso è SQL Server 2017 o SQL Server 2016 con la funzionalità R abilitata. 

Il cambio di contesto di calcolo si basa sul fatto che la stessa versione di **RevoScaleR** sia in sistemi locali che remoti. In una workstation locale è possibile ottenere i pacchetti **RevoScaleR** e i provider correlati installando Microsoft R client.

Se è necessario inserire client e server nello stesso computer, assicurarsi di installare un secondo set di librerie Microsoft R per l'invio di script R da un client "remoto". Non usare le librerie R installate nei file di programma dell'istanza di SQL Server. In particolare, se si usa un solo computer, per supportare le operazioni client e server è necessaria la libreria **RevoScaleR** in entrambi i percorsi.

+ C:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Programmi\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\RevoScaleR

Per istruzioni sulla configurazione del client, vedere [configurare un client Data Science per lo sviluppo R](../r/set-up-a-data-science-client.md).


## <a name="r-development-tools"></a>Strumenti di sviluppo di R

Gli sviluppatori r usano in genere IDE per la scrittura e il debug del codice R. Di seguito sono riportati alcuni suggerimenti:

- **R Tools per Visual Studio** (RTVS) è un plug-in gratuito che fornisce IntelliSense, debug e supporto per Microsoft R. È possibile usarlo con R Server e SQL Server Machine Learning Services. Per scaricarlo, vedere [R Tools per Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- **RStudio** è uno degli ambienti più diffusi per lo sviluppo di R. Per ulteriori informazioni, vedere [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/).

- Per impostazione predefinita, vengono installati anche gli strumenti R di base (R. exe, RTerm. exe, RScripts. exe) quando si installa R in SQL Server o R client. Se non si vuole installare un IDE, è possibile usare gli strumenti R predefiniti per eseguire il codice in questa esercitazione.

Tenere presente che **RevoScaleR** è obbligatorio sia nei computer locali che in quelli remoti. Non è possibile completare questa esercitazione usando un'installazione generica di RStudio o di un altro ambiente in cui mancano le librerie Microsoft R. Per altre informazioni, vedere [Configurare un client per l'analisi scientifica dei dati](../r/set-up-a-data-science-client.md).

## <a name="summary-of-tasks"></a>Riepilogo delle attività

+ I dati vengono inizialmente ottenuti dai file CSV o XDF. I dati vengono importati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando le funzioni nel pacchetto **RevoScaleR** .
+ Il training del modello e il punteggio vengono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguiti usando il contesto di calcolo. 
+ Usare le funzioni **RevoScaleR** per creare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nuove tabelle per salvare i risultati del punteggio.
+ Creare tracciati sia nel server che nel contesto di calcolo locale.
+ Eseguire il training di un modello [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sui dati nel database, eseguendo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R nell'istanza.
+ Estrarre un subset di dati e salvarlo come file XDF per usarlo di nuovo nell'analisi nella workstation locale.
+ Ottenere nuovi dati per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] punteggio, aprendo una connessione ODBC al database. Il Punteggio viene eseguito sulla workstation locale.
+ Creare una funzione R personalizzata ed eseguirla nel contesto di calcolo del server per eseguire una simulazione.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Lezione 1: Creare database e autorizzazioni](deepdive-work-with-sql-server-data-using-r.md)