---
title: Installare Machine Learning Server (Standalone)
description: Configurare un'istanza autonoma di Machine Learning Server per Python e R. Un server autonomo installato dal programma di installazione di SQL Server è equivalente, dal punto di vista funzionale, alle versioni non SQL di Microsoft Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/03/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 319ae61fbdca64bc6f27143bdd4a42aec635d129
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338929"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Installare Machine Learning Server (Standalone) o R Server (Standalone) con il programma di installazione di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Il programma di installazione di SQL Server include un'opzione di **Funzionalità condivise** per l'installazione di un'istanza autonoma di Machine Learning Server che viene eseguita all'esterno di SQL Server. Questa funzionalità è denominata **Machine Learning Server (Standalone)** e include Python e R. 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Il programma di installazione di SQL Server include un'opzione di **Funzionalità condivise** per l'installazione di un'istanza autonoma di Machine Learning Server che viene eseguita all'esterno di SQL Server. In SQL Server 2016 questa funzionalità è denominata **R Server (Standalone)** .  
::: moniker-end

Un server autonomo installato dal programma di installazione di SQL Server è equivalente, dal punto di vista funzionale, alle versioni non SQL di [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) e supporta gli stessi scenari e casi d'uso, tra cui:

+ Esecuzione remota, passaggio da sessione locale a remota nella stessa console
+ Operazionalizzazione con nodi Web e nodi di calcolo
+ Distribuzione di servizi Web: possibilità di includere un pacchetto di script R e Python in servizi Web
+ Raccolta completa delle librerie di funzioni R e Python

Come server indipendente, separato da SQL Server, l'ambiente R e Python viene configurato e protetto ed è accessibile tramite il sistema operativo sottostante e gli strumenti disponibili nel server autonomo, non SQL Server.

Come server da usare in aggiunta a SQL Server, un server autonomo è utile se è necessario sviluppare soluzioni di Machine Learning ad alte prestazioni che possono usare contesti di calcolo remoti per la gamma completa di piattaforme dati supportate. È possibile spostare l'esecuzione dal server locale a un server di Machine Learning remoto in un cluster Spark o in un'altra istanza di SQL Server.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>Elenco di controllo preliminare all'installazione

Se è stata installata una versione precedente, ad esempio SQL Server 2016 R Server (Standalone) o Microsoft R Server, disinstallare l'installazione esistente prima di continuare.

Come regola generale, è consigliabile considerare un'installazione di server autonomo e una dipendente dall'istanza del motore di database come mutualmente esclusive al fine di evitare conflitti di risorse. Se tuttavia sono disponibili risorse sufficienti, non è vietato installarle entrambe nel stesso computer fisico.

È anche possibile installare nel computer un solo server autonomo: SQL Server Machine Learning Server (Standalone) o SQL Server R Server (Standalone). Assicurarsi di disinstallare una versione prima di aggiungerne una nuova.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>Requisito di installazione di patch 

Solo per SQL Server 2016: Microsoft ha rilevato un problema con una versione specifica dei file binari di Microsoft VC++ 2013 Runtime installati come prerequisito da SQL Server. Se l'aggiornamento dei file binari di VC++ Runtime non viene installato, potrebbero verificarsi problemi di stabilità di SQL Server in determinati scenari. Prima di installare SQL Server, seguire le istruzioni in [Note sulla versione di SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) per vedere se il computer richiede una patch per i file binari di VC++ Runtime.  
::: moniker-end

## <a name="get-the-installation-media"></a>Ottenere il supporto di installazione

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'Installazione guidata.

2. Fare clic sulla scheda **Installazione** e selezionare **Nuova installazione di Machine Learning Server (Standalone)** .
    
   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![Installare Machine Learning Server (Standalone)](media/2017setup-installation-page-mlsvr.png "Avviare l'installazione di Machine Learning Server (Standalone)")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![Installare Machine Learning Server (Standalone)](media/2019setup-installation-page-mlsvr.png "Avviare l'installazione di Machine Learning Server (Standalone)")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

3. Al termine del controllo delle regole, accettare le condizioni di licenza di SQL Server e selezionare una nuova installazione.

