---
title: Installare SQL Server Machine Learning Services (In-Database) in Windows - SQL Server Machine Learning
description: R in SQL Server o Python sui passaggi di installazione di SQL Server per SQL Server 2017 Machine Learning Services in Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/03/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 088a553b28e968c1241486040de3c628fd6299cc
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65097297"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>Installare SQL Server Machine Learning Services in Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A partire da SQL Server 2017, R e Python supportano per analitica nel database viene fornito **servizi di SQL Server Machine Learning**, il successore [SQL Server R Services](../r/sql-server-r-services.md) introdotta in SQL Server 2016. Librerie di funzioni sono disponibili in R e Python ed eseguire come script esterni in un'istanza del motore di database. 

Questo articolo illustra come installare il componente di machine learning tramite l'esecuzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installazione guidata e segue il le istruzioni visualizzate.

## <a name="bkmk_prereqs"> </a> Elenco di controllo pre-installazione

+ Installazione SQL Server 2017 (o versione successiva) è obbligatorio se si desidera installare servizi di Machine Learning con supporto del linguaggio R, Python o Java. Se invece si dispone di supporto di installazione di SQL Server 2016, è possibile installare [SQL Server 2016 R Services (In-Database)](sql-r-services-windows-install.md) per ottenere supporto del linguaggio R.

+ È necessaria un'istanza di motore di database. È possibile installare solo le funzionalità R o Python, anche se è possibile aggiungerli in modo incrementale a un'istanza esistente.

+ Per la continuità aziendale, [Availabilty gruppi AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) sono supportati per i servizi di Machine Learning. È necessario installare servizi di Machine Learning e configurare pacchetti, in ogni nodo.

+ L'installazione di servizi di Machine Learning è *non è supportato* in un cluster di failover in SQL Server 2017. Tuttavia, si *è supportata* con SQL Server 2019. 
 
+ Non installare servizi di Machine Learning in un controller di dominio. La parte di servizi di Machine Learning del programma di installazione avrà esito negativo.

+ Non installare **funzionalità condivise** > **Machine Learning Server (Standalone)** nello stesso computer che esegue un'istanza nel database. Un server autonomo verrà si contendono le risorse stesse, compromettendo le prestazioni di entrambe le installazioni.

+ Installazione side-by-side con altre versioni di R e Python è supportata ma non consigliata. È supportata perché istanza di SQL Server Usa una proprio copie delle distribuzioni open source R e Anaconda. Ma non è consigliabile perché l'esecuzione del codice che usa R e Python nel computer SQL Server all'esterno di SQL Server può causare problemi diversi:
    
  + Si usa una libreria diversa e un diverso eseguibile e ottengano risultati diversi, rispetto a quando si eseguono in SQL Server.
  + Gli script R e Python in esecuzione nelle librerie esterne non possono essere gestiti da SQL Server, causando una contesa delle risorse.
  
> [!IMPORTANT]
> Al termine dell'installazione, assicurarsi di completare i passaggi di post-configurazione descritti in questo articolo. Tali passaggi includono l'abilitazione di SQL Server per usare gli script esterni e l'aggiunta di account necessari per SQL Server eseguire processi R e Python per tuo conto. Le modifiche alla configurazione in genere richiedono un riavvio dell'istanza o un riavvio del servizio Launchpad.

## <a name="get-the-installation-media"></a>Ottenere il supporto di installazione

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'installazione guidata di SQL Server 2017. È possibile scaricare 
  
2. Nel **installazione** scheda, seleziona **nuova installazione SQL Server autonomo o aggiungere caratteristiche a un'installazione esistente**.

   ![Nuova installazione autonoma di SQL Server](media/2017setup-installation-page-mlsvcs.PNG)
   
3. Nella pagina **Selezione funzionalità** selezionare queste opzioni:
  
    -   **Servizi motore di database**
  
         Per usare R e Python con SQL Server, è necessario installare un'istanza del motore di database. È possibile usare un valore predefinito o un'istanza denominata.
  
    -   **Machine Learning Services (In-Database)**
  
         Questa opzione per installare i servizi di database che supportano R e l'esecuzione di script Python.

    -   **R**

        Selezionare questa opzione per aggiungere i pacchetti Microsoft R, interprete e open source R. 

    -   **Python**

        Selezionare questa opzione per aggiungere i pacchetti Python di Microsoft, il file eseguibile Python 3.5 e selezionare la distribuzione Anaconda librerie.
        
        ![Opzioni per R e Python delle funzionalità](media/2017setup-features-page-mls-rpy.png "opzioni di installazione per Python")

        > [!NOTE]
        > 
        > Non selezionare l'opzione **Machine Learning Server (Standalone)**. L'opzione di installazione di Machine Learning Server sotto **Caratteristiche condivise** è destinato all'uso in un computer separato.

