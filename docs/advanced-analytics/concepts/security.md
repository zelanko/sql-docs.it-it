---
title: Panoramica della sicurezza per le estensioni R e Python
description: Panoramica della sicurezza per il Framework di estendibilità in SQL Server Machine Learning Services. Sicurezza per account di accesso e account utente, servizio Launchpad di SQL Server, account di lavoro, esecuzione di più script e autorizzazioni per file.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f5b0af74633fb13b9cfd0b187bc2b180d7fd87b4
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715855"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>Panoramica della sicurezza per il Framework di estendibilità in SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive l'architettura di sicurezza complessiva usata per integrare il motore di database di SQL Server e i componenti correlati con Extensibility Framework. Esamina le entità a protezione diretta, i servizi, l'identità del processo e le autorizzazioni. Per ulteriori informazioni sui concetti chiave e i componenti di estendibilità in SQL Server, vedere [architettura di estendibilità in SQL Server Machine Learning Services](extensibility-framework.md)].

## <a name="securables-for-external-script"></a>Entità a protezione diretta per script esterno

Uno script esterno scritto in R o Python viene inviato come parametro di input a un [stored procedure di sistema](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) creato a questo scopo oppure è incluso in un stored procedure definito dall'utente. In alternativa, è possibile disporre di modelli di cui viene eseguita la preformazione e che vengono archiviati in un formato binario in una tabella di database, richiamabili in una funzione di [stima](../../t-sql/queries/predict-transact-sql.md) T-SQL.

Poiché lo script viene fornito tramite gli oggetti dello schema del database, le stored procedure e le tabelle esistenti, non sono presenti nuove [entità a protezione diretta](../../relational-databases/security/securables.md) per SQL Server Machine Learning Services.

Indipendentemente dalla modalità di utilizzo dello script o, di come sono costituiti, gli oggetti di database verranno creati e probabilmente salvati, ma non viene introdotto alcun nuovo tipo di oggetto per l'archiviazione dello script. Di conseguenza, la possibilità di utilizzare, creare e salvare oggetti di database dipende in gran parte dalle autorizzazioni per i database già definite per gli utenti.

<a name="permissions"></a>

## <a name="permissions"></a>Permissions

Il modello di sicurezza dei dati di SQL Server per gli account di accesso e i ruoli del database si estende allo script R e Python. Per eseguire script esterni che usano SQL Server dati o che vengono eseguiti con SQL Server come contesto di calcolo, è necessario un account di accesso SQL Server o utente di Windows. Gli utenti del database che dispongono delle autorizzazioni per eseguire una query ad hoc possono accedere agli stessi dati dallo script R o Python.

L'account di accesso o l'account utente identifica l' *entità di sicurezza*che potrebbe richiedere più livelli di accesso, a seconda dei requisiti di script esterni:

+ Autorizzazione per accedere al database in cui sono abilitati gli script esterni.
+ Autorizzazioni per la lettura di dati da oggetti protetti, ad esempio tabelle.
+ Possibilità di scrivere nuovi dati in una tabella, ad esempio un modello, o i risultati dei punteggi.
+ Possibilità di creare nuovi oggetti, ad esempio tabelle, stored procedure che usano lo script esterno o funzioni personalizzate che usano il processo R o Python.
+ Diritto di installare nuovi pacchetti nel computer SQL Server o di usare i pacchetti forniti a un gruppo di utenti.

Ogni persona che esegue uno script esterno utilizzando SQL Server come contesto di esecuzione deve essere mappata a un utente nel database. Anziché impostare individualmente le autorizzazioni utente del database, è possibile creare ruoli per gestire i set di autorizzazioni e assegnare gli utenti a tali ruoli, anziché impostare individualmente le autorizzazioni utente.

Per ulteriori informazioni, vedere [concedere agli utenti le autorizzazioni per SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md).

## <a name="permissions-when-using-an-external-client-tool"></a>Autorizzazioni quando si usa uno strumento client esterno

Per gli utenti che usano R o Python in uno strumento client esterno è necessario che l'account di accesso o l'account sia mappato a un utente nel database, se è necessario eseguire uno script esterno nel database o accedere a dati e oggetti di database. Sono necessarie le stesse autorizzazioni se lo script esterno viene inviato da un client di data science remoto o eseguito usando un stored procedure T-SQL.