4. Nella pagina **Selezione funzionalità** dovrebbero essere già selezionate le opzioni seguenti:

    - **Microsoft Machine Learning Server (Standalone)**

    - Le opzioni **R** e **Python** sono entrambe selezionate per impostazione predefinita. È possibile deselezionare uno dei due linguaggi, ma è consigliabile installare almeno uno dei linguaggi supportati.

   ::: moniker-end
   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   ![Scegliere le funzionalità di R o Python](media/2017setup-features-page-mlsvr-rpy.png "Avviare l'installazione di Machine Learning Server (Standalone)")
   ::: moniker-end
   ::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
   ![Scegliere le funzionalità di R o Python](media/2019setup-features-page-mlsvr-rpy.png "Avviare l'installazione di Machine Learning Server (Standalone)")
   ::: moniker-end
   ::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
    
   Tutte le altre opzioni devono essere ignorate. 
    
   > [!NOTE]
   > Evitare di installare **Funzionalità condivise** se nel computer è già installato Machine Learning Services per l'analisi nel database di SQL Server. Prima di tutto, in questo modo vengono create librerie duplicate.
   > 
   > Inoltre, mentre gli script R o Python in esecuzione in SQL Server vengono gestiti da SQL Server in modo da non entrare in conflitto con la memoria usata da altri servizi del motore di database, il server di Machine Learning autonomo non presenta vincoli di questo tipo e può interferire con altre operazioni di database. Infine, l'accesso remoto tramite sessione RDP, che viene spesso usato per l'operazionalizzazione, viene in genere bloccato dagli amministratori del database.
   > 
   > Per questi motivi, è in genere consigliabile installare Machine Learning Server (Standalone) in un computer separato da SQL Server Machine Learning Services.

5. Accettare le condizioni di licenza per il download e l'installazione delle distribuzioni di base del linguaggio. Quando il pulsante **Accetto** non è più disponibile, è possibile fare clic su **Avanti**. 

6. Nella pagina **Inizio installazione** verificare le opzioni selezionate e fare clic su **Installa**.

Al termine dell'installazione, vedere [Report personalizzati per SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md). Per informazioni su eventuali errori o avvisi, vedere [Domande frequenti sull'installazione e sull'aggiornamento per Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'Installazione guidata.

