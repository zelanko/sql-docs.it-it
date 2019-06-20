---
title: Uso delle parole chiave delle stringhe di connessione con driver OLE DB per SQL Server | Microsoft Docs
description: Uso delle parole chiave delle stringhe di connessione con driver OLE DB per SQL Server
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], connection string keywords
- MSOLEDBSQL, connection string keywords
- connection strings [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, connection string keywords
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 91e498a1db30df380d7f2009f0fe34a9b4541467
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778024"
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>Uso delle parole chiave delle stringhe di connessione con driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Alcuni Driver OLE DB per API SQL Server utilizzare stringhe di connessione per specificare gli attributi di connessione. Le stringhe di connessione sono elenchi di parole chiave con i relativi valori associati. Ogni parola chiave identifica un particolare attributo di connessione.  
  
> [!NOTE]
> Il driver OLE DB per SQL Server supporta l'ambiguità nelle stringhe di connessione per mantenere la compatibilità con le versioni precedenti. È ad esempio possibile specificare alcune parole chiave più volte e usare parole chiave in conflitto con una risoluzione basata sulla posizione o sulla precedenza. Le versioni future del Driver OLE DB per SQL Server potrebbero non consentire l'ambiguità nelle stringhe di connessione. Quando si modificano le applicazioni, è consigliabile usare il driver OLE DB per SQL Server per eliminare l'eventuale dipendenza dall'ambiguità delle stringhe di connessione.  
  
 Le sezioni seguenti descrivono le parole chiave che sono utilizzabili con il Driver OLE DB per SQL Server e gli oggetti ADO (ActiveX Data) quando si usa il Driver OLE DB per SQL Server come provider di dati.  

  
## <a name="ole-db-driver-connection-string-keywords"></a>Parole chiave delle stringhe di connessione per il driver OLE DB  
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
|**Indirizzo**|SSPROP_INIT_NETWORKADDRESS|Indirizzo di rete del server che esegue un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **Address** è in genere il nome di rete del server, ma può corrispondere ad altri nomi, ad esempio una pipe, un indirizzo IP o un indirizzo socket e una porta TCP/IP.<br /><br /> Se si specifica un indirizzo IP, assicurarsi che i protocolli TCP/IP o Named Pipes siano abilitati in Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Il valore di **indirizzi** ha la precedenza sul valore passato a **Server** nelle stringhe di connessione quando si usa il Driver OLE DB per SQL Server. Tenere anche presente che, se si specifica `Address=;`, verrà stabilita una connessione al server specificato nella parola chiave **Server**, mentre, se si specifica `Address= ;, Address=.;`, `Address=localhost;` e `Address=(local);`, verrà stabilita una connessione al server locale.<br /><br /> La sintassi completa per la parola chiave **Address** è la seguente:<br /><br /> [_protocol_ **:** ]_indirizzo_[ **,** _porta &#124;\pipe\pipename_]<br /><br /> _protocol_ può essere **tcp** (TCP/IP), **lpc** (memoria condivisa) o **np** (named pipe). Per altre informazioni sui protocolli, vedere [Configure Client Protocols](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Se nessuno di essi _protocol_ né la **Network** (parola chiave) viene specificato, il Driver OLE DB per SQL Server userà l'ordine dei protocolli specificato in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *port* indica la porta a cui connettersi nel server specificato. Per impostazione predefinita, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene utilizzata la porta 1433.|   
|**APP**|SSPROP_INIT_APPNAME|Stringa che identifica l'applicazione.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. I valori possibili sono **ReadOnly** e **ReadWrite**.<br /><br /> Il valore predefinito è **ReadWrite**. Per altre informazioni sui Driver OLE DB per il supporto di SQL Server per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [Driver OLE DB per SQL Server il supporto per la disponibilità elevata, ripristino di emergenza](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|Nome del file primario, incluso il nome completo del percorso, di un database collegabile. Per usare **AttachDBFileName**, è necessario specificare anche il nome del database con la parola chiave Database della stringa del provider. Se il database è stato collegato in precedenza, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non lo ricollega e utilizza il database collegato come impostazione predefinita per la connessione.|  
|**L'autenticazione**<a href="#table1_1"><sup id="table1_authmode">**1**</sup></a>|SSPROP_AUTH_MODE|Specifica l'autenticazione di Active Directory o SQL usata. I valori validi sono:<br/><ul><li>`(not set)`: Modalità di autenticazione determinata da altre parole chiave.</li><li>`ActiveDirectoryPassword:` Autenticazione di Active Directory usando l'ID di accesso e la password.</li><li>`ActiveDirectoryIntegrated:` Autenticazione integrata di Active Directory usando le credenziali dell'account di Windows dell'utente connesso.</li><br/>**Nota:** ha **consigliati** che le applicazioni usando `Integrated Security` (o `Trusted_Connection`) le proprietà corrispondenti o le parole chiave di autenticazione impostare il valore della `Authentication` (parola chiave) (o dai relativi proprietà corrispondente) a `ActiveDirectoryIntegrated` per abilitare il comportamento di convalida crittografia e il certificato nuovo.<br/><br/><li>`SqlPassword:` Autenticazione usando l'ID di accesso e la password.</li><br/>**Nota:** ha **consigliati** che le applicazioni usando `SQL Server` autenticazione imposta il valore della `Authentication` parola chiave o la proprietà corrispondente per `SqlPassword` per abilitare la nuova crittografia e comportamento di convalida di certificati.</ul>|
|**Conversione automatica**|SSPROP_INIT_AUTOTRANSLATE|Sinonimo di "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la conversione dei caratteri OEM/ANSI. I valori riconosciuti sono "yes" e "no".|  
|**Database**|DBPROP_INIT_CATALOG|Nome del database.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Specifica la modalità di gestione dei tipi di dati da utilizzare. I valori riconosciuti sono "0" per i tipi di dati del provider e "80" per i tipi di dati di SQL Server 2000.|  
|**Encrypt**<a href="#table1_1"><sup>**1**</sup></a>|SSPROP_INIT_ENCRYPT|Specifica se i dati devono essere crittografati prima del relativo invio in rete. I valori possibili sono "yes" e "no". Il valore predefinito è "no".|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|Nome del server di failover utilizzato per il mirroring del database.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Nome SPN del partner di failover. Il valore predefinito è una stringa vuota. Una stringa vuota fa sì che il Driver OLE DB per SQL Server per utilizzare il valore predefinito generato dal provider SPN.|  
|**Lingua**|SSPROPT_INIT_CURRENTLANGUAGE|Lingua di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|Abilita o disabilita MARS (Multiple Active Result Sets) nella connessione se il server è [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva. I valori possibili sono "yes" e "no". Il valore predefinito è "no".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Specificare sempre **MultiSubnetFailover=Yes** in caso di connessione al listener del gruppo di disponibilità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o a un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Con **MultiSubnetFailover=Yes** è possibile configurare il driver OLE DB per SQL Server per fornire un rilevamento e una connessione più veloci al server attualmente attivo. I valori possibili sono **Sì** e **No**. Il valore predefinito è **No**. Esempio:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> Per altre informazioni sui Driver OLE DB per il supporto di SQL Server per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [Driver OLE DB per SQL Server il supporto per la disponibilità elevata, ripristino di emergenza](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|Sinonimo di "Network".|  
|**Network**|SSPROP_INIT_NETWORKLIBRARY|Libreria di rete utilizzata per stabilire una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|Sinonimo di "Network".|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|Dimensioni del pacchetto di rete. Il valore predefinito è 4096.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Accetta le stringhe "yes" e "no" come valori. Se impostata su "no", l'oggetto origine dati non è in grado di rendere persistenti le informazioni di autenticazione riservate|  
|**PWD**|DBPROP_AUTH_PASSWORD|Password di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Server**|DBPROP_INIT_DATASOURCE|Nome di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il valore deve corrispondere al nome di un server in rete, a un indirizzo IP o al nome di un alias di Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Se non viene specificato un nome, viene stabilita una connessione all'istanza predefinita nel computer locale.<br /><br /> Il **indirizzi** esegue l'override (parola chiave) il **Server** (parola chiave).<br /><br /> È possibile connettersi all'istanza predefinita nel server locale specificando uno dei valori seguenti:<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Local;**<br /><br /> **Local;**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** *nomeistanza* **;**<br /><br /> Per altre informazioni sul supporto per LocalDB, vedere [Driver OLE DB per SQL Server il supporto per LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md).<br /><br /> Per specificare un'istanza denominata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], aggiungere **\\** _NomeIstanza_.<br /><br /> Se non viene specificato un server, viene stabilita una connessione all'istanza predefinita nel computer locale.<br /><br /> Se si specifica un indirizzo IP, assicurarsi che i protocolli TCP/IP o Named Pipes siano abilitati in Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> La sintassi completa per la parola chiave **Server** è la seguente:<br /><br /> **Server=** [_protocollo_ **:** ]*Server*[ **,** _porta_]<br /><br /> _protocol_ può essere **tcp** (TCP/IP), **lpc** (memoria condivisa) o **np** (named pipe).<br /><br /> Nell'esempio seguente si illustra come specificare una named pipe:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Questa riga specifica un protocollo Named Pipes, una named pipe nel computer locale (`\\.\pipe`), il nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (`MSSQL$MYINST01`) e il nome predefinito della named pipe (`sql/query`).<br /><br /> Se non si specifica un *protocol* né la **Network** (parola chiave) viene specificato, il Driver OLE DB per SQL Server userà l'ordine dei protocolli specificato in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *port* indica la porta a cui connettersi nel server specificato. Per impostazione predefinita, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene utilizzata la porta 1433.<br /><br /> Gli spazi vengono ignorati all'inizio del valore passato a **Server** nelle stringhe di connessione quando si usa il Driver OLE DB per SQL Server.|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|Nome SPN del server. Il valore predefinito è una stringa vuota. Una stringa vuota fa sì che il Driver OLE DB per SQL Server per utilizzare il valore predefinito generato dal provider SPN.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|Tempo di attesa in secondi per il completamento dell'inizializzazione dell'origine dati.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|Quando "Sì", indica al Driver OLE DB per SQL Server per utilizzare la modalità di autenticazione di Windows per la convalida dell'accesso. In caso contrario, indica al driver OLE DB per SQL Server di usare un nome utente e una password di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la convalida dell'accesso e richiede la specifica delle parole chiave UID e PWD.|  
|**TrustServerCertificate**<a href="#table1_1"><sup>**1**</sup></a>|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Accetta le stringhe "yes" e "no" come valori. Il valore predefinito è "no", il quale indica che il certificato server verrà convalidato.|  
|**UID**|DBPROP_AUTH_USERID|Nome dell'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**UseFMTONLY**|SSPROP_INIT_USEFMTONLY|Controlla la modalità di recupero dei metadati durante la connessione a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e versioni successive. I valori possibili sono "yes" e "no". Il valore predefinito è "no".<br /><br />Per impostazione predefinita, Usa il Driver OLE DB per SQL Server [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) e [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) stored procedure per recuperare i metadati. Queste stored procedure hanno alcune limitazioni (ad esempio, hanno esito negativo quando si opera su tabelle temporanee). L'impostazione **UseFMTONLY** su "Sì" indica al driver di usare [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md) per il recupero di metadati invece.|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|Questa parola chiave è deprecata e relativa impostazione viene ignorata dal Driver OLE DB per SQL Server.|  
|**WSID**|SSPROP_INIT_WSID|Identificatore della workstation.|  
  
<b id="table1_1">[1]:</b> per migliorare la sicurezza, il comportamento di convalida crittografia e il certificato viene modificato quando si usano Token di autenticazione o accesso delle proprietà di inizializzazione o le parole chiave delle stringhe di connessione corrispondente. Per informazioni dettagliate, vedere [crittografia e convalida dei certificati](../features/using-azure-active-directory.md#encryption-and-certificate-validation).

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
|**Access Token**<a href="#table2_1"><sup id="table2_accesstoken">**1**</sup></a>|SSPROP_AUTH_ACCESS_TOKEN|Il token di accesso utilizzato per eseguire l'autenticazione ad Azure Active Directory. <br/><br/>**Nota:** è un errore per specificare questa parola chiave, nonché `UID`, `PWD`, `Trusted_Connection`, o `Authentication` parole chiave delle stringhe di connessione o le proprietà o le parole chiave corrispondenti.|
|**Application Name**|SSPROP_INIT_APPNAME|Stringa che identifica l'applicazione.|  
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. I valori possibili sono **ReadOnly** e **ReadWrite**.<br /><br /> Il valore predefinito è **ReadWrite**. Per altre informazioni sui Driver OLE DB per il supporto di SQL Server per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [Driver OLE DB per SQL Server il supporto per la disponibilità elevata, ripristino di emergenza](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**L'autenticazione**<a href="#table2_1"><sup>**1**</sup></a>|SSPROP_AUTH_MODE|Specifica l'autenticazione di Active Directory o SQL usata. I valori validi sono:<br/><ul><li>`(not set)`: Modalità di autenticazione determinata da altre parole chiave.</li><li>`ActiveDirectoryPassword:` Autenticazione di Active Directory usando l'ID di accesso e la password.</li><li>`ActiveDirectoryIntegrated:` Autenticazione integrata di Active Directory usando le credenziali dell'account di Windows dell'utente connesso.</li><br/>**Nota:** ha **consigliati** che le applicazioni usando `Integrated Security` (o `Trusted_Connection`) le proprietà corrispondenti o le parole chiave di autenticazione impostare il valore della `Authentication` (parola chiave) (o dai relativi proprietà corrispondente) a `ActiveDirectoryIntegrated` per abilitare il comportamento di convalida crittografia e il certificato nuovo.<br/><br/><li>`SqlPassword:` Autenticazione usando l'ID di accesso e la password.</li><br/>**Nota:** ha **consigliati** che le applicazioni usando `SQL Server` autenticazione imposta il valore della `Authentication` parola chiave o la proprietà corrispondente per `SqlPassword` per abilitare la nuova crittografia e comportamento di convalida di certificati.</ul>|
|**Conversione automatica**|SSPROP_INIT_AUTOTRANSLATE|Sinonimo di "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la conversione dei caratteri OEM/ANSI. I valori riconosciuti sono "true" e "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Tempo di attesa in secondi per il completamento dell'inizializzazione dell'origine dati.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|Nome della lingua di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Data Source**|DBPROP_INIT_DATASOURCE|Nome di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Se non viene specificato un nome, viene stabilita una connessione all'istanza predefinita nel computer locale.<br /><br /> Per altre informazioni sulla sintassi valida per gli indirizzi, vedere la descrizione della parola chiave **Server** in questo argomento.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Specifica la modalità di gestione dei tipi di dati da utilizzare. I valori riconosciuti sono "0" per i tipi di dati del provider e "80" per i tipi di dati di [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)].|  
|**Partner di failover**|SSPROP_INIT_FAILOVERPARTNER|Nome del server di failover utilizzato per il mirroring del database.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Nome SPN del partner di failover. Il valore predefinito è una stringa vuota. Una stringa vuota fa sì che il Driver OLE DB per SQL Server per utilizzare il valore predefinito generato dal provider SPN.|  
|**Catalogo iniziale**|DBPROP_INIT_CATALOG|Nome del database.|  
|**Nome File iniziale**|SSPROP_INIT_FILENAME|Nome del file primario, incluso il nome completo del percorso, di un database collegabile. Per usare **AttachDBFileName**, è necessario specificare anche il nome del database con la parola chiave DATABASE della stringa del provider. Se il database è stato collegato in precedenza, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non lo ricollega e utilizza il database collegato come impostazione predefinita per la connessione.|  
|**Sicurezza integrata**|DBPROP_AUTH_INTEGRATED|Accetta il valore "SSPI" per l'autenticazione di Windows.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|Abilita o disabilita MARS (Multiple Active Result Sets) nella connessione. I valori riconosciuti sono "true" e "false". Il valore predefinito è "false".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Specificare sempre **MultiSubnetFailover=True** in caso di connessione al listener del gruppo di disponibilità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o a un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Con **MultiSubnetFailover=True** è possibile configurare il driver OLE DB per SQL Server per offrire un rilevamento e una connessione più veloci al server attualmente attivo. I valori possibili sono **True** e **False**. Il valore predefinito è **False**. Esempio:<br /><br /> `MultiSubnetFailover=True`<br /><br /> Per altre informazioni sui Driver OLE DB per il supporto di SQL Server per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [Driver OLE DB per SQL Server il supporto per la disponibilità elevata, ripristino di emergenza](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|Indirizzo di rete di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Per altre informazioni sulla sintassi valida per gli indirizzi, vedere la descrizione della parola chiave **Address** in questo argomento.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|Libreria di rete utilizzata per stabilire una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Dimensioni del pacchetto di rete. Il valore predefinito è 4096.|  
|**Password**|DBPROP_AUTH_PASSWORD|Password di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Accetta le stringhe "true" e "false" come valori. Se il valore è impostato su "false", l'oggetto origine dati non è in grado di rendere persistenti le informazioni di autenticazione riservate|  
|**Provider**||Per Driver OLE DB per SQL Server, deve essere "MSOLEDBSQL".|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|Nome SPN del server. Il valore predefinito è una stringa vuota. Una stringa vuota fa sì che il Driver OLE DB per SQL Server per utilizzare il valore predefinito generato dal provider SPN.|  
|**Trust Server Certificate**<a href="#table2_1"><sup>**1**</sup></a>|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Accetta le stringhe "true" e "false" come valori. Il valore predefinito è "false", il quale indica che il certificato server verrà convalidato.|  
|**Use Encryption for Data**<a href="#table2_1"><sup>**1**</sup></a>|SSPROP_INIT_ENCRYPT|Specifica se i dati devono essere crittografati prima del relativo invio in rete. I valori possibili sono "true" e "false". Il valore predefinito è "false".|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|Controlla la modalità di recupero dei metadati durante la connessione a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e versioni successive. I valori possibili sono "true" e "false". Il valore predefinito è "false".<br /><br />Per impostazione predefinita, Usa il Driver OLE DB per SQL Server [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) e [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) stored procedure per recuperare i metadati. Queste stored procedure hanno alcune limitazioni (ad esempio, hanno esito negativo quando si opera su tabelle temporanee). L'impostazione **Usa FMTONLY** su "true" si indica al driver di usare [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md) per il recupero di metadati invece.|  
|**ID utente**|DBPROP_AUTH_USERID|Nome dell'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Workstation ID**|SSPROP_INIT_WSID|Identificatore della workstation.|  
  
<b id="table2_1">[1]:</b> per migliorare la sicurezza, il comportamento di convalida crittografia e il certificato viene modificato quando si usano Token di autenticazione o accesso delle proprietà di inizializzazione o le parole chiave delle stringhe di connessione corrispondente. Per informazioni dettagliate, vedere [crittografia e convalida dei certificati](../features/using-azure-active-directory.md#encryption-and-certificate-validation).

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
|**Access Token**<a href="#table3_1"><sup id="table3_accesstoken">**1**</sup></a>|SSPROP_AUTH_ACCESS_TOKEN|Il token di accesso utilizzato per eseguire l'autenticazione ad Azure Active Directory.<br/><br/>**Nota:** è un errore per specificare questa parola chiave, nonché `UID`, `PWD`, `Trusted_Connection`, o `Authentication` parole chiave delle stringhe di connessione o le proprietà o le parole chiave corrispondenti.|
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|Dichiara il tipo di carico di lavoro dell'applicazione in caso di connessione a un server. I valori possibili sono **ReadOnly** e **ReadWrite**.<br /><br /> Il valore predefinito è **ReadWrite**. Per altre informazioni sui Driver OLE DB per il supporto di SQL Server per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [Driver OLE DB per SQL Server il supporto per la disponibilità elevata, ripristino di emergenza](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Application Name**|SSPROP_INIT_APPNAME|Stringa che identifica l'applicazione.|  
|**L'autenticazione**<a href="#table3_1"><sup>**1**</sup></a>|SSPROP_AUTH_MODE|Specifica l'autenticazione di Active Directory o SQL usata. I valori validi sono:<br/><ul><li>`(not set)`: Modalità di autenticazione determinata da altre parole chiave.</li><li>`ActiveDirectoryPassword:` Autenticazione di Active Directory usando l'ID di accesso e la password.</li><li>`ActiveDirectoryIntegrated:` Autenticazione integrata di Active Directory usando le credenziali dell'account di Windows dell'utente connesso.</li><br/>**Nota:** ha **consigliati** che le applicazioni usando `Integrated Security` (o `Trusted_Connection`) le proprietà corrispondenti o le parole chiave di autenticazione impostare il valore della `Authentication` (parola chiave) (o dai relativi proprietà corrispondente) a `ActiveDirectoryIntegrated` per abilitare il comportamento di convalida crittografia e il certificato nuovo.<br/><br/><li>`SqlPassword:` Autenticazione usando l'ID di accesso e la password.</li><br/>**Nota:** ha **consigliati** che le applicazioni usando `SQL Server` autenticazione imposta il valore della `Authentication` parola chiave o la proprietà corrispondente per `SqlPassword` per abilitare la nuova crittografia e comportamento di convalida di certificati.</ul>|
|**Conversione automatica**|SSPROP_INIT_AUTOTRANSLATE|Sinonimo di "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la conversione dei caratteri OEM/ANSI. I valori riconosciuti sono "true" e "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Tempo di attesa in secondi per il completamento dell'inizializzazione dell'origine dati.|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|Nome della lingua di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Data Source**|DBPROP_INIT_DATASOURCE|Nome di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Se non viene specificato un nome, viene stabilita una connessione all'istanza predefinita nel computer locale.<br /><br /> Per altre informazioni sulla sintassi valida per gli indirizzi, vedere la descrizione della parola chiave **Server** in questo argomento.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Specifica la modalità di gestione dei tipi di dati che verrà utilizzata. I valori riconosciuti sono "0" per i tipi di dati del provider e "80" per i tipi di dati di SQL Server 2000.|  
|**Partner di failover**|SSPROP_INIT_FAILOVERPARTNER|Nome del server di failover utilizzato per il mirroring del database.|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|Nome SPN del partner di failover. Il valore predefinito è una stringa vuota. Una stringa vuota fa sì che il Driver OLE DB per SQL Server per utilizzare il valore predefinito generato dal provider SPN.|  
|**Catalogo iniziale**|DBPROP_INIT_CATALOG|Nome del database.|  
|**Nome File iniziale**|SSPROP_INIT_FILENAME|Nome del file primario, incluso il nome completo del percorso, di un database collegabile. Per usare **AttachDBFileName**, è necessario specificare anche il nome del database con la parola chiave DATABASE della stringa del provider. Se il database è stato collegato in precedenza, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non lo ricollega e utilizza il database collegato come impostazione predefinita per la connessione.|  
|**Sicurezza integrata**|DBPROP_AUTH_INTEGRATED|Accetta il valore "SSPI" per l'autenticazione di Windows.|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|Abilita o disabilita MARS (Multiple Active Result Sets) nella connessione se il server è [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva. I valori riconosciuti sono "true" e "false". Il valore predefinito è "false".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Specificare sempre **MultiSubnetFailover=True** in caso di connessione al listener del gruppo di disponibilità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o a un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Con **MultiSubnetFailover=True** è possibile configurare il driver OLE DB per SQL Server per offrire un rilevamento e una connessione più veloci al server attualmente attivo. I valori possibili sono **True** e **False**. Il valore predefinito è **False**. Esempio:<br /><br /> `MultiSubnetFailover=True`<br /><br /> Per altre informazioni sui Driver OLE DB per il supporto di SQL Server per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [Driver OLE DB per SQL Server il supporto per la disponibilità elevata, ripristino di emergenza](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|Indirizzo di rete di un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.<br /><br /> Per altre informazioni sulla sintassi valida per gli indirizzi, vedere la descrizione della parola chiave **Address** in questo argomento.|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|Libreria di rete utilizzata per stabilire una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nell'organizzazione.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Dimensioni del pacchetto di rete. Il valore predefinito è 4096.|  
|**Password**|DBPROP_AUTH_PASSWORD|Password di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Accetta le stringhe "true" e "false" come valori. Se il valore è impostato su "false", l'oggetto origine dati non è in grado di rendere persistenti le informazioni di autenticazione riservate.|  
|**Provider**||Per Driver OLE DB per SQL Server, deve essere "MSOLEDBSQL".|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|Nome SPN del server. Il valore predefinito è una stringa vuota. Una stringa vuota fa sì che il Driver OLE DB per SQL Server per utilizzare il valore predefinito generato dal provider SPN.|  
|**Trust Server Certificate**<a href="#table3_1"><sup>**1**</sup></a>|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Accetta le stringhe "true" e "false" come valori. Il valore predefinito è "false", il quale indica che il certificato server verrà convalidato.|  
|**Use Encryption for Data**<a href="#table3_1"><sup>**1**</sup></a>|SSPROP_INIT_ENCRYPT|Specifica se i dati devono essere crittografati prima del relativo invio in rete. I valori possibili sono "true" e "false". Il valore predefinito è "false".|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|Controlla la modalità di recupero dei metadati durante la connessione a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e versioni successive. I valori possibili sono "true" e "false". Il valore predefinito è "false".<br /><br />Per impostazione predefinita, Usa il Driver OLE DB per SQL Server [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) e [sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md) stored procedure per recuperare i metadati. Queste stored procedure hanno alcune limitazioni (ad esempio, hanno esito negativo quando si opera su tabelle temporanee). L'impostazione **Usa FMTONLY** su "true" si indica al driver di usare [SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md) per il recupero di metadati invece.|  
|**ID utente**|DBPROP_AUTH_USERID|Nome dell'account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Workstation ID**|SSPROP_INIT_WSID|Identificatore della workstation.|  
  
<b id="table3_1">[1]:</b> per migliorare la sicurezza, il comportamento di convalida crittografia e il certificato viene modificato quando si usano Token di autenticazione o accesso delle proprietà di inizializzazione o le parole chiave delle stringhe di connessione corrispondente. Per informazioni dettagliate, vedere [crittografia e convalida dei certificati](../features/using-azure-active-directory.md#encryption-and-certificate-validation).

 **Nota** Nella stringa di connessione la proprietà "Vecchia password" imposta SSPROP_AUTH_OLD_PASSWORD, ovvero la password corrente (probabilmente scaduta) che non è disponibile tramite una proprietà della stringa del provider.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con il driver OLE DB per SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
