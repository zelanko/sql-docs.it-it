---
title: Installare SQL Server 2016 R Services (In-Database)
description: Aggiungere il supporto del linguaggio di programmazione R a un motore di database in R Services per SQL Server 2016 in Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6fcb4245d4efff00002dea9b490312792e0d83d6
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338931"
---
# <a name="install-sql-server-2016-r-services"></a>Installare R Services per SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come installare e configurare **R Services per SQL Server 2016**. Se si dispone di SQL Server 2016, installare questa funzionalità per abilitare l'esecuzione di codice R in SQL Server.

In SQL Server 2017, l'integrazione di R è disponibile in [Machine Learning Services](../r/r-server-standalone.md), di riflesso all'aggiunta di Python. Se si vuole avere l'integrazione di R insieme al supporto di installazione di SQL Server 2017, vedere [Installare Machine Learning Services per SQL Server](sql-machine-learning-services-windows-install.md) per aggiungere la funzionalità. 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Elenco di controllo preliminare all'installazione

+ È necessaria un'istanza del motore di database. Non è possibile installare solo il componente per R, ma è possibile aggiungerlo in modo incrementale a un'istanza esistente.

+ Per assicurare la continuità aziendale, per R Services è disponibile il supporto di [Gruppi di disponibilità AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server). È necessario installare R Services e configurare i pacchetti in ogni nodo.

+ Non installare R Services in un cluster di failover. Questo requisito è dovuto al fatto che il meccanismo di sicurezza usato per isolare i processi R non è compatibile con un ambiente di cluster di failover Windows Server.

+ Non installare R Services in un controller di dominio. La parte del programma di installazione relativa a R Services avrà esito negativo.

+ Non installare **Funzionalità condivise** > **R Server (Standalone)** nello stesso computer su cui è in esecuzione un'istanza di tipo In-Database. 

  L'installazione side-by-side con altre versioni di R e Python è possibile perché l'istanza di SQL Server usa le proprie copie delle distribuzioni R e Anaconda open source. Tuttavia, l'esecuzione di codice che usa R e Python nel computer di SQL Server al di fuori di SQL Server può causare vari problemi:
    
  + Si usano una libreria e un file eseguibile diverso e quindi si ottengono risultati diversi rispetto all'esecuzione del codice in SQL Server.
  + Gli script R e Python in esecuzione in librerie esterne non possono essere gestiti da SQL Server, con conseguenti conflitti di risorse.
  
Se è stata usata una versione precedente dell'ambiente di sviluppo Revolution Analytics o dei pacchetti RevoScaleR oppure è stata installata una versione non definitiva di SQL Server 2016, è prima necessario eseguirne la disinstallazione. L'esecuzione di versioni precedenti e più recenti di RevoScaleR e di altri pacchetti proprietari non è supportata. Per informazioni sulla rimozione delle versioni precedenti, vedere [Domande frequenti sull'installazione e sull'aggiornamento di Machine Learning Services per SQL Server](../r/upgrade-and-installation-faq-sql-server-r-services.md)

> [!IMPORTANT]
> Al termine dell'installazione, assicurarsi di completare i passaggi aggiuntivi di post-configurazione descritti in questo articolo, tra cui l'abilitazione di SQL Server per l'uso di script esterni e l'aggiunta degli account necessari per consentire a SQL Server di eseguire i processi R per conto dell'utente. Per completare le modifiche alla configurazione è in genere necessario riavviare l'istanza o riavviare il servizio Launchpad.

## <a name="get-the-installation-media"></a>Ottenere il supporto di installazione

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Requisito di installazione di patch 

Microsoft ha rilevato un problema con una versione specifica dei file binari di Microsoft VC++ 2013 Runtime installati come prerequisito da SQL Server. Se l'aggiornamento dei file binari di VC++ Runtime non viene installato, potrebbero verificarsi problemi di stabilità di SQL Server in determinati scenari. Prima di installare SQL Server, seguire le istruzioni in [Note sulla versione di SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) per vedere se il computer richiede una patch per i file binari di VC++ Runtime.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'Installazione guidata di SQL Server 2016.

