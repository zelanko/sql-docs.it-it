---
title: Installare R Server o Machine Learning Server (standalone) usando SQL Server installazione
description: Configurare un server di Machine Learning autonomo non compatibile con le istanze per lo sviluppo di R e Python usando RevoScaleR, revoscalepy, MicrosoftML e altri pacchetti.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 94ca7b3646b9005e11b3ee4968cbfaaa65d42264
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715843"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Installare Machine Learning Server (autonomo) o R Server (autonomo) utilizzando il programma di installazione di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Il programma di installazione di SQL Server include un'opzione di **funzionalità condivisa** per l'installazione di un server di Machine Learning autonomo non compatibile con l'istanza che viene eseguito all'esterno di SQL Server. Viene chiamato **Machine Learning Server (standalone)** e include R e Python. 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Il programma di installazione di SQL Server include un'opzione di **funzionalità condivisa** per l'installazione di un server di Machine Learning autonomo non compatibile con l'istanza che viene eseguito all'esterno di SQL Server. In SQL Server 2016 questa funzionalità è denominata **R Server (standalone)** .  
::: moniker-end

Un server autonomo installato dal programma di installazione SQL Server è equivalente dal punto di vista funzionale alle versioni non SQL di [Microsoft Machine Learning server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), supportando gli stessi casi d'uso e scenari, tra cui:

+ Esecuzione remota, spostamento tra sessioni locali e remote nella stessa console
+ Operatività con nodi Web e nodi di calcolo
+ Distribuzione del servizio Web: la possibilità di creare un pacchetto di script R e Python in servizi Web
+ Raccolta completa di librerie di funzioni R e Python

Poiché un server indipendente separato da SQL Server, l'ambiente R e Python viene configurato, protetto e a cui si accede usando il sistema operativo sottostante e gli strumenti forniti nel server autonomo, non SQL Server.

In aggiunta alla SQL Server, un server autonomo è utile se è necessario sviluppare soluzioni di apprendimento automatico a prestazioni elevate che possono usare contesti di calcolo remoti per la gamma completa di piattaforme dati supportate. È possibile spostare l'esecuzione dal server locale a una Machine Learning Server remota in un cluster Spark o in un'altra istanza di SQL Server.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>Elenco di controllo pre-installazione

Se è stata installata una versione precedente, ad esempio SQL Server 2016 R Server (autonomo) o Microsoft R Server, disinstallare l'installazione esistente prima di continuare.

Come regola generale, si consiglia di considerare le installazioni autonome e compatibili con l'istanza del motore di database, che si escludono a vicenda per evitare conflitti di risorse, ma se si dispone di risorse sufficienti, non vi è alcun divieto di installarle entrambi nel stesso computer fisico.

Nel computer può essere presente un solo server autonomo: SQL Server Machine Learning Server (autonomo) o SQL Server R Server (standalone). Assicurarsi di disinstallare una versione prima di aggiungerne una nuova.

::: moniker range="=sql-server-2016"
<a name="bkmk_ga_instalpatch"></a> 

 ###  <a name="install-patch-requirement"></a>Requisito di installazione patch 

Solo per SQL Server 2016: Microsoft ha rilevato un problema con una versione specifica dei file binari di Microsoft VC++ 2013 Runtime installati come prerequisito da SQL Server. Se l'aggiornamento dei file binari di VC++ Runtime non viene installato, potrebbero verificarsi problemi di stabilità di SQL Server in determinati scenari. Prima di installare SQL Server, seguire le istruzioni in [Note sulla versione di SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) per vedere se il computer richiede una patch per i file binari di VC++ Runtime.  
::: moniker-end

## <a name="get-the-installation-media"></a>Ottenere il supporto di installazione

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'installazione guidata di.

2. Fare clic sulla scheda **installazione** e selezionare **nuova installazione di Machine Learning Server (standalone)** .
    
     ![Installare Machine Learning server autonomo](media/2017setup-installation-page-mlsvr.png "Avvia l'installazione di Machine Learning server autonomo")

3. Al termine del controllo delle regole, accettare SQL Server condizioni di licenza e selezionare una nuova installazione.