2. Nella scheda **Installazione** fare clic su **Nuova installazione di R Server (Standalone)** .
    
   ![Avviare l'installazione di R Server (Standalone)](media/2016-setup-installation-rsvr.png "Avviare l'installazione di R Server (Standalone)")

3. Al termine del controllo delle regole, accettare le condizioni di licenza di SQL Server e selezionare una nuova installazione.

4. Nella pagina **Selezione funzionalità** dovrebbe essere già selezionata l'opzione seguente:
    
   - **R Server (Standalone)**  
    
   ![Opzioni di selezione delle funzionalità per R Server (Standalone)](media/2016setup-rserver-features.png "Opzioni di selezione delle funzionalità per R Server (Standalone)")
    
   Tutte le altre opzioni possono essere ignorate. 
    
   > [!NOTE]
   > Evitare di installare **Funzionalità condivise** se nel computer è già installato R Services per l'analisi nel database di SQL Server. Prima di tutto, in questo modo vengono create librerie duplicate.
   > 
   > Inoltre, mentre gli script R in esecuzione in SQL Server vengono gestiti da SQL Server in modo da non entrare in conflitto con la memoria usata da altri servizi del motore di database, R Server (Standalone) non presenta vincoli di questo tipo e può interferire con altre operazioni di database.
   > 
   > È in genere consigliabile installare R Server (Standalone) in un computer separato da SQL Server R Services (In-Database).

5. Accettare le condizioni di licenza per il download e l'installazione delle distribuzioni di base del linguaggio. Quando il pulsante **Accetto** non è più disponibile, è possibile fare clic su **Avanti**. 

6. Nella pagina **Inizio installazione** verificare le opzioni selezionate e fare clic su **Installa**.

Al termine dell'installazione, vedere [Report personalizzati per SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md). Per informazioni su eventuali errori o avvisi, vedere [Domande frequenti sull'installazione e sull'aggiornamento per Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente

Per integrare solo le funzionalità di R, è necessario impostare la variabile di ambiente **MKL_CBWR** per avere la certezza di [ottenere un output coerente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli di Intel Math Kernel Library (MKL).

1. Nel Pannello di controllo fare clic su **Sistema e sicurezza** > **Sistema** > **Impostazioni di sistema avanzate** > **Variabili d'ambiente**.

2. Creare una nuova variabile dell'utente o di sistema. 

  + Impostare `MKL_CBWR` come nome della variabile
  + Impostare `AUTO` come valore della variabile

3. Riavviare il server.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>Cartelle di installazione predefinite

Per lo sviluppo in R e Python, è pratica comune avere più versioni nello stesso computer. Con l'installazione di SQL Server, la distribuzione di base viene installata in una cartella associata alla versione di SQL Server usata per la configurazione.

La tabella seguente elenca i percorsi relativi alle distribuzioni R e Python create dai programmi di installazione Microsoft. Per completezza, la tabella include i percorsi generati dal programma di installazione di SQL Server e dal programma di installazione autonomo per Microsoft Machine Learning Server.

|Versione| Metodo di installazione | Cartella predefinita|
|----|----|----|
|SQL Server 2019 Machine Learning Server (Standalone) |  Installazione guidata di SQL Server 2019 |`C:\Program Files\Microsoft SQL Server\150\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\150\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning Server (Standalone) |  Installazione guidata di SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (Standalone) |  Programma di installazione autonomo di Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server Machine Learning Services (In-Database) |Installazione guidata di SQL Server 2019, con l'opzione per il linguaggio R|`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL15.<instance_name>\PYTHON_SERVICES` |
|SQL Server Machine Learning Services (In-Database) |Installazione guidata di SQL Server 2017, con l'opzione per il linguaggio R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (Standalone) |  Installazione guidata di SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (In-Database) |Installazione guidata di SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Applicare gli aggiornamenti

È consigliabile applicare l'aggiornamento cumulativo più recente sia al motore di database sia ai componenti di Machine Learning. Gli aggiornamenti cumulativi vengono installati tramite il programma di installazione. 

Nei dispositivi connessi a Internet è possibile scaricare un file eseguibile autoestraente. L'applicazione di un aggiornamento per il motore di database esegue automaticamente il pull degli aggiornamenti cumulativi per le funzionalità di R e Python esistenti. 

Nei server che non sono connessi a Internet sono necessari alcuni passaggi aggiuntivi. È necessario ottenere l'aggiornamento cumulativo per il motore di database e i file CAB per le funzionalità di Machine Learning. Tutti i file devono essere trasferiti al server isolato e applicati manualmente.

1. Iniziare con un'istanza di base. È possibile applicare gli aggiornamenti cumulativi solo alle installazioni esistenti:

  + Machine Learning Server (Standalone) dalla versione iniziale di SQL Server 2019
  + Machine Learning Server (Standalone) dalla versione iniziale di SQL Server 2017
  + R Server (Standalone) dalla versione iniziale di SQL Server 2016 oppure da SQL Server 2016 SP 1 o SQL Server 2016 SP 2

2. Chiudere tutte le sessioni di R o Python aperte e arrestare tutti i processi ancora in esecuzione nel sistema.

3. Se è stata abilitata l'operazionalizzazione per l'esecuzione come nodi Web e nodi di calcolo per le distribuzioni di servizi Web, per precauzione eseguire il backup del file **AppSettings.json**. L'applicazione di SQL Server 2017 CU13 o versioni successive apporta alcune modifiche a questo file e quindi può essere opportuno creare una copia di backup della versione originale.

4. In un computer connesso a Internet scaricare l'aggiornamento cumulativo più recente per la versione in uso da [Aggiornamenti più recenti per Microsoft SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/latest-updates-for-microsoft-sql-server).

5. Scaricare l'aggiornamento cumulativo più recente. Si tratta di un file eseguibile.

6. In un dispositivo connesso a Internet, fare doppio clic sul file con estensione exe per eseguire il programma di installazione e seguire la procedura guidata per accettare le condizioni di licenza, rivedere le funzionalità interessate e monitorare lo stato di avanzamento fino al completamento.

7. In un server senza connettività Internet:

   + Scaricare i file CAB corrispondenti per R e Python. Per i collegamenti di download, vedere [Download dei file CAB per gli aggiornamenti cumulativi nelle istanze per l'analisi nel database di SQL Server](sql-ml-cab-downloads.md).

   + Trasferire tutti i file, l'eseguibile principale e i file CAB, in una cartella del computer offline.

   + Fare doppio clic sul file con estensione exe per eseguire il programma di installazione. Quando si installa un aggiornamento cumulativo in un server senza connettività Internet, viene chiesto di selezionare il percorso dei file con estensione cab per R e Python.

8. Dopo l'installazione, in un server per cui è stata abilitata la distribuzione con nodi Web e nodi di calcolo, modificare **AppSettings.json**, aggiungendo una voce "MMLResourcePath" direttamente in "MMLNativePath". Ad esempio:

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [Eseguire l'utilità dell'interfaccia della riga di comando di amministrazione](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) per riavviare i nodi Web e di calcolo. Per la procedura e la sintassi, vedere [Monitorare, avviare e arrestare i nodi Web e di calcolo](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start).

## <a name="development-tools"></a>Strumenti di sviluppo

Durante la procedura di installazione non viene installato un ambiente di sviluppo integrato. Per altre informazioni sulla configurazione di un ambiente di sviluppo, vedere [Configurare gli strumenti per R](../r/set-up-a-data-science-client.md) e [Configurare gli strumenti per Python](../python/setup-python-client-tools-sql.md).

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori R possono iniziare alcuni semplici esempi e con le nozioni di base sul funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Esercitazione: Analisi nel database per sviluppatori R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Gli sviluppatori Python possono apprendere come usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analisi nel database per sviluppatori Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

Per esempi di Machine Learning basati su scenari reali, vedere [Esercitazioni su Machine Learning](../tutorials/machine-learning-services-tutorials.md).
