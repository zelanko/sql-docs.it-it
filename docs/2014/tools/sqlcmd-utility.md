---
title: Utilità sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- statements [SQL Server], command prompt
- QUIT command
- Transact-SQL statements, command prompt
- EXIT command
- sqlcmd commands
- ED command
- sqlcmd utility
- command prompt utilities [SQL Server], sqlcmd
- '!! command'
- stored procedures [SQL Server], command prompt
- system stored procedures [SQL Server], command prompt
- sqlcmd utility, about sqlcmd utility
- scripts [SQL Server], command prompt
- RESET command
- GO command
ms.assetid: e1728707-5215-4c04-8320-e36f161b834a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d128085012c0ef3a9bc58b147f982a26d2c094b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63035386"
---
# <a name="sqlcmd-utility"></a>sqlcmd
  Il `sqlcmd` utilità consente di immettere [!INCLUDE[tsql](../includes/tsql-md.md)] istruzioni, le procedure di sistema e file script al prompt dei comandi, in **Editor di Query** in modalità SQLCMD, in un file di script Windows o in un passaggio di processo del sistema operativo (Cmd.exe) di un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Processo dell'agente. e utilizza ODBC per eseguire batch [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] Usa il [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]SqlClient per l'esecuzione nei normali e la modalità SQLCMD nel **Editor di Query**. Se `sqlcmd` viene eseguita dalla riga di comando, `sqlcmd` utilizza il driver ODBC. Poiché possono essere applicate opzioni predefinite diverse, l'esecuzione della stessa query nella modalità SQLCMD di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e nell'utilità `sqlcmd` potrebbe generare risultati diversi.  
  
 Attualmente in `sqlcmd` non è necessario utilizzare uno spazio tra l'opzione della riga di comando e il valore. In una versione futura, tuttavia, è possibile che tra l'opzione della riga di comando e il valore sia necessario inserire uno spazio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
   sqlcmd  
   -a  
   packet_size  
   -A (dedicated administrator connection)  
-b (terminate batch job if there is an error)  
-cbatch_terminator-C (trust the server certificate)  
-ddb_name-e (echo input)  
-E (use trusted connection)  
-fcodepage | i:codepage[,o:codepage] | o:codepage[,i:codepage]  
-hrows_per_header-Hworkstation_name-iinput_file-I (enable quoted identifiers)  
-k[1 | 2] (remove or replace control characters)  
-Kapplication_intent-llogin_timeout-L[c] (list servers, optional clean output)  
-merror_level-Mmultisubnet_failover-N (encrypt connection)  
-ooutput_file-p[1] (print statistics, optional colon format)  
-Ppassword-q "cmdline query"-Q "cmdline query" (and exit)  
-r[0 | 1] (msgs to stderr)  
-R (use client regional settings)  
-scol_separator-S [protocol:]server[\instance_name][,port]  
-tquery_timeout-u (unicode output file)  
-Ulogin_id-vvar = "value"-Verror_severity_level-wcolumn_width-W (remove trailing spaces)  
-x (disable variable substitution)  
-X[1] (disable commands, startup script, environment variables and optional exit)  
-yvariable_length_type_display_width-Yfixed_length_type_display_width-znew_password -Znew_password (and exit)  
  
-? (usage)  
```  
  
## <a name="command-line-options"></a>Opzioni della riga di comando  
 **Opzioni correlate all'account di accesso**  
  **-A**  
 Stabilisce la connessione a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite una connessione amministrativa dedicata (DAC, Dedicated Administrator Connection). Questo tipo di connessione viene utilizzato per eseguire la risoluzione dei problemi a livello di server e funziona solo in computer server che supportano le connessioni DAC. Se la connessione DAC non è disponibile, l'utilità `sqlcmd` genera un messaggio di errore e viene chiusa. Per altre informazioni sulle connessioni DAC, vedere [Connessione di diagnostica per gli amministratori di database](../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
 **-C**  
 Questa opzione viene utilizzata dal client per configurare l'attendibilità implicita del certificato del server senza necessità di convalida ed equivale all'opzione ADO.NET `TRUSTSERVERCERTIFICATE = true`.  
  
 **-d** _db_name_  
 Problemi di un `USE` *db_name* istruzione quando si avvia `sqlcmd`. Questa opzione imposta la variabile di scripting SQLCMDDBNAME di `sqlcmd` per specificare il database iniziale. Il valore predefinito corrisponde alla proprietà relativa al database predefinito dell'accesso. Se il database non esiste, viene generato un messaggio di errore e l'utilità `sqlcmd` viene chiusa.  
  
 **-l** _login_timeout_  
 Specifica il numero dei secondi che devono trascorrere prima che si verifichi il timeout di un accesso di `sqlcmd` al driver ODBC quando si tenta la connessione a un server. Questa opzione imposta la variabile di scripting SQLCMDLOGINTIMEOUT di `sqlcmd`. Il valore predefinito per il timeout di accesso a `sqlcmd` è otto secondi. Il valore del timeout deve essere un numero compreso tra 0 e 65.534. Se il valore specificato non è numerico o non è compreso in tale intervallo, `sqlcmd` genera un messaggio di errore. Il valore 0 specifica un timeout infinito.  
  
 **-E**  
 Utilizza una connessione trusted anziché un nome utente e una password per l'accesso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. In caso di omissione di -E, `sqlcmd` utilizza l'opzione della connessione trusted per impostazione predefinita.  
  
 L'opzione **-E** ignora eventuali impostazioni delle variabili di ambiente relative a nome utente e password, ad esempio SQLCMDPASSWORD. Se si usa l'opzione **-E** in combinazione con l'opzione **-U** o con l'opzione **-P** , viene generato un messaggio di errore.  
  
 **-H** _workstation_name_  
 Nome di una workstation. Questa opzione imposta la variabile di scripting SQLCMDWORKSTATION di `sqlcmd`. Il nome della workstation è riportato nella colonna **hostname** della vista del catalogo **sys.processes** oppure è possibile ottenerlo tramite la stored procedure **sp_who**. Se questa opzione viene omessa, il valore predefinito è costituito dal nome del computer corrente. È possibile utilizzare questo nome per identificare sessioni di `sqlcmd` diverse.  
  
 **-K** _application_intent_  
 Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. L'unico valore attualmente supportato è **ReadOnly**. Se l'opzione **-K** non è specificata, l'utilità sqlcmd non supporta la connettività a una replica secondaria in un gruppo di disponibilità AlwaysOn. Per altre informazioni, vedere [Repliche secondarie attive: repliche secondarie leggibili](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 `-M` *multisubnet_failover*  
 Specificare sempre `-M` in caso di connessione al listener del gruppo di disponibilità di un gruppo di disponibilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o a un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Tramite `-M` viene fornito un rilevamento più veloce di una connessione al server attualmente attivo. Se `-M` non è specificato, significa che `-M` è disabilitato. Per altre informazioni sulle [!INCLUDE[ssHADR](../includes/sshadr-md.md)], vedere [listener del gruppo di disponibilità, connettività Client e Failover dell'applicazione &#40;SQL Server&#41;](../database-engine/listeners-client-connectivity-application-failover.md), [la creazione e configurazione di gruppi di disponibilità &#40;SQL Server&#41;](../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clustering di Failover e gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md), e [repliche secondarie attive: Repliche secondarie leggibili](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) .  
  
 **-N**  
 Questa opzione viene utilizzata dal client per richiedere una connessione crittografata.  
  
 **-P** _password_  
 Password specificata dall'utente. Alle password viene applicata la distinzione tra maiuscole e minuscole. Se viene utilizzata l'opzione - U e il **-P** opzione non viene utilizzata e la variabile di ambiente SQLCMDPASSWORD non è stata impostata, `sqlcmd` chiede all'utente una password. Se il **-P** opzione viene specificata alla fine del prompt dei comandi senza indicare una password `sqlcmd` Usa la password predefinita (NULL).  
  
> [!IMPORTANT]  
>  Non usare una password vuota. Usare una password complessa. Per altre informazioni, vedere [Strong Passwords](../relational-databases/security/strong-passwords.md).  
  
 La richiesta della password viene visualizzata mediante la stampa nella console, come indicato di seguito: `Password:`  
  
 L'input dell'utente è nascosto. L'input non viene pertanto visualizzato e il cursore rimane in posizione.  
  
 La variabile di ambiente SQLCMDPASSWORD consente di impostare una password predefinita per la sessione corrente. Per tale motivo, non è necessario specificare le password a livello di codice in file batch.  
  
 Nell'esempio seguente viene innanzitutto impostata la variabile SQLCMDPASSWORD al prompt dei comandi e quindi si accede all'utilità `sqlcmd`. Al prompt dei comandi digitare:  
  
 `SET SQLCMDPASSWORD= p@a$$w0rd`  
  
> [!IMPORTANT]  
>  La password risulterà visibile a chiunque si trovi davanti allo schermo del computer.  
  
 Al prompt dei comandi successivo digitare:  
  
 `sqlcmd`  
  
 Se la combinazione di nome utente e password non è corretta, viene generato un messaggio di errore.  
  
> [!NOTE]  
>  La variabile di ambiente OSQLPASSWORD è disponibile per motivi di compatibilità con le versioni precedenti. La variabile di ambiente SQLCMDPASSWORD è prioritaria rispetto alla variabile di ambiente OSQLPASSWORD; Ciò significa che `sqlcmd` e **osql** possono essere usati senza creare conflitti e che gli script precedenti continueranno a funzionare.  
  
 Se si usa l'opzione **-P** in combinazione con l'opzione **-E** , viene generato un messaggio di errore.  
  
 Se l'opzione **-P** è seguita da più di un argomento, viene generato un messaggio di errore e il programma viene chiuso.  
  
 **-S** [*protocol*:]*server*[**\\**_instance_name_][**,**_port_]  
 Specifica l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a cui connettersi. Imposta la variabile di scripting SQLCMDSERVER di `sqlcmd`.  
  
 Specificare *server_name* per connettersi all'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel computer server. Specificare *server_name* [ **\\**_instance_name_ ] per connettersi a un'istanza denominata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel computer server. Se non si specifica alcun server, `sqlcmd` si connette all'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] del computer locale. Questa opzione è richiesta per l'esecuzione di `sqlcmd` da un computer remoto in rete.  
  
 *protocollo* può essere `tcp` (TCP/IP), `lpc` (shared memory) o `np` (named pipe).  
  
 Se non si specifica un *nome_server* [ **\\** _nome_istanza_ ] quando si avvia `sqlcmd`, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Cerca e Usa il Variabile di ambiente SQLCMDSERVER.  
  
> [!NOTE]  
>  La variabile di ambiente OSQLSERVER è disponibile per motivi di compatibilità con le versioni precedenti. La variabile di ambiente SQLCMDSERVER è prioritaria rispetto alla variabile di ambiente OSQLSERVER; Ciò significa che `sqlcmd` e **osql** possono essere usati senza creare conflitti e che gli script precedenti continueranno a funzionare.  
  
 **-U** _login_id_  
 ID di accesso dell'utente.  
  
> [!NOTE]  
>  La variabile di ambiente OSQLUSER è disponibile per motivi di compatibilità con le versioni precedenti. La variabile di ambiente SQLCMDUSER ha la priorità rispetto alla variabile di ambiente OSQLUSER. Ciò significa che `sqlcmd` e **osql** può essere usato uno accanto a altro senza interferenze. e gli script **osql** esistenti continueranno a funzionare correttamente.  
  
 Se non si specifica la **- U** opzione né la **-P** opzioni viene specificata, `sqlcmd` tenta di connettersi tramite [!INCLUDE[msCoName](../includes/msconame-md.md)] modalità di autenticazione di Windows. L'autenticazione si basa sull'account di Windows dell'utente che esegue `sqlcmd`.  
  
 Se si usa l'opzione **-U** in combinazione con l'opzione **-E** , descritta più avanti in questo argomento, viene generato un messaggio di errore. Se l'opzione **-U** è seguita da più di un argomento, viene generato un messaggio di errore e il programma viene chiuso.  
  
 **-z** _new_password_  
 Modifica la password:  
  
 `sqlcmd -U someuser -P s0mep@ssword -z a_new_p@a$$w0rd`  
  
 **-Z** _new_password_  
 Consente di modificare la password e di chiudere l'utilità:  
  
 `sqlcmd -U someuser -P s0mep@ssword -Z a_new_p@a$$w0rd`  
  
 **Opzioni di input/output**  
  **-f** _codepage_ | **i:**_codepage_[**,o:**_codepage_] | **o:**_codepage_[**,i:**_codepage_]  
 Specifica le tabelle codici di input e output. Il numero specificato per codepage è un valore numerico che indica una tabella codici di Windows installata.  
  
 Regole di conversione delle tabelle codici  
  
-   Se non viene specificata una tabella codici, `sqlcmd` utilizzerà la tabella codici corrente per i file sia di input che di output, a meno che il file di input non sia un file Unicode per cui non è necessaria alcuna conversione.  
  
-   `sqlcmd` riconosce automaticamente file di input Unicode sia di tipo big-endian che di tipo little-endian. Se è stata specificata l'opzione **-u** , l'output sarà sempre in formato Unicode Little-Endian.  
  
-   Se non viene specificato alcun file di output, la tabella codici di output sarà costituita dalla tabella codici della console. Ciò consente la visualizzazione corretta dell'output nella console.  
  
-   Se sono disponibili più file di input, vengono considerati appartenenti alla stessa tabella codici. È possibile combinare file di input Unicode e non Unicode.  
  
 Immettere `chcp` al prompt dei comandi per verificare la tabella codici di Cmd.exe.  
  
 **-i** _input_file_[**,**_input_file2_...]  
 Identifica il file che include un batch di istruzioni SQL o stored procedure. È possibile specificare più file che verranno letti ed elaborati nell'ordine in cui sono stati indicati. Non utilizzare alcuno spazio tra i nomi di file. `sqlcmd` verificherà innanzitutto che tutti i file specificati esistano. Se uno o più file non esistono, l'utilità `sqlcmd` viene chiusa. Le opzioni -i e -Q/-q si escludono a vicenda.  
  
 Percorsi di esempio:  
  
 **-i** c:\\< nome file\>  
  
 **-i** \\\\<Server\>\\<Share$>\\<filename\>  
  
 **-i** "C:\Cartella\\<nomefile\>"  
  
 È necessario racchiudere tra virgolette i percorsi dei file contenenti spazi.  
  
 Questa opzione può essere usata più di una volta: **-i**_input_file_ **-I**_I input_file._  
  
 **-o** _output_file_  
 Identifica il file che riceve l'output di `sqlcmd`.  
  
 Se si specifica **-u** , *output_file* viene archiviato in formato Unicode. Se il nome file non è valido, viene generato un messaggio di errore e l'utilità `sqlcmd` viene chiusa. `sqlcmd` non supporta la scrittura simultanea di più processi `sqlcmd` nello stesso file. L'output del file risulterà danneggiato o non corretto. Per altre informazioni sui formati di file, vedere l'opzione **-f** . Se il file non esiste, verrà creato. Un file con lo stesso nome di una sessione di `sqlcmd` precedente verrà sovrascritto. Il file specificato in questa posizione non corrisponde al file **stdout** . Se viene specificato un file **stdout** , questo file non verrà utilizzato.  
  
 Percorsi di esempio:  
  
 **-o** C:\\<nomefile>  
  
 **-o** \\\\<Server\>\\<Share$>\\<filename\>  
  
 **-o "** C:\Cartella\\<nomefile\>"  
  
 È necessario racchiudere tra virgolette i percorsi dei file contenenti spazi.  
  
 **-r**[**0** | **1**]  
 Reindirizza l'output dei messaggi di errore sullo schermo (**stderr**). Se il parametro viene omesso o si specifica **0**, vengono reindirizzati solo i messaggi di errore con livello di gravità 11 o superiore. Se si specifica **1**, viene reindirizzato l'output di tutti i messaggi di errore che includono PRINT. Non ha effetto se si utilizza -o. Per impostazione predefinita, i messaggi sono inviati a **stdout**.  
  
 **-R**  
 Fa sì che `sqlcmd` localizzare numeric, currency, data e le colonne di ora recuperate da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] basate sulle impostazioni locali del client. Per impostazione predefinita, tali colonne vengono visualizzate usando le impostazioni internazionali del server.  
  
 **-u**  
 Specifica l'archiviazione di *output_file* in formato Unicode, indipendentemente dal formato di *input_file*.  
  
 **Opzioni relative all'esecuzione di query**  
  **-e**  
 Scrive gli script di input nel dispositivo di output standard (**stdout**).  
  
 **-I**  
 Imposta l'opzione di connessione SET QUOTED_IDENTIFIER su ON. Per impostazione predefinita, l'opzione è impostata su OFF. Per altre informazioni, vedere [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).  
  
 **-q"** _cmdline query_ **"**  
 Esegue una query all'avvio di `sqlcmd` senza chiudere `sqlcmd` al termine dell'esecuzione della query. È possibile eseguire più query delimitandole con punti e virgola. Racchiudere la query tra virgolette come illustrato nell'esempio seguente.  
  
 Al prompt dei comandi digitare:  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  Non utilizzare il carattere di terminazione GO nella query.  
  
 Se insieme a questa opzione si specifica `-b`, l'utilità `sqlcmd` viene chiusa in caso di errore. L'opzione `-b` è descritta di seguito in questo argomento.  
  
 **-Q"** _cmdline query_ **"**  
 Esegue una query all'avvio di `sqlcmd` e quindi chiude immediatamente `sqlcmd`. È possibile eseguire più query delimitandole con punti e virgola.  
  
 Racchiudere la query tra virgolette come illustrato nell'esempio seguente.  
  
 Al prompt dei comandi digitare:  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  Non utilizzare il carattere di terminazione GO nella query.  
  
 Se insieme a questa opzione si specifica `-b`, l'utilità `sqlcmd` viene chiusa in caso di errore. L'opzione `-b` è descritta di seguito in questo argomento.  
  
 **-t** _query_timeout_  
 Specifica il numero di secondi prima del timeout del comando o dell'istruzione SQL. Questa opzione imposta la `sqlcmd` variabile di scripting SQLCMDSTATTIMEOUT. Se per *time_out* non viene specificato un valore, non si verifica il timeout del comando. Il valore di *query**time_out* deve essere un numero compreso tra 1 e 65534. Se il valore specificato non è numerico o non è compreso in tale intervallo, `sqlcmd` genera un messaggio di errore.  
  
> [!NOTE]  
>  Il valore di timeout effettivo può variare di diversi secondi rispetto al valore specificato per *time_out* .  
  
 **-vvar =** _value_[ **var =** _value_...]  
 Crea una `sqlcmd`variabile di scripting che può essere usato in un `sqlcmd` script. Se il valore contiene spazi, racchiuderlo tra virgolette. È possibile specificare più  **_var_**=**"*`values`*"** valori. Se in uno dei valori specificati è incluso un errore, l'utilità `sqlcmd` genera un messaggio di errore e viene chiusa.  
  
 `sqlcmd -v MyVar1=something MyVar2="some thing"`  
  
 `sqlcmd -v MyVar1=something -v MyVar2="some thing"`  
  
 **-x**  
 Indica a `sqlcmd` di ignorare le variabili di scripting. Ciò risulta utile quando uno script contiene numerose istruzioni INSERT che possono includere stringhe con lo stesso formato di variabili normali, ad esempio $(*variable_name*).  
  
 **Opzioni di formattazione**  
  **-h** _headers_  
 Specifica il numero di righe da stampare tra le intestazioni delle colonne. Per impostazione predefinita, le intestazioni vengono stampate una volta per ogni set di risultati delle query. Questa opzione imposta la variabile di scripting SQLCMDHEADERS di `sqlcmd`. Usare **-1** per non stampare alcuna intestazione. Eventuali valori non validi comportano la generazione di un messaggio di errore e la chiusura di `sqlcmd`.  
  
 **-k** [**1** | **2**]  
 Rimuove tutti i caratteri di controllo, ad esempio i caratteri di tabulazione e nuova riga, dall'output. In questo modo viene conservata la formattazione di colonna quando vengono restituiti i dati. Se si specifica 1, i caratteri di controllo vengono sostituiti da un singolo spazio. Se si specifica 2, i caratteri di controllo consecutivi vengono sostituiti da uno spazio singolo. **-k** corrisponde a **-k1**.  
  
 **-s** _col_separator_  
 Specifica il carattere separatore di colonna. L'impostazione predefinita è uno spazio vuoto. Questa opzione imposta la variabile di scripting SQLCMDCOLSEP di `sqlcmd`. Per utilizzare caratteri con un significato speciale per il sistema operativo, ad esempio il carattere e commerciale (&) o il punto e virgola (;), racchiudere il carattere specifico tra virgolette ("). Il separatore di colonna può essere un carattere a 8 bit qualsiasi.  
  
 **-w** _column_width_  
 Specifica la larghezza della schermata per l'output. Questa opzione imposta la variabile di scripting SQLCMDCOLWIDTH di `sqlcmd`. La larghezza della colonna deve essere un numero maggiore di 8 e minore di 65.536. Se la larghezza della colonna specificata non rientra in tale intervallo, `sqlcmd` genera e messaggio di errore. La lunghezza predefinita è di 80 caratteri. Se una riga di output supera la larghezza di colonna specificata, la riga viene riportata nella riga successiva.  
  
 **-W**  
 Questa opzione rimuove gli spazi finali da una colonna. Usare questa opzione in combinazione con l'opzione **-s** quando si preparano i dati per l'esportazione in un'altra applicazione. Non è possibile usare questa opzione con **-y** o **-Y** .  
  
 **-y** _variable_length_type_display_width_  
 Imposta la variabile di scripting SQLCMDMAXVARTYPEWIDTH di `sqlcmd`. L'impostazione predefinita è 256. Limita il numero di caratteri restituiti per i tipi di dati a lunghezza variabile di grandi dimensioni:  
  
-   `varchar(max)`  
  
-   `nvarchar(max)`  
  
-   `varbinary(max)`  
  
-   `xml`  
  
-   `UDT (user-defined data types)`  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
> [!NOTE]  
>  I tipi definiti dall'utente (UDT) possono essere a lunghezza fissa in base all'implementazione. Se la lunghezza di un tipo definito dall'utente (UDT) a lunghezza fissa è inferiore a *display_width*, il valore del tipo definito dall'utente (UDT) restituito non viene alterato. Se invece la lunghezza è superiore a *display_width*, l'output viene troncato.  
  
 
> [!IMPORTANT]  
>  Usare l'opzione **-y 0** con estrema cautela, poiché potrebbe causare gravi problemi a livello di prestazioni del server e della rete, a seconda delle dimensioni dei dati restituiti.  
  
 **-Y** _fixed_length_type_display_width_  
 Imposta la variabile di scripting SQLCMDMAXFIXEDTYPEWIDTH di `sqlcmd`. Il valore predefinito è 0 (illimitato). Limita il numero di caratteri restituiti per i tipi di dati seguenti:  
  
-   `char(` *n* `)`, dove 1 < = n < = 8000  
  
-   `nchar(n` *n* `)`, dove 1 < = n < = 4000  
  
-   `varchar(n` *n* `)`, dove 1 < = n < = 8000  
  
-   `nvarchar(n` *n* `)`, dove 1 < = n < = 4000  
  
-   `varbinary(n` *n* `)`, dove 1 < = n < = 4000  
  
-   `variant`  
  
 **Opzioni relative alla segnalazione degli errori**  
  `-b`  
 Specifica che, in caso di errore, `sqlcmd` termini, restituendo un valore DOS ERRORLEVEL. Il valore restituito alla variabile DOS ERRORLEVEL è **1** se il messaggio di errore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ha un livello di gravità maggiore di 10. In caso contrario, il valore restituito è **0**. Se è stata impostata l'opzione `-V` in combinazione con `-b`, `sqlcmd` non segnalerà l'errore se il livello di gravità è minore dei valori impostati tramite `-V`. I file batch del prompt dei comandi consentono di verificare il valore di ERRORLEVEL nonché di gestire correttamente l'errore. `sqlcmd` non segnala errori per livello di gravità 10 (messaggi informativi).  
  
 Se lo script `sqlcmd` contiene un commento errato o un errore di sintassi o se una variabile di scripting risulta mancante, il valore di ERRORLEVEL restituito è 1.  
  
 **-m** _error_level_  
 Controlla i messaggi di errore inviati a **stdout**. Vengono inviati i messaggi a cui è associato un livello di gravità maggiore o uguale a questo livello. Quando questo valore è impostato su **-1**, vengono inviati tutti i messaggi, inclusi quelli informativi. Non sono consentiti spazi tra **-m** e **-1**. Ad esempio, **-m-1** è un formato valido, mentre **-m-1** non lo è.  
  
 Questa opzione imposta inoltre la variabile di scripting SQLCMDERRORLEVEL di `sqlcmd`. Per impostazione predefinita, il valore di questa variabile è 0.  
  
 `-V` *error_severity_level*  
 Controlla il livello di gravità utilizzato per impostare la variabile ERRORLEVEL. Tramite i messaggi di errore a cui sono associati livelli di gravità maggiori o uguali a questo valore viene impostato ERRORLEVEL. I valori minori di 0 vengono indicati come 0. È possibile utilizzare file batch e CMD per verificare il valore della variabile ERRORLEVEL.  
  
 **Opzioni varie**  
  **-a** _packet_size_  
 Richiede un pacchetto di dimensione diversa. Questa opzione imposta la variabile di scripting SQLCMDPACKETSIZE di `sqlcmd`. Il valore di*packet_size* deve essere compreso tra 512 e 32767. Il valore predefinito è 4096. Dimensioni più estese del pacchetto possono migliorare le prestazioni per l'esecuzione di script che dispongono di molte istruzioni SQL tra comandi GO. È possibile richiedere dimensioni di pacchetto superiori. Se tale richiesta viene negata, tuttavia, `sqlcmd` utilizza le dimensioni di pacchetto predefinite del server.  
  
 **-c** _batch_terminator_  
 Specifica il carattere di terminazione di batch. Per impostazione predefinita, i comandi vengono terminati e inviati a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite l'immissione della parola "GO" su una riga a sé stante. Se il carattere di terminazione di batch viene reimpostato, non utilizzare parole chiave riservate [!INCLUDE[tsql](../includes/tsql-md.md)] o caratteri con un significato speciale per il sistema operativo anche se sono preceduti da una barra rovesciata.  
  
 **-L**[**c**]  
 Elenca i computer server configurati localmente e i nomi dei computer server che trasmettono in rete. Questo parametro non può essere utilizzato in combinazione con altri parametri. Il numero massimo di computer del server che è possibile specificare è 3000. Se l'elenco server è troncato a causa della dimensione del buffer, verrà visualizzato un messaggio di avviso.  
  
> [!NOTE]  
>  A causa della natura delle trasmissioni in rete, è possibile che `sqlcmd` non riceva una risposta tempestiva da tutti i server e pertanto che l'elenco di server restituito sia diverso per ogni chiamata di questa opzione.  
  
 Se si specifica il parametro facoltativo **c** , l'output viene visualizzato senza la riga di intestazione Servers e ogni riga del server viene elencata senza spazi iniziali. Questo tipo di output viene definito pulito. L'output pulito consente di migliorare le prestazioni di elaborazione dei linguaggi di scripting.  
  
 **-p**[**1**]  
 Stampa le statistiche delle prestazioni per ogni set di risultati. Di seguito è riportato un esempio del formato delle statistiche delle prestazioni:  
  
 `Network packet size (bytes): n`  
  
 `x xact[s]:`  
  
 `Clock Time (ms.): total       t1  avg       t2 (t3 xacts per sec.)`  
  
 Dove:  
  
 `x` = numero di transazioni elaborate da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 `t1` = tempo totale per tutte le transazioni.  
  
 `t2` = tempo medio per una singola transazione.  
  
 `t3` = numero medio di transazioni al secondo.  
  
 Tutti i valori relativi al tempo sono espressi in millisecondi.  
  
 Se si specifica il parametro facoltativo **1** , l'output delle statistiche è in formato separato da due punti. Questo formato può essere facilmente importato in un foglio di calcolo o elaborato da uno script.  
  
 Se il parametro facoltativo è un valore qualsiasi diverso da **1**, viene generato un errore e `sqlcmd` viene chiuso.  
  
 `-X`[**1**]  
 Disabilita i comandi che potrebbero pregiudicare la sicurezza del sistema quando `sqlcmd` viene eseguito da un file batch. I comandi disabilitati vengono comunque riconosciuti. `sqlcmd` genera un messaggio di avviso e continua l'esecuzione. Se il parametro facoltativo **1** è specificato, `sqlcmd` genera un messaggio di errore e viene chiusa. Se si specifica l'opzione `-X`, vengono disabilitati i comandi seguenti:  
  
-   **ED**  
  
-   **!!** _comando_  
  
 Se si specifica l'opzione `-X`, le variabili di ambiente non vengono trasmesse a `sqlcmd`. Questa opzione impedisce inoltre che venga eseguito lo script di avvio specificato utilizzando la variabile di scripting SQLCMDINI. Per altre informazioni sulle `sqlcmd` variabili di scripting, vedere [utilizzo di sqlcmd con variabili di Scripting](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md).  
  
 **-?**  
 Visualizza il riepilogo della sintassi delle opzioni di `sqlcmd`.  
  
## <a name="remarks"></a>Note  
 Le opzioni non devono essere necessariamente utilizzate nell'ordine illustrato nella sezione della sintassi.  
  
 Se vengono restituiti più risultati, `sqlcmd` stampa una riga vuota tra ogni set di risultati in un batch. Inoltre, il "\<x > righe interessate" messaggio non viene visualizzato se non è riferibile all'istruzione eseguita.  
  
 Per utilizzare `sqlcmd` in modo interattivo, digitare `sqlcmd` al prompt dei comandi con una o più delle opzioni precedentemente descritte in questo argomento. Per altre informazioni, vedere [Utilizzo dell'utilità sqlcmd](../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
> [!NOTE]  
>  Le opzioni **-L**, **-Q**, **-Z** oppure **-i** causare `sqlcmd` di chiudersi dopo l'esecuzione.  
  
 La lunghezza totale della riga di comando di `sqlcmd` nell'ambiente di comando (Cmd.exe), inclusi tutti gli argomenti e le variabili espanse, corrisponde alla lunghezza determinata dal sistema operativo per Cmd.exe.  
  
## <a name="variable-precedence-low-to-high"></a>Precedenza delle variabili (in ordine crescente)  
  
1.  Variabili di ambiente a livello di sistema.  
  
2.  Variabili di ambiente a livello di utente.  
  
3.  Shell dei comandi (**impostata** X = Y) impostata al prompt dei comandi prima dell'esecuzione `sqlcmd`.  
  
4.  **sqlcmd-v** X=Y  
  
5.  **:Setvar** X Y  
  
> [!NOTE]  
>  Per visualizzare le variabili di ambiente, nel **Pannello di controllo**aprire **Sistema**quindi fare clic sulla scheda **Avanzate** .  
  
## <a name="sqlcmd-scripting-variables"></a>Variabili di scripting di sqlcmd  
  
|Variabile|Opzione correlata|L/S|Impostazione predefinita|  
|--------------|--------------------|----------|-------------|  
|SQLCMDUSER|-U|R|""|  
|SQLCMDPASSWORD|-P|--|""|  
|SQLCMDSERVER|-S|R|"DefaultLocalInstance"|  
|SQLCMDWORKSTATION|-H|R|"ComputerName"|  
|SQLCMDDBNAME|-d|R|""|  
|SQLCMDLOGINTIMEOUT|-l|L/S|"8" (secondi)|  
|SQLCMDSTATTIMEOUT|-T|L/S|"0" = attesa illimitata|  
|SQLCMDHEADERS|-H|L/S|"0"|  
|SQLCMDCOLSEP|-S|L/S|" ".|  
|SQLCMDCOLWIDTH|-w|L/S|"0"|  
|SQLCMDPACKETSIZE|-A|R|"4096"|  
|SQLCMDERRORLEVEL|-M|L/S|0|  
|SQLCMDMAXVARTYPEWIDTH|-y|L/S|"256"|  
|SQLCMDMAXFIXEDTYPEWIDTH|-y|L/S|"0" = numero illimitato|  
|SQLCMDEDITOR||L/S|"edit.com"|  
|SQLCMDINI||R|""|  
  
 Le variabili SQLCMDUSER, SQLCMDPASSWORD e SQLCMDSERVER vengono impostate quando viene utilizzato il comando **:Connect**  
  
 .  
  
 La lettera L indica che il valore può essere impostato una sola volta durante l'inizializzazione del programma.  
  
 L/S indica che è possibile modificare il valore tramite il comando **setvar** e che il nuovo valore influirà sui comandi successivi.  
  
## <a name="sqlcmd-commands"></a>Comandi sqlcmd  
 In aggiunta alle istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] all'interno di `sqlcmd`, sono inoltre disponibili i comandi seguenti.  
  
|||  
|-|-|  
|**GO** [*count*]|**:List**|  
|[**:**] **RESET**|**:Error**|  
|[**:**] **ED**|**:Out**|  
|[**:**] **!!**|**:Perftrace**|  
|[**:**] **QUIT**|**:Connect**|  
|[**:**] **EXIT**|**:On Error**|  
|**:r**|**:Help**|  
|**:ServerList**|**:XML** [**ON** &#124; **OFF**]|  
|**:Setvar**|**:Listvar**|  
  
 Quando si utilizzano comandi `sqlcmd`, tenere presente quanto segue:  
  
-   Tutti i comandi `sqlcmd`, ad eccezione di GO, devono essere preceduti da due punti (:).  
  
    > [!IMPORTANT]  
    >  Per garantire la compatibilità con le versioni precedenti per gli script **osql** esistenti, alcuni comandi verranno riconosciuti anche senza i due punti. Questa caratteristica è indicata da [**:**].  
  
-   I comandi `sqlcmd` vengono riconosciuti solo se si trovano all'inizio di una riga.  
  
-   Tutti i comandi `sqlcmd` non fanno distinzione tra maiuscole e minuscole.  
  
-   Ogni comando deve trovarsi in una riga distinta. Un comando non può essere seguito da un'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] o da un altro comando.  
  
-   I comandi vengono eseguiti immediatamente e non vengono inseriti nel buffer di esecuzione come le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] .  
  
 **Comandi di modifica**  
  [**:**] **ED**  
 Avvia l'editor di testo. Questo editor può essere utilizzato per modificare il batch [!INCLUDE[tsql](../includes/tsql-md.md)] corrente o l'ultimo batch eseguito. Per modificare l'ultimo batch eseguito, il comando **ED** deve essere specificato subito dopo il completamento dell'esecuzione dell'ultimo batch.  
  
 L'editor di testo viene definito dalla variabile di ambiente SQLCMDEDITOR. L'editor predefinito è "Edit". Per modificare l'editor, impostare la variabile di ambiente SQLCMDEDITOR. Ad esempio, per impostare l'editor su Blocco note di [!INCLUDE[msCoName](../includes/msconame-md.md)] , al prompt dei comandi digitare:  
  
 `SET SQLCMDEDITOR=notepad`  
  
 [**:**] **RESET**  
 Cancella la cache dell'istruzione.  
  
 **:List**  
 Stampa il contenuto della cache dell'istruzione.  
  
 **Variabili**  
  **:Setvar** \<**var**> [ **"*`value`*"** ]  
 Definisce le variabili di scripting `sqlcmd`. Il formato delle variabili di scripting è il seguente: `$(VARNAME)`.  
  
 I nomi delle variabili non fanno distinzione tra maiuscole e minuscole.  
  
 È possibile impostare le variabili di scripting nei modi seguenti:  
  
-   In modo implicito utilizzando un'opzione della riga di comando. Ad esempio, il **-l** opzione imposta la SQLCMDLOGINTIMEOUT `sqlcmd` variabile.  
  
-   In modo esplicito utilizzando il comando **:Setvar** .  
  
-   Mediante la definizione di una variabile di ambiente prima dell'esecuzione di `sqlcmd`.  
  
> [!NOTE]  
>  L'opzione `-X` impedisce la trasmissione delle variabili di ambiente a `sqlcmd`.  
  
 Se il nome di una variabile definita mediante il comando **:Setvar** e di una variabile di ambiente è lo stesso, la variabile definita con **:Setvar** ha la precedenza.  
  
 I nomi delle variabili non devono contenere spazi vuoti.  
  
 I nomi delle variabili non possono disporre dello stesso formato delle espressioni con variabili, ad esempio $(var).  
  
 Se il valore stringa della variabile di scripting contiene spazi vuoti, racchiudere il valore tra virgolette. Se per una variabile di scripting non viene specificato alcun valore, la variabile di scripting viene eliminata.  
  
 **:Listvar**  
 Visualizza l'elenco delle variabili di scripting impostate.  
  
> [!NOTE]  
>  Solo le variabili vengono impostate di scripting `sqlcmd`e quelle impostate usando il **: Setvar** comando verrà visualizzato.  
  
 **Comandi di output**  
  **:Error**   
 **_\<_** _filename_  **_>|_ STDERR|STDOUT**  
 Reindirizza tutti gli output degli errori nel file specificato da *filename*, in **stderr** oppure in **stdout**. Il comando **Error** può essere utilizzato più volte in uno script. Per impostazione predefinita, l'output degli errori viene inviato in **stderr**.  
  
 *file name*  
 Crea e apre un file che riceverà l'output. Se il file esiste già, verrà troncato a zero byte. Se il file non è disponibile a causa delle autorizzazioni o per altri motivi, l'output non verrà trasferito e verrà inviato all'ultima destinazione specificata oppure alla destinazione predefinita.  
  
 **STDERR**  
 Trasferisce l'output degli errori al flusso **stderr** . Se l'output è stato reindirizzato, la destinazione alla quale il flusso è stato reindirizzato riceverà l'output degli errori.  
  
 **STDOUT**  
 Trasferisce l'output degli errori al flusso **stdout** . Se l'output è stato reindirizzato, la destinazione alla quale il flusso è stato reindirizzato riceverà l'output degli errori.  
  
 **:Out \<** _filename_ **>**| **STDERR**| **STDOUT**  
 Crea e reindirizza tutti i risultati delle query nel file specificato da *filename*, in **stderr** oppure in **stdout**. Per impostazione predefinita, l'output viene inviato in **stdout**. Se il file esiste già, verrà troncato a zero byte. Il comando **Out** può essere utilizzato più volte in uno script.  
  
 **:Perftrace \<** _filename_ **>**| **STDERR**| **STDOUT**  
 Crea e reindirizza tutte le informazioni di traccia delle prestazioni nel file specificato da *filename*, in **stderr** oppure in **stdout**. Per impostazione predefinita, l'output della traccia delle prestazioni viene inviato in **stdout**. Se il file esiste già, verrà troncato a zero byte. Il comando **Perftrace** può essere utilizzato più volte in uno script.  
  
 **Comandi di controllo dell'esecuzione**  
  **: In caso di errore**[ `exit`  |  `ignore`]  
 Imposta l'azione da eseguire quando si verifica un errore durante l'esecuzione dello script o del batch.  
  
 Se si specifica l'opzione `exit`, l'utilità `sqlcmd` viene chiusa con il valore di errore appropriato.  
  
 Se viene utilizzata l'opzione `ignore`, `sqlcmd` ignora l'errore e continua l'esecuzione del batch o dello script. Per impostazione predefinita, verrà stampato un messaggio di errore.  
  
 [**:**] **QUIT**  
 Provoca la chiusura di `sqlcmd`.  
  
 [**:**] **EXIT**[ **(*`statement`*)** ]  
 Consente di utilizzare il risultato di un'istruzione SELECT come valore restituito da `sqlcmd`. Se numerica, la prima colonna dell'ultima riga di risultati viene convertita in un valore integer di 4 byte (long). MS-DOS passa il byte di ordine inferiore al processo padre o al livello di errore del sistema operativo. Windows 200x passa l'intero valore intero di 4 byte. La sintassi è:  
  
 `:EXIT(query)`  
  
 Ad esempio:   
  
 `:EXIT(SELECT @@ROWCOUNT)`  
  
 È inoltre possibile includere il parametro **EXIT** in un file batch. Al prompt dei comandi, ad esempio, digitare:  
  
 `sqlcmd -Q "EXIT(SELECT COUNT(*) FROM '%1')"`  
  
 Il `sqlcmd` utilità consente di inviare dati tra parentesi **()** al server. Se una stored procedure di sistema seleziona un set e restituisce un valore, viene restituita solo la selezione. Se non si specifica alcun elemento tra le parentesi dell'istruzione EXIT **()** , viene eseguito tutto ciò che la precede nel batch e l'operazione viene quindi terminata senza restituire alcun valore.  
  
 Se si specifica una query non corretta, l'utilità `sqlcmd` viene chiusa senza restituire alcun valore.  
  
 Di seguito è riportato l'elenco dei formati supportati dall'istruzione EXIT.  
  
-   :EXIT  
  
 L'utilità non esegue il batch, quindi viene chiusa immediatamente e non restituisce alcun valore.  
  
-   :EXIT( )  
  
 L'utilità esegue il batch, viene chiusa e non restituisce alcun valore.  
  
-   :EXIT(query)  
  
 L'utilità esegue il batch in cui è inclusa la query e quindi viene chiusa dopo aver restituito i risultati della query.  
  
 Se in uno script `sqlcmd` si utilizza RAISERROR e si verifica una condizione con stato 127, l'utilità `sqlcmd` viene chiusa e restituisce al client l'ID di messaggio. Ad esempio:   
  
 `RAISERROR(50001, 10, 127)`  
  
 Questo errore comporta la chiusura di `sqlcmd` e la restituzione dell'ID di messaggio 50001 al client.  
  
 I valori restituiti compresi tra -1 e -99 sono riservati a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. L'utilità `sqlcmd` definisce i valori restituiti aggiuntivi elencati di seguito.  
  
|Valori restituiti|Descrizione|  
|-------------------|-----------------|  
|-100|Si è verificato un errore prima di selezionare il valore restituito.|  
|-101|Selezionando il valore restituito non si sono trovate righe.|  
|-102|Si è verificato un errore di conversione durante la selezione del valore restituito.|  
  
 **GO** [*count*]  
 GO indica sia la fine di un batch che l'esecuzione di eventuali istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] memorizzate nella cache. Se si specifica un valore per *count*, le istruzioni memorizzate nella cache verranno eseguite come batch singolo il numero di volte specificato da *count* .  
  
 **Comandi vari**  
  **:r \<** _filename_ **>**  
 Analizza altre [!INCLUDE[tsql](../includes/tsql-md.md)] istruzioni e `sqlcmd` comandi dal file specificato da **< *`filename`* >** nella cache delle istruzioni.  
  
 Se il file contiene istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] non seguite da **GO**, è necessario immettere **GO** nella riga successiva a **:r**.  
  
> [!NOTE]  
>  **\<** _nome file_ **>** viene letto in relazione alla directory di avvio in cui `sqlcmd` è stata eseguita.  
  
 Il file verrà letto ed eseguito dopo che è stato rilevato un carattere di terminazione di batch. È possibile eseguire più comandi **:r** . Il file può contenere qualsiasi comando `sqlcmd`, incluso il carattere di terminazione di batch **GO**.  
  
> [!NOTE]  
>  Il conteggio delle righe visualizzato in modalità interattiva viene incrementato di 1 per ogni comando **:r** rilevato. Il comando **:r** verrà visualizzato nell'output del comando LIST.  
  
 **:Serverlist**  
 Elenca i server configurati localmente e i nomi dei server che trasmettono in rete tramite broadcast.  
  
 **:Connect** _server_name_[**\\**_instance_name_] [-l *timeout*] [-U *user_name* [-P *password*]]  
 Stabilisce la connessione a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. e inoltre chiude la connessione corrente.  
  
 Opzioni di timeout:  
  
|||  
|-|-|  
|0|attesa infinita|  
|n>0|attesa di n secondi|  
  
 La variabile di scripting SQLCMDSERVER si adatterà alla connessione attiva corrente.  
  
 Se *timeout* viene omesso, il valore predefinito corrisponde al valore della variabile SQLCMDLOGINTIMEOUT.  
  
 Se si specifica solo *user_name* , come opzione o come variabile di ambiente, all'utente verrà chiesto di immettere una password. Ciò non si verifica se è stata impostata la variabile di ambiente SQLCMDUSER o SQLCMDPASSWORD. Se non si specificano opzioni o variabili di ambiente, per la connessione verrà utilizzata la modalità di autenticazione di Windows. Per connettersi all'istanza `instance1`di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] `myserver`utilizzando la sicurezza integrata, ad esempio, specificare:  
  
 `:connect myserver\instance1`  
  
 Per connettersi all'istanza predefinita di `myserver` utilizzando le variabili di scripting, specificare:  
  
 `:setvar myusername test`  
  
 `:setvar myservername myserver`  
  
 `:connect $(myservername) $(myusername)`  
  
 [**:**] **!!**\< *command*>  
 Esegue i comandi del sistema operativo. Per eseguire un comando del sistema operativo, digitare due punti esclamativi all'inizio della riga (**!!**) seguiti dal comando del sistema operativo. Ad esempio:  
  
 `:!! Dir`  
  
> [!NOTE]  
>  Il comando viene eseguito nel computer in cui è in esecuzione `sqlcmd`.  
  
 **:XML** [**ON** | **OFF**]  
 Per ulteriori informazioni, vedere "Formato di output XML" di seguito in questo argomento.  
  
 **:Help**  
 Elenca i comandi `sqlcmd` con una breve descrizione di ogni comando.  
  
### <a name="sqlcmd-file-names"></a>Nomi di file per sqlcmd  
 `sqlcmd` i file di input possono essere specificati con il **-i** opzione o il **: r** comando. I file di output possono essere specificati con l'opzione **-o** oppure con i comandi **:Error**, **:Out** e **:Perftrace** . Di seguito vengono illustrate alcune linee guida per l'utilizzo di tali file:  
  
-   **: Error**, **: Out** e **: Perftrace** utilizzino separato **< *`filename`* >**. Se lo stesso **< *`filename`* >** viene usata, gli input dai comandi potrebbero combinati.  
  
-   Se un file di input che risiede in un server remoto viene chiamato da `sqlcmd` in un computer locale e contiene un percorso di file con unità come :out c:\OutputFile.txt, il file di output verrà creato nel computer locale e non nel server remoto.  
  
-   Percorsi di file validi includono: C:\\**<*`filename`*>**, \\\\<Server\>\\<Share$>\\**<*`filename`*>** and "C:\Some Folder\\**<*`file name`*>**". Se il percorso contiene uno spazio, utilizzare le virgolette.  
  
-   Ogni nuova sessione di `sqlcmd` sovrascriverà i file esistenti con gli stessi nomi.  
  
### <a name="informational-messages"></a>Messaggi informativi  
 `sqlcmd` stampa qualsiasi messaggio informativo inviato dal server. Nell'esempio seguente al termine dell'esecuzione delle istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] viene stampato un messaggio informativo.  
  
 Al prompt dei comandi digitare quanto segue:  
  
 `sqlcmd`  
  
 `At the sqlcmd prompt type:`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 Quando si preme INVIO, viene stampato il messaggio informativo seguente: "Contesto di database è stato sostituito con 'adventureworks2012'".  
  
### <a name="output-format-from-transact-sql-queries"></a>Formato di output delle query Transact-SQL  
 `sqlcmd` stampa innanzitutto un'intestazione di colonna contenente i nomi delle colonne specificati nell'elenco di selezione. I nomi di colonna sono delimitati tramite il carattere specificato da SQLCMDCOLSEP. Per impostazione predefinita, viene utilizzato uno spazio. Se la lunghezza del nome di colonna è minore della larghezza della colonna, nell'output vengono inseriti caratteri di riempimento fino alla colonna successiva.  
  
 La riga sarà seguita da una riga di separazione costituita da una serie di trattini. Di seguito è riportato un esempio di output.  
  
 Avviare `sqlcmd`. Al prompt dei comandi `sqlcmd` digitare quanto segue:  
  
 `USE AdventureWorks2012;`  
  
 `SELECT TOP (2) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 Quando si preme INVIO, viene restituito il set di risultati seguente.  
  
 `BusinessEntityID FirstName    LastName`  
  
 `---------------- ------------ ----------`  
  
 `285              Syed         Abbas`  
  
 `293              Catherine    Abel`  
  
 `(2 row(s) affected)`  
  
 Nonostante la larghezza della colonna `BusinessEntityID` sia soltanto di 4 caratteri, la colonna viene espansa in modo da contenere un nome di colonna più lungo. Per impostazione predefinita, l'output viene troncato a 80 caratteri. Questo valore può essere modificato usando l'opzione **-w** oppure impostando la variabile di scripting SQLCMDCOLWIDTH.  
  
### <a name="xml-output-format"></a>Formato di output XML  
 L'output XML risultante dalla clausola FOR XML viene restituito non formattato in un flusso continuo.  
  
 Quando è previsto output XML, utilizzare il comando: `:XML ON`.  
  
> [!NOTE]  
>  `sqlcmd` restituisce messaggi di errore nel formato standard. Si noti che anche l'output dei messaggi di errore viene generato nel flusso di testo XML in formato XML. Utilizzando `:XML ON`, `sqlcmd` non visualizza messaggi informativi.  
  
 Per disattivare la modalità XML, utilizzare il comando: `:XML OFF`.  
  
 Il comando GO non deve essere immesso prima dell'esecuzione del comando XML OFF, poiché il comando XML OFF reimposta `sqlcmd` sull'output orientato alle righe.  
  
 Non possono essere contemporaneamente presenti dati XML (di flusso) e dati del set di righe. Se il comando XML ON non è stato eseguito prima dell'esecuzione di un'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] che genera flussi XML, l'output non verrà visualizzato correttamente. Se il comando XML ON è stato eseguito, non è possibile eseguire istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] che generano normali set di righe come output.  
  
> [!NOTE]  
>  Il comando **:XML** non supporta l'istruzione SET STATISTICS XML.  
  
## <a name="sqlcmd-best-practices"></a>Procedure consigliate per sqlcmd  
 Utilizzare le procedure seguenti per ottimizzare i livelli di sicurezza ed efficienza.  
  
-   Utilizzare la sicurezza integrata.  
  
-   Utilizzare `-X` negli ambienti automatizzati.  
  
-   Proteggere i file di input e di output utilizzando autorizzazioni del file system NTFS appropriate.  
  
-   Per incrementare le prestazioni, eseguire il maggior numero di operazioni possibile in un'unica sessione di `sqlcmd`, anziché in una serie di sessioni.  
  
-   Per l'esecuzione di batch o query, impostare valori di timeout superiori rispetto al tempo che si prevede sarà necessario per eseguire il batch o la query.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio dell'utilità sqlcmd](../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [Esecuzione di file script Transact-SQL mediante sqlcmd](../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)   
 [Utilizzo dell'utilità sqlcmd](../relational-databases/scripting/sqlcmd-use-the-utility.md)   
 [Utilizzo di sqlcmd con variabili di scripting](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [Connessione al Motore di database tramite sqlcmd](../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)   
 [Modifica di script SQLCMD con l'editor di query](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)   
 [Gestire passaggi di processo](../ssms/agent/manage-job-steps.md)   
 [Creare un passaggio di processo CmdExec](../ssms/agent/create-a-cmdexec-job-step.md)  
  
  
