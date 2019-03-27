---
title: sp_addlinkedserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlinkedserver_TSQL
- sp_addlinkedserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedserver
ms.assetid: fed3adb0-4c15-4a1a-8acd-1b184aff558f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b4ff861015fc669defee69fece5c26ee45d66eaa
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493912"
---
# <a name="spaddlinkedserver-transact-sql"></a>sp_addlinkedserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un server collegato, il quale consente l'accesso a query distribuite ed eterogenee in origini dati OLE DB. Dopo la creazione di un server collegato mediante **sp_addlinkedserver**distribuito le query possono essere eseguite su questo server. Se il server collegato viene definito come un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile eseguire stored procedure remote.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addlinkedserver [ @server= ] 'server' [ , [ @srvproduct= ] 'product_name' ]   
     [ , [ @provider= ] 'provider_name' ]  
     [ , [ @datasrc= ] 'data_source' ]   
     [ , [ @location= ] 'location' ]   
     [ , [ @provstr= ] 'provider_string' ]   
     [ , [ @catalog= ] 'catalog' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @server = ] 'server'` È il nome del server collegato da creare. *server* è di tipo **sysname**e non prevede alcun valore predefinito.  
  
`[ @srvproduct = ] 'product_name'` È il nome del prodotto dell'origine dati OLE DB da aggiungere come server collegato. *product_name* viene **nvarchar (** 128 **)**, con un valore predefinito è NULL. Se **SQL Server**, *provider_name*, *data_source*, *posizione*, *provider_string*, e *catalogo* non è necessario specificare.  
  
`[ @provider = ] 'provider_name'` È l'identificatore univoco a livello di codice (PROGID) del provider OLE DB che corrisponde a questa origine dati. *provider_name* deve essere univoco per il provider OLE DB specificato installato nel computer corrente. *provider_name* viene **nvarchar (** 128 **)**, con un valore predefinito è NULL; tuttavia, se *provider_name* viene omesso, viene utilizzato SQLNCLI. (L'utilizzo di SQLNCLI e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reindirizza alla versione più recente del provider OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.) Il provider OLE DB deve essere registrato nel Registro di configurazione con il valore PROGID specificato.  
  
`[ @datasrc = ] 'data_source'` È il nome dell'origine dati interpretato dal provider OLE DB. *data_source* viene **nvarchar (** 4000 **)**. *data_source* viene passato come proprietà DBPROP_INIT_DATASOURCE per inizializzare il provider OLE DB.  
  
`[ @location = ] 'location'` È il percorso del database interpretato dal provider OLE DB. *ubicazione* viene **nvarchar (** 4000 **)**, con un valore predefinito è NULL. *percorso* viene passato come proprietà DBPROP_INIT_LOCATION per inizializzare il provider OLE DB.  
  
`[ @provstr = ] 'provider_string'` È la stringa di connessione specifica del provider OLE DB che identifica un'origine dati univoca. *provider_string* viene **nvarchar (** 4000 **)**, con un valore predefinito è NULL. *provstr* viene passato a IDataInitialize o impostato come proprietà DBPROP_INIT_PROVIDERSTRING per inizializzare il provider OLE DB.  
  
 Quando il server collegato viene creato con il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client, l'istanza può essere specificato usando la parola chiave SERVER come SERVER =*servername*\\*NomeIstanza*per specificare un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *ServerName* è il nome del computer in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione, e *instancename* è il nome dell'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui l'utente verrà connesso.  
  
> [!NOTE]
>  Per accedere a un database con mirroring, è necessario che la stringa di connessione contenga il nome del database, al fine di consentire i tentativi di failover da parte del provider di accesso ai dati. Il database può essere specificato nella **@provstr** oppure **@catalog** parametro. Facoltativamente, la stringa di connessione può specificare anche il nome di un partner di failover.  
  
`[ @catalog = ] 'catalog'` È il catalogo da utilizzare quando viene stabilita una connessione al provider OLE DB. *catalogo* viene **sysname**, con un valore predefinito è NULL. *catalogo* viene passato come proprietà DBPROP_INIT_CATALOG per inizializzare il provider OLE DB. Quando il server collegato viene definito in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il catalogo si riferisce al database predefinito a cui viene eseguito il mapping del server collegato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna.  
  
## <a name="remarks"></a>Note  
 Nella tabella seguente vengono descritte le possibili configurazioni di un server collegato per origini dati accessibili tramite OLE DB. Un server collegato può essere configurato in modi diversi per un'origine dati specifica. Per un tipo di origine dati possono essere disponibili più righe. Questa tabella mostra anche il **sp_addlinkedserver** i valori dei parametri da utilizzare per la configurazione del server collegato.  
  
|Origine dati OLE DB remota|Provider OLE DB|product_name|provider_name|data_source|posizione|provider_string|catalogo|  
|-------------------------------|---------------------|-------------------|--------------------|------------------|--------------|----------------------|-------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Provider OLE DB Native Client|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <sup>1</sup> (impostazione predefinita)||||||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Provider OLE DB Native Client||**SQLNCLI**|Nome di rete di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (per l'istanza predefinita)|||Nome di database (facoltativo)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Provider OLE DB Native Client||**SQLNCLI**|*ServerName*\\*instancename* (per un'istanza specifica)|||Nome di database (facoltativo)|  
|Oracle, versione 8 e successive|Provider Oracle per OLE DB|Qualsiasi|**OraOLEDB.Oracle**|Alias per il database Oracle||||  
|Access/Jet|Provider Microsoft OLE DB per Jet|Qualsiasi|**Microsoft.Jet.OLEDB.4.0**|Percorso completo del file di database Jet||||  
|Origine dati ODBC|Provider Microsoft OLE DB per ODBC|Qualsiasi|**MSDASQL**|DSN di sistema dell'origine dati ODBC||||  
|Origine dati ODBC|Provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per ODBC|Qualsiasi|**MSDASQL**|||Stringa di connessione ODBC||  
|File system|Provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per il servizio di indicizzazione|Qualsiasi|**MSIDXS**|Nome del catalogo del Servizio di indicizzazione||||  
|Foglio di calcolo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel|Provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per Jet|Qualsiasi|**Microsoft.Jet.OLEDB.4.0**|Percorso completo del file di Excel||Excel 5.0||  
|Database IBM DB2|Provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per DB2|Qualsiasi|**DB2OLEDB**|||Vedere [!INCLUDE[msCoName](../../includes/msconame-md.md)] Provider OLE DB per DB2 documentazione.|Nome del catalogo del database DB2|  
  
 <sup>1</sup> questa modalità di configurazione di un server collegato impone che il nome del server collegato sia identico al nome di rete dell'istanza remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uso *data_source* per specificare il server.  
  
 <sup>2</sup> "Any" indica che il nome del prodotto può essere qualsiasi elemento.  
  
 Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client è il provider utilizzata con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se viene specificato alcun nome di provider o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene specificato come nome del prodotto. Anche se si specifica il nome del provider meno recente, SQLOLEDB, verrà modificato in SQLNCLI se persiste nel catalogo.  
  
 Il *data_source*, *posizione*, *provider_string*, e *catalogo* parametri identificano uno o più database collegati Server punta a. Se uno di questi parametri è NULL, la proprietà di inizializzazione OLE DB corrispondente non viene impostata.  
  
 In un ambiente cluster, quando si specificano nomi di file che puntano a origini dati OLE DB, la posizione deve essere specificata nel formato UNC oppure deve corrispondere a un'unità condivisa.  
  
 **sp_addlinkedserver** non può essere eseguita all'interno di una transazione definita dall'utente.  
  
> [!IMPORTANT]
>  Quando viene creato un server collegato mediante **sp_addlinkedserver**, un mapping automatico predefinito viene aggiunto per tutti gli account di accesso locale. Per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli account di accesso autenticato potrebbe essere in grado di effettuare l'accesso al provider con il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account del servizio. Si consiglia agli amministratori di considerare l'utilizzo di `sp_droplinkedsrvlogin <linkedserver_name>, NULL` per rimuovere il mapping globale.  
  
## <a name="permissions"></a>Permissions  
 Il `sp_addlinkedserver` istruzione richiede il `ALTER ANY LINKED SERVER` l'autorizzazione. (SSMS **nuovo Server collegato** finestra di dialogo viene implementata in modo da richiedere l'appartenenza di `sysadmin` ruolo predefinito del server.)  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-the-microsoft-sql-server-native-client-ole-db-provider"></a>A. Utilizzo del provider OLE DB per Microsoft SQL Server Native Client  
 Nell'esempio seguente viene creato un server collegato denominato `SEATTLESales`. Il nome del prodotto è `SQL Server` e non vengono utilizzati nomi di provider.  
  
```  
USE master;  
GO  
EXEC sp_addlinkedserver   
   N'SEATTLESales',  
   N'SQL Server';  