2. Nella scheda **Installazione** selezionare **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.
    
   ![Installare R Services (In-Database)](media/2016-setup-installation-rsvcs.png "Avviare l'installazione del motore di database con R Services")
   
3. Nella pagina **Selezione funzionalità** selezionare le opzioni seguenti:

   - Selezionare **Servizi motore di database**. Il motore di database è necessario in ogni istanza che usa funzionalità di Machine Learning.
   - Selezionare **R Services (In-Database)** . Questa opzione consente di installare il supporto per l'uso nel database di R.
    
     ![Selezione della funzionalità R Services](media/2016setup-rsvcs-features.png "Selezionare queste funzionalità per R Services In-Database")

    > [!IMPORTANT]
    > Non installare contemporaneamente R Server e R Services. In genere si installa R Server (Standalone) per creare un ambiente che un data scientist o uno sviluppatore usa per connettersi a SQL Server e distribuire soluzioni R. Non è quindi necessario installare entrambe le soluzioni nello stesso computer.

4.  Nella pagina **Consenso per installare Microsoft R Open** fare clic su **Accetto**.
  
    Questo contratto di licenza deve essere accettato per il download di Microsoft R Open, che include una distribuzione di pacchetti e strumenti R open source di base, insieme a pacchetti R avanzati e a provider di connettività del team Microsoft dedicato allo sviluppo di soluzioni R.
  
5. Dopo l'accettazione del contratto di licenza, si verifica una breve pausa di preparazione del programma di installazione. Quando il pulsante diventa disponibile, fare clic su **Avanti**.

6. Nella pagina **Inizio installazione** verificare che siano incluse le opzioni seguenti e selezionare **Installa**.

   + Servizi motore di database
   + R Services (In-Database)

    Si noti la posizione della cartella nel percorso `..\Setup Bootstrap\Log` in cui sono archiviati i file di configurazione. Al termine dell'installazione, è possibile esaminare i componenti installati nel file Summary.

7. Dopo che l'installazione è completata, riavviare il computer, se richiesto. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente

Per integrare solo le funzionalità di R, è necessario impostare la variabile di ambiente **MKL_CBWR** per avere la certezza di [ottenere un output coerente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli di Intel Math Kernel Library (MKL).

1. Nel Pannello di controllo fare clic su **Sistema e sicurezza** > **Sistema** > **Impostazioni di sistema avanzate** > **Variabili d'ambiente**.

2. Creare una nuova variabile dell'utente o di sistema. 

  + Impostare `MKL_CBWR` come nome della variabile
  + Impostare `AUTO` come valore della variabile

Per questo passaggio è necessario riavviare il server. Se si intende abilitare l'esecuzione di script, è possibile sospendere il riavvio fino a quando non sono state completate tutte le operazioni di configurazione.

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>Abilitare l'esecuzione di script

1. Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > È possibile scaricare e installare la versione appropriata da questa pagina: [Scaricare SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > È anche possibile usare [Azure Data Studio](../../azure-data-studio/what-is.md), che supporta l'esecuzione di attività amministrative e query in SQL Server.
  
2. Connettersi all'istanza in cui è stato installato Machine Learning Services, fare clic su **Nuova query** per aprire una finestra di query ed eseguire il comando seguente:

   ```sql
   sp_configure
   ```
    A questo punto, il valore della proprietà `external scripts enabled` deve essere **0**. Questo perché la funzionalità è disattivata per impostazione predefinita. Prima di poter eseguire script R o Python, la funzionalità deve essere abilitata in modo esplicito da un amministratore.
     
3. Per abilitare la funzionalità per script esterni, eseguire l'istruzione seguente:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Riavviare il servizio.

Al termine dell'installazione, riavviare il motore di database prima di continuare con il passaggio successivo, abilitando l'esecuzione degli script.

Il riavvio del servizio ha l'effetto di riavviare automaticamente anche il servizio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] correlato.

Per riavviare il servizio è possibile eseguire il comando **Riavvia** del menu di scelta rapida per l'istanza in SSMS oppure usare il pannello **Servizi** del Pannello di controllo o [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verificare l'installazione

Verificare lo stato di installazione dell'istanza usando [report personalizzati](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Usare la procedura seguente per verificare che tutti i componenti usati per avviare lo script esterno siano in esecuzione.

1. In SQL Server Management Studio aprire una nuova finestra di query ed eseguire il comando seguente:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    Il valore di **run_value** dovrebbe ora essere impostato su 1.

2. Aprire il pannello **Servizi** o Gestione configurazione SQL Server e verificare che il **servizio Launchpad di SQL Server** sia in esecuzione. Dovrebbe essere in esecuzione un solo servizio per ogni istanza del motore di database in cui è installato R o Python. Per altre informazioni sul servizio, vedere [Framework di estendibilità](../concepts/extensibility-framework.md).

7. Se Launchpad è in esecuzione, dovrebbe essere possibile eseguire codice R semplice per verificare che i runtime di script esterni possano comunicare con SQL Server. 

    Aprire una nuova finestra **Query** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e quindi eseguire uno script come il seguente:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    La prima volta che viene caricato il runtime di uno script esterno, l'esecuzione dello script può richiedere un po' di tempo. I risultati saranno simili ai seguenti:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Applicare gli aggiornamenti

È consigliabile applicare l'aggiornamento cumulativo più recente sia al motore di database sia ai componenti di Machine Learning.

Nei dispositivi connessi a Internet, gli aggiornamenti cumulativi vengono in genere applicati tramite Windows Update, ma è anche possibile usare la procedura seguente per eseguire aggiornamenti controllati. Quando si applica l'aggiornamento per il motore di database, il programma di installazione esegue il pull degli aggiornamenti cumulativi per le librerie R installate nella stessa istanza. 

Nei server che non sono connessi a Internet sono necessari alcuni passaggi aggiuntivi. Per altre informazioni, vedere [Installare in computer senza accesso a Internet > Applicare aggiornamenti cumulativi](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Iniziare con un'istanza di base già installata: la versione iniziale di SQL Server 2016 oppure SQL Server 2016 SP 1 o SQL Server 2016 SP 2.

2. Passare all'elenco degli aggiornamenti cumulativi: [Aggiornamenti di SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Selezionare l'aggiornamento cumulativo più recente. L'eseguibile viene scaricato ed estratto automaticamente.

4. Eseguire il programma di installazione. Accettare le condizioni di licenza e nella pagina Selezione funzionalità esaminare le funzionalità per le quali vengono applicati gli aggiornamenti cumulativi. Dovrebbero essere visualizzate tutte le funzionalità installate per l'istanza corrente, incluso R Services. Il programma di installazione scarica i file CAB necessari per aggiornare tutte le funzionalità.

5. Continuare con la procedura guidata, accettando le condizioni di licenza per la distribuzione R. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Configurazione aggiuntiva

Se la verifica degli script esterni ha esito positivo, è possibile eseguire comandi Python da SQL Server Management Studio, Visual Studio Code o qualsiasi altro client che può inviare istruzioni T-SQL al server.

Se durante l'esecuzione del comando è stato restituito un errore, rivedere i passaggi di configurazione aggiuntivi in questa sezione. Potrebbe essere necessario eseguire specifiche configurazioni aggiuntive per il servizio o il database.

A livello di istanza, la configurazione aggiuntiva può includere:

* [Configurare il firewall per SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Abilitare protocolli di rete aggiuntivi](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Abilitare connessioni remote](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Gestire le quote disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) per evitare che gli script esterni eseguano attività che esauriscono lo spazio su disco

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

Nel database potrebbero essere necessari gli aggiornamenti di configurazione seguenti:

* [Concedere agli utenti l'autorizzazione per SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md)
* [Aggiungere SQLRUserGroup come utente del database](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> Non tutte le modifiche elencate sono obbligatorie ed è anche possibile che nessuna di queste lo sia. I requisiti dipendono dallo schema di sicurezza, dal percorso in cui è stato installato SQL Server e dalla modalità presumibilmente adottata dagli utenti per connettersi al database ed eseguire script esterni. Altri suggerimenti per la risoluzione dei problemi sono disponibili qui: [Domande frequenti sull'installazione e sull'aggiornamento](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Ottimizzazioni suggerite

Ora che tutto il sistema funziona, può essere necessario ottimizzare il server per supportare le funzionalità di Machine Learning o installare modelli già sottoposti a un training preliminare.

### <a name="add-more-worker-accounts"></a>Aggiungere altri account di lavoro

Se si pensa di usare R in modo intensivo o si prevede che molti utenti eseguano script contemporaneamente, è possibile aumentare il numero di account di lavoro assegnati al servizio Launchpad. Per altre informazioni, vedere [Modificare il pool di account utente per Machine Learning Services per SQL Server](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Ottimizzare il server per l'esecuzione di script esterni

Le impostazioni predefinite per il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consentono di ottimizzare il bilanciamento del server per un'ampia gamma di servizi supportati dal motore di database, che possono includere processi di estrazione, trasformazione e caricamento (ETL), servizi di controllo e creazione di report e applicazioni che usano dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Di conseguenza, con le impostazioni predefinite, è possibile che alle risorse per il Machine Learning siano applicate restrizioni o limitazioni, in particolare nel caso di operazioni che richiedono molta memoria.

Per assicurarsi che i processi di Machine Learning siano considerati come prioritari e dispongano delle risorse appropriate, è consigliabile usare la funzionalità Resource Governor di SQL Server per configurare un pool di risorse esterne. Può inoltre essere opportuno modificare la quantità di memoria allocata al motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o aumentare il numero di account eseguiti con il servizio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)].

- Per configurare un pool di risorse per la gestione delle risorse esterne, vedere [Creare un pool di risorse esterne](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Per modificare la quantità di memoria riservata per il database, vedere [Opzioni di configurazione server memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Per modificare il numero di account R che possono essere avviati da [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], vedere [Modificare il pool di account utente per Machine Learning](../administration/modify-user-account-pool.md).

Se si usa l'edizione Standard e non è disponibile Resource Governor, per gestire le risorse del server usate da R è possibile usare le viste a gestione dinamica (DMV) e gli eventi estesi, oltre che il monitoraggio eventi di Windows. Per altre informazioni, vedere [Gestione e monitoraggio di soluzioni R](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Installare pacchetti R aggiuntivi

Le soluzioni R create per SQL Server possono chiamare funzioni R di base, funzioni dei pacchetti proprietari installati con SQL Server e pacchetti R di terze parti compatibili con la versione di R open source installata da SQL Server.

I pacchetti di SQL Server da usare devono essere installati nella libreria predefinita usata dall'istanza. Se si ha un'installazione separata di R nel computer oppure se i pacchetti sono stati installati nelle librerie utente, non sarà possibile usare tali pacchetti da T-SQL.

Il processo di installazione e gestione dei pacchetti R in SQL Server 2016 è diverso da quello in SQL Server 2017. In SQL Server 2016, un amministratore di database deve installare i pacchetti R necessari agli utenti. In SQL Server 2017, è possibile configurare gruppi di utenti per condividere i pacchetti a livello di singolo database oppure configurare ruoli di database per consentire agli utenti di installare i propri pacchetti. Per altre informazioni, vedere [Installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori R possono iniziare alcuni semplici esempi e con le nozioni di base sul funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Esercitazione: Analisi nel database per sviluppatori R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Per esempi di Machine Learning basati su scenari reali, vedere [Esercitazioni su Machine Learning](../tutorials/machine-learning-services-tutorials.md).