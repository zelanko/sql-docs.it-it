---
title: 'Installare R Server o Machine Learning Server (Standalone) con installazione di SQL Server: SQL Server Machine Learning'
description: Configurare un server di apprendimento automatico non dipendenti dall'istanza autonoma per lo sviluppo di R e Python con RevoScaleR, revoscalepy, MicrosoftML e altri pacchetti.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f721a840b6fba4a840484fccb1cafb334b1ba438
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962851"
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone-using-sql-server-setup"></a>Installare R Server (Standalone) con il programma di installazione di SQL Server o Machine Learning Server (Standalone)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Il programma di installazione di SQL Server include un **funzionalità condivisa** opzione per l'installazione di un non specifici dell'istanza, server di formazione machine autonomo eseguito all'esterno di SQL Server. In SQL Server 2016, questa funzionalità è detta **R Server (Standalone)** . In SQL Server 2017, bensì **Machine Learning Server (Standalone)** e include R e Python. 

Un server autonomo come installato dal programma di installazione di SQL Server è funzionalmente equivalente alle versioni non SQL personalizzata di [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), lo stesso supporto di casi d'uso e scenari, tra cui:

+ Esecuzione remota, il passaggio tra le sessioni locali e remote nella stessa console
+ Operazionalizzazione con nodi web e i nodi di calcolo
+ Distribuzione del servizio Web: la possibilità di creare il pacchetto dello script R e Python nei servizi web
+ Completamento della raccolta di librerie di funzioni R e Python

Come server indipendenti disaccoppiati da SQL Server, viene configurato l'ambiente R e Python, protetto e a cui si accede usando il sistema operativo sottostante e gli strumenti forniti nel server autonomo, non SQL Server.

A complemento di SQL Server, un server autonomo è utile se è necessario sviluppare soluzioni che possono usare contesti di calcolo remoto per l'intera gamma di piattaforme di dati supportati di apprendimento automatico ad alte prestazioni. È possibile spostare l'esecuzione dal server locale a una versione remota di Machine Learning Server in un cluster Spark o in un'altra istanza di SQL Server.

<a name="bkmk_prereqs"> </a>

## <a name="pre-install-checklist"></a>Elenco di controllo pre-installazione

Se è installata una versione precedente, ad esempio SQL Server 2016 R Server (Standalone) o Microsoft R Server, disinstallare l'installazione esistente prima di continuare.

Come regola generale, è consigliabile che si considera server autonomo e motore specifici dell'istanza installazioni del database come reciprocamente esclusive per evitare conflitti di risorse, ma se si dispone di risorse sufficienti, non vi è alcun divieto di installazione di entrambe le di stesso computer fisico.

Può avere solo un server autonomo nel computer: SQL Server 2017 Machine Learning Server o SQL Server 2016 R Server (Standalone). Assicurarsi di disinstallare una versione prima di aggiungerne uno nuovo.

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

1. Avviare l'installazione guidata.

2. Scegliere il **installazione** scheda e selezionare **installazione nuova Machine Learning Server (Standalone)** .
    
     ![Installazione di Machine Learning Server (Standalone)](media/2017setup-installation-page-mlsvr.png "avviare l'installazione di Machine Learning Server (Standalone)")

3. Al termine del controllo delle regole, accettare le condizioni di licenza di SQL Server e selezionare una nuova installazione.

4. Nel **Selezione funzionalità** pagina, le seguenti opzioni dovrebbero essere già selezionate:

    - Microsoft Machine Learning Server (Standalone)

    - R e Python sono entrambe selezionate per impostazione predefinita. È possibile deselezionare entrambi i linguaggi, ma è consigliabile installare almeno uno dei linguaggi supportati.

     ![Scegliere le funzionalità di R o Python](media/2017setup-features-page-mlsvr-rpy.png "avviare l'installazione di Machine Learning Server (Standalone)")
    
    Tutte le altre opzioni devono essere ignorate. 
    
    > [!NOTE]
    > Evitare di installare il **Caratteristiche condivise** se il computer dispone già di servizi di Machine Learning per analitica nel database di SQL Server installato. Ciò consente di creare librerie duplicate.
    > 
    > Inoltre, mentre gli script R o Python in esecuzione in SQL Server vengono gestiti da SQL Server a come non in conflitto con la memoria utilizzata da altri servizi del motore di database, server autonomo machine learning senza tali vincoli e può interferire con altre operazioni di database . Infine, accesso remoto tramite una sessione RDP, che viene spesso usata per l'operazionalizzazione, in genere è bloccata dagli amministratori di database.
    > 
    > Per questi motivi, è generalmente consigliabile installare Machine Learning Server (Standalone) in un computer separato da servizi di SQL Server Machine Learning.

