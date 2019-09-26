---
title: Installare SQL Server 2016 R Services (In-Database)
description: Aggiungere il supporto del linguaggio di programmazione R a un motore di database in SQL Server 2016 R Services in Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/03/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: a255b70b71f29f9cc28e4022ecfdf2741f9a838d
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271878"
---
# <a name="install-sql-server-2016-r-services"></a>Installare SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come installare e configurare **SQL Server 2016 R Services**. Se si dispone di SQL Server 2016, installare questa funzionalità per abilitare l'esecuzione del codice R in SQL Server.

In SQL Server 2017, l'integrazione di R è disponibile in [Machine Learning Services](../r/r-server-standalone.md), che riflette l'aggiunta di Python. Per l'integrazione di R e il supporto di installazione di SQL Server 2017, vedere [Install SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md) per aggiungere la funzionalità. 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Elenco di controllo pre-installazione

+ È necessaria un'istanza del motore di database. Non è possibile installare solo R, sebbene sia possibile aggiungerlo in modo incrementale a un'istanza esistente.

+ Per la continuità aziendale, i [gruppi di disponibilità always on](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) sono supportati per R Services. È necessario installare R Services e configurare i pacchetti in ogni nodo.

+ Non installare R Services in un cluster di failover. Il meccanismo di sicurezza usato per isolare i processi R non è compatibile con un ambiente Windows Server failover cluster.

+ Non installare R Services in un controller di dominio. La parte relativa a R Services dell'installazione avrà esito negativo.

+ Non installare le **funzionalità** > condivise**R Server (standalone)** nello stesso computer in cui è in esecuzione un'istanza di nel database. 

  L'installazione side-by-side con altre versioni di R e Python è possibile perché l'istanza SQL Server usa le proprie copie delle distribuzioni R e Anaconda open source. Tuttavia, l'esecuzione di codice che usa R e Python nel computer SQL Server al di fuori SQL Server può causare vari problemi:
    
  + Si usa una libreria diversa e un file eseguibile diverso e si ottengono risultati diversi rispetto a quando si esegue in SQL Server.
  + Gli script R e Python in esecuzione in librerie esterne non possono essere gestiti da SQL Server, causando conflitti di risorse.
  