4. Nella pagina **Selezione funzionalità** sono già selezionate le opzioni seguenti:

    - Microsoft Machine Learning Server (autonomo)

    - R e Python sono entrambi selezionati per impostazione predefinita. È possibile deselezionare una delle due lingue, ma è consigliabile installare almeno una delle lingue supportate.

     ![Scegliere le funzionalità di R o Python](media/2017setup-features-page-mlsvr-rpy.png "Avvia l'installazione di Machine Learning server autonomo")
    
    Tutte le altre opzioni devono essere ignorate. 
    
    > [!NOTE]
    > Evitare di installare le **funzionalità condivise** se il computer ha già Machine Learning Services installato per SQL Server analisi nel database. Viene creata una libreria duplicata.
    > 
    > Inoltre, mentre gli script R o Python in esecuzione in SQL Server vengono gestiti da SQL Server, in modo da non essere in conflitto con la memoria usata da altri servizi del motore di database, il server di Machine Learning autonomo non presenta vincoli di questo tipo e può interferire con altre operazioni di database . Infine, l'accesso remoto tramite sessione RDP, che viene spesso usato per la messa in funzione, viene in genere bloccato dagli amministratori del database.
    > 
    > Per questi motivi, in genere è consigliabile installare Machine Learning Server (standalone) in un computer separato da SQL Server Machine Learning Services.

5.  Accettare le condizioni di licenza per il download e l'installazione delle distribuzioni della lingua di base. Quando il pulsante **Accetto** non è più disponibile, è possibile fare clic su **Avanti**. 

     ![Contratto di licenza con Python](media/2017setup-python-license.png "Contratto di licenza con Python")

6.  Nella pagina **Inizio installazione** verificare le opzioni selezionate e fare clic su **Installa**.

Al termine dell'installazione, vedere la pagina relativa ai [report personalizzati per R Services per SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md) per assistenza con eventuali errori o avvisi, vedere [domande frequenti sull'installazione e sull'aggiornamento Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'installazione guidata di.