5.  Accettare le condizioni di licenza per il download e installazione di distribuzioni di lingua di base. Quando il pulsante **Accetto** non è più disponibile, è possibile fare clic su **Avanti**. 

     ![Contratto di licenza di Python](media/2017setup-python-license.png "contratto di licenza di Python")

6.  Nella pagina **Inizio installazione** verificare le opzioni selezionate e fare clic su **Installa**.

Al termine dell'installazione, vedere [report personalizzati per SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) per informazioni su eventuali errori o avvisi, vedere [aggiornamento e installazione domande frequenti: servizi di Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

::: moniker range="=sql-server-2016"
## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'installazione guidata.

2. Nel **installazione** scheda, fare clic su **installazione nuovo R Server (Standalone)** .
    
     ![Avviare l'installazione di R Server Standalone](media/2016-setup-installation-rsvr.png "avviare l'installazione di R Server (Standalone)")

3. Al termine del controllo delle regole, accettare le condizioni di licenza di SQL Server e selezionare una nuova installazione.

4.  Nella pagina **Selezione funzionalità** dovrebbe essere già selezionata l'opzione seguente:
    
    **R Server (Standalone)**  
    
    ![Le selezioni per R Server (Standalone) di funzionalità](media/2016setup-rserver-features.png "funzionalità le selezioni per R Server (Standalone)")
    
    Tutte le altre opzioni possono essere ignorate. 
    
    > [!NOTE]
    > Evitare di installare il **Caratteristiche condivise** se si esegue il programma di installazione in un computer in cui è già installato R Services per analitica nel database di SQL Server. Ciò consente di creare librerie duplicate.
    > 
    > Mentre gli script R in esecuzione in SQL Server vengono gestiti da SQL Server a come non in conflitto con la memoria utilizzata da altri servizi del motore di database, la versione autonoma di R Server non dispone di alcun vincolo di questo tipo e può interferire con altre operazioni di database.
    > 
    > È in genere consiglia di installare R Server (Standalone) in un computer distinto da SQL Server R Services (In-Database).

5.  Accettare le condizioni di licenza per il download e installazione di distribuzioni di lingua di base. Quando il pulsante **Accetto** non è più disponibile, è possibile fare clic su **Avanti**. 

6.  Nella pagina **Inizio installazione** verificare le opzioni selezionate e fare clic su **Installa**.

Al termine dell'installazione, vedere [report personalizzati per SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md) per informazioni su eventuali errori o avvisi, vedere [aggiornamento e installazione domande frequenti: servizi di Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).
::: moniker-end

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente

Per l'integrazione solo con R funzionalità, è consigliabile impostare il **MKL_CBWR** variabile di ambiente [garantire coerenti con l'output](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli Intel Math Kernel Library (MKL).

1. Nel Pannello di controllo, fare clic su **sistema e sicurezza** > **System** > **impostazioni di sistema avanzate**  >   **Le variabili di ambiente**.

2. Creare una nuova variabile di sistema o dell'utente. 

  + Nome della variabile set a `MKL_CBWR`
  + Impostare il valore della variabile `AUTO`

3. Riavviare il server.

<a name="install-path"></a>

### <a name="default-installation-folders"></a>Cartelle di installazione predefinito

Per lo sviluppo di R e Python, è comune disporre di più versioni nello stesso computer. Installato dal programma di installazione di SQL Server, la distribuzione di base viene installata in una cartella associata alla versione di SQL Server usata per il programma di installazione.

La tabella seguente elenca i percorsi per le distribuzioni R e Python create da programmi di installazione di Microsoft. Per motivi di completezza, la tabella include percorsi di navigazione generati dal programma di installazione di SQL Server, nonché il programma di installazione autonomo per Microsoft Machine Learning Server.

|Version| Metodo di installazione | Cartella predefinita|
|----|----|----|
|Machine Learning Server (Standalone) di SQL Server 2017 |  Installazione guidata di SQL Server 2017 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft Machine Learning Server (Standalone) |  Programma di installazione di Windows autonomo |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 2017 Machine Learning Services (In-Database) |Installazione guidata di SQL Server 2017, con l'opzione di linguaggio R|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|R Server (Standalone) di SQL Server 2016 |  Installazione guidata di SQL Server 2016 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (In-Database) |Installazione guidata di SQL Server 2016|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Applicazione degli aggiornamenti

È consigliabile applicare l'aggiornamento cumulativo più recente per il motore di database e i componenti di apprendimento automatico. Gli aggiornamenti cumulativi vengono installati tramite il programma di installazione. 

Sui dispositivi connessi a internet, è possibile scaricare un file eseguibile autoestraente. Applicare un aggiornamento del motore di database automaticamente effettua il pull degli aggiornamenti cumulativi per le funzionalità esistenti di R e Python. 

Nei server disconnesso, sono necessarie operazioni aggiuntive. È necessario ottenere l'aggiornamento cumulativo per il motore di database, nonché i file CAB per funzionalità di machine learning. Tutti i file devono essere trasferiti al server di tipo isolato e applicati manualmente.

1. Iniziare con un'istanza della linea di base. È possibile applicare gli aggiornamenti cumulativi solo per le installazioni esistenti:

  + Machine Learning Server (Standalone) dalla versione iniziale di SQL Server 2017
  + R Server (Standalone) dalla versione iniziale di SQL Server 2016, SQL Server 2016 Service Pack 1 o SQL Server 2016 Service Pack 2

2. Chiudere tutte le sessioni di R o Python open e arrestare i processi ancora in esecuzione nel sistema.

3. Se è abilitata la messa in funzione per l'esecuzione come nodi web e i nodi di calcolo per le distribuzioni del servizio web, eseguire il backup di **appSettings. JSON** file come misura precauzionale. Applicazione di SQL Server 2017 CU13 o revises più avanti in questo file, pertanto è consigliabile una copia di backup per conservare la versione originale.

4. In un dispositivo connesso a internet, fare clic sul collegamento di aggiornamento cumulativo per la versione di SQL Server.

  + [Aggiornamenti di SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [Aggiornamenti di SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

5. Scaricare l'aggiornamento cumulativo più recente. È un file eseguibile.

6. In un dispositivo connesso a internet, fare doppio clic sul file .exe per eseguire il programma di installazione e il passaggio tramite la procedura guidata accettare le condizioni di licenza, esaminare le funzionalità interessate e monitorare lo stato di avanzamento fino al completamento.

7. In un server senza connettività internet:

   + Ottenere i file CAB corrispondenti per R e Python. Per i collegamenti ai download, vedere [CAB download per gli aggiornamenti cumulativi in analitica nel database di SQL Server istanze](sql-ml-cab-downloads.md).

   + Trasferimento di tutti i file, il file eseguibile principale e i file CAB, in una cartella nel computer offline.

   + Fare doppio clic sul file .exe per eseguire l'installazione. Quando si installa un aggiornamento cumulativo in un server senza connettività internet, viene chiesto di selezionare il percorso dei file con estensione CAB per R e Python.

8. Dopo l'installazione, su un server per cui sono stati abilitati operazionalizzazione con nodi web e i nodi di calcolo, modifica **appSettings. JSON**, aggiunta di una voce "MMLResourcePath", direttamente sotto "MMLNativePath":

    ```json
    "ScorerParameters": {
        "MMLNativePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\",
        "MMLResourcePath": "C:\Program Files\Microsoft SQL Server\140\R_SERVER\library\MicrosoftML\mxLibs\x64\"
    }
    ```

9. [Eseguire l'utilità della riga di comando admin](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-launch) per riavviare il web e i nodi di calcolo. Per questa procedura e la sintassi, vedere [Monitor, avvia e arresta nodi di calcolo e web](https://docs.microsoft.com/machine-learning-server/operationalize/configure-admin-cli-stop-start).

## <a name="development-tools"></a>Strumenti di sviluppo

Un IDE di sviluppo non è installato come parte del programma di installazione. Per altre informazioni sulla configurazione di un ambiente di sviluppo, vedere [configurare gli strumenti R](../r/set-up-a-data-science-client.md) e [configurare gli strumenti Python](../python/setup-python-client-tools-sql.md).

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori di R possono iniziare a usare alcuni semplici esempi e informazioni di base del funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Esercitazione: Analitica nel database per gli sviluppatori di R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Gli sviluppatori di Python è possono imparare a usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analitica nel database per sviluppatori Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)
::: moniker-end

Per visualizzare esempi di machine learning basate su scenari reali, vedere [di Machine learning esercitazioni](../tutorials/machine-learning-services-tutorials.md).