Se sono state usate versioni precedenti dell'ambiente di sviluppo Revolution Analytics o dei pacchetti RevoScaleR oppure se sono state installate versioni non definitive di SQL Server 2016, è necessario disinstallarle. L'esecuzione di versioni precedenti e più recenti di RevoScaleR e di altri pacchetti proprietari non è supportata. Per informazioni sulla rimozione di versioni precedenti, vedere [domande frequenti sull'installazione e sull'aggiornamento per SQL Server Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Al termine dell'installazione, assicurarsi di completare i passaggi aggiuntivi successivi alla configurazione descritti in questo articolo. Questi passaggi includono l'abilitazione di SQL Server per l'uso di script esterni e l'aggiunta di account necessari per SQL Server per l'esecuzione di processi R per conto dell'utente. Per le modifiche di configurazione è in genere necessario riavviare l'istanza o riavviare il servizio launchpad.

## <a name="get-the-installation-media"></a>Ottenere il supporto di installazione

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Requisito di installazione patch 

Microsoft ha rilevato un problema con una versione specifica dei file binari di Microsoft VC++ 2013 Runtime installati come prerequisito da SQL Server. Se l'aggiornamento dei file binari di VC++ Runtime non viene installato, potrebbero verificarsi problemi di stabilità di SQL Server in determinati scenari. Prima di installare SQL Server, seguire le istruzioni in [Note sulla versione di SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) per vedere se il computer richiede una patch per i file binari di VC++ Runtime.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'installazione guidata di SQL Server 2016.

2. Nella scheda **installazione** selezionare **nuovo SQL Server installazione autonoma di o aggiunta di funzionalità a un'installazione esistente**.
    
   ![Installare R Services (in-database)](media/2016-setup-installation-rsvcs.png "Avviare l'installazione del motore di database con R Services")
   
3. Nella pagina **Selezione funzionalità** selezionare le opzioni seguenti:

   - Selezionare **servizi motore di database**. Il motore di database è necessario in ogni istanza che usa Machine Learning.
   - Selezionare **R Services (in-database)** . Installa il supporto per l'uso nel database di R.
    
     ![Selezione delle funzionalità di R Services](media/2016setup-rsvcs-features.png "Selezionare queste funzionalità per R Services nel database")

    > [!IMPORTANT]
    > Non installare R Server e R Services nello stesso momento. Normalmente si installeranno R Server (standalone) per creare un ambiente usato da un data scientist o da uno sviluppatore per connettersi SQL Server e distribuire soluzioni R. Non è quindi necessario installare entrambe le soluzioni nello stesso computer.

4.  Nella pagina **consenso per l'installazione di Microsoft R Open** fare clic su **Accetto**.
  
    Questo contratto di licenza è necessario per scaricare Microsoft R Open, che include una distribuzione di pacchetti e strumenti di base R Open Source, insieme a pacchetti R avanzati e provider di connettività del team di sviluppo Microsoft R.
  
5. Dopo aver accettato il contratto di licenza, si verifica una breve pausa durante la preparazione del programma di installazione. Quando il pulsante diventa disponibile, fare clic su **Avanti** .

6. Nella pagina **pronto per l'installazione** verificare che siano inclusi gli elementi seguenti e quindi selezionare **Installa**.

   + Servizi motore di database
   + R Services (In-Database)

    Prendere nota del percorso della cartella nel percorso `..\Setup Bootstrap\Log` in cui sono archiviati i file di configurazione. Al termine dell'installazione, è possibile esaminare i componenti installati nel file di riepilogo.

7. Al termine dell'installazione, se viene richiesto di riavviare il computer, eseguirlo ora. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Imposta variabili di ambiente

Per l'integrazione della funzionalità R, è necessario impostare la variabile di ambiente **MKL_CBWR** per [garantire l'output coerente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli di Intel Math Kernel Library (MKL).

1. Nel pannello di controllo fare clic su sistema **e sicurezza** > **sistema** > **Impostazioni** > di sistema avanzate**variabili di ambiente**.

2. Creare un nuovo utente o una variabile di sistema. 

  + Imposta nome variabile su`MKL_CBWR`
  + Impostare il valore della variabile su`AUTO`

Per questo passaggio è necessario riavviare il server. Se si sta per abilitare l'esecuzione di script, è possibile disattivare il riavvio fino a quando non vengono eseguite tutte le operazioni di configurazione.

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>Abilitare l'esecuzione di script

1. Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > È possibile scaricare e installare la versione appropriata da questa pagina: [Scaricare SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > È anche possibile provare la versione di anteprima di [Azure Data Studio](../../azure-data-studio/what-is.md), che supporta le attività amministrative e le query su SQL Server.
  
2. Connettersi all'istanza di in cui è stato installato Machine Learning Services, fare clic su **nuova query** per aprire una finestra di query ed eseguire il comando seguente:

   ```sql
   sp_configure
   ```
    A questo punto, il valore della proprietà `external scripts enabled` deve essere **0**. Questo perché la funzionalità è disattivata per impostazione predefinita. Per poter eseguire script R o Python, la funzionalità deve essere abilitata in modo esplicito da un amministratore.
     
3. Per abilitare la funzionalità di scripting esterno, eseguire l'istruzione seguente:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Riavviare il servizio.

Al termine dell'installazione, riavviare il motore di database prima di continuare con il successivo, abilitando l'esecuzione degli script.

Il riavvio del servizio riavvia automaticamente anche il servizio correlato [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] .

È possibile riavviare il servizio usando il comando di **riavvio** con il pulsante destro del mouse per l'istanza in SSMS oppure usando il pannello **Servizi** nel pannello di controllo oppure usando [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verificare l'installazione

Verificare lo stato di installazione dell'istanza di utilizzando [report personalizzati](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Usare la procedura seguente per verificare che tutti i componenti usati per avviare lo script esterno siano in esecuzione.

1. In SQL Server Management Studio aprire una nuova finestra di query ed eseguire il comando seguente:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    Il valore di **run_value** dovrebbe ora essere impostato su 1.

2. Aprire il pannello **Servizi** o Gestione configurazione SQL Server e verificare che **launchpad di SQL Server servizio** sia in esecuzione. È necessario disporre di un servizio per ogni istanza del motore di database in cui è installato R o Python. Per ulteriori informazioni sul servizio, vedere [Extensibility Framework](../concepts/extensibility-framework.md).

7. Se la finestra di avvio è in esecuzione, dovrebbe essere possibile eseguire una semplice R per verificare che i runtime di scripting esterni possano comunicare con SQL Server. 

    Aprire una nuova finestra di query [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]in, quindi eseguire uno script come il seguente:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    L'esecuzione dello script può richiedere un po' di tempo, al primo caricamento del runtime di script esterno. I risultati dovrebbero essere simili ai seguenti:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Applicazione degli aggiornamenti

Si consiglia di applicare l'aggiornamento cumulativo più recente ai componenti del motore di database e di machine learning.

Nei dispositivi connessi a Internet, gli aggiornamenti cumulativi vengono in genere applicati tramite Windows Update, ma è anche possibile usare la procedura seguente per gli aggiornamenti controllati. Quando si applica l'aggiornamento per il motore di database, il programma di installazione esegue il pull degli aggiornamenti cumulativi per le librerie R installate nella stessa istanza. 

Nei server disconnessi sono necessari passaggi aggiuntivi. Per ulteriori informazioni, vedere [installare in computer senza accesso a internet > applicare aggiornamenti cumulativi](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Iniziare con un'istanza di base già installata: SQL Server 2016 versione iniziale, SQL Server 2016 SP 1 o SQL Server 2016 SP 2.

2. Passare all'elenco degli aggiornamenti cumulativi: [Aggiornamenti di SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Selezionare l'aggiornamento cumulativo più recente. Un eseguibile viene scaricato ed estratto automaticamente.

4. Eseguire il programma di installazione. Accettare le condizioni di licenza e nella pagina Selezione funzionalità esaminare le funzionalità per le quali vengono applicati gli aggiornamenti cumulativi. Dovrebbero essere visualizzate tutte le funzionalità installate per l'istanza corrente, inclusi R Services. Il programma di installazione Scarica i file CAB necessari per aggiornare tutte le funzionalità.

5. Continuare con la procedura guidata, accettando le condizioni di licenza per la distribuzione di R. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Configurazione aggiuntiva

Se il passaggio di verifica dello script esterno ha avuto esito positivo, è possibile eseguire i comandi Python da SQL Server Management Studio, Visual Studio Code o qualsiasi altro client in grado di inviare istruzioni T-SQL al server.

Se si verifica un errore durante l'esecuzione del comando, rivedere i passaggi di configurazione aggiuntivi in questa sezione. Potrebbe essere necessario eseguire configurazioni aggiuntive appropriate per il servizio o il database.

A livello di istanza, la configurazione aggiuntiva potrebbe includere:

* [Configurazione del firewall per SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Abilita protocolli di rete aggiuntivi](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Abilita connessioni remote](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Gestire le quote disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) per evitare che script esterni eseguano attività che esauriscono lo spazio su disco

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

Nel database potrebbero essere necessari gli aggiornamenti della configurazione seguenti:

* [Concedere agli utenti le autorizzazioni per SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md)
* [Aggiungere SQLRUserGroup come utente del database](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> Non tutte le modifiche elencate sono necessarie e nessuna potrebbe essere necessaria. I requisiti dipendono dallo schema di sicurezza, dal punto in cui è stato installato SQL Server e dal modo in cui si prevede che gli utenti si connettano al database ed eseguono script esterni. Ulteriori suggerimenti per la risoluzione dei problemi sono disponibili qui: [Domande frequenti sull'installazione e sull'aggiornamento](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Ottimizzazioni suggerite

Ora che tutto funziona, potrebbe essere necessario ottimizzare il server per supportare l'apprendimento automatico o installare modelli con training.

### <a name="add-more-worker-accounts"></a>Aggiungere altri account di lavoro

Se si pensa di usare R in modo intensivo o se si prevede che molti utenti eseguano script contemporaneamente, è possibile aumentare il numero di account di lavoro assegnati al servizio launchpad. Per ulteriori informazioni, vedere [modificare il pool di account utente per SQL Server Machine Learning Services](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Ottimizzare il server per l'esecuzione di script esterni

Le impostazioni predefinite per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il programma di installazione di consentono di ottimizzare il bilanciamento del server per un'ampia gamma di servizi supportati dal motore di database, che possono includere processi ETL (Extract, Transform and Load), Reporting, controllo e applicazioni che utilizzano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati. Pertanto, in base alle impostazioni predefinite, è possibile che le risorse per Machine Learning siano a volte limitate o limitate, in particolare nelle operazioni con utilizzo intensivo di memoria.

Per assicurarsi che i processi di Machine Learning siano classificati in ordine di priorità e vengano rioriginati in modo appropriato, è consigliabile usare SQL Server Resource Governor per configurare un pool di risorse esterne. Potrebbe anche essere necessario modificare la quantità di memoria allocata al motore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database o aumentare il numero di account eseguiti [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] nel servizio.

- Per configurare un pool di risorse per la gestione delle risorse esterne, vedere [creare un pool di risorse esterne](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Per modificare la quantità di memoria riservata per il database, vedere [Opzioni di configurazione della memoria del server](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Per modificare il numero di account R che possono essere avviati [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]da, vedere [modificare il pool di account utente per Machine Learning](../administration/modify-user-account-pool.md).

Se si usa Standard Edition e non si dispone di Resource Governor, è possibile usare le viste a gestione dinamica (DMV) ed eventi estesi, nonché il monitoraggio degli eventi di Windows, per semplificare la gestione delle risorse del server usate da R. Per altre informazioni, vedere [monitoraggio e gestione di R Services](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Installare pacchetti R aggiuntivi

Le soluzioni R create per SQL Server possono chiamare funzioni R di base, funzioni dei pacchetti proprietari installati con SQL Server e pacchetti R di terze parti compatibili con la versione di R Open Source installata da SQL Server.

I pacchetti di SQL Server da usare devono essere installati nella libreria predefinita usata dall'istanza. Se si dispone di un'installazione separata di R nel computer o se sono stati installati pacchetti nelle librerie utente, non sarà possibile usare tali pacchetti da T-SQL.

Il processo di installazione e gestione dei pacchetti R è diverso in SQL Server 2016 e SQL Server 2017. In SQL Server 2016, un amministratore di database deve installare i pacchetti R necessari agli utenti. In SQL Server 2017 è possibile configurare i gruppi di utenti per condividere i pacchetti a livello di database oppure configurare i ruoli del database per consentire agli utenti di installare i propri pacchetti. Per altre informazioni, vedere [installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori R possono iniziare alcuni semplici esempi e con le nozioni di base sul funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Esercitazione: Analisi nel database per sviluppatori R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Per esempi di Machine Learning basati su scenari reali, vedere [Esercitazioni su Machine Learning](../tutorials/machine-learning-services-tutorials.md).