4. Nel **fornire il consenso per installare R** pagina, selezionare **Accept**. Il contratto di licenza include Microsoft R Open, che include una distribuzione di pacchetti R open source di base e strumenti, insieme a pacchetti R avanzati e provider di connettività dal team di sviluppo Microsoft.

5. Nel **fornire il consenso per installare Python** pagina, selezionare **Accept**. Il contratto di licenza open source di Python include inoltre Anaconda e strumenti correlati, nonché alcune nuove librerie Python dal team di sviluppo Microsoft.
     
     ![Contratto di licenza di Python](media/2017setup-python-license.png "licenza contratto per Python")
  
    > [!NOTE]
    >  Se il computer in che uso non ha accesso a internet, è possibile sospendere il programma di installazione in questo momento per scaricare i programmi di installazione separatamente. Per altre informazioni, vedere [installa i componenti di apprendimento automatico senza accesso a internet](../install/sql-ml-component-install-without-internet-access.md).
  
     Selezionare **Accept**, attendere finché il **successiva** pulsante diventa attivo e quindi selezionare **Avanti**.
  
6. Nel **pronto per l'installazione** pagina, verificare che queste selezioni sono incluse e selezionare **installare**.
  
    + Servizi motore di database
    + Machine Learning Services (In-Database)
    + R o Python oppure entrambi

    Nota del percorso della cartella nel percorso `..\Setup Bootstrap\Log` in cui sono archiviati i file di configurazione. Una volta completato il programma di installazione, è possibile esaminare i componenti installati nel file di riepilogo.

7. Al termine dell'installazione, se viene richiesto di riavviare il computer, farlo ora. È importante leggere il messaggio visualizzato nell'Installazione guidata al termine dell'installazione. Per altre informazioni, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente

Per l'integrazione solo con R funzionalità, è consigliabile impostare il **MKL_CBWR** variabile di ambiente [garantire coerenti con l'output](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli Intel Math Kernel Library (MKL).

1. Nel Pannello di controllo, fare clic su **sistema e sicurezza** > **System** > **impostazioni di sistema avanzate**  >   **Le variabili di ambiente**.

2. Creare una nuova variabile di sistema o dell'utente. 

  + Nome della variabile set a `MKL_CBWR`
  + Impostare il valore della variabile `AUTO`

Questo passaggio richiede un riavvio del server. Se sta tentando di abilitare l'esecuzione dello script, è possibile rimandare il riavvio fino al completamento del tutto il lavoro di configurazione.

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>Abilitare l'esecuzione di script

1. Aprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > È possibile scaricare e installare la versione appropriata da questa pagina: [Scaricare SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > È anche possibile provare la versione di anteprima dei [Studio di Azure Data](../../azure-data-studio/what-is.md), che supporta le attività amministrative e query su SQL Server.
  
2. Connettersi all'istanza in cui è installato Servizi di Machine Learning, fare clic su **nuova Query** per aprire una finestra query ed eseguire il comando seguente:

   ```sql
   sp_configure
   ```

    A questo punto, il valore della proprietà `external scripts enabled` deve essere **0**. Ciò avviene perché la funzionalità è disattivata per impostazione predefinita. La funzionalità deve essere abilitata in modo esplicito da un amministratore prima di poter eseguire script R o Python.
    
3.  Per abilitare la funzionalità di script esterne, eseguire l'istruzione seguente:
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    Se è già stata abilitata la funzionalità per il linguaggio R, non vengono eseguiti riconfigurare una seconda volta per Python. La piattaforma di estendibilità sottostante supporta entrambi i linguaggi.

## <a name="restart-the-service"></a>Riavviare il servizio.

Una volta completata l'installazione, riavviare il motore di database prima di procedere al successivo, consentendo l'esecuzione dello script.

Riavviare automaticamente anche il servizio viene riavviato correlato [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servizio.

È possibile riavviare il servizio utilizzando il pulsante destro del mouse **riavviare** comando per l'istanza di SQL Server Management Studio o tramite il **Services** pannello nel Pannello di controllo oppure usando [Gestione configurazione SQL Server ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verificare l'installazione

Controllare lo stato di installazione dell'istanza nel [report personalizzati](../r/monitor-r-services-using-custom-reports-in-management-studio.md) o log di installazione.

Utilizzare la procedura seguente per verificare che tutti i componenti usati per avviare script esterni siano in esecuzione.

1. In SQL Server Management Studio, aprire una nuova finestra query ed eseguire il comando seguente:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    Il valore di **run_value** dovrebbe ora essere impostato su 1.
    
2. Aprire il **Services** pannello o Gestione configurazione SQL Server e verificare **Launchpad di SQL Server service** è in esecuzione. È necessario un servizio per ogni istanza di motore di database con R o Python installato. Per altre informazioni sul servizio, vedere [framework di estendibilità](../concepts/extensibility-framework.md). 
   
3. Se Launchpad è in esecuzione, è necessario essere in grado di eseguire semplici script R e Python per verificare che il runtime di scripting esterno possa comunicare con SQL Server.

   Aprire una nuova **Query** finestra in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], quindi eseguire uno script simile al seguente:
    
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

    Lo script può richiedere del tempo per l'esecuzione, la prima volta che viene caricato il runtime dello script esterno. I risultati dovrebbero essere simile al seguente:

    | hello |
    |----|
    | 1|


<!--  The preceding 'hello' table is NOT rendering properly on live Docs.
Instead, the RAW markdown for the table is being displayed.  Probable bug in this markdown source,
due to stricter rules imposed by 'markdig' engine (replaced 'DFM').
I will inform HeidiSteen  [GeneMi, 2019/01/17]
-->


> [!NOTE]
> Le colonne o le intestazioni usate nello script di Python non vengono restituite, per impostazione predefinita. Per aggiungere nomi di colonna per l'output, è necessario specificare lo schema per il set di dati restituito. Eseguire questa operazione usando il parametro con risultati della stored procedure, le colonne di denominazione e specificando il tipo di dati SQL.
> 
> Ad esempio, è possibile aggiungere la riga seguente per generare un nome di colonna arbitrario: `WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Applicazione degli aggiornamenti

È consigliabile applicare l'aggiornamento cumulativo più recente per il motore di database e i componenti di apprendimento automatico.

Sui dispositivi connessi a internet, gli aggiornamenti cumulativi vengono in genere applicati tramite Windows Update, ma è anche possibile usare i passaggi seguenti per gli aggiornamenti controllati. Quando si applica l'aggiornamento del motore di database, il programma di installazione esegue il pull gli aggiornamenti cumulativi per qualsiasi funzionalità di R o Python che è installato nella stessa istanza. 

Nei server disconnesso, sono necessarie operazioni aggiuntive. Per altre informazioni, vedere [installare nei computer senza accesso a internet > applicare aggiornamenti cumulativi](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Iniziare con un'istanza della linea di base già installata: Versione iniziale di SQL Server 2017

2. Passare all'elenco di aggiornamenti cumulativi: [Aggiornamenti di SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)

3. Selezionare l'aggiornamento cumulativo più recente. Un file eseguibile viene scaricato ed estratto automaticamente.

4. Eseguire il programma di installazione. Accettare le condizioni di licenza, quindi nella pagina Selezione funzionalità, esaminare le funzionalità per il quale vengono applicati aggiornamenti cumulativi. Verrà visualizzata ogni funzionalità installata per l'istanza corrente, incluse le funzionalità di machine learning. Programma di installazione scaricherà i file CAB necessari per aggiornare tutte le funzionalità.

  ![Riepilogo delle funzionalità installate](media/cumulative-update-feature-selection.png)

5. Continuare la procedura guidata, accettando le condizioni di licenza per le distribuzioni R e Python. 

## <a name="additional-configuration"></a>Configurazione aggiuntiva

Se il passaggio di verifica dello script esterno ha esito positivo, è possibile eseguire comandi R o Python da SQL Server Management Studio, Visual Studio Code o qualsiasi altro client che può inviare istruzioni T-SQL al server.

Se è stato visualizzato un errore quando si esegue il comando, rivedere i passaggi di configurazione aggiuntive in questa sezione. Si potrebbe essere necessario effettuare altre configurazioni appropriate per il servizio o il database.

A livello di istanza, potrebbe includere un'ulteriore configurazione:

* [Configurazione del firewall per SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Abilitare i protocolli di rete aggiuntivi](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Abilitare le connessioni remote](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Creare un account di accesso per SQLRUserGroup](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)
* [Gestire le quote disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) per evitare gli script esterni che eseguono attività che esaurire lo spazio su disco

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

Il database, potrebbe essere necessario gli aggiornamenti di configurazione seguenti:

* [Consentire agli utenti di SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md)

> [!NOTE]
> Se è necessaria una configurazione aggiuntiva dipende dallo schema di sicurezza, in cui è installato SQL Server e come si prevede che gli utenti per connettersi al database ed eseguire gli script esterni.

## <a name="suggested-optimizations"></a>Delle ottimizzazioni suggerite

Ora che avete accertato il corretto funzionamento, si potrebbe anche voler ottimizzare il server per supportare l'apprendimento automatico o installazione pretrained modelli.

### <a name="add-more-worker-accounts"></a>Aggiungere altri account di lavoro

Se si prevede che molti utenti sia in esecuzione gli script contemporaneamente, è possibile aumentare il numero di account di lavoro assegnati al servizio Launchpad. Per altre informazioni, vedere [modificare il pool di account utente per SQL Server Machine Learning Services](../administration/modify-user-account-pool.md).

### <a name="optimize-the-server-for-script-execution"></a>Ottimizzare il server per l'esecuzione di script

Le impostazioni predefinite per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il programma di installazione consentono di ottimizzare l'equilibrio tra il server per un'ampia gamma di servizi che sono supportati dal motore di database, che potrebbe includere estrazione, trasformazione e caricamento (ETL) dei processi, creazione di report, il controllo, e le applicazioni che usano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei dati. Di conseguenza, le impostazioni predefinite, si noterà che le risorse per machine learning vengono talvolta limitate o limitate, in particolare nelle operazioni a elevato utilizzo di memoria.

Per garantire che i processi di machine learning sono la priorità e risorse assegnati in modo appropriato, è consigliabile utilizzare SQL Server Resource Governor per configurare un pool di risorse esterne. Potrebbe anche voler modificare la quantità di memoria allocata per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motore di database o aumentare il numero di account che vengono eseguiti nel [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servizio.

- Per configurare un pool di risorse per la gestione delle risorse esterne, vedere [creare un pool di risorse esterne](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Per modificare la quantità di memoria riservata per il database, vedere [opzioni di configurazione memoria Server](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Per modificare il numero di account R che può essere avviata dal [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], vedere [modificare il pool di account utente per l'apprendimento](../administration/modify-user-account-pool.md).

Se si usa l'edizione Standard e sono privi di Resource Governor, è possibile utilizzare viste a gestione dinamica (DMV) e degli eventi estesi, nonché eventi di Windows, che consente di gestire le risorse del server di monitoraggio. Per altre informazioni, vedere [monitoraggio e gestione dei servizi R](../r/managing-and-monitoring-r-solutions.md) e [monitoraggio e gestione dei servizi Python](../python/managing-and-monitoring-python-solutions.md).

### <a name="install-additional-r-packages"></a>Installare pacchetti R aggiuntivi

Le soluzioni R create per SQL Server, è possono chiamare funzioni R di base, funzioni dai pacchetti proprietari installati con SQL Server e i pacchetti R di terze parti compatibile con la versione di R open source installati tramite SQL Server.

I pacchetti di SQL Server da usare devono essere installati nella libreria predefinita usata dall'istanza. Se si dispone di un'installazione separata di R nel computer, o se si installano pacchetti nelle librerie utente, sarà possibile usare questi pacchetti da T-SQL.

Il processo per l'installazione e la gestione dei pacchetti di R è diverso in SQL Server 2016 e SQL Server 2017. In SQL Server 2016, un amministratore del database è necessario installare pacchetti R che gli utenti devono avere. In SQL Server 2017, è possibile configurare i gruppi di utenti di condividere i pacchetti in un livello di database, o configurare i ruoli di database per consentire agli utenti di installare i propri pacchetti. Per altre informazioni, vedere [installare nuovi pacchetti R in SQL Server](../r/install-additional-r-packages-on-sql-server.md).


## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori di R possono iniziare a usare alcuni semplici esempi e informazioni di base del funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Esercitazione: Analitica nel database per gli sviluppatori di R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Gli sviluppatori di Python è possono imparare a usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione: Eseguire Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Esercitazione: Analitica nel database per sviluppatori Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Per visualizzare esempi di machine learning basate su scenari reali, vedere [di Machine learning esercitazioni](../tutorials/machine-learning-services-tutorials.md).