2. Nella scheda **installazione** fare clic su **nuova installazione di R Server (standalone)** .
    
     ![Avvia l'installazione di R server autonomo](media/2016-setup-installation-rsvr.png "Avvia l'installazione di R server autonomo")

3. Al termine del controllo delle regole, accettare SQL Server condizioni di licenza e selezionare una nuova installazione.

4.  Nella pagina **Selezione funzionalità** dovrebbe essere già selezionata l'opzione seguente:
    
    **R Server (Standalone)**  
    
    ![Selezioni delle funzionalità per R server autonomo](media/2016setup-rserver-features.png "Selezioni delle funzionalità per R server autonomo")
    
    Tutte le altre opzioni possono essere ignorate. 
    
    > [!NOTE]
    > Evitare di installare le **funzionalità condivise** se si esegue il programma di installazione in un computer in cui R Services è già stato installato per SQL Server analisi nel database. Viene creata una libreria duplicata.
    > 
    > Mentre gli script R in esecuzione in SQL Server vengono gestiti da SQL Server, in modo da non essere in conflitto con la memoria usata da altri servizi del motore di database, il R Server autonomo non ha tali vincoli e può interferire con altre operazioni di database.
    > 
    > È in genere consigliabile installare R Server (standalone) in un computer separato da R Services per SQL Server (in-database).

5.  Accettare le condizioni di licenza per il download e l'installazione delle distribuzioni della lingua di base. Quando il pulsante **Accetto** non è più disponibile, è possibile fare clic su **Avanti**. 

6.  Nella pagina **Inizio installazione** verificare le opzioni selezionate e fare clic su **Installa**.

Al termine dell'installazione, vedere la pagina relativa ai [report personalizzati per R Services per SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md) per assistenza con eventuali errori o avvisi, vedere [domande frequenti sull'installazione e sull'aggiornamento Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente

Per l'integrazione della funzionalità R, è necessario impostare la variabile di ambiente **MKL_CBWR** per [garantire l'output coerente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli di Intel Math Kernel Library (MKL).

1. Nel pannello di controllo fare clic su sistema **e sicurezza** > **sistema** > **Impostazioni** > di sistema avanzate**variabili di ambiente**.

2. Creare un nuovo utente o una variabile di sistema. 

  + Imposta nome variabile su`MKL_CBWR`
  + Impostare il valore della variabile su`AUTO`

3. Riavviare il server.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>Cartelle di installazione predefinite

Per lo sviluppo di R e Python, è comune avere più versioni nello stesso computer. Come installato da SQL Server installazione, la distribuzione di base viene installata in una cartella associata alla versione SQL Server utilizzata per l'installazione.

La tabella seguente elenca i percorsi per le distribuzioni R e Python create dai programmi di installazione Microsoft. Per completezza, la tabella include i percorsi generati dal programma di installazione di SQL Server e il programma di installazione autonomo per Microsoft Machine Learning Server.

|Version| Metodo di installazione | Cartella predefinita|
|----|----|----|
|SQL Server 2017 Machine Learning Server (autonomo) |  Installazione guidata di SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (autonomo) |  Programma di installazione autonomo di Windows |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server Machine Learning Services (in-database) |Installazione guidata di SQL Server 2017, opzione con linguaggio R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (autonomo) |  Installazione guidata di SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (in-database) |Installazione guidata di SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Applicazione degli aggiornamenti

Si consiglia di applicare l'aggiornamento cumulativo più recente ai componenti del motore di database e di machine learning. Gli aggiornamenti cumulativi vengono installati tramite il programma di installazione. 

Nei dispositivi connessi a Internet è possibile scaricare un file eseguibile autoestraente. L'applicazione di un aggiornamento per il motore di database esegue automaticamente il pull degli aggiornamenti cumulativi per le funzionalità esistenti di R e Python. 

Nei server disconnessi sono necessari passaggi aggiuntivi. È necessario ottenere l'aggiornamento cumulativo per il motore di database e i file CAB per le funzionalità di machine learning. Tutti i file devono essere trasferiti al server isolato e applicati manualmente.

1. Iniziare con un'istanza di base. È possibile applicare gli aggiornamenti cumulativi solo alle installazioni esistenti:

  + Machine Learning Server (autonomo) dalla versione iniziale SQL Server 2017
  + R Server (autonomo) da SQL Server versione iniziale 2016, SQL Server 2016 SP 1 o SQL Server 2016 SP 2

2. Chiudere tutte le sessioni R o Python aperte e arrestare tutti i processi ancora in esecuzione nel sistema.

3. Se è stata abilitata l'esecuzione della messa in funzione come nodi Web e nodi di calcolo per le distribuzioni di servizi Web, eseguire il backup del file **appSettings. JSON** come precauzione. Applicando SQL Server 2017 CU13 o versioni successive, il file può essere modificato in modo da mantenere la versione originale di una copia di backup.

4. In un dispositivo connesso a Internet fare clic sul collegamento aggiornamento cumulativo per la versione di SQL Server.

  + [Aggiornamenti di SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [Aggiornamenti di SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

5. Scaricare l'aggiornamento cumulativo più recente. Si tratta di un file eseguibile.

6. Su un dispositivo connesso a Internet, fare doppio clic sul file con estensione exe per eseguire il programma di installazione e seguire la procedura guidata per accettare le condizioni di licenza, rivedere le funzionalità interessate e monitorare lo stato di avanzamento fino al completamento.

7. In un server senza connettività Internet:

   + Ottenere i file CAB corrispondenti per R e Python. Per i collegamenti di download, vedere la pagina relativa ai [download di CAB per gli aggiornamenti cumulativi in SQL Server istanze di analisi nel database](sql-ml-cab-downloads.md).

   + Trasferire tutti i file, i file eseguibili e CAB principali, in una cartella nel computer offline.

   + Fare doppio clic su exe per eseguire il programma di installazione. Quando si installa un aggiornamento cumulativo in un server senza connettività Internet, viene richiesto di selezionare il percorso dei file con estensione cab per R e Python.

8. Dopo l'installazione, in un server per cui è stata abilitata la messa in funzione con nodi Web e nodi di calcolo, modificare **appSettings. JSON**, aggiungendo una voce "MMLResourcePath", direttamente in "MMLNativePath":

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [Eseguire l'utilità dell'interfaccia della riga](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) di comando di amministrazione per riavviare i nodi Web e di calcolo. Per i passaggi e la sintassi, vedere [monitorare, avviare e arrestare i nodi Web e di calcolo](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start).

## <a name="development-tools"></a>Strumenti di sviluppo

Nell'ambito dell'installazione di non viene installato un IDE di sviluppo. Per altre informazioni sulla configurazione di un ambiente di sviluppo, vedere [configurare gli strumenti R](../r/set-up-a-data-science-client.md) e [configurare gli strumenti di Python](../python/setup-python-client-tools-sql.md).

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori r possono iniziare a usare alcuni semplici esempi e apprendere le nozioni di base sul funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Esercitazione: Analisi nel database per sviluppatori R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Gli sviluppatori Python possono apprendere come usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analisi nel database per sviluppatori Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

Per visualizzare esempi di machine learning basati su scenari reali, vedere Esercitazioni su [Machine Learning](../tutorials/machine-learning-services-tutorials.md).
