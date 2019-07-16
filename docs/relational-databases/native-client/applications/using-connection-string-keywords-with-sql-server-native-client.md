---
title: Utilizzo di Connection String Keywords with SQL Server Native Client | Documenti di Microsoft
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [SQL Server Native Client], connection string keywords
- SQLNCLI, connection string keywords
- connection strings [SQL Server Native Client]
- SQL Server Native Client, connection string keywords
ms.assetid: 16008eec-eddf-4d10-ae99-29db26ed6372
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7d5bd6584316ceb1da4462ab2459781b1cf1e32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069193"
---
# <a name="using-connection-string-keywords-with-sql-server-native-client"></a>Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In alcune API di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client vengono utilizzate stringhe di connessione per specificare gli attributi di connessione. Le stringhe di connessione sono elenchi di parole chiave con i relativi valori associati. Ogni parola chiave identifica un particolare attributo di connessione.  

> [!IMPORTANT]
> Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB (SQLNCLI) rimane deprecati e non è consigliabile usarlo per nuovi progetti di sviluppo. In alternativa, usare il nuovo [Driver Microsoft OLE DB per SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) che verrà aggiornato con le funzionalità server più recenti.    
> Per informazioni, vedere [Using Connection String Keywords con il Driver OLE DB per SQL Server](../../../connect/oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta l'ambiguità nelle stringhe di connessione per mantenere la compatibilità con le versioni precedenti. È ad esempio possibile specificare alcune parole chiave più volte e utilizzare parole chiave in conflitto con una risoluzione basata sulla posizione o sulla precedenza. Quando si modificano le applicazioni, è consigliabile utilizzare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per eliminare l'eventuale dipendenza dall'ambiguità delle stringhe di connessione.  
  
 Nelle sezioni seguenti vengono descritte le parole chiave che è possibile specificare con il provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e gli oggetti ADO (ActiveX Data Objects) quando si utilizza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client come provider di dati.  
  
## <a name="odbc-driver-connection-string-keywords"></a>Parole chiave delle stringhe di connessione ODBC Driver  
 Le applicazioni ODBC utilizzano stringhe di connessione come parametri il [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) e [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) funzioni.  
  
 Le stringhe di connessione utilizzate da ODBC presentano la sintassi seguente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 È consigliabile racchiudere i valori di attributo tra parentesi graffe per evitare i problemi determinati dalla presenza di caratteri non alfanumerici nei valori di attributo. Poiché si suppone che la prima parentesi graffa chiusa indichi la fine del valore, l'uso di tali parentesi nei valori non è consentito.  
  
 Nella tabella seguente vengono descritte le parole chiave che possono essere utilizzate con una stringa di connessione ODBC.  
  
|Parola chiave|Descrizione|  
|-------------|-----------------|  
|**Addr**|Sinonimo di "Address".|  
|**Indirizzo**|Indirizzo di rete del server che esegue un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **Address** è in genere il nome di rete del server, ma può corrispondere ad altri nomi, ad esempio una pipe, un indirizzo IP o un indirizzo socket e una porta TCP/IP.<br /><br /> Se si specifica un indirizzo IP, assicurarsi che i protocolli TCP/IP o Named Pipes siano abilitati in Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Il valore di **indirizzi** ha la precedenza sul valore passato a **Server** nelle stringhe di connessione ODBC quando si usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Tenere anche presente che, se si specifica `Address=;`, verrà stabilita una connessione al server specificato nella parola chiave **Server**, mentre, se si specifica `Address= ;, Address=.;`, `Address=localhost;` e `Address=(local);`, verrà stabilita una connessione al server locale.<br /><br /> La sintassi completa per la parola chiave **Address** è la seguente:<br /><br /> [_protocol_ **:** ]*indirizzo*[ **,** _porta &#124;\pipe\pipename_]<br /><br /> *protocol* può essere **tcp** (TCP/IP), **lpc** (memoria condivisa) o **np** (named pipe). Per altre informazioni sui protocolli, vedere [Configure Client Protocols](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Se nessuno di essi *protocol* né la **Network** viene specificata una parola chiave, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client viene utilizzato l'ordine dei protocolli specificato in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *port* indica la porta a cui connettersi nel server specificato. Per impostazione predefinita, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene utilizzata la porta 1433.|  
|**AnsiNPW**|Se l'opzione è impostata su "yes", nel driver vengono utilizzati i comportamenti definiti da ANSI per la gestione dei confronti NULL, del riempimento dei dati di tipo carattere, degli avvisi e della concatenazione NULL. Se impostata su "no", i comportamenti definiti da ANSI non vengono esposti. Per altre informazioni sui comportamenti ANSI NPW, vedere [effetti delle opzioni ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|**APP**|Nome dell'applicazione che chiama [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) (facoltativo). Se specificato, questo valore viene archiviato nel **program_name** colonna **program_name** e viene restituito da [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) e il [APP_NAME](../../../t-sql/functions/app-name-transact-sql.md)le funzioni.|  
|**ApplicationIntent**|Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. I valori possibili sono **ReadOnly** e **ReadWrite**. Il valore predefinito è **ReadWrite**.  Ad esempio:<br /><br /> `ApplicationIntent=ReadOnly`<br /><br /> Per altre informazioni sulle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per il supporto del Client nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [SQL Server Native Client il supporto per la disponibilità elevata, ripristino di emergenza](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|Nome del file primario di un database collegabile. Includere il percorso completo e utilizzare la sequenza di escape dei caratteri \ se si utilizza una variabile di tipo stringa di caratteri C:<br /><br /> `AttachDBFileName=c:\\MyFolder\\MyDB.mdf`<br /><br /> Questo database viene collegato e diventa il database predefinito per la connessione. Usare **AttachDBFileName** è anche necessario specificare il nome del database in entrambi i [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) parametro del DATABASE o l'attributo di connessione SQL_COPT_CURRENT_CATALOG. Se il database è stato collegato in precedenza, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non lo ricollega e utilizza il database collegato come impostazione predefinita per la connessione.|  
|**AutoTranslate**|Se impostata su "yes", le stringhe di caratteri ANSI inviate tra il client e il server vengono convertite in Unicode per ridurre al minimo i problemi di corrispondenza dei caratteri estesi tra le tabelle codici sul client e sul server.<br /><br /> Dati SQL_C_CHAR del client inviati a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**, **varchar**, oppure **testo** colonna, parametro o variabile è convertita da caratteri in Unicode utilizzando il client Tabella codici ANSI (ACP), quindi vengono convertiti da Unicode a caratteri utilizzando l'ACP del server.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **Char**, **varchar**, o **testo** dati inviati a una variabile SQL_C_CHAR del client sono convertiti da caratteri in Unicode utilizzando l'ACP del server, quindi vengono convertiti da Unicode a caratteri utilizzando il client ACP.<br /><br /> Queste conversioni vengono eseguite sul client dal driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e richiedono che sul client sia disponibile la stessa tabella codici ANSI (ACP) utilizzata sul server.<br /><br /> Queste impostazioni non influiscono sulle conversioni eseguite per i trasferimenti seguenti:<br /><br /> \* Dati client SQL_C_WCHAR Unicode inviati a **char**, **varchar**, o **testo** nel server.<br /><br /> &#42;**char**, **varchar**, o **testo** data server inviati a una variabile SQL_C_WCHAR Unicode sul client.<br /><br /> \* I dati client SQL_C_CHAR ANSI inviati a Unicode **nchar**, **nvarchar**, o **ntext** nel server.<br /><br /> \* Unicode **nchar**, **nvarchar**, o **ntext** data server inviati a una variabile SQL_C_CHAR ANSI sul client.<br /><br /> Se impostata su "no", la conversione dei caratteri non viene eseguita.<br /><br /> Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client non converte i dati SQL_C_CHAR carattere ANSI del client inviati a **char**, **varchar**, oppure **testo** variabili, parametri, o di colonne nel server. Non viene eseguita alcuna conversione **char**, **varchar**, o **testo** i dati inviati dal server alle variabili SQL_C_CHAR sul client.<br /><br /> Se il client e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzano ACP differenti, i caratteri estesi potrebbero essere interpretati in modo errato.|  
|**Database**|Nome del database [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] predefinito per la connessione. Se **Database** viene omesso, viene utilizzato il database predefinito definito per l'account di accesso. Il database predefinito dell'origine dati ODBC esegue l'override del database predefinito specificato per l'accesso. Il database deve essere un database esistente, a meno che **AttachDBFileName** viene anche specificato. Se **AttachDBFileName** viene specificato anche, punta al file primario viene collegato e dato il nome del database specificato da **Database**.|  
|**Driver**|Nome del driver restituito da [SQLDrivers](../../../relational-databases/native-client-odbc-api/sqldrivers.md). Il valore della parola chiave per il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è "{SQL Server Native Client 11.0}". Il **Server** parola chiave è obbligatoria se **Driver** specificato e **DriverCompletion** è impostato su SQL_DRIVER_NOPROMPT.<br /><br /> Per altre informazioni sui nomi dei driver, vedere [usando l'intestazione di SQL Server Native Client e i file di libreria](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md).|  
|**DSN**|Nome di un'origine dati di sistema o di un utente ODBC esistente. Questa parola chiave override dei valori che potrebbero essere specificati nel **Server**, **Network**, e **indirizzo** parole chiave.|  
|**Encrypt**|Specifica se i dati devono essere crittografati prima del relativo invio in rete. I valori possibili sono "yes" e "no". Il valore predefinito è "no".|  
|**Fallback**|Questa parola chiave è deprecata e la relativa impostazione viene ignorata dal driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**Failover_Partner**|Nome del server partner di failover da utilizzare se non è possibile stabilire una connessione al server primario.|  
|**FailoverPartnerSPN**|Nome SPN del partner di failover. Il valore predefinito è una stringa vuota. In presenza di una stringa vuota, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilizza il nome SPN predefinito generato dal driver.|  
|**FileDSN**|Nome di un'origine dati dei file ODBC esistente.|  
|**Lingua**|Nome della lingua di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (facoltativo). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può memorizzare messaggi per più lingue **sysmessages**. Se la connessione a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con più lingue, **Language** specifica il set di messaggi utilizzato per la connessione.|  
|**MARS_Connection**|Abilita o disabilita MARS (Multiple Active Result Sets) nella connessione. I valori riconosciuti sono "yes" e "no". Il valore predefinito è "no".|  
|**MultiSubnetFailover**|Specificare sempre **multiSubnetFailover = Yes** durante la connessione al listener del gruppo di disponibilità di un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gruppo di disponibilità o un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] istanza Cluster di Failover. **multiSubnetFailover = Yes** consente di configurare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client per fornire un rilevamento più veloce di connessione al server attualmente attivo. I valori possibili sono **Sì** e **No**. Il valore predefinito è **No**. Ad esempio:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> Per altre informazioni sulle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per il supporto del Client nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [SQL Server Native Client il supporto per la disponibilità elevata, ripristino di emergenza](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**Net**|Sinonimo di "Network".|  
|**Network**|I valori validi sono **dbnmpntw** (named pipe) e **dbmssocn** (TCP/IP).<br /><br /> È possibile specificare sia un valore per il **rete** parola chiave e un protocollo di prefisso nel **Server** (parola chiave).|  
|**PWD**|Password per l'account di accesso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] specificato nel parametro UID. **PWD** non è necessario specificare se l'account di accesso dispone di una password NULL o quando si usa l'autenticazione di Windows (`Trusted_Connection = yes`).|  
|**QueryLog_On**|Se impostata su "yes", la registrazione dei dati di query con esecuzione prolungata viene abilitata per la connessione. Se impostata su "no", i dati di query con esecuzione prolungata non vengono registrati.|  
|**QueryLogFile**|Nome e percorso completo di un file da utilizzare per registrare dati nelle query con esecuzione prolungata.|  
|**QueryLogTime**|Stringa di cifre che specifica la soglia (in millisecondi) per la registrazione delle query con esecuzione prolungata. Tutte le query che non ottengono una risposta nell'intervallo di tempo specificato vengono scritte nel file di log delle query con esecuzione prolungata.|  
|**QuotedId**|Se impostata su "yes", QUOTED_IDENTIFIERS viene impostata su ON per la connessione e in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono utilizzate le regole ISO relative all'uso delle virgolette nelle istruzioni SQL. Se impostata su no, QUOTED_IDENTIFIERS viene impostata su OFF per la connessione. In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono quindi seguite le regole [!INCLUDE[tsql](../../../includes/tsql-md.md)] legacy relative all'utilizzo delle virgolette nelle istruzioni SQL. Per altre informazioni, vedere [effetti delle opzioni ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|**Regional**|Se impostata su "yes", nel driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client vengono utilizzate le impostazioni client per la conversione dei dati di valuta, data e ora in dati di tipo carattere. La conversione viene eseguita in una sola direzione. Il driver non riconosce i formati standard non ODBC per le stringhe di data o i valori di valuta all'interno, ad esempio, di un parametro utilizzato in un'istruzione INSERT o UPDATE. Se impostata su "no", nel driver vengono utilizzate le stringhe standard ODBC per rappresentare i dati di valuta, data e ora convertiti in dati di tipo carattere.|  
|**SaveFile**|Nome di un file di origine dati ODBC nel quale vengono salvati gli attributi della connessione corrente se la connessione riesce.|  
|**Server**|Nome di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il valore deve corrispondere al nome di un server in rete, a un indirizzo IP o al nome di un alias di Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Il **indirizzi** esegue l'override (parola chiave) il **Server** (parola chiave).<br /><br /> È possibile connettersi all'istanza predefinita nel server locale specificando uno dei valori seguenti:<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** _nomeistanza_ **;**<br /><br /> Per altre informazioni sul supporto per LocalDB, vedere [SQL Server Native Client il supporto per LocalDB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md).<br /><br /> Per specificare un'istanza denominata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], aggiungere **\\** _NomeIstanza_.<br /><br /> Se non viene specificato un server, viene stabilita una connessione all'istanza predefinita nel computer locale.<br /><br /> Se si specifica un indirizzo IP, assicurarsi che i protocolli TCP/IP o Named Pipes siano abilitati in Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> La sintassi completa per la parola chiave **Server** è la seguente:<br /><br /> **Server=** [_protocollo_ **:** ]*Server*[ **,** _porta_]<br /><br /> *protocol* può essere **tcp** (TCP/IP), **lpc** (memoria condivisa) o **np** (named pipe).<br /><br /> Nell'esempio seguente si illustra come specificare una named pipe:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Questa riga specifica un protocollo Named Pipes, una named pipe nel computer locale (`\\.\pipe`), il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (`MSSQL$MYINST01`) e il nome predefinito della named pipe (`sql/query`).<br /><br /> Se non si specifica un *protocol* né la **Network** viene specificata una parola chiave, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client viene utilizzato l'ordine dei protocolli specificato in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *port* indica la porta a cui connettersi nel server specificato. Per impostazione predefinita, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene utilizzata la porta 1433.<br /><br /> Gli spazi vengono ignorati all'inizio del valore passato a **Server** nelle stringhe di connessione ODBC quando si usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**ServerSPN**|Nome SPN del server. Il valore predefinito è una stringa vuota. In presenza di una stringa vuota, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilizza il nome SPN predefinito generato dal driver.|  
|**StatsLog_On**|Se impostata su "yes", abilita l'acquisizione dei dati relativi alle prestazioni del driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Se impostata su "no", i dati relativi alle prestazioni del driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non sono disponibili nella connessione.|  
|**StatsLogFile**|Nome e percorso completo di un file utilizzato per registrare le statistiche sulle prestazioni del driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**Trusted_Connection**|Se impostata su "yes", indica al driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client di utilizzare la Modalità di autenticazione di Windows per la convalida dell'accesso. In caso contrario, indica al driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client di utilizzare un nome utente e una password di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la convalida dell'accesso e richiede la specifica delle parole chiave UID e PWD.|  
|**TrustServerCertificate**|Quando abbinata **Encrypt**, abilita la crittografia tramite un certificato server autofirmato.|  
|**UID**|Account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] valido. Quando si utilizza l'autenticazione di Windows non è necessario specificare l'UID.|  
|**UseProcForPrepare**|Questa parola chiave è deprecata e la relativa impostazione viene ignorata dal driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**WSID**|ID della workstation. In genere, si tratta del nome di rete del computer nel quale risiede l'applicazione (facoltativo). Se specificato, questo valore viene archiviato nel **program_name** colonna **hostname** e viene restituito da [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) e il [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md)(funzione).|  
  
> **NOTA:** Ai dati di tipo valuta, numerico, data e ora vengono applicate le impostazioni di conversione internazionali. L'impostazione di conversione è applicabile solo alla conversione di output ed è visibile solo quando i valori di valuta, data, ora o numerici vengono convertiti in stringhe di caratteri.  
  
 Nel driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client vengono utilizzate le impostazioni locali del Registro di sistema per l'utente corrente. Il driver non rispetta le impostazioni locali del thread corrente se l'applicazione le imposta dopo la connessione, ad esempio, la chiamata **SetThreadLocale**.  
  
 La modifica del comportamento internazionale di un'origine dati può generare un errore nell'applicazione. Un'applicazione che analizza le stringhe relative alla data e ne prevede la visualizzazione in base a quanto definito da ODBC, potrebbe essere influenzata negativamente dalla modifica di questo valore.  
  
## <a name="ole-db-provider-connection-string-keywords"></a>Parole chiave delle stringhe di connessione per il provider OLE DB  
 Quando si utilizzano le applicazioni OLE DB, è possibile inizializzare gli oggetti origine dati in due modi diversi:  
  
-   **IDBInitialize::Initialize**  
  
-   **IDataInitialize::GetDataSource**  
  
 Nel primo caso è possibile utilizzare una stringa del provider per inizializzare le proprietà di connessione impostando la proprietà DBPROP_INIT_PROVIDERSTRING nel set di proprietà DBPROPSET_DBINIT. Nel secondo caso è possibile passare una stringa di inizializzazione al metodo **IDataInitialize::GetDataSource** per inizializzare le proprietà di connessione. Entrambi i metodi inizializzano le stesse proprietà di connessione OLE DB, sebbene con set di parole chiave differenti. Il set di parole chiave usato con **IDataInitialize::GetDataSource** rappresenta almeno la descrizione delle proprietà contenute nel gruppo delle proprietà di inizializzazione.  
  
 Per qualsiasi impostazione di stringa del provider con una proprietà OLE DB corrispondente impostata su un valore predefinito o impostata in modo esplicito su un valore, tramite il valore della proprietà OLE DB verrà eseguito l'override dell'impostazione nella stringa del provider.  
  
 Per le proprietà booleane impostate nelle stringhe del provider mediante i valori DBPROP_INIT_PROVIDERSTRING vengono utilizzati i valori "yes" e "no". Per le proprietà booleane impostate nelle stringhe di inizializzazione con **IDataInitialize::GetDataSource** vengono usati i valori "true" e "false".  
  
 Le applicazioni che usano **IDataInitialize::GetDataSource** supportano anche le parole chiave usate da **IDBInitialize::Initialize**, ma solo per le proprietà che non hanno un valore predefinito. Se in un'applicazione viene usata sia la parola chiave **IDataInitialize::GetDataSource** che la parola chiave **IDBInitialize::Initialize** nella stringa di inizializzazione, viene usata l'impostazione della parola chiave **IDataInitialize::GetDataSource**. Nelle applicazioni è consigliabile non specificare le parole chiave **IDBInitialize::Initialize** nelle stringhe di connessione **IDataInitialize:GetDataSource**, perché questo comportamento potrebbe non essere supportato nelle versioni successive.  
  
> [!NOTE]  
>  Una stringa di connessione passata a **IDataInitialize::GetDataSource** viene convertita in proprietà e applicata tramite **IDBProperties::SetProperties**. Se i Servizi componenti hanno rilevato la descrizione della proprietà in **IDBProperties::GetPropertyInfo**, la proprietà verrà applicata come autonoma. In caso contrario, verrà applicata mediante la proprietà DBPROP_PROVIDERSTRING. Ad esempio, se si specifica una stringa di connessione **Zdroj dat Source=Server1; Server server=Server2**, **Zdroj dat** verrà impostato come proprietà, ma **Server** entra in una stringa del provider.  
  
 Se si indicano più istanze per la stessa proprietà specifica del provider, verrà utilizzato il primo valore della prima proprietà.  
  
 Le stringhe di connessione usate nelle applicazioni OLE DB che usano DBPROP_INIT_PROVIDERSTRING con **IDBInitialize::Initialize** presentano la sintassi seguente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 È consigliabile racchiudere i valori di attributo tra parentesi graffe per evitare i problemi determinati dalla presenza di caratteri non alfanumerici nei valori di attributo. Poiché si suppone che la prima parentesi graffa chiusa indichi la fine del valore, l'uso di tali parentesi nei valori non è consentito.  
  
 Uno spazio dopo il segno = in una parola chiave di una stringa di connessione verrà interpretato come valore letterale, anche se il valore è racchiuso tra virgolette.  
  
 Nella tabella seguente vengono descritte le parole chiave che possono essere utilizzate con DBPROP_INIT_PROVIDERSTRING.  
  
|Parola chiave|Proprietà di inizializzazione|Descrizione|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|Sinonimo di "Address".|  
|**Indirizzo**|SSPROP_INIT_NETWORKADDRESS|Indirizzo di rete di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Per altre informazioni sulla sintassi dell'indirizzo validi, vedere la descrizione del **indirizzo** parola chiave ODBC, più avanti in questo argomento.|  
|**APP**|SSPROP_INIT_APPNAME|Stringa che identifica l'applicazione.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. I valori possibili sono **ReadOnly** e **ReadWrite**.<br /><br /> Il valore predefinito è **ReadWrite**. Per altre informazioni sulle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per il supporto del Client nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [SQL Server Native Client il supporto per la disponibilità elevata, ripristino di emergenza](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|Nome del file primario, incluso il nome completo del percorso, di un database collegabile. Per usare **AttachDBFileName**, è necessario specificare anche il nome del database con la parola chiave Database della stringa del provider. Se il database è stato collegato in precedenza, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non lo ricollega e utilizza il database collegato come impostazione predefinita per la connessione.|  
|**Conversione automatica**|SSPROP_INIT_AUTOTRANSLATE|Sinonimo di "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la conversione dei caratteri OEM/ANSI. I valori riconosciuti sono "yes" e "no".|  
|**Database**|DBPROP_INIT_CATALOG|Nome del database.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Specifica la modalità di gestione dei tipi di dati da utilizzare. I valori riconosciuti sono "0" per i tipi di dati del provider e "80" per i tipi di dati di SQL Server 2000.|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|Specifica se i dati devono essere crittografati prima del relativo invio in rete. I valori possibili sono "yes" e "no". Il valore predefinito è "no".|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|Nome del server di failover utilizzato per il mirroring del database.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Nome SPN del partner di failover. Il valore predefinito è una stringa vuota. In presenza di una stringa vuota, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilizza il nome SPN predefinito generato dal provider.|  
|**Lingua**|SSPROPT_INIT_CURRENTLANGUAGE|Lingua di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|Abilita o disabilita MARS (Multiple Active Result Sets) nella connessione se il server è [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva. I valori possibili sono "yes" e "no". Il valore predefinito è "no".|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|Sinonimo di "Network".|  
|**Network**|SSPROP_INIT_NETWORKLIBRARY|Libreria di rete utilizzata per stabilire una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|Sinonimo di "Network".|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|Dimensioni del pacchetto di rete. Il valore predefinito è 4096.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Accetta le stringhe "yes" e "no" come valori. Se impostata su "no", l'oggetto origine dati non è in grado di rendere persistenti le informazioni di autenticazione riservate|  
|**PWD**|DBPROP_AUTH_PASSWORD|Password di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Server**|DBPROP_INIT_DATASOURCE|Nome di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Se non viene specificato un nome, viene stabilita una connessione all'istanza predefinita nel computer locale.<br /><br /> Per altre informazioni sulla sintassi dell'indirizzo validi, vedere la descrizione del **Server** parola chiave ODBC, in questo argomento.|  
|**ServerSPN**|SSPROP_INIT_SERVERSPN|Nome SPN del server. Il valore predefinito è una stringa vuota. In presenza di una stringa vuota, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilizza il nome SPN predefinito generato dal provider.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|Tempo di attesa in secondi per il completamento dell'inizializzazione dell'origine dati.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|Se impostata su "yes", indica al provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client di utilizzare la Modalità di autenticazione di Windows per la convalida dell'accesso. In caso contrario, indica al provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client di utilizzare un nome utente e una password di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la convalida dell'accesso e richiede la specifica delle parole chiave UID e PWD.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Accetta le stringhe "yes" e "no" come valori. Il valore predefinito è "no", il quale indica che il certificato server verrà convalidato.|  
|**UID**|DBPROP_AUTH_USERID|Nome dell'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|Questa parola chiave è deprecata e la relativa impostazione viene ignorata dal provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**WSID**|SSPROP_INIT_WSID|Identificatore della workstation.|  
  
 Le stringhe di connessione usate nelle applicazioni OLE DB che usano **IDataInitialize::GetDataSource** presentano la sintassi seguente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 L'utilizzo delle proprietà deve essere conforme alla sintassi consentita nel relativo ambito.  Per **WSID** vengono ad esempio usate le parentesi graffe ( **{}** ) come virgolette e per **Application Name** vengono usate le virgolette semplici ( **'** ) o doppie ( **"** ). Solo per le proprietà delle stringhe è possibile utilizzare le virgolette. Se si tenta di utilizzare le virgolette con una proprietà Integer o enumerata, verrà generato un errore che indica che la stringa di connessione non è conforme alla specifica OLE DB.  
  
 È consigliabile racchiudere i valori di attributo tra virgolette semplici o doppie per evitare i problemi determinati dalla presenza di caratteri non alfanumerici nei valori. Se raddoppiato, il carattere virgoletta può essere visualizzato anche per i valori.  
  
 Uno spazio dopo il segno = in una parola chiave di una stringa di connessione verrà interpretato come valore letterale, anche se il valore è racchiuso tra virgolette.  
  
 Se una stringa di connessione include più di una delle proprietà elencate nella tabella seguente, verrà utilizzato il valore dell'ultima proprietà.  
  
 Nella tabella seguente vengono descritte le parole chiave che possono essere usate con **IDataInitialize::GetDataSource**:  
  
|Parola chiave|Proprietà di inizializzazione|Descrizione|  
|-------------|-----------------------------|-----------------|  
|**Application Name**|SSPROP_INIT_APPNAME|Stringa che identifica l'applicazione.|  
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. I valori possibili sono **ReadOnly** e **ReadWrite**.<br /><br /> Il valore predefinito è **ReadWrite**. Per altre informazioni sulle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per il supporto del Client nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [SQL Server Native Client il supporto per la disponibilità elevata, ripristino di emergenza](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**Conversione automatica**|SSPROP_INIT_AUTOTRANSLATE|Sinonimo di "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la conversione dei caratteri OEM/ANSI. I valori riconosciuti sono "true" e "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Tempo di attesa in secondi per il completamento dell'inizializzazione dell'origine dati.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|Nome della lingua di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Data Source**|DBPROP_INIT_DATASOURCE|Nome di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Se non viene specificato un nome, viene stabilita una connessione all'istanza predefinita nel computer locale.<br /><br /> Per altre informazioni sulla sintassi dell'indirizzo validi, vedere la descrizione del **Server** parola chiave ODBC, più avanti in questo argomento.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Specifica la modalità di gestione dei tipi di dati da utilizzare. I valori riconosciuti sono "0" per i tipi di dati del provider e "80" per i tipi di dati di [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)].|  
|**Partner di failover**|SSPROP_INIT_FAILOVERPARTNER|Nome del server di failover utilizzato per il mirroring del database.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Nome SPN del partner di failover. Il valore predefinito è una stringa vuota. In presenza di una stringa vuota, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilizza il nome SPN predefinito generato dal provider.|  
|**Catalogo iniziale**|DBPROP_INIT_CATALOG|Nome del database.|  
|**Nome File iniziale**|SSPROP_INIT_FILENAME|Nome del file primario, incluso il nome completo del percorso, di un database collegabile. Per usare **AttachDBFileName**, è necessario specificare anche il nome del database con la parola chiave DATABASE della stringa del provider. Se il database è stato collegato in precedenza, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non lo ricollega e utilizza il database collegato come impostazione predefinita per la connessione.|  
|**Sicurezza integrata**|DBPROP_AUTH_INTEGRATED|Accetta il valore "SSPI" per l'autenticazione di Windows.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|Abilita o disabilita MARS (Multiple Active Result Sets) nella connessione. I valori riconosciuti sono "true" e "false". Il valore predefinito è "false".|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|Indirizzo di rete di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Per altre informazioni sulla sintassi dell'indirizzo validi, vedere la descrizione del **indirizzo** parola chiave ODBC, più avanti in questo argomento.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|Libreria di rete utilizzata per stabilire una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Dimensioni del pacchetto di rete. Il valore predefinito è 4096.|  
|**Password**|DBPROP_AUTH_PASSWORD|Password di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Accetta le stringhe "true" e "false" come valori. Se il valore è impostato su "false", l'oggetto origine dati non è in grado di rendere persistenti le informazioni di autenticazione riservate|  
|**Provider**||Per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, deve essere "SQLNCLI11".|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|Nome SPN del server. Il valore predefinito è una stringa vuota. In presenza di una stringa vuota, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilizza il nome SPN predefinito generato dal provider.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Accetta le stringhe "true" e "false" come valori. Il valore predefinito è "false", il quale indica che il certificato server verrà convalidato.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Specifica se i dati devono essere crittografati prima del relativo invio in rete. I valori possibili sono "true" e "false". Il valore predefinito è "false".|  
|**ID utente**|DBPROP_AUTH_USERID|Nome dell'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Workstation ID**|SSPROP_INIT_WSID|Identificatore della workstation.|  
  
 **Nota** Nella stringa di connessione la proprietà "Vecchia password" imposta SSPROP_AUTH_OLD_PASSWORD, ovvero la password corrente (probabilmente scaduta) che non è disponibile tramite una proprietà della stringa del provider.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>Parole chiave delle stringhe di connessione per gli oggetti ADO (ActiveX Data Objects)  
 Le applicazioni ADO impostano la proprietà **ConnectionString** degli oggetti **ADODBConnection** o forniscono una stringa di connessione come parametro al metodo **Open** degli oggetti **ADODBConnection**.  
  
 Le applicazioni ADO supportano anche le parole chiave usate dal metodo **IDBInitialize::Initialize** OLE DB, ma solo per le proprietà che non hanno un valore predefinito. Se in un'applicazione vengono usate sia le parole chiave ADO che le parole chiave **IDBInitialize::Initialize** nella stringa di inizializzazione, verrà usata l'impostazione della parola chiave ADO. Nelle applicazioni è consigliabile utilizzare solo le parole chiave delle stringhe di connessione ADO.  
  
 Le stringhe di connessione utilizzate da ADO presentano la sintassi seguente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 È consigliabile racchiudere i valori di attributo tra virgolette doppie per evitare i problemi determinati dalla presenza di caratteri non alfanumerici nei valori. I valori attributo non possono contenere virgolette doppie.  
  
 Nella tabella seguente vengono descritte le parole chiave che possono essere utilizzate con una stringa di connessione ADO:  
  
|Parola chiave|Proprietà di inizializzazione|Descrizione|  
|-------------|-----------------------------|-----------------|  
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. I valori possibili sono **ReadOnly** e **ReadWrite**.<br /><br /> Il valore predefinito è **ReadWrite**. Per altre informazioni sulle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per il supporto del Client nativo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [SQL Server Native Client il supporto per la disponibilità elevata, ripristino di emergenza](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**Application Name**|SSPROP_INIT_APPNAME|Stringa che identifica l'applicazione.|  
|**Conversione automatica**|SSPROP_INIT_AUTOTRANSLATE|Sinonimo di "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la conversione dei caratteri OEM/ANSI. I valori riconosciuti sono "true" e "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Tempo di attesa in secondi per il completamento dell'inizializzazione dell'origine dati.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|Nome della lingua di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Data Source**|DBPROP_INIT_DATASOURCE|Nome di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Se non viene specificato un nome, viene stabilita una connessione all'istanza predefinita nel computer locale.<br /><br /> Per altre informazioni sulla sintassi dell'indirizzo validi, vedere la descrizione del **Server** parola chiave ODBC, in questo argomento.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Specifica la modalità di gestione dei tipi di dati che verrà utilizzata. I valori riconosciuti sono "0" per i tipi di dati del provider e "80" per i tipi di dati di SQL Server 2000.|  
|**Partner di failover**|SSPROP_INIT_FAILOVERPARTNER|Nome del server di failover utilizzato per il mirroring del database.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Nome SPN del partner di failover. Il valore predefinito è una stringa vuota. In presenza di una stringa vuota, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilizza il nome SPN predefinito generato dal provider.|  
|**Catalogo iniziale**|DBPROP_INIT_CATALOG|Nome del database.|  
|**Nome File iniziale**|SSPROP_INIT_FILENAME|Nome del file primario, incluso il nome completo del percorso, di un database collegabile. Per usare **AttachDBFileName**, è necessario specificare anche il nome del database con la parola chiave DATABASE della stringa del provider. Se il database è stato collegato in precedenza, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non lo ricollega e utilizza il database collegato come impostazione predefinita per la connessione.|  
|**Sicurezza integrata**|DBPROP_AUTH_INTEGRATED|Accetta il valore "SSPI" per l'autenticazione di Windows.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|Abilita o disabilita MARS (Multiple Active Result Sets) nella connessione se il server è [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva. I valori riconosciuti sono "true" e "false". Il valore predefinito è "false".|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|Indirizzo di rete di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Per altre informazioni sulla sintassi dell'indirizzo validi, vedere la descrizione del **indirizzo** parola chiave ODBC, in questo argomento.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|Libreria di rete utilizzata per stabilire una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Dimensioni del pacchetto di rete. Il valore predefinito è 4096.|  
|**Password**|DBPROP_AUTH_PASSWORD|Password di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Accetta le stringhe "true" e "false" come valori. Se il valore è impostato su "false", l'oggetto origine dati non è in grado di rendere persistenti le informazioni di autenticazione riservate.|  
|**Provider**||Per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, deve essere "SQLNCLI11".|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|Nome SPN del server. Il valore predefinito è una stringa vuota. In presenza di una stringa vuota, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilizza il nome SPN predefinito generato dal provider.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Accetta le stringhe "true" e "false" come valori. Il valore predefinito è "false", il quale indica che il certificato server verrà convalidato.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Specifica se i dati devono essere crittografati prima del relativo invio in rete. I valori possibili sono "true" e "false". Il valore predefinito è "false".|  
|**ID utente**|DBPROP_AUTH_USERID|Nome dell'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Workstation ID**|SSPROP_INIT_WSID|Identificatore della workstation.|  
  
 **Nota** Nella stringa di connessione la proprietà "Vecchia password" imposta SSPROP_AUTH_OLD_PASSWORD, ovvero la password corrente (probabilmente scaduta) che non è disponibile tramite una proprietà della stringa del provider.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
