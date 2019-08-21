---
title: Installare SQL Server Machine Learning Services (Python, R) in Windows
titleSuffix: ''
description: Questo articolo illustra come installare SQL Server Machine Learning Services in Windows. È possibile usare Machine Learning Services per eseguire gli script Python e R nel database.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/20/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 28e4681808348df97e61709745e9b59e0a44d3be
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69634561"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>Installare SQL Server Machine Learning Services in Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come installare SQL Server Machine Learning Services in Windows. È possibile usare Machine Learning Services per eseguire gli script Python e R nel database.

## <a name="bkmk_prereqs"></a> Elenco di controllo pre-installazione

+ SQL Server 2017 (o versione successiva) è necessario se si vuole installare Machine Learning Services con il supporto del linguaggio R o Python. Se invece si dispone di SQL Server supporto di installazione di 2016, è possibile installare [R Services per SQL Server (in-database)](sql-r-services-windows-install.md) per ottenere supporto per il linguaggio R.

+ È necessaria un'istanza del motore di database. Non è possibile installare solo le funzionalità di R o Python, sebbene sia possibile aggiungerle in modo incrementale a un'istanza esistente.

+ Per la continuità aziendale, i [gruppi di disponibilità always on](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) sono supportati per Machine Learning Services. È necessario installare Machine Learning Services e configurare i pacchetti in ogni nodo.

+ L'installazione di Machine Learning Services *non è supportata* in un cluster di failover di SQL Server 2017. Tuttavia, *è supportato* con SQL Server 2019. 
 
+ Non installare Machine Learning Services in un controller di dominio. Il Machine Learning Services parte del programma di installazione avrà esito negativo.

+ Non installare le **funzionalità** > condivise**Machine Learning Server (standalone)** nello stesso computer in cui è in esecuzione un'istanza di nel database. Un server autonomo eseguirà la competizione per le stesse risorse, compromettendo le prestazioni di entrambe le installazioni.

+ L'installazione side-by-side con altre versioni di R e Python è supportata ma non consigliata. È supportato perché SQL Server istanza usa le proprie copie delle distribuzioni R e Anaconda open source. Tuttavia, non è consigliabile perché l'esecuzione di codice che usa R e Python nel computer SQL Server al di fuori SQL Server può causare vari problemi:
    
  + Si usa una libreria diversa e un file eseguibile diverso e si ottengono risultati diversi rispetto a quando si esegue in SQL Server.
  + Gli script R e Python in esecuzione in librerie esterne non possono essere gestiti da SQL Server, causando conflitti di risorse.
  
> [!IMPORTANT]
> Al termine dell'installazione, assicurarsi di completare i passaggi di post-configurazione descritti in questo articolo. Questi passaggi includono l'abilitazione di SQL Server per l'uso di script esterni e l'aggiunta di account necessari per SQL Server per eseguire i processi R e Python per conto dell'utente. Per le modifiche di configurazione è in genere necessario riavviare l'istanza o riavviare il servizio launchpad.

## <a name="get-the-installation-media"></a>Ottenere il supporto di installazione

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'installazione guidata di SQL Server 2017. 
  
2. Nella scheda **installazione** selezionare **nuovo SQL Server installazione autonoma di o aggiunta di funzionalità a un'installazione esistente**.

   ![Nuova installazione autonoma di SQL Server](media/2017setup-installation-page-mlsvcs.PNG)
   
3. Nella pagina **Selezione funzionalità** selezionare queste opzioni:
  
    -   **Servizi motore di database**
  
         Per usare R e Python con SQL Server, è necessario installare un'istanza del motore di database. È possibile utilizzare un'istanza predefinita o denominata.
  
    -   **Machine Learning Services (In-Database)**
  
         Questa opzione consente di installare i servizi di database che supportano l'esecuzione di script R e Python.

    -   **R**

        Selezionare questa opzione per aggiungere i pacchetti Microsoft R, l'interprete e R Open Source. 

    -   **Python**

        Selezionare questa opzione per aggiungere i pacchetti Microsoft Python, il file eseguibile di Python 3,5 e selezionare le librerie dalla distribuzione anaconda.
        
        ![Opzioni delle funzionalità per R e Python](media/2017setup-features-page-mls-rpy.png "Opzioni di installazione per Python")

        > [!NOTE]
        > 
        > Non selezionare l'opzione per **Machine Learning Server (standalone)** . L'opzione per installare Machine Learning Server in **funzionalità condivise** è destinata all'uso in un computer separato.

4. Nella pagina **consenso all'installazione di R** selezionare **accetta**. Questo contratto di licenza riguarda Microsoft R Open, che include una distribuzione di pacchetti e strumenti di base R Open Source, insieme a pacchetti R avanzati e provider di connettività del team di sviluppo Microsoft.

5. Nella pagina **consenso per l'installazione di Python** selezionare **Accetto**. Il contratto di licenza open source per Python copre anche Anaconda e gli strumenti correlati, oltre ad alcune nuove librerie Python del team di sviluppo Microsoft.
     
     ![Contratto per la licenza Python](media/2017setup-python-license.png "Contratto di licenza per Python")
  
    > [!NOTE]
    >  Se il computer in uso non dispone di accesso a Internet, è possibile sospendere l'installazione a questo punto per scaricare i programmi di installazione separatamente. Per altre informazioni, vedere [installare componenti di Machine Learning senza accesso a Internet](../install/sql-ml-component-install-without-internet-access.md).
  
     Selezionare **accetta**, attendere fino a quando il pulsante **Avanti** diventa attivo e quindi fare clic su **Avanti**.
  
6. Nella pagina **pronto per l'installazione** verificare che queste selezioni siano incluse e selezionare **Installa**.
  
    + Servizi motore di database
    + Machine Learning Services (In-Database)
    + R o Python o entrambi

    Prendere nota del percorso della cartella nel percorso `..\Setup Bootstrap\Log` in cui sono archiviati i file di configurazione. Al termine dell'installazione, è possibile esaminare i componenti installati nel file di riepilogo.

7. Al termine dell'installazione, se viene richiesto di riavviare il computer, eseguirlo ora. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente

Per l'integrazione della funzionalità R, è necessario impostare la variabile di ambiente **MKL_CBWR** per [garantire l'output coerente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli di Intel Math Kernel Library (MKL).

1. Nel pannello di controllo fare clic su sistema **e sicurezza** > **sistema** > **Impostazioni** > di sistema avanzate**variabili di ambiente**.

2. Creare un nuovo utente o una variabile di sistema. 

  + Imposta nome variabile su`MKL_CBWR`
  + Impostare il valore della variabile su`AUTO`

Per questo passaggio è necessario riavviare il server. Se si sta per abilitare l'esecuzione di script, è possibile disattivare il riavvio fino a quando non vengono eseguite tutte le operazioni di configurazione.

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>Abilitare l'esecuzione di script

1. Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > È possibile scaricare e installare la versione appropriata da questa pagina: [Scaricare SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > È inoltre possibile utilizzare [Azure Data Studio](../../azure-data-studio/what-is.md), che supporta le attività amministrative e le query su SQL Server.
  
2. Connettersi all'istanza di in cui è stato installato Machine Learning Services, fare clic su **nuova query** per aprire una finestra di query ed eseguire il comando seguente:

    ```sql
    sp_configure
    ```

    A questo punto, il valore della proprietà `external scripts enabled` deve essere **0**. Questo perché la funzionalità è disattivata per impostazione predefinita. Per poter eseguire script R o Python, la funzionalità deve essere abilitata in modo esplicito da un amministratore.
    
3.  Per abilitare la funzionalità di scripting esterno, eseguire l'istruzione seguente:
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    Se è già stata abilitata la funzionalità per il linguaggio R, non eseguire RECONFIGURE una seconda volta per Python. La piattaforma di estensibilità sottostante supporta entrambi i linguaggi.

## <a name="restart-the-service"></a>Riavviare il servizio.

Al termine dell'installazione, riavviare il motore di database prima di continuare con il successivo, abilitando l'esecuzione degli script.

Il riavvio del servizio riavvia automaticamente anche il servizio correlato [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] .

È possibile riavviare il servizio usando il comando di **riavvio** con il pulsante destro del mouse per l'istanza in SSMS oppure usando il pannello **Servizi** nel pannello di controllo oppure usando [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verificare l'installazione

Verificare lo stato di installazione dell'istanza nei [report personalizzati](../r/monitor-r-services-using-custom-reports-in-management-studio.md) o nei log di installazione.

Usare la procedura seguente per verificare che tutti i componenti usati per avviare lo script esterno siano in esecuzione.

1. In SQL Server Management Studio aprire una nuova finestra di query ed eseguire il comando seguente:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    Il valore di **run_value** dovrebbe ora essere impostato su 1.
    
2. Aprire il pannello **Servizi** o Gestione configurazione SQL Server e verificare che **launchpad di SQL Server servizio** sia in esecuzione. È necessario disporre di un servizio per ogni istanza del motore di database in cui è installato R o Python. Per ulteriori informazioni sul servizio, vedere [Extensibility Framework](../concepts/extensibility-framework.md). 
   
3. Se è in esecuzione Launchpad, dovrebbe essere possibile eseguire semplici script R e Python per verificare che i runtime di scripting esterni possano comunicare con SQL Server.

   Aprire una nuova finestra di query [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]in, quindi eseguire uno script come il seguente:
    
    + Per R
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Per Python
    
    ```sql
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    **Risultati**

    L'esecuzione dello script può richiedere un po' di tempo, al primo caricamento del runtime di script esterno. I risultati dovrebbero essere simili ai seguenti:

    | hello |
    |----|
    | 1|

> [!NOTE]
> Le colonne o le intestazioni usate nello script Python non vengono restituite, da progettazione. Per aggiungere nomi di colonna per l'output, è necessario specificare lo schema per il set di dati restituito. A tale scopo, usare il parametro WITH RESULTs del stored procedure, assegnando un nome alle colonne e specificando il tipo di dati SQL.
> 
> È ad esempio possibile aggiungere la riga seguente per generare un nome di colonna arbitrario:`WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Applicazione degli aggiornamenti

Si consiglia di applicare l'aggiornamento cumulativo più recente ai componenti del motore di database e di machine learning.

Nei dispositivi connessi a Internet, gli aggiornamenti cumulativi vengono in genere applicati tramite Windows Update, ma è anche possibile usare la procedura seguente per gli aggiornamenti controllati. Quando si applica l'aggiornamento per il motore di database, il programma di installazione esegue il pull degli aggiornamenti cumulativi per le funzionalità di R o Python installate nella stessa istanza. 

Nei server disconnessi sono necessari passaggi aggiuntivi. Per ulteriori informazioni, vedere [installare in computer senza accesso a internet > applicare aggiornamenti cumulativi](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Iniziare con un'istanza di base già installata: SQL Server 2017 versione iniziale

2. Passare all'elenco degli aggiornamenti cumulativi: [Aggiornamenti di SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)

3. Selezionare l'aggiornamento cumulativo più recente. Un eseguibile viene scaricato ed estratto automaticamente.

4. Eseguire il programma di installazione. Accettare le condizioni di licenza e nella pagina Selezione funzionalità esaminare le funzionalità per le quali vengono applicati gli aggiornamenti cumulativi. Dovrebbero essere visualizzate tutte le funzionalità installate per l'istanza corrente, incluse le funzionalità di machine learning. Il programma di installazione Scarica i file CAB necessari per aggiornare tutte le funzionalità.

  ![Riepilogo delle funzionalità installate](media/cumulative-update-feature-selection.png)

5. Continuare con la procedura guidata, accettando le condizioni di licenza per le distribuzioni R e Python. 

## <a name="additional-configuration"></a>Configurazione aggiuntiva

Se il passaggio di verifica dello script esterno ha avuto esito positivo, è possibile eseguire i comandi R o Python da SQL Server Management Studio, Visual Studio Code o qualsiasi altro client in grado di inviare istruzioni T-SQL al server.

Se si verifica un errore durante l'esecuzione del comando, rivedere i passaggi di configurazione aggiuntivi in questa sezione. Potrebbe essere necessario eseguire configurazioni aggiuntive appropriate per il servizio o il database.

A livello di istanza, la configurazione aggiuntiva potrebbe includere:

* [Configurazione del firewall per SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Abilita protocolli di rete aggiuntivi](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Abilita connessioni remote](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Creare un account di accesso per SQLRUserGroup](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)
* [Gestire le quote disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) per evitare che script esterni eseguano attività che esauriscono lo spazio su disco

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
In SQL Server 2019 in Windows, il meccanismo di isolamento è stato modificato. Ciò influiscono su **SQLRUserGroup**, le regole del firewall, l'autorizzazione per i file e l'autenticazione implicita. Per ulteriori informazioni, vedere [modifiche di isolamento per Machine Learning Services](sql-server-machine-learning-services-2019.md).
::: moniker-end

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

Nel database potrebbero essere necessari gli aggiornamenti della configurazione seguenti:

* [Concedere agli utenti le autorizzazioni per SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md)

> [!NOTE]
> Se è necessaria una configurazione aggiuntiva, dipende dallo schema di sicurezza, da dove è stato installato SQL Server e dal modo in cui si prevede che gli utenti si connettano al database ed eseguano script esterni.

## <a name="suggested-optimizations"></a>Ottimizzazioni suggerite

Ora che tutto funziona, potrebbe essere necessario ottimizzare il server per supportare l'apprendimento automatico o installare modelli con training.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
### <a name="add-more-worker-accounts"></a>Aggiungere altri account di lavoro

Se si prevede che molti utenti eseguano script contemporaneamente, è possibile aumentare il numero di account di lavoro assegnati al servizio launchpad. Per ulteriori informazioni, vedere [modificare il pool di account utente per SQL Server Machine Learning Services](../administration/modify-user-account-pool.md).
::: moniker-end

### <a name="optimize-the-server-for-script-execution"></a>Ottimizzare il server per l'esecuzione di script

Le impostazioni predefinite per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il programma di installazione di consentono di ottimizzare il bilanciamento del server per un'ampia gamma di servizi supportati dal motore di database, che possono includere processi ETL (Extract, Transform and Load), Reporting, controllo e applicazioni che utilizzano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati. Pertanto, in base alle impostazioni predefinite, è possibile che le risorse per Machine Learning siano a volte limitate o limitate, in particolare nelle operazioni con utilizzo intensivo di memoria.

Per assicurarsi che i processi di Machine Learning siano classificati in ordine di priorità e vengano rioriginati in modo appropriato, è consigliabile usare SQL Server Resource Governor per configurare un pool di risorse esterne. Potrebbe anche essere necessario modificare la quantità di memoria allocata al motore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database o aumentare il numero di account eseguiti [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] nel servizio.

- Per configurare un pool di risorse per la gestione delle risorse esterne, vedere [creare un pool di risorse esterne](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Per modificare la quantità di memoria riservata per il database, vedere [Opzioni di configurazione della memoria del server](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Per modificare il numero di account R che possono essere avviati [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]da, vedere [modificare il pool di account utente per Machine Learning](../administration/modify-user-account-pool.md).

Se si utilizza Standard Edition e non si dispone di Resource Governor, è possibile utilizzare le viste a gestione dinamica (DMV) ed eventi estesi, nonché il monitoraggio degli eventi di Windows, per semplificare la gestione delle risorse del server. Per altre informazioni, vedere [monitoraggio e gestione](../r/managing-and-monitoring-r-solutions.md) dei servizi R e [monitoraggio e gestione dei servizi Python](../python/managing-and-monitoring-python-solutions.md).

### <a name="install-additional-r-packages"></a>Installare pacchetti R aggiuntivi

Le soluzioni R create per SQL Server possono chiamare funzioni R di base, funzioni dei pacchetti proprietari installati con SQL Server e pacchetti R di terze parti compatibili con la versione di R Open Source installata da SQL Server.

I pacchetti di SQL Server da usare devono essere installati nella libreria predefinita usata dall'istanza. Se si dispone di un'installazione separata di R nel computer o se sono stati installati pacchetti nelle librerie utente, non sarà possibile usare tali pacchetti da T-SQL.

Per installare e gestire i pacchetti R, è possibile configurare i gruppi di utenti per la condivisione di pacchetti a livello di singolo database o per configurare i ruoli del database per consentire agli utenti di installare i propri pacchetti. Per altre informazioni, vedere [installare nuovi pacchetti R in SQL Server](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori R possono iniziare alcuni semplici esempi e con le nozioni di base sul funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Esercitazione: Analisi nel database per sviluppatori R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Gli sviluppatori Python possono apprendere come usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analisi nel database per sviluppatori Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Per esempi di Machine Learning basati su scenari reali, vedere [Esercitazioni su Machine Learning](../tutorials/machine-learning-services-tutorials.md).
