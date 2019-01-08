---
title: 'Installare SQL Server 2016 R Services (In-Database): SQL Server Machine Learning'
description: Aggiungere il supporto linguistico a un motore di database in SQL Server 2016 R Services a Windows di programmazione R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 69b3b9a57b2a4f6120c88552ca3100b288968b69
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645320"
---
# <a name="install-sql-server-2016-r-services"></a>Installare SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo illustra come installare e configurare **SQL Server 2016 R Services**. Se si dispone di SQL Server 2016, installare questa funzionalità per consentire l'esecuzione del codice R in SQL Server.

In SQL Server 2017, integrazione di R è disponibile in [servizi di Machine Learning](../r/r-server-standalone.md), che riflette l'aggiunta di Python. Se si vuole eseguire l'integrazione di R e disporre dei supporti di installazione di SQL Server 2017, vedere [installare SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md) per aggiungere la funzionalità. 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Elenco di controllo pre-installazione

+ È necessaria un'istanza di motore di database. È possibile installare solo R, anche se è possibile aggiungerlo in modo incrementale a un'istanza esistente.

+ Non installare R Services in un cluster di failover. Il meccanismo di sicurezza usato per isolare i processi R non è compatibile con un ambiente cluster di failover di Windows Server.

+ Non installare R Services in un controller di dominio. La parte di R Services del programma di installazione avrà esito negativo.

+ Non installare **funzionalità condivise** > **R Server (Standalone)** nello stesso computer che esegue un'istanza nel database. 

  Installazione side-by-side con altre versioni di R e Python sono possibili in quanto l'istanza di SQL Server Usa una proprio copie delle distribuzioni open source R e Anaconda. Esecuzione di codice che usa R e Python nel computer SQL Server all'esterno di SQL Server, tuttavia, può causare problemi diversi:
    
  + Si usa una libreria diversa e un diverso eseguibile e ottengano risultati diversi, rispetto a quando si eseguono in SQL Server.
  + Gli script R e Python in esecuzione nelle librerie esterne non possono essere gestiti da SQL Server, causando una contesa delle risorse.
  
Se è stata usata una versione precedente dell'ambiente di sviluppo Revolution Analitica o dei pacchetti RevoScaleR o se è installata una versione di versioni non definitive di SQL Server 2016, è necessario disinstallarle. Che eseguono versioni precedenti e più recenti di RevoScaleR e altri pacchetti proprietari non è supportato. Per informazioni sulla rimozione di versioni precedenti, vedere [aggiornamento e domande frequenti sull'installazione di SQL Server Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Al termine dell'installazione, assicurarsi di completare i passaggi di post-configurazione aggiuntivi descritti in questo articolo. Tali passaggi includono l'abilitazione di SQL Server per usare gli script esterni e l'aggiunta di account necessari per SQL Server eseguire processi R per tuo conto. Le modifiche alla configurazione in genere richiedono un riavvio dell'istanza o un riavvio del servizio Launchpad.

## <a name="get-the-installation-media"></a>Ottenere il supporto di installazione

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Requisito di installazione patch 

Microsoft ha rilevato un problema con una versione specifica dei file binari di Microsoft VC++ 2013 Runtime installati come prerequisito da SQL Server. Se l'aggiornamento dei file binari di VC++ Runtime non viene installato, potrebbero verificarsi problemi di stabilità di SQL Server in determinati scenari. Prima di installare SQL Server, seguire le istruzioni in [Note sulla versione di SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) per vedere se il computer richiede una patch per i file binari di VC++ Runtime.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Esecuzione del programma di installazione

Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.

1. Avviare l'installazione guidata di SQL Server 2016.

2. Nel **installazione** scheda, seleziona **nuova installazione SQL Server autonomo o aggiungere caratteristiche a un'installazione esistente**.
    
   ![Installare R Services (In-Database)](media/2016-setup-installation-rsvcs.png "avviare l'installazione del motore di database con R Services")
   
3. Nel **Selezione funzionalità** pagina, selezionare le opzioni seguenti:

   - Selezionare **servizi motore di Database**. Il motore di database è obbligatorio in ogni istanza che usa machine learning.
   - Selezionare **R Services (In-Database)**. Installa il supporto per l'uso nel database di R.
    
     ![Selezione delle funzionalità R Services](media/2016setup-rsvcs-features.png "selezionare queste funzionalità per R Services In-Database")

    > [!IMPORTANT]
    > Non installare R Server e R Services nello stesso momento. È in genere necessario installare R Server (Standalone) per creare un ambiente che usa un data scientist o sviluppatore per la connessione a SQL Server e distribuire soluzioni R. Non è quindi necessario installare entrambe le soluzioni nello stesso computer.

4.  Nel **fornire il consenso per installare Microsoft R Open** pagina, fare clic su **Accept**.
  
    Il contratto di licenza è necessario per scaricare Microsoft R Open, che include una distribuzione di pacchetti R open source di base e strumenti, insieme a pacchetti R avanzati e provider di connettività dal team di sviluppo di Microsoft R.
  
5. Dopo aver accettato il contratto di licenza, si verifica una breve pausa durante il programma di installazione è pronto. Fare clic su **successivo** quando il pulsante diventa disponibile.

6. Nel **pronto per l'installazione** pagina, verificare che gli elementi seguenti sono inclusi e quindi selezionare **installare**.

   + Servizi motore di database
   + R Services (In-Database)

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

##  <a name="enable-script-execution"></a>Abilitare l'esecuzione di script

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
     
3. Per abilitare la funzionalità di script esterne, eseguire l'istruzione seguente:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Riavviare il servizio.

Una volta completata l'installazione, riavviare il motore di database prima di procedere al successivo, consentendo l'esecuzione dello script.

Riavviare automaticamente anche il servizio viene riavviato correlato [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servizio.

È possibile riavviare il servizio utilizzando il pulsante destro del mouse **riavviare** comando per l'istanza di SQL Server Management Studio o tramite il **Services** pannello nel Pannello di controllo oppure usando [Gestione configurazione SQL Server ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verificare l'installazione

Controllare lo stato di installazione dell'istanza mediante [report personalizzati](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Utilizzare la procedura seguente per verificare che tutti i componenti usati per avviare script esterni siano in esecuzione.

1. In SQL Server Management Studio, aprire una nuova finestra query ed eseguire il comando seguente:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    Il valore di **run_value** dovrebbe ora essere impostato su 1.

2. Aprire il **Services** pannello o Gestione configurazione SQL Server e verificare **Launchpad di SQL Server service** è in esecuzione. È necessario un servizio per ogni istanza di motore di database con R o Python installato. Per altre informazioni sul servizio, vedere [framework di estendibilità](../concepts/extensibility-framework.md).

7. Se Launchpad è in esecuzione, sarà possibile eseguire R semplice per verificare che il runtime di scripting esterno possa comunicare con SQL Server. 

    Aprire una nuova **Query** finestra in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], quindi eseguire uno script simile al seguente:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    Lo script può richiedere del tempo per l'esecuzione, la prima volta che viene caricato il runtime dello script esterno. I risultati dovrebbero essere simile al seguente:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Applicazione degli aggiornamenti

È consigliabile applicare l'aggiornamento cumulativo più recente per il motore di database e i componenti di apprendimento automatico.

Sui dispositivi connessi a internet, gli aggiornamenti cumulativi vengono in genere applicati tramite Windows Update, ma è anche possibile usare i passaggi seguenti per gli aggiornamenti controllati. Quando si applica l'aggiornamento del motore di database, il programma di installazione esegue il pull di aggiornamenti cumulativi per librerie di R che è installato nella stessa istanza. 

Nei server disconnesso, sono necessarie operazioni aggiuntive. Per altre informazioni, vedere [installare nei computer senza accesso a internet > applicare aggiornamenti cumulativi](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Iniziare con un'istanza della linea di base già installata: Versione iniziale di SQL Server 2016, SQL Server 2016 Service Pack 1 o SQL Server 2016 Service Pack 2.

2. Passare all'elenco di aggiornamenti cumulativi: [Aggiornamenti di SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Selezionare l'aggiornamento cumulativo più recente. Un file eseguibile viene scaricato ed estratto automaticamente.

4. Eseguire il programma di installazione. Accettare le condizioni di licenza, quindi nella pagina Selezione funzionalità, esaminare le funzionalità per il quale vengono applicati aggiornamenti cumulativi. Verrà visualizzata ogni funzionalità installata per l'istanza corrente, tra cui R Services. Programma di installazione scaricherà i file CAB necessari per aggiornare tutte le funzionalità.

5. Continuare la procedura guidata, accettando le condizioni di licenza per la distribuzione di R. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Configurazione aggiuntiva

Se il passaggio di verifica dello script esterno ha esito positivo, è possibile eseguire i comandi di Python da SQL Server Management Studio, Visual Studio Code o qualsiasi altro client che può inviare istruzioni T-SQL al server.

Se è stato visualizzato un errore quando si esegue il comando, rivedere i passaggi di configurazione aggiuntive in questa sezione. Si potrebbe essere necessario effettuare altre configurazioni appropriate per il servizio o il database.

A livello di istanza, potrebbe includere un'ulteriore configurazione:

* [Configurazione del firewall per SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Abilitare i protocolli di rete aggiuntivi](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Abilitare le connessioni remote](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

Il database, potrebbe essere necessario gli aggiornamenti di configurazione seguenti:

* [Consentire agli utenti di SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md)
* [Aggiungere SQLRUserGroup come utente del database](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)

> [!NOTE]
> Non tutte le modifiche elencate sono necessari e nessuno potrebbero essere necessarie. I requisiti variano a seconda lo schema di sicurezza, in cui è installato SQL Server e come si prevede che gli utenti per connettersi al database ed eseguire gli script esterni. Altri suggerimenti sulla risoluzione dei problemi sono disponibili qui: [Domande frequenti sull'installazione e sull'aggiornamento](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Delle ottimizzazioni suggerite

Ora che avete accertato il corretto funzionamento, si potrebbe anche voler ottimizzare il server per supportare l'apprendimento automatico o installazione pretrained modelli.

### <a name="add-more-worker-accounts"></a>Aggiungere altri account di lavoro

Se si ritiene che è possibile usare R in modo rilevante, o se si prevede che molti utenti sia gli script in esecuzione contemporaneamente, è possibile aumentare il numero di account di lavoro assegnati al servizio Launchpad. Per altre informazioni, vedere [modificare il pool di account utente per SQL Server Machine Learning Services](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Ottimizzare il server per l'esecuzione di script esterni

Le impostazioni predefinite per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il programma di installazione consentono di ottimizzare l'equilibrio tra il server per un'ampia gamma di servizi che sono supportati dal motore di database, che potrebbe includere estrazione, trasformazione e caricamento (ETL) dei processi, creazione di report, il controllo, e le applicazioni che usano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei dati. Di conseguenza, le impostazioni predefinite, si noterà che le risorse per machine learning vengono talvolta limitate o limitate, in particolare nelle operazioni a elevato utilizzo di memoria.

Per garantire che i processi di machine learning sono la priorità e risorse assegnati in modo appropriato, è consigliabile utilizzare SQL Server Resource Governor per configurare un pool di risorse esterne. Potrebbe anche voler modificare la quantità di memoria allocata per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motore di database o aumentare il numero di account che vengono eseguiti nel [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servizio.

- Per configurare un pool di risorse per la gestione delle risorse esterne, vedere [creare un pool di risorse esterne](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Per modificare la quantità di memoria riservata per il database, vedere [opzioni di configurazione memoria Server](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Per modificare il numero di account R che può essere avviata dal [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], vedere [modificare il pool di account utente per l'apprendimento](../administration/modify-user-account-pool.md).

Se si usa l'edizione Standard e sono privi di Resource Governor, è possibile utilizzare viste a gestione dinamica (DMV) e degli eventi estesi, nonché eventi di Windows di monitoraggio, che consente di gestire le risorse di server che vengono usate da R. Per altre informazioni, vedere [monitoraggio e gestione dei servizi R](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Installare pacchetti R aggiuntivi

Le soluzioni R create per SQL Server, è possono chiamare funzioni R di base, funzioni dai pacchetti proprietari installati con SQL Server e i pacchetti R di terze parti compatibile con la versione di R open source installati tramite SQL Server.

I pacchetti di SQL Server da usare devono essere installati nella libreria predefinita usata dall'istanza. Se si dispone di un'installazione separata di R nel computer, o se si installano pacchetti nelle librerie utente, sarà possibile usare questi pacchetti da T-SQL.

Il processo per l'installazione e la gestione dei pacchetti di R è diverso in SQL Server 2016 e SQL Server 2017. In SQL Server 2016, un amministratore del database è necessario installare pacchetti R che gli utenti devono avere. In SQL Server 2017, è possibile configurare i gruppi di utenti di condividere i pacchetti in un livello di database, o configurare i ruoli di database per consentire agli utenti di installare i propri pacchetti. Per altre informazioni, vedere [installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori di R possono iniziare a usare alcuni semplici esempi e informazioni di base del funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Esercitazione: Analitica nel database per gli sviluppatori di R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Per visualizzare esempi di machine learning basate su scenari reali, vedere [di Machine learning esercitazioni](../tutorials/machine-learning-services-tutorials.md).