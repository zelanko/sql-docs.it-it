---
title: Problemi comuni con il servizio Launchpad e l'esecuzione di script esterni
ms.prod: sql
ms.technology: ''
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c90c59f3b59850bb0e2d1cf4cf40eb569e965eba
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715278"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>Problemi comuni con il servizio Launchpad e l'esecuzione di script esterni in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server servizio Launchpad attendibile supporta l'esecuzione di script esterni per R e Python. 

Più problemi possono impedire l'avvio di Launchpad, inclusi problemi di configurazione o modifiche o protocolli di rete mancanti. Questo articolo fornisce indicazioni per la risoluzione di molti problemi. Per eventuali problemi, è possibile pubblicare domande nel [forum Machine Learning server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR).

## <a name="determine-whether-launchpad-is-running"></a>Determinare se è in esecuzione Launchpad

1. Aprire il pannello **Servizi** (Services. msc). In alternativa, dalla riga di comando digitare **SQLServerManager13. msc** o **SQLServerManager14. msc** per aprire [Gestione configurazione SQL Server](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Prendere nota dell'account del servizio in cui è in esecuzione launchpad. Ogni istanza in cui è abilitato R o Python deve avere una propria istanza del servizio launchpad. Il servizio per un'istanza denominata, ad esempio, potrebbe essere simile a _MSSQLLaunchpad $ NomeIstanza_.

3. Se il servizio è arrestato, riavviarlo. Al riavvio, se si verificano problemi con la configurazione, viene pubblicato un messaggio nel registro eventi di sistema e il servizio viene arrestato nuovamente. Consultare il registro eventi di sistema per informazioni dettagliate sui motivi per cui il servizio è stato arrestato.

4. Esaminare il contenuto di RSetup. log e verificare che non siano presenti errori durante l'installazione. Ad esempio, il messaggio che *termina con il codice 0* indica un errore di avvio del servizio.

5. Per cercare altri errori, esaminare il contenuto di rlauncher. log.

## <a name="check-the-launchpad-service-account"></a>Controllare l'account del servizio Launchpad

L'account del servizio predefinito potrebbe essere "NT\$Service sql2016" o "NT\$Service sql2017". La parte finale può variare in base al nome dell'istanza di SQL.

Il servizio Launchpad (Launchpad. exe) viene eseguito utilizzando un account del servizio con privilegi limitati. Tuttavia, per avviare R e Python e comunicare con l'istanza di database, l'account del servizio Launchpad richiede i diritti utente seguenti:

- Accesso come servizio (SeServiceLogonRight)
- Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)
- Ignorare controllo incrociato (SeChangeNotifyPrivilege)
- Regolazione delle quote di memoria per un processo (SeIncreaseQuotaSizePrivilege)

Per informazioni su questi diritti utente, vedere la sezione "privilegi e diritti di Windows" in [configurare account di servizio e autorizzazioni di Windows](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

> [!TIP]
> Se si ha familiarità con l'uso dello strumento SDP (Support Diagnostics Platform) per la diagnostica SQL Server, è possibile usare SDP per esaminare il file di output con il nome MachineName_UserRights. txt.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>Il gruppo utenti per Launchpad non può accedere localmente

Durante l'installazione di Machine Learning Services, SQL Server crea il gruppo di utenti di Windows **SQLRUserGroup** e quindi ne effettua il provisioning con tutti i diritti necessari per la connessione di Launchpad al SQL Server ed esecuzione di processi di script esterni. Se questo gruppo di utenti è abilitato, viene usato anche per eseguire gli script Python.

Tuttavia, nelle organizzazioni in cui vengono applicati criteri di sicurezza più restrittivi, i diritti richiesti da questo gruppo potrebbero essere stati rimossi manualmente o potrebbero essere revocati automaticamente dai criteri. Se i diritti sono stati rimossi, Launchpad non può più connettersi a SQL Server e SQL Server non può chiamare il runtime esterno.

Per correggere il problema, assicurarsi che il gruppo **SQLRUserGroup** abbia il diritto di sistema **Consenti accesso locale**.

Per altre informazioni, vedere [Configurare account di servizio e autorizzazioni di Windows](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

## <a name="permissions-to-run-external-scripts"></a>Autorizzazioni per l'esecuzione di script esterni

Anche se la finestra di avvio è configurata correttamente, viene restituito un errore se l'utente non dispone delle autorizzazioni necessarie per eseguire script R o Python.

Se è stato installato SQL Server come amministratore di database o se si è proprietari del database, l'autorizzazione viene concessa automaticamente. Tuttavia, in genere altri utenti dispongono di autorizzazioni più limitate. Se tentano di eseguire uno script R, ricevono un errore di Launchpad.

Per risolvere il problema, in SQL Server Management Studio un amministratore della sicurezza può modificare l'account di accesso SQL o l'account utente di Windows eseguendo lo script seguente:

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

Per ulteriori informazioni, vedere [Grant (Transact-SQL](../t-sql/statements/grant-transact-sql.md)).

## <a name="common-launchpad-errors"></a>Errori comuni di Launchpad

Questa sezione elenca i messaggi di errore più comuni restituiti da Launchpad.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="unable-to-launch-runtime-for-r-script"></a>"Impossibile avviare il runtime per lo script R"

Se il gruppo di Windows per gli utenti R (usato anche per Python) non è in grado di accedere all'istanza che esegue R Services, è possibile che vengano visualizzati gli errori seguenti:

- Errori generati quando si tenta di eseguire gli script R:

    * *Non è stato possibile avviare il runtime per lo script 'R'. Verificare la configurazione del runtime di 'R'.*

    * *Si è verificato un errore dello script esterno. Non è stato possibile avviare il runtime.*

- Errori generati dal [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] servizio:

    * *Failed to initialize the launcher RLauncher.dll*

    * *No launcher dlls were registered!*

    * *I registri di sicurezza indicano che il servizio NT account non è stato in grado di eseguire l'accesso*

Per informazioni su come concedere a questo gruppo di utenti le autorizzazioni necessarie, vedere [Install R Services per SQL Server](install/sql-r-services-windows-install.md).

> [!NOTE]
> Questa limitazione non si applica se si usano account di accesso SQL per eseguire script R da una workstation remota.
::: moniker-end

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"Errore di accesso: all'utente non è stato concesso il tipo di accesso richiesto"

Per impostazione predefinita [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] , all'avvio di viene usato l' `NT Service\MSSQLLaunchpad`account seguente:. L'account viene configurato dal [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] programma di installazione di per disporre di tutte le autorizzazioni necessarie.

Se si assegna a Launchpad un account diverso o il diritto viene rimosso da un criterio nel computer SQL Server, è possibile che l'account non disponga delle autorizzazioni necessarie e che venga visualizzato questo errore:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Errore durante l'accesso. L'utente non ha ottenuto il tipo di accesso richiesto a questo computer.*

Per concedere le autorizzazioni necessarie al nuovo account del servizio, usare l'applicazione criteri di sicurezza locali e aggiornare le autorizzazioni per l'account in modo da includere le autorizzazioni seguenti:

+ Regolazione quote di memoria per un processo (SeIncreaseQuotaPrivilege)
+ Ignorare controllo incrociato (SeChangeNotifyPrivilege)
+ Accesso come servizio (SeServiceLogonRight)
+ Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"Impossibile comunicare con il servizio Launchpad"

Se è stato installato e quindi abilitato Machine Learning, ma si riceve questo errore quando si tenta di eseguire uno script R o Python, il servizio Launchpad per l'istanza potrebbe avere smesso di funzionare.

1. Dal prompt dei comandi di Windows aprire Gestione configurazione SQL Server. Per altre informazioni, vedere [Gestione configurazione SQL Server](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Fare clic con il pulsante destro del mouse su Launchpad di SQL Server per l'istanza, quindi scegliere **Proprietà**.

3. Selezionare la scheda **servizio** , quindi verificare che il servizio sia in esecuzione. Se non è in esecuzione, impostare la **modalità di avvio** su **automatico**e quindi selezionare **applica**.

4. Il riavvio del servizio in genere corregge il problema in modo che sia possibile eseguire gli script di machine learning. Se il riavvio non risolve il problema, annotare il percorso e gli argomenti nella proprietà **percorso binario** ed eseguire le operazioni seguenti:

    a. Esaminare il file config dell'utilità di avvio e assicurarsi che la directory di lavoro sia valida.

    b. Verificare che il gruppo di Windows usato da Launchpad possa connettersi all'istanza di SQL Server.

    c. Se si modifica una qualsiasi delle proprietà del servizio, riavviare il servizio launchpad.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"Impossibile creare tmpFile errore irreversibile"

In questo scenario sono state installate correttamente le funzionalità di machine learning e Launchpad è in esecuzione. Si tenta di eseguire un semplice codice R o Python, ma Launchpad non riesce con un errore simile al seguente: 

>*Non è possibile comunicare con il runtime per lo script R. Verificare i requisiti del runtime di R.*

Allo stesso tempo, il runtime di script esterni scrive il messaggio seguente come parte del messaggio STDERR: 

>*Errore irreversibile: la creazione di tmpfile non è riuscita.*

Questo errore indica che l'account che sta tentando di utilizzare Launchpad non dispone dell'autorizzazione per accedere al database. Questa situazione può verificarsi quando vengono implementati criteri di sicurezza restrittivi. Per determinare se questo è il caso, esaminare i registri SQL Server e verificare se l'account MSSQLSERVER01 è stato negato all'accesso. Le stesse informazioni vengono fornite nei log specifici dei servizi R\_o Python.\_ Cercare ExtLaunchError. log.

Per impostazione predefinita, vengono impostati 20 account e associati al processo launchpad. exe, con i nomi MSSQLSERVER01 tramite MSSQLSERVER20. Se si usa in modo intensivo R o Python, è possibile aumentare il numero di account.

Per risolvere il problema, assicurarsi che il gruppo abbia le autorizzazioni *Consenti accesso locale* all'istanza locale in cui sono state installate e abilitate le funzionalità di machine learning. In alcuni ambienti, questo livello di autorizzazione potrebbe richiedere un'eccezione GPO dall'amministratore di rete.

## <a name="not-enough-quota-to-process-this-command"></a>"Quota insufficiente per l'elaborazione del comando"

Questo errore può indicare uno dei diversi aspetti seguenti:

- La finestra di avvio potrebbe non avere utenti esterni sufficienti per eseguire la query esterna. Se ad esempio si eseguono più di 20 query esterne simultaneamente e sono presenti solo 20 utenti predefiniti, una o più query potrebbero avere esito negativo.

- La memoria disponibile non è sufficiente per elaborare l'attività R. Questo errore si verifica in genere in un ambiente predefinito, in cui SQL Server potrebbe utilizzare fino al 70% delle risorse del computer. Per informazioni su come modificare la configurazione del server per supportare maggiormente l'uso delle risorse da parte di R, vedere [operatività your r code](r/operationalizing-your-r-code.md).

## <a name="cant-find-package"></a>"Impossibile trovare il pacchetto"

Se si esegue il codice R in SQL Server e si riceve questo messaggio, ma il messaggio non è stato ricevuto quando è stato eseguito lo stesso codice all'esterno SQL Server, significa che il pacchetto non è stato installato nel percorso di libreria predefinito usato da SQL Server.

Questo errore può verificarsi in molti modi:

- È stato installato un nuovo pacchetto sul server, ma l'accesso è stato negato, quindi R ha installato il pacchetto in una libreria utente.

- R Services è stato installato, quindi è stato installato un altro strumento R o un set di librerie, tra cui Microsoft R Server (standalone), Microsoft R Client, RStudio e così via.

Per determinare il percorso della libreria di pacchetti R usata dall'istanza di, aprire SQL Server Management Studio (o qualsiasi altro strumento di query di database), connettersi all'istanza di, quindi eseguire il stored procedure seguente:

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>Risultati dell'esempio

*Messaggi STDOUT dallo script esterno:*

*[1] "C:\\Program Files\\Microsoft SQL Server\\MSSQL13. Sql2016\\R_SERVICES "*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13. Sql2016/R_SERVICES/Library "*

Per risolvere il problema, è necessario reinstallare il pacchetto nella libreria di istanze SQL Server.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
>[!NOTE]
>Se è stata aggiornata un'istanza di SQL Server 2016 per usare la versione più recente di Microsoft R, il percorso predefinito della libreria è diverso. Per altre informazioni, vedere [usare Sqlbindr per aggiornare un'istanza di R Services](install/upgrade-r-and-python.md).
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>La finestra di avvio viene arrestata a causa di dll non corrispondenti

Se si installa il motore di database con altre funzionalità, applicare una patch al server e successivamente aggiungere la funzionalità Machine Learning utilizzando il supporto originale, potrebbe essere installata la versione errata dei componenti del Machine Learning. Quando Launchpad rileva una versione non corrispondente, viene arrestata e viene creato un file dump.

Per evitare questo problema, assicurarsi di installare tutte le nuove funzionalità con lo stesso livello di patch dell'istanza del server.

**Il modo errato per eseguire l'aggiornamento:**

1. Installare SQL Server 2016 senza R Services.
2. Aggiornamento SQL Server 2016 aggiornamento cumulativo 2.
3. Installare R Services (in-database) utilizzando il supporto RTM.

**Il modo corretto per eseguire l'aggiornamento:**

1. Installare SQL Server 2016 senza R Services.
2. Aggiornare SQL Server 2016 al livello di patch desiderato. Ad esempio, installare il Service Pack 1 e quindi l'aggiornamento cumulativo 2.
3. Per aggiungere la funzionalità a livello di patch corretto, eseguire di nuovo il programma di installazione di SP1 e CU2, quindi scegliere R Services (in-database). 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>Non è possibile avviare launchpad se è richiesta la notazione 8dot3

> [!NOTE] 
> Nei sistemi precedenti, la finestra di avvio può non riuscire se è presente un requisito per la notazione 8dot3. Questo requisito è stato rimosso nelle versioni successive. SQL Server 2016 i clienti di R Services devono installare uno dei seguenti elementi:
> * SQL Server 2016 SP1 e CU1: [Aggiornamento cumulativo 1 per SQL Server](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, aggiornamento cumulativo 3 e questo [hotfix](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), disponibile su richiesta.

Per la compatibilità con R, SQL Server 2016 R Services (in-database) richiede l'unità in cui è installata la funzionalità per supportare la creazione di nomi di file brevi con la *notazione 8dot3*. Il nome di un file 8,3 è denominato anche *nome breve*e viene usato per la compatibilità con le versioni precedenti di Microsoft Windows o come alternativa ai nomi di file lunghi.

Se il volume in cui si sta installando R non supporta nomi di file brevi, i processi che avviano R da SQL Server potrebbero non essere in grado di individuare l'eseguibile corretto e la finestra di avvio non verrà avviata.

Come soluzione alternativa, è possibile abilitare la notazione 8dot3 nel volume in cui è installato SQL Server e in cui è installato R Services. È quindi necessario specificare il nome breve per la directory di lavoro nel file di configurazione di R Services.

1. Per abilitare la notazione 8dot3, eseguire l'utilità fsutil con l'argomento *8dot3name* come descritto qui: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

2. Dopo aver abilitato la notazione 8dot3, aprire il file RLauncher. config e prendere nota della proprietà `WORKING_DIRECTORY`di. Per informazioni su come trovare questo file, vedere la pagina [relativa alla raccolta dei dati per Machine Learning la risoluzione dei problemi](data-collection-ml-troubleshooting-process.md).

3. Utilizzare l'utilità fsutil con l'argomento *file* per specificare un percorso di file breve per la cartella specificata in WORKING_DIRECTORY.

4. Modificare il file di configurazione per specificare la stessa directory di lavoro immessa nella proprietà WORKING_DIRECTORY. In alternativa, è possibile specificare una directory di lavoro diversa e scegliere un percorso esistente già compatibile con la notazione 8dot3.
::: moniker-end

## <a name="next-steps"></a>Passaggi successivi

[Machine Learning Services risoluzione dei problemi e problemi noti](machine-learning-troubleshooting-faq.md)

[Raccolta di dati per la risoluzione dei problemi di Machine Learning](data-collection-ml-troubleshooting-process.md)

[Domande frequenti sull'installazione e sull'aggiornamento](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Risolvere i problemi delle connessioni al motore di database](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