Si supponga, ad esempio, che sia stato creato uno script esterno eseguito nel computer locale e che si desideri eseguire lo script in SQL Server. È necessario assicurarsi che siano soddisfatte le condizioni seguenti:

+ Il database consente le connessioni remote.
+ L'account di accesso SQL o l'account di Windows utilizzato per l'accesso al database è stato aggiunto al SQL Server a livello di istanza.
+ L'account di accesso SQL o l'utente di Windows deve disporre dell'autorizzazione per eseguire script esterni. In genere, questa autorizzazione può essere aggiunta solo da un amministratore del database.
+ L'account di accesso SQL o l'utente della finestra deve essere aggiunto come utente, con le autorizzazioni appropriate, in ogni database in cui lo script esterno esegue una delle operazioni seguenti:
  + Recupero dei dati.
  + Scrittura o aggiornamento dei dati.
  + Creazione di nuovi oggetti, ad esempio tabelle o stored procedure.

Dopo aver eseguito il provisioning dell'account di accesso o dell'account utente di Windows e avere fornito le autorizzazioni necessarie, è possibile eseguire uno script esterno in SQL Server usando un oggetto origine dati in R o la libreria **revoscalepy** in Python oppure chiamando un stored procedure contiene lo script esterno.

Ogni volta che viene avviato uno script esterno da SQL Server, la sicurezza del motore di database ottiene il contesto di sicurezza dell'utente che ha avviato il processo e gestisce i mapping dell'utente o dell'account di accesso agli oggetti a protezione diretta.

Pertanto, tutti gli script esterni avviati da un client remoto devono specificare le informazioni relative all'account di accesso o all'utente come parte della stringa di connessione.

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>Servizi usati nell'elaborazione esterna (Launchpad)

