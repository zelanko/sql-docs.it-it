---
title: Problemi comuni con il servizio Launchpad e l'esecuzione di script esterni - servizi di SQL Server Machine Learning
ms.prod: sql
ms.technology: ''
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a3437e5f7081aa47cb33e33546a79aca0b100309
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644921"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>Problemi comuni con il servizio Launchpad e l'esecuzione di script esterni in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 Servizio Trusted Launchpad di SQL Server supporta l'esecuzione di script esterni per R e Python. In SQL Server 2016 R Services, SP1 fornisce il servizio. SQL Server 2017 include il servizio Launchpad come parte dell'installazione iniziale.

Diversi problemi possono impedire Launchpad dall'avvio, inclusi i problemi di configurazione o le modifiche o i protocolli di rete mancante. Questo articolo fornisce indicazioni sulla risoluzione dei problemi per molti problemi. Per qualsiasi viene perso, è possibile pubblicare domande per la [forum di Machine Learning Server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR).

## <a name="determine-whether-launchpad-is-running"></a>Determinare se Launchpad è in esecuzione

1. Aprire il **Services** pannello (Services. msc). In alternativa, dalla riga di comando, digitare **SQLServerManager13.msc** oppure **SQLServerManager14.msc** per aprire [Gestione configurazione SQL Server](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Prendere nota dell'account del servizio cui Launchpad è in esecuzione. Ogni istanza in cui è abilitato R o Python deve avere una propria istanza del servizio Launchpad. Ad esempio, potrebbe essere simile al servizio per un'istanza denominata _MSSQLLaunchpad$ InstanceName_.

3. Se il servizio viene arrestato, riavviarlo. Al riavvio, se si verificano problemi con la configurazione, un messaggio viene pubblicato nel registro eventi di sistema e il servizio viene arrestato anche in questo caso. Controllare il registro eventi di sistema per informazioni dettagliate sui motivi per cui il servizio è stato arrestato.

4. Esaminare il contenuto di RSetup.log e assicurarsi che non siano presenti errori nel programma di installazione. Ad esempio, il messaggio *uscire con il codice 0* indica errori del servizio di avvio.

5. Per cercare altri errori, esaminare il contenuto di rlauncher. log.

## <a name="check-the-launchpad-service-account"></a>Verificare l'account del servizio Launchpad

L'account del servizio predefinito potrebbe essere "NT Service\$SQL2016" o "NT Service\$SQL2017". La parte finale può variare a seconda del nome dell'istanza SQL.

Il servizio Launchpad (Launchpad.exe) viene eseguita usando un account di servizio con privilegi limitati. Tuttavia, per avviare R e Python e comunicare con l'istanza del database, l'account del servizio Launchpad richiede diritti utente seguenti:

- Accesso come servizio (SeServiceLogonRight)
- Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)
- Ignorare controllo incrociato (SeChangeNotifyPrivilege)
- Regolazione limite risorse memoria per un processo (SeIncreaseQuotaSizePrivilege)

Per informazioni su tali diritti utente, vedere la sezione "diritti e i privilegi di Windows" nella [configurare Windows account del servizio e autorizzazioni](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

> [!TIP]
> Se si ha familiarità con l'uso dello strumento Support Diagnostics Platform (SDP) per la diagnostica di SQL Server, è possibile utilizzare SDP per esaminare il file di output con il nome MachineName_UserRights.txt.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>Gruppo di utenti per Launchpad non può accedere localmente

Durante l'installazione di servizi di Machine Learning, SQL Server crea il gruppo di utenti di Windows **SQLRUserGroup** e quindi si effettua il provisioning con tutti i diritti necessari per Launchpad per connettersi a SQL Server ed eseguire processi di script esterni. Se questo gruppo di utenti è abilitato, si utilizza anche per eseguire gli script Python.

Tuttavia, nelle organizzazioni in cui vengono applicati criteri più severi, potrebbero avere i diritti necessari per questo gruppo sia stato rimosso manualmente oppure potrebbe essere revocati automaticamente dai criteri. Se sono stati rimossi i diritti, Launchpad non può più connettersi a SQL Server e SQL Server non è possibile chiamare il runtime esterno.

Per correggere il problema, assicurarsi che il gruppo **SQLRUserGroup** abbia il diritto di sistema **Consenti accesso locale**.

Per altre informazioni, vedere [configurare Windows account del servizio e autorizzazioni](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

## <a name="permissions-to-run-external-scripts"></a>Autorizzazioni per l'esecuzione di script esterni

Anche se Launchpad è configurato correttamente, restituisce un errore se l'utente non dispone dell'autorizzazione per eseguire script R o Python.

Se è stato installato SQL Server come un amministratore del database o dispone di un database, si ottengono automaticamente questa autorizzazione. Tuttavia, altri utenti in genere sono più autorizzazioni limitate. Se si prova a eseguire uno script R, ricevono un errore di Launchpad.

Per risolvere il problema, in SQL Server Management Studio, un amministratore della sicurezza può modificare l'account di accesso SQL o un account utente di Windows eseguendo lo script seguente:

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

Per altre informazioni, vedere [GRANT (Transact-SQL](../t-sql/statements/grant-transact-sql.md).

## <a name="common-launchpad-errors"></a>Errori comuni durante la finestra di avvio

Questa sezione elenca i messaggi di errore più comuni che restituisce Launchpad.

## <a name="unable-to-launch-runtime-for-r-script"></a>"Impossibile avviare il runtime per lo script R"

Se il gruppo di Windows per gli utenti di R (utilizzato anche per Python) non è possibile accedere all'istanza che esegue R Services, è possibile visualizzare i seguenti errori:

- Errori generati quando si prova a eseguire gli script R:

    * *Non è stato possibile avviare il runtime per lo script 'R'. Verificare la configurazione del runtime di 'R'.*

    * *Si è verificato un errore dello script esterno. Non è stato possibile avviare il runtime.*

- Gli errori generati dal [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] servizio:

    * *Failed to initialize the launcher RLauncher.dll*

    * *No launcher dlls were registered!*

    * *I log di sicurezza indicano che l'account NT SERVICE è riuscito a eseguire l'accesso*

Per informazioni su come concedere a questo gruppo di utenti le autorizzazioni necessarie, vedere [installare SQL Server 2016 R Services](install/sql-r-services-windows-install.md).

> [!NOTE]
> Questa limitazione non si applica se si usano account di accesso SQL per eseguire script R da una workstation remota.

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"Errore durante l'accesso: l'utente non ha ottenuto il tipo di accesso richiesto"

Per impostazione predefinita [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] utilizza il seguente account all'avvio: `NT Service\MSSQLLaunchpad`. L'account è configurato per [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] il programma di installazione con tutte le autorizzazioni necessarie.

Se assegna a Launchpad un account diverso o il diritto viene rimosso da un criterio nel computer di SQL Server, l'account non disponga delle autorizzazioni necessarie e si potrebbe essere visualizzato questo errore:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Errore durante l'accesso. L'utente non ha ottenuto il tipo di accesso richiesto a questo computer.*

Per concedere le autorizzazioni necessarie per il nuovo account del servizio, usare l'applicazione di criteri di sicurezza locali e aggiornare le autorizzazioni per l'account da includere le autorizzazioni seguenti:

+ Regolazione quote di memoria per un processo (SeIncreaseQuotaPrivilege)
+ Ignorare controllo incrociato (SeChangeNotifyPrivilege)
+ Accesso come servizio (SeServiceLogonRight)
+ Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"Impossibile comunicare con il servizio Launchpad"

Se è stato installato e attivato quindi apprendimento automatico, ma viene visualizzato questo errore quando si prova a eseguire uno script R o Python, il servizio Launchpad per l'istanza può avere più in esecuzione.

1. Dal prompt dei comandi di Windows aprire Gestione configurazione SQL Server. Per altre informazioni, vedere [Gestione configurazione SQL Server](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Fare doppio clic su Launchpad di SQL Server per l'istanza e quindi selezionare **proprietà**.

3. Selezionare il **servizio** scheda e quindi verificare che il servizio sia in esecuzione. Se non è in esecuzione, modificare il **modalità di avvio** al **automatica**e quindi selezionare **Apply**.

4. Il riavvio del servizio in genere corregge il problema in modo che sia possibile eseguire gli script di machine learning. Se il riavvio non risolve il problema, tenere presente il percorso e gli argomenti in di **percorso binario** proprietà ed eseguire le operazioni seguenti:

    a. Esaminare i file con estensione config dell'utilità di avvio e verificare che la directory di lavoro sia valida.

    b. Assicurarsi che il gruppo di Windows che viene usato da Launchpad possa connettersi all'istanza di SQL Server.

    c. Se si modifica una qualsiasi delle proprietà del servizio, riavviare il servizio Launchpad.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"Creazione di un errore irreversibile del tmpFile non riuscita"

In questo scenario, è stato installato correttamente le funzionalità di machine learning e Launchpad è in esecuzione. Si prova a eseguire codice R o Python semplice, ma Launchpad ha esito negativo con un errore simile al seguente: 

>*Impossibile comunicare con il runtime per lo script R. Verificare i requisiti del runtime di R.*

Allo stesso tempo, il runtime dello script esterno scrive il messaggio seguente come parte del messaggio STDERR: 

>*Errore irreversibile: la creazione di tmpfile non è riuscita.*

Questo errore indica che l'account che sta tentando di usare Launchpad non dispone dell'autorizzazione per accedere al database. Questa situazione può verificarsi quando vengono implementati criteri di sicurezza restrittivi. Per determinare se questo è il caso, esaminare i log di SQL Server e controllare per verificare se l'account MSSQLSERVER01 è stato negato all'accesso. Le stesse informazioni vengono fornite nei log che sono specifiche di R\_SERVICES o PYTHON\_servizi. Cercare ExtLaunchError.log.

Per impostazione predefinita, 20 account sono configurato e associato al processo Launchpad.exe, con i nomi MSSQLSERVER01 tramite MSSQLSERVER20. Se si apportata un uso massiccio di R o Python, è possibile aumentare il numero di account.

Per risolvere il problema, assicurarsi che il gruppo disponga *Consenti accesso locale* delle autorizzazioni per l'istanza locale in cui sono state installate e abilitate funzionalità di machine learning. In alcuni ambienti, questo livello di autorizzazione potrebbe richiedere un'eccezione di oggetto Criteri di gruppo dell'amministratore di rete.

## <a name="not-enough-quota-to-process-this-command"></a>"Non una quota sufficiente per elaborare il comando"

Questo errore può indicare una delle diverse operazioni:

- Finestra di avvio potrebbe essere insufficienti utenti esterni per eseguire la query esterna. Ad esempio, se si eseguono contemporaneamente più di 20 query esterna, e sono disponibili solo per 20 utenti predefiniti, uno o più query potrebbe non riuscire.

- Memoria disponibile è insufficiente per l'elaborazione dell'attività di R. Questo errore si verifica più spesso in un ambiente predefinito, in cui SQL Server potrebbe essere usato fino al 70% delle risorse del computer. Per informazioni su come modificare la configurazione del server per il supporto maggiore utilizzo delle risorse per R, vedere [operatività del codice R](r/operationalizing-your-r-code.md).

## <a name="cant-find-package"></a>"Impossibile trovare il pacchetto"

Se si esegue codice R in SQL Server e visualizzato questo messaggio, ma non hanno ricevuto il messaggio quando è stato eseguito lo stesso codice all'esterno di SQL Server, significa che il pacchetto non è stato installato nel percorso di libreria predefinita usata da SQL Server.

Questo errore può verificarsi in molti modi:

- È stato installato un nuovo pacchetto nel server, ma è stato negato l'accesso, in modo che R sia installato il pacchetto in una libreria utente.

- È installato R Services e quindi installato un altro strumento di R o set di librerie, tra cui Microsoft R Server (Standalone), Microsoft R Client, RStudio e così via.

Per determinare il percorso della libreria di pacchetti R che viene utilizzato dall'istanza, aprire SQL Server Management Studio (o qualsiasi altro strumento di query di database), connettersi all'istanza e quindi eseguire la stored procedure seguente:

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>Risultati dell'esempio

*Messaggi STDOUT dallo script esterno:*

*[1] "c:\\file di programma\\Microsoft SQL Server\\MSSQL13. SQL2016\\R_SERVICES "*

*[1] "c: / Program file/Microsoft SQL Server/MSSQL13. Libreria/R_SERVICES/SQL2016"*

Per risolvere il problema, è necessario reinstallare il pacchetto nella raccolta di istanza di SQL Server.

>[!NOTE]
>Se è stato eseguito l'aggiornamento di un'istanza di SQL Server 2016 per usare la versione più recente di Microsoft R, il percorso di libreria predefinito è diverso. Per altre informazioni, vedere [usare sqlbindr. exe per aggiornare un'istanza di R Services](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>Finestra di avvio viene arrestato a causa di DLL non corrispondenti

Se si installa il motore di database con altre funzionalità, patch, il server e quindi aggiungerla la funzionalità di Machine Learning usando il supporto originale, potrebbe essere installata la versione errata dei componenti di Machine Learning. Quando Launchpad rileva una mancata corrispondenza delle versioni, arresta e viene creato un file di dump.

Per evitare questo problema, assicurarsi di installare le nuove funzionalità a livello di patch stesso come istanza del server.

**Il modo non corretto per eseguire l'aggiornamento:**

1. Installare SQL Server 2016 senza R Services.
2. Eseguire l'aggiornamento di SQL Server 2016 aggiornamento cumulativo 2.
3. Installare R Services (In-Database) utilizzando i supporti RTM.

**Il modo corretto per eseguire l'aggiornamento:**

1. Installare SQL Server 2016 senza R Services.
2. Aggiornare SQL Server 2016 per il livello di patch desiderato. Ad esempio, installare Service Pack 1 e quindi l'aggiornamento cumulativo 2.
3. Per aggiungere la funzionalità a livello di patch corretto, eseguire nuovamente l'installazione di SP1 e CU2 e quindi scegliere R Services (In-Database). 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>LaunchPad non viene avviato se la notazione 8.3 è obbligatorio

> [!NOTE] 
> Nei sistemi precedenti, Launchpad può non riuscire iniziare se è presente un requisito di notazione 8dot3. Questo requisito è stato rimosso nelle versioni successive. I clienti di SQL Server 2016 R Services è necessario installare uno dei seguenti:
> * SQL Server 2016 SP1 e CU1: [Aggiornamento cumulativo 1 per SQL Server](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, aggiornamento cumulativo 3 e ciò [hotfix](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), disponibile su richiesta.

Per garantire la compatibilità con R, SQL Server 2016 R Services (In-Database) richiesto nell'unità in cui è installata la funzionalità per supportare la creazione di nomi file brevi usando *la notazione 8.3*. Un nome di 8.3 file è l'acronimo di un *nome file breve*, e viene usato per la compatibilità con le versioni precedenti di Microsoft Windows o come alternativa ai nomi file lunghi.

Se il volume in cui si installa R non supporta nomi file brevi, i processi che avviano R da SQL Server potrebbero non essere in grado di individuare il file eseguibile corretto e Launchpad non verrà avviato.

In alternativa, è possibile abilitare la notazione 8.3 nel volume in cui è installato SQL Server e in cui è installato R Services. È quindi necessario specificare il nome breve per la directory di lavoro nel file di configurazione di R Services.

1. Per abilitare la notazione 8.3, eseguire l'utilità fsutil con il *8dot3name* argomento come descritto qui: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

2. Dopo aver abilitata la notazione 8.3, aprire il file Rlauncher config e notare la proprietà di `WORKING_DIRECTORY`. Per informazioni su come trovare questo file, vedere [raccolta di dati per la risoluzione dei problemi di Machine Learning](data-collection-ml-troubleshooting-process.md).

3. Usare l'utilità fsutil con il *file* argomento per specificare un percorso di file brevi per la cartella specificata in WORKING_DIRECTORY.

4. Modificare il file di configurazione per specificare la stessa directory di lavoro che è stato immesso nella proprietà WORKING_DIRECTORY. In alternativa, è possibile specificare un'altra directory di lavoro e scegliere un percorso esistente che già è compatibile con la notazione 8.3.


## <a name="next-steps"></a>Passaggi successivi

[Problemi noti e risoluzione dei problemi di Machine Learning Services](machine-learning-troubleshooting-faq.md)

[Raccolta dei dati per la risoluzione dei problemi di apprendimento automatico](data-collection-ml-troubleshooting-process.md)

[Domande frequenti sull'installazione e sull'aggiornamento](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Risolvere i problemi di connessioni al motore del database](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