GO  
```  
  
 L'esempio seguente crea un server collegato `S1_instance1` in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client.  
  
```  
EXEC sp_addlinkedserver     
   @server=N'S1_instance1',   
   @srvproduct=N'',  
   @provider=N'SQLNCLI',   
   @datasrc=N'S1\instance1';  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-microsoft-access"></a>b. Utilizzo del provider Microsoft OLE DB per Microsoft Access  
 Il provider Microsoft.Jet.OLEDB.4.0 si connette al database di Microsoft Access che utilizza il formato 2002-2003. Nell'esempio seguente viene creato un server collegato denominato `SEATTLE Mktg`.  
  
> [!NOTE]  
>  Questo esempio si presuppone che entrambe [!INCLUDE[msCoName](../../includes/msconame-md.md)] accesso e il codice di esempio **Northwind** database sono installati e che il **Northwind** in c:\Msoffice\Access\Samples. situato il database.  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.Jet.OLEDB.4.0',   
   @srvproduct = N'OLE DB Provider for Jet',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.mdb';  
GO  
```  
  
 Il provider Microsoft.ACE.OLEDB.12.0 si connette al database di Microsoft Access che utilizza il formato 2007. Nell'esempio seguente viene creato un server collegato denominato `SEATTLE Mktg`.  
  
> [!NOTE]  
>  Questo esempio si presuppone che entrambe [!INCLUDE[msCoName](../../includes/msconame-md.md)] accesso e il codice di esempio **Northwind** database sono installati e che il **Northwind** in c:\Msoffice\Access\Samples. situato il database.  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.ACE.OLEDB.12.0',   
   @srvproduct = N'OLE DB Provider for ACE',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.accdb';  
GO  
```  
  
### <a name="c-using-the-microsoft-ole-db-provider-for-odbc-with-the-datasource-parameter"></a>C. Utilizzo del provider Microsoft OLE DB per ODBC con il parametro data_source  
 L'esempio seguente crea un server collegato denominato `SEATTLE Payroll` che usa la [!INCLUDE[msCoName](../../includes/msconame-md.md)] Provider OLE DB per ODBC (`MSDASQL`) e il *data_source* parametro.  
  
> [!NOTE]  
>  Il nome dell'origine dati ODBC specificato deve essere definito come System DSN nel server prima di utilizzare il server collegato.  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Payroll',   
   @srvproduct = N'',  
   @provider = N'MSDASQL',   
   @datasrc = N'LocalServer';  
GO  
```  
  
### <a name="d-using-the-microsoft-ole-db-provider-for-excel-spreadsheet"></a>D. Utilizzo del provider Microsoft OLE DB per un foglio di calcolo di Excel  
 Per creare una definizione di server collegato usando il [!INCLUDE[msCoName](../../includes/msconame-md.md)] Provider OLE DB per Jet accedere a un foglio di calcolo di Excel nel formato 1997-2003, prima di tutto creare un intervallo denominato in Excel specificando le colonne e righe del foglio di lavoro di Excel per selezionare. È quindi possibile fare riferimento al nome dell'intervallo come a un nome di tabella in una query distribuita.  
  
```  
EXEC sp_addlinkedserver 'ExcelSource',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   'c:\MyData\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
GO  
```  
  
 Per accedere ai dati di un foglio di calcolo di Microsoft Excel, assegnare un nome a un intervallo di celle. Per accedere a un intervallo denominato `SalesData` come tabella tramite il server collegato impostato nell'esempio precedente è possibile utilizzare la query seguente.  
  
```  
SELECT *  
   FROM ExcelSource...SalesData;  
GO  
```  
  
 Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in un account di dominio che ha accesso a una condivisione remota, è possibile utilizzare un percorso UNC invece di un'unità sulla quale viene eseguito il mapping.  
  
```  
EXEC sp_addlinkedserver 'ExcelShare',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   '\\MyServer\MyShare\Spreadsheets\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
```  
  
 Per connettersi a un foglio di calcolo di Excel nel formato 2007 utilizzare il provider ACE.  
  
```  
EXEC sp_addlinkedserver @server = N'ExcelDataSource',   
@srvproduct=N'ExcelData', @provider=N'Microsoft.ACE.OLEDB.12.0',   
@datasrc=N'C:\DataFolder\People.xlsx',  
@provstr=N'EXCEL 12.0' ;  
  
```  
  
### <a name="e-using-the-microsoft-ole-db-provider-for-jet-to-access-a-text-file"></a>E. Utilizzo del provider Microsoft OLE DB per Jet per accedere a un file di testo  
 Nell'esempio seguente viene creato un server collegato per accedere direttamente a file di testo senza dover collegare i file come tabelle in un file di Access con estensione mdb. Il provider è `Microsoft.Jet.OLEDB.4.0` e la stringa corrispondente è `Text`.  
  
 L'origine dati corrisponde al percorso completo della directory che include i file di testo. In questa directory è necessario creare un file schema.ini che descriva la struttura dei file di testo. Per ulteriori informazioni sulla creazione di un file Schema.ini, vedere la documentazione del motore di database Jet.  
  
```  
--Create a linked server.  
EXEC sp_addlinkedserver txtsrv, N'Jet 4.0',   
   N'Microsoft.Jet.OLEDB.4.0',  
   N'c:\data\distqry',  
   NULL,  
   N'Text';  
GO  
  
--Set up login mappings.  
EXEC sp_addlinkedsrvlogin txtsrv, FALSE, Admin, NULL;  
GO  
  
--List the tables in the linked server.  
EXEC sp_tables_ex txtsrv;  
GO  
  
--Query one of the tables: file1#txt  
--using a four-part name.   
SELECT *   
FROM txtsrv...[file1#txt];  
```  
  
### <a name="f-using-the-microsoft-ole-db-provider-for-db2"></a>F. Utilizzo del provider Microsoft OLE DB per DB2  
 Nell'esempio seguente viene creato un server collegato denominato `DB2` in cui viene utilizzato `Microsoft OLE DB Provider for DB2`.  
  
```  
EXEC sp_addlinkedserver  
   @server=N'DB2',  
   @srvproduct=N'Microsoft OLE DB Provider for DB2',  
   @catalog=N'DB2',  
   @provider=N'DB2OLEDB',  
   @provstr=N'Initial Catalog=PUBS;  
       Data Source=DB2;  
       HostCCSID=1252;  
       Network Address=XYZ;  
       Network Port=50000;  
       Package Collection=admin;  
       Default Schema=admin;';  
```  
  
### <a name="g-add-a-includesssdsfullincludessssdsfull-mdmd-as-a-linked-server-for-use-with-distributed-queries-on-cloud-and-on-premise-databases"></a>G. Aggiungere [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] come server collegato per l'utilizzo con le query distribuite in database locali e sul cloud  
 È possibile aggiungere [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] come server collegato e quindi utilizzato con query distribuite che si estendono su database locali e cloud. Si tratta di un componente per le soluzioni di database ibride che si estendono su reti aziendali locali e sul cloud di Windows Azure.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prodotto contiene la funzionalità di query distribuite, che consente di scrivere query per combinare dati provenienti da origini dati locali e i dati da origini remote (compresi i dati non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zdroje dat) definite come server collegati. Ogni [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (ad eccezione del database master virtuale) può essere aggiunto come singolo server collegato e quindi essere utilizzato direttamente nelle applicazioni di database come qualsiasi altro database.  
  
 I vantaggi offerti da [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] includono gestibilità, disponibilità elevata, scalabilità, compatibilità con un modello di sviluppo noto e un modello di dati relazionale. I requisiti dell'applicazione di database determinano la modalità di utilizzo di [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] nel cloud. È possibile spostare contemporaneamente tutti i dati in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] o spostare progressivamente alcuni dati mantenendo quelli rimanenti in locale. Per le applicazioni di database ibride, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] potrà essere aggiunto come server collegati e l'applicazione di database potrà eseguire query distribuite per combinare dati da [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e origini dati locali.  
  
 Ecco un semplice esempio che illustra come connettersi a un [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] mediante query distribuite:  
  
```  
------ Configure the linked server  
-- Add one Windows Azure SQL DB as Linked Server  
EXEC sp_addlinkedserver  
@server='myLinkedServer', -- here you can specify the name of the linked server  
@srvproduct='',       
@provider='sqlncli', -- using SQL Server Native Client  
@datasrc='myServer.database.windows.net',   -- add here your server name  
@location='',  
@provstr='',  
@catalog='myDatabase'  -- add here your database name as initial catalog (you cannot connect to the master database)  
-- Add credentials and options to this linked server  
EXEC sp_addlinkedsrvlogin  
@rmtsrvname = 'myLinkedServer',  
@useself = 'false',  
@rmtuser = 'myLogin',             -- add here your login on Azure DB  
@rmtpassword = 'myPassword' -- add here your password on Azure DB  
EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;  
------ Now you can use the linked server to execute 4-part queries  
-- You can create a new table in the Azure DB  
exec ('CREATE TABLE t1tutut2(col1 int not null CONSTRAINT PK_col1 PRIMARY KEY CLUSTERED (col1) )') at myLinkedServer  
-- Insert data from your local SQL Server  
exec ('INSERT INTO t1tutut2 VALUES(1),(2),(3)') at myLinkedServer  
  
-- Query the data using 4-part names  
select * from myLinkedServer.myDatabase.dbo.myTable  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Distributed query Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [sp_setnetname &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setnetname-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