Il Framework di estendibilità aggiunge un nuovo servizio NT all' [elenco dei servizi](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) in un'installazione di SQL Server: [**Launchpad di SQL Server (MSSSQLSERVER)** ](extensibility-framework.md#launchpad).

Il motore di database usa il servizio Launchpad di SQL Server per creare un'istanza di una sessione R o Python come processo separato. Il processo viene eseguito con un account con privilegi limitati. distinto da SQL Server, Launchpad e dall'identità utente in cui è stata eseguita la query stored procedure o host. L'esecuzione di script in un processo separato, con account con privilegi limitati, costituisce la base del modello di sicurezza e isolamento per R e Python in SQL Server.

Oltre a avviare i processi esterni, Launchpad è anche responsabile del rilevamento dell'identità dell'utente chiamante e del mapping dell'identità all'account di lavoro con privilegi limitati usato per avviare il processo. In alcuni scenari, in cui script o codice richiama SQL Server per i dati e le operazioni, Launchpad è in genere in grado di gestire facilmente il trasferimento di identità. Lo script che contiene istruzioni SELECT o funzioni di chiamata e altri oggetti di programmazione avrà in genere esito positivo se l'utente chiamante dispone di autorizzazioni sufficienti.

> [!NOTE]
> Per impostazione predefinita [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] , è configurato per l'esecuzione in **NT Service\MSSQLLaunchpad**, di cui viene effettuato il provisioning con tutte le autorizzazioni necessarie per eseguire script esterni. Per ulteriori informazioni sulle opzioni configurabili, vedere [configurazione del servizio launchpad di SQL Server](../security/sql-server-launchpad-service-account.md).

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>Identità utilizzate nell'elaborazione (SQLRUserGroup)

**SQLRUserGroup** (Gruppo di utenti con restrizioni SQL) viene creato dal programma di installazione di SQL Server e contiene un pool di account utente di Windows locali con privilegi limitati. Quando è necessario un processo esterno, Launchpad accetta un account di lavoro disponibile e lo usa per eseguire un processo. In particolare, Launchpad attiva un account di lavoro disponibile, ne esegue il mapping all'identità dell'utente chiamante ed esegue lo script nell'account di lavoro.

+ **SQLRUserGroup** è collegato a un'istanza specifica. Per ogni istanza in cui è stato abilitato Machine Learning è necessario un pool separato di account di lavoro. Gli account non possono essere condivisi tra istanze.

+ La dimensione del pool di account utente è statica e il valore predefinito è 20, che supporta 20 sessioni simultanee. Il numero di sessioni di runtime esterne che possono essere avviate simultaneamente è limitato dalle dimensioni del pool di account utente. 

+ I nomi degli account di lavoro nel pool sono nel formato SqlInstanceName*nn*. Ad esempio, in un'istanza predefinita, **SQLRUserGroup** contiene gli account denominati MSSQLSERVER01, MSSQLSERVER02 e così via fino a MSSQLSERVER20.

Le attività in parallelo non utilizzano account aggiuntivi. Se, ad esempio, un utente esegue un'attività di assegnazione dei punteggi che utilizza l'elaborazione parallela, viene riutilizzato lo stesso account di lavoro per tutti i thread. Se si intende usare in modo intensivo Machine Learning, è possibile aumentare il numero di account usati per eseguire gli script esterni. Per altre informazioni, vedere [modificare il pool di account utente per Machine Learning](../../advanced-analytics/administration/modify-user-account-pool.md).

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>Isolamento AppContainer in SQL Server 2019

In SQL Server 2019, il programma di installazione non crea più account di lavoro per **SQLRUserGroup**. Viene invece realizzata l'isolamento tramite [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). In fase di esecuzione, quando viene rilevato uno script esterno in una stored procedure o una query, SQL Server chiama Launchpad con una richiesta per un'utilità di avvio specifica dell'estensione. Launchpad richiama l'ambiente di runtime appropriato in un processo con la relativa identità e crea un'istanza di un AppContainer per contenerlo. Questa modifica è vantaggiosa perché la gestione di account e password locali non è più necessaria. Inoltre, nelle installazioni in cui gli account utente locali non sono consentiti, l'eliminazione della dipendenza dell'account utente locale significa che è ora possibile usare questa funzionalità.

Come implementato da SQL Server, AppContainers sono un meccanismo interno. Sebbene non venga visualizzata la prova fisica di AppContainers in Process Monitor, è possibile trovarli nelle regole del firewall in uscita create dal programma di installazione per impedire ai processi di effettuare chiamate di rete. Per ulteriori informazioni, vedere la pagina relativa alla [configurazione del firewall per SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md).

> [!Note]
> In SQL Server 2019, **SQLRUserGroup** dispone solo di un membro che è ora il singolo account del servizio launchpad di SQL Server invece di più account di lavoro.
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>Autorizzazioni concesse a SQLRUserGroup

Per impostazione predefinita, i membri di **SQLRUserGroup** dispongono delle autorizzazioni di lettura ed esecuzione per i file nelle directory SQL Server **contenitori**, **R_SERVICES**e **PYTHON_SERVICES** , con accesso a file eseguibili, librerie e set di dati predefiniti in R e le distribuzioni di Python installate con SQL Server. 

Per proteggere le risorse sensibili in SQL Server, è possibile definire facoltativamente un elenco di controllo di accesso (ACL) che nega l'accesso a **SQLRUserGroup**. Viceversa, è anche possibile concedere le autorizzazioni per le risorse di dati locali presenti nel computer host, oltre a SQL Server stesso. 

Per impostazione predefinita, **SQLRUserGroup** non dispone di un account di accesso al database o delle autorizzazioni per i dati. In alcuni casi, potrebbe essere necessario creare un account di accesso per consentire le connessioni di loopback, in particolare quando un'identità Windows attendibile è l'utente chiamante. Questa funzionalità è denominata [*autenticazione implicita*](#implied-authentication). Per altre informazioni, vedere [aggiungere SQLRUserGroup come utente del database](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="identity-mapping"></a>Mapping di identità

Quando viene avviata una sessione, Launchpad mappa l'identità dell'utente chiamante a un account di lavoro. Il mapping di un utente di Windows esterno o di un account di accesso SQL valido a un account di lavoro è valido solo per la durata del stored procedure SQL che esegue lo script esterno. Le query parallele dallo stesso account di accesso sono mappate allo stesso account utente di lavoro.

Durante l'esecuzione, Launchpad crea cartelle temporanee per archiviare i dati della sessione, eliminando i dati alla conclusione della sessione. Le directory sono con restrizioni di accesso. Per R, RLauncher esegue questa attività. Per Python, PythonLauncher esegue questa attività. Ogni singolo account di lavoro è limitato alla propria cartella e non può accedere ai file nelle cartelle sopra il proprio livello. Tuttavia, l'account di lavoro può leggere, scrivere o eliminare gli elementi figlio nella cartella di lavoro della sessione creata. Un amministratore del computer può visualizzare le directory create per ogni processo. Ogni directory è identificata dal relativo GUID di sessione.

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>Autenticazione implicita (richieste loop back)

*L'autenticazione implicita* descrive il comportamento della richiesta di connessione in base al quale i processi esterni in esecuzione come account di lavoro con privilegi limitati vengono presentati come identità utente attendibile per SQL Server sulle richieste del ciclo per i dati o le operazioni. Come concetto, l'autenticazione implicita è univoca per l'autenticazione di Windows, in SQL Server stringhe di connessione che specificano una connessione trusted, sulle richieste provenienti da processi esterni, ad esempio R o Python script. Viene talvolta indicato anche come *ciclo indietro*.

Le connessioni attendibili sono realizzabili da script R e Python, ma solo con la configurazione aggiuntiva. Nell'architettura di estendibilità, i processi R e Python vengono eseguiti con account di lavoro, ereditando le autorizzazioni dal **SQLRUserGroup**padre. Quando una stringa di connessione `Trusted_Connection=True`specifica, l'identità dell'account di lavoro viene presentata nella richiesta di connessione, che per impostazione predefinita è sconosciuta per SQL Server.

Per garantire la corretta connessione trusted, è necessario creare un account di accesso al database per **SQLRUserGroup**. Al termine di questa operazione, qualsiasi connessione trusted da qualsiasi membro di **SQLRUserGroup** dispone dei diritti di accesso per SQL Server. Per istruzioni dettagliate, vedere [aggiungere SQLRUserGroup a un account di accesso al database](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

Le connessioni attendibili non sono la formulazione più utilizzata di una richiesta di connessione. Quando lo script R o Python specifica una connessione, può essere più comune usare un account di accesso SQL oppure un nome utente e una password completamente specificati se la connessione è a un'origine dati ODBC.

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>Funzionamento dell'autenticazione implicita per le sessioni R e Python

Il diagramma seguente illustra l'interazione dei componenti di SQL Server con il runtime di R e il modo in cui esegue l'autenticazione implicita per R.

![Autenticazione implicita per R](../security/media/implied-auth-rsql.png)

Il diagramma seguente illustra l'interazione dei componenti di SQL Server con il runtime di Python e il modo in cui esegue l'autenticazione implicita per Python.

![Autenticazione implicita per Python](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>Nessun supporto per Transparent Data Encryption inattivi

[Transparent Data Encryption (](../../relational-databases/security/encryption/transparent-data-encryption.md) Transparent Data Encryption) non è supportato per i dati inviati o ricevuti dal runtime di script esterno. Il motivo è che il processo esterno (R o Python) viene eseguito all'esterno del processo di SQL Server. I dati utilizzati dal runtime esterno non sono pertanto protetti dalle funzionalità di crittografia del motore di database. Questo comportamento non è diverso da qualsiasi altro client in esecuzione nel computer SQL Server che legge i dati dal database e crea una copia.

Di conseguenza, Transparent Data Encryption **non viene** applicato a tutti i dati utilizzati negli script R o Python, né a tutti i dati salvati su disco o ai risultati intermedi resi permanente. Tuttavia, altri tipi di crittografia, ad esempio la crittografia BitLocker di Windows o la crittografia di terze parti applicata a livello di file o di cartella, sono comunque validi.

Nel caso di [Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md), i runtime esterni non hanno accesso alle chiavi di crittografia. Non è pertanto possibile inviare i dati agli script.

## <a name="next-steps"></a>Passaggi successivi

In questo articolo sono stati appresi i componenti e il modello di interazione dell'architettura di sicurezza incorporata nel [Framework](../../advanced-analytics/concepts/extensibility-framework.md)di estendibilità. I punti chiave trattati in questo articolo includono lo scopo di Launchpad, SQLRUserGroup e account di lavoro, l'isolamento dei processi di R e Python e il modo in cui viene eseguito il mapping delle identità utente agli account di lavoro. 

Come passaggio successivo, rivedere le istruzioni per la [concessione di autorizzazioni](../../advanced-analytics/security/user-permission.md). Per i server che utilizzano l'autenticazione di Windows, è necessario esaminare anche [Aggiungi SQLRUserGroup a un account di accesso al database](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md) per apprendere quando è necessaria una configurazione aggiuntiva.