---
title: Modifiche di rilievo apportate al Database del motore Features in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d7b5bf6ff2324c8e63b030d03e36794faf0ec9d4
ms.sourcegitcommit: ab867100949e932f29d25a3c41171f01156e923d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2019
ms.locfileid: "67419040"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2014"></a>Modifiche che possono causare problemi di funzionamento apportate alle funzionalità del Motore di database in SQL Server 2014.
  Questo argomento descrive le modifiche di rilievo apportate al [!INCLUDE[ssDE](../includes/ssde-md.md)] di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Tali modifiche potrebbero interrompere il funzionamento di applicazioni, funzionalità o script basati su versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È possibile che questi problemi si verifichino quando viene effettuato un aggiornamento. Per altre informazioni, vedere [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
##  <a name="SQL14"></a> Modifiche di rilievo in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Nessun nuovo problema.  
  
##  <a name="Denali"></a> Modifiche di rilievo in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|Selezione dalle colonne o tabelle denominate NEXT.|Nelle sequenze viene usata la funzione NEXT VALUE FOR dello standard ANSI. Se una tabella o una colonna viene denominata NEXT e la tabella o la colonna è associato un alias come valore e se la clausola AS standard ANSI viene omessa, l'istruzione risultante può causare un errore. Per risolvere il problema, includere la parola chiave AS dello standard ANSI. Ad esempio, `SELECT NEXT VALUE FROM Table` deve essere riscritto come `SELECT NEXT AS VALUE FROM Table` e `SELECT Col1 FROM NEXT VALUE` deve essere riscritto come `SELECT Col1 FROM NEXT AS VALUE`.|  
|Operatore PIVOT|L'operatore PIVOT non è consentito in una query ricorsiva dell'espressione di tabella comune quando il livello di compatibilità del database è impostato su 110. Riscrivere la query o impostare il livello di compatibilità su 100 o un valore inferiore. L'uso di PIVOT in una query ricorsiva dell'espressione di tabella comune genera risultati non corretti quando sono presenti più righe per raggruppamento.|  
|sp_setapprole e sp_unsetapprole|Il parametro `OUTPUT` del cookie per `sp_setapprole` è disponibile attualmente come `varbinary(8000)` che è la lunghezza massima corretta. Tuttavia, dall'implementazione corrente viene restituito `varbinary(50)`. Le applicazioni devono continuare a riservare `varbinary(8000)` in modo siano in grado di funzionare correttamente se le dimensioni restituite del cookie aumentano in una versione successiva. Per altre informazioni, vedere [sp_setapprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql).|  
|EXECUTE AS|Il parametro OUTPUT del cookie per EXECUTE AS è attualmente disponibile come `varbinary(8000)` che rappresenta la lunghezza massima corretta. Tuttavia, dall'implementazione corrente viene restituito `varbinary(100)`. Le applicazioni devono continuare a riservare `varbinary(8000)` in modo siano in grado di funzionare correttamente se le dimensioni restituite del cookie aumentano in una versione successiva. Per altre informazioni, vedere [EXECUTE AS &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-transact-sql).|  
|Funzione sys.fn_get_audit_file|Due colonne aggiuntive (**user_defined_event_id** e **user_defined_information**) sono stati aggiunti per supportare gli eventi di controllo definiti dall'utente. Nelle applicazioni in cui le colonne non vengono selezionate in base al nome è possibile che venga restituito un numero di colonne maggiore del previsto. Selezionare le colonne in base al nome oppure modificare l'applicazione in modo che vengano accettate queste colonne aggiuntive.|  
|Parola chiave riservata WITHIN|WITHIN è ora una parola chiave riservata. I riferimenti a oggetti o colonne denominate 'within' avranno esito negativo. Rinominare l'oggetto o la colonna oppure delimitare il nome tramite parentesi quadre o virgolette,  Ad esempio `SELECT * FROM [within]`.|  
|Operazioni CAST e CONVERT su colonne calcolate di tipo `time` o `datetime2`|Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] lo stile predefinito per le operazioni CAST e CONVERT sui tipi di dati `time` e `datetime2` è 121, tranne quando uno dei due tipi viene usato in un'espressione di colonna calcolata. Per le colonne calcolate, lo stile predefinito è 0. Questo comportamento influisce sulle colonne calcolate quando vengono create o usate nelle query con parametrizzazione automatica o nelle definizioni dei vincoli.<br /><br /> Con il livello di compatibilità 110, lo stile predefinito per le operazioni CAST e CONVERT sui tipi di dati `time` e `datetime2` è sempre 121. Se la query si basa sul comportamento obsoleto, usare un livello di compatibilità inferiore a 110 oppure specificare in modo esplicito lo stile 0 nella query interessata.<br /><br /> L'aggiornamento del database al livello di compatibilità 110 non comporta la modifica dei dati utente archiviati su disco. È necessario correggere manualmente questi dati nel modo opportuno. Se ad esempio si usa SELECT INTO per creare una tabella da un'origine che contiene un'espressione di colonna calcolata descritta in precedenza, vengono archiviati i dati (con stile 0), non la definizione della colonna calcolata. Sarà necessario aggiornare manualmente questi dati in base allo stile 121.|  
|ALTER TABLE|L'istruzione ALTER TABLE supporta unicamente nomi di tabella in due parti (schema.oggetto). Specificare un nome di tabella utilizzando i seguenti formati di ora non riesce in fase di compilazione dell'errore 117:<br /><br /> server.database.schema.tabella<br /><br /> .database.schema.tabella<br /><br /> ..schema.tabella<br /><br /> Nelle versioni precedenti l'uso del formato server.database.schema.tabella genera l'errore 4902. L'uso del formato .database.schema.tabella o ..schema.tabella è supportato. Per risolvere il problema, rimuovere l'uso di un prefisso in quattro parti.|  
|Esplorazione dei metadati|L'esecuzione di una query su una vista tramite FOR BROWSE o SET NO_BROWSETABLE ON comporta la restituzione dei metadati della vista, non dell'oggetto sottostante. Questo comportamento corrisponde ad altri metodi di esplorazione dei metadati.|  
|SOUNDEX|Con il livello di compatibilità del database 110, la funzione SOUNDEX consente di implementare nuove regole che potrebbero generare una differenza tra i valori calcolati dalla funzione e quelli calcolati con livelli di compatibilità precedenti. Dopo aver effettuato l'aggiornamento al livello di compatibilità 110, potrebbe essere necessario ricompilare gli indici, gli heap o i vincoli CHECK in cui viene usata la funzione SOUNDEX. Per altre informazioni, vedere [SOUNDEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/soundex-transact-sql)
|Messaggio sul numero di righe per le istruzioni DML che hanno esito negativo|Nelle [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], il [!INCLUDE[ssDE](../includes/ssde-md.md)] invierà regolarmente il token TDS DONE con RowCount: 0 ai client quando un'istruzione DML ha esito negativo. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] un valore errato -1 viene inviato al client quando l'istruzione DML non riuscita si trova all'interno di un blocco TRY-CATCH e il [!INCLUDE[ssDE](../includes/ssde-md.md)] attiva la parametrizzazione automatica oppure il blocco TRY-CATCH non si trova sullo stesso livello dell'istruzione non riuscita. Ad esempio, se un blocco TRY-CATCH chiama una stored procedure e un'istruzione DML nella procedura ha esito negativo, il client riceverà erroneamente un valore -1.<br /><br /> Le applicazioni basate su questo comportamento errato avranno esito negativo.|  
|SERVERPROPERTY ('edizione')|Edizione del prodotto installata per l'istanza di [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Usare il valore di questa proprietà per determinare le funzionalità e i limiti, come il numero massimo di CPU, supportati dal prodotto installato.<br /><br /> In base all'edizione Enterprise installata, può restituire 'Enterprise Edition' o ' Enterprise Edition: Core-based Licensing'. Le edizioni Enterprise sono differenziate in base alla capacità di calcolo massima per una sola istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per altre informazioni sui limiti di capacità di calcolo in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], vedere [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).|  
|CREATE LOGIN|Il `CREATE LOGIN WITH PASSWORD = '` *password* `' HASHED` opzione non può essere usata con hash creati da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 7 o versioni precedenti.|  
|Operazioni CAST e CONVERT per `datetimeoffset`|Gli unici stili supportati nella conversione di tipi date e time in `datetimeoffset` sono 0 e 1. Tutti gli altri stili di conversione restituiscono l'errore 9809. Il codice seguente, ad esempio, restituisce un errore 9809.<br /><br /> `SELECT CONVERT(date, CAST('7070-11-25 16:25:01.00986 -02:07' as datetimeoffset(5)), 107);`|  
  
### <a name="dynamic-management-views"></a>DMV  
  
|visualizzazione|Descrizione|  
|----------|-----------------|  
|sys.dm_exec_requests|La colonna del comando viene modificata da `nvarchar(16)` a `nvarchar(32)`.|  
|sys.dm_os_memory_cache_counters|Sono state rinominate le colonne seguenti:<br /><br /> single_pages_kb è ora: <br />                          pages_kb<br /><br /> multi_pages_kb<br />                           è ora: pages_in_use_kb|  
|sys.dm_os_memory_cache_entries|La colonna pages_allocated_count colonna è stata rinominata pages_kb.|  
|sys.dm_os_memory_clerks|Multi_pages_kb la colonna è stata rimossa.<br /><br /> Single_pages_kb colonna colonne è stato rinominato pages_kb.|  
|sys.dm_os_memory_nodes|Sono state rinominate le colonne seguenti:<br /><br /> single_pages_kb è ora: <br />                            pages_kb<br /><br /> è ora multi_pages_kb: <br />                            foreign_committed_kb|  
|sys.dm_os_memory_objects|Le colonne seguenti sono state rinominate.<br /><br /> è ora pages_allocated_count:<br />                            pages_in_bytes<br /><br /> è ora max_pages_allocated_count: max_pages_in_bytes|  
|sys.dm_os_sys_info|Sono state rinominate le colonne seguenti:<br /><br /> è ora physical_memory_in_bytes: <br />                            physical_memory_kb<br /><br /> valore di bpool_commit_target è ora: <br />                            committed_target_kb<br /><br /> bpool_visible è ora: <br />                            visible_target_kb<br /><br /> è ora virtual_memory_in_bytes from sys: <br />                            virtual_memory_kb<br /><br /> è ora bpool_commited:<br />                            committed_kb|  
|sys.dm_os_workers|La colonna delle impostazioni locali è stata rimossa.|  
  
### <a name="catalog-views"></a>Viste del catalogo  
  
|visualizzazione|Descrizione|  
|----------|-----------------|  
|sys.data_spaces<br /><br /> sys.partition_schemes<br /><br /> sys.filegroups<br /><br /> sys.partition_functions|Una colonna nuova, is_system, è stata aggiunta a sys.data_spaces e a sys.partition_functions. sys.partition_schemes e sys.filegroups ereditano le colonne di sys.data_spaces.<br /><br /> Un valore 1 in questa colonna indica che l'oggetto viene usato per i frammenti dell'indice full-text.<br /><br /> In sys.partition_functions, sys.partition_schemes e sys.filegroups, la nuova colonna non è l'ultima. Rivedere le query esistenti basate sull'ordine delle colonne restituito da queste viste del catalogo.|  
  
### <a name="sql-clr-data-types-geometry-geography-and-hierarchyid"></a>Tipi di dati CLR SQL (hierarchyid, geometry e geography)  
 L'assembly **Microsoft.SqlServer.Types.dll**, che contiene i tipi di dati spaziali e il tipo hierarchyid, è stato aggiornato dalla versione 10.0 alla versione 11.0. È possibile che le applicazioni personalizzate che fanno riferimento a questo assembly abbiano esito negativo quando sussistono le condizioni seguenti.  
  
-   Quando si sposta un'applicazione personalizzata da un computer in cui [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] era stato installato in un computer in cui solo [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] è installato, l'applicazione avrà esito negativo perché la versione di cui viene fatto riferimento 10.0 del **SqlTypes** assembly non è presente. È possibile che venga visualizzato questo messaggio di errore: `"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`  
  
-   Quando si fa riferimento il **SqlTypes** assembly versione 11.0 e viene installata anche la versione 10.0, è possibile visualizzare questo messaggio di errore: `"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   Quando si fa riferimento il **SqlTypes** assembly versione 11.0 da un'applicazione personalizzata destinata a .NET 3.5, 4 o 4.5, l'applicazione avrà esito negativo perché SqlClient in base alla progettazione carica la versione 10.0 dell'assembly. Questo errore si verifica quando l'applicazione chiama uno dei metodi seguenti:  
  
    -   Metodo `GetValue` della classe `SqlDataReader`  
  
    -   Metodo `GetValues` della classe `SqlDataReader`  
  
    -   Operatore di indice parentesi quadre [] della classe `SqlDataReader`  
  
    -   Metodo `ExecuteScalar` della classe `SqlCommand`  
  
 È possibile risolvere questo problema usando uno dei metodi seguenti:  
  
-   È possibile risolvere questo problema nel codice chiamando il metodo `GetSqlBytes`, anziché i metodi Get elencati in precedenza, per recuperare i tipi di sistema CLR di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], come illustrato nell'esempio seguente:  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   È possibile risolvere questo problema usando il reindirizzamento degli assembly nel file di configurazione dell'applicazione, come illustrato nell'esempio seguente:  
  
    ```xml  
    <runtime>  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    <runtime>  
    ```  
  
-   È possibile risolvere questo problema nella stringa di connessione specificando il valore "SQL Server 2012" per l'attributo "Type System Version" per forzare il caricamento della versione 11.0 dell'assembly da parte di SqlClient. Questo attributo della stringa di connessione è disponibile unicamente in .NET 4.5 e versioni successive.  
  
-   È consigliabile includere il tag `assemblyBinding` nel tag `runtime`.  
  
### <a name="support-for-awe"></a>Supporto per AWE  
 Address Windowing Extensions (AWE) a 32 bit non è più supportato. Ciò potrebbe comportare un calo delle prestazioni nei sistemi operativi a 32 bit. Per installazioni che richiedono grandi quantità di memoria, eseguire la migrazione a un sistema operativo a 64 bit.  
  
### <a name="xquery-functions-are-surrogate-aware"></a>Le funzioni XQuery riconoscono i surrogati  
 L'indicazione W3C per gli operatori e le funzioni XQuery richiede il riconoscimento di una coppia di surrogati che rappresenti un carattere Unicode surrogato alto come un singolo glifo nella codifica UTF-16. Tuttavia, nelle versioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], le funzioni stringa non riconoscono le coppie di surrogati come singolo carattere. Alcune operazioni di stringa - ad esempio calcoli della lunghezza di stringa ed estrazioni delle sottostringhe, restituiscono risultati non corretti. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] supporta ora il formato UTF-16 e la gestione corretta di coppie di surrogati.  
  
 Il tipo di dati XML in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] consente unicamente coppie di surrogati con formati corretti. In alcune circostanze alcune funzioni possono tuttavia restituire ancora risultati non definiti o non previsti, poiché è possibile passare coppie di surrogati parziali o non valide alle funzioni XQuery come valori stringa. Si considerino i metodi seguenti per la generazione di valori stringa quando si usa XQuery in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Fornire un valore stringa costante come valore binario. Quando si usa questo metodo, è ancora possibile passare coppie di surrogati non valide o parziali.  
  
-   Fornire un valore stringa costante fornendo entità carattere. Quando si usa questo metodo, non è possibile passare coppie di surrogati non valide. Le funzioni XQuery richiedono un'entità a singolo carattere per il carattere di alto livello. Viene generato un errore se vengono fornite le entità carattere per i caratteri della coppia di surrogati.  
  
-   Importare valori esterni tramite **SQL: Column** oppure **SQL: variable**. Quando si usano questi metodi, è ancora possibile introdurre coppie di surrogati non valide o parziali.  
  
#### <a name="affected-xquery-functions-and-operators"></a>Funzioni e operatori XQuery interessati  
 Gli operatori e le funzioni XQuery seguenti gestiscono correttamente le coppie di surrogati UTF-16 in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]:  
  
-   **fn:string-length**. Tuttavia, se una coppia di surrogati non valide o parziali viene passata come argomento, il comportamento delle **lunghezza della stringa** è definito.  
  
-   **fn:substring**.  
  
-   **fn:contains**. Tuttavia, se una coppia di surrogati parziale viene passata come valore, **contiene** possono restituire risultati imprevisti, poiché potrebbe trovare la coppia di surrogati parziale contenuta nella coppia di surrogati con formato corretto.  
  
-   **fn:concat**. Tuttavia, se una coppia di surrogati parziale viene passata come valore, **concat** può generare coppie di surrogati non corrette o coppie di surrogati parziale.  
  
-   Gli operatori di confronto e il **ordinare in base a** clausola. Gli operatori di confronto includono +, \<, >, \<=, > = `eq`, `lt`, `gt`, `le`, e `ge`.  
  
#### <a name="distributed-query-calls-to-a-system-procedure"></a>Chiamate di query distribuite a una procedura di sistema  
 Le chiamate di query distribuite tramite `OPENQUERY` ad alcune procedure di sistema avranno esito negativo se chiamate da un server [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] a un altro. Si verifica se il [!INCLUDE[ssDE](../includes/ssde-md.md)] non è in grado di individuare i metadati per una procedura, Ad esempio `SELECT * FROM OPENQUERY(..., 'EXEC xp_loginfo')`.  
  
#### <a name="isolation-level-and-spresetconnection"></a>Livello di isolamento e sp_reset_connection  
 Il livello di isolamento per le connessioni viene gestito nel modo seguente dai driver client:  
  
-   Tutti i driver nativi (ODBC SNAC, MDAC) impostano il livello di isolamento (in base all'impostazione dell'app) su sp_reset_connection.  
  
-   Per ADO.NET essenzialmente si otterrà un livello di isolamento casuale a seconda della connessione che si ottiene dal pool (e se l'applicazione usa un livello di isolamento diverso). Poiché il pool ADO.NET può riciclare connessioni internamente e in modo trasparente, non è possibile prevedere cosa proverrà dal pool.  
  
-   Per il driver JDBC si ottiene lo stesso comportamento osservato per ADO.NET  
  
     Per ottenere quanto previsto, l'applicazione deve impostare sempre in modo esplicito il livello di isolamento dopo l'apertura della connessione.  
  
     La connessione JDBC può essere inserita in pool, pertanto l'applicazione potrebbe ricevere un livello di isolamento casuale senza esserne al corrente.  
  
 Per mantenere la compatibilità con le versioni precedenti, questo nuovo comportamento si applica solo ai client recenti a partire da TDS 7.4.  
  
#### <a name="backward-compatibility"></a>Backward Compatibility  
 **Nuovo comportamento dipende dal livello di compatibilità**  
  
 Le funzioni e gli operatori seguenti dimostrano il nuovo comportamento descritto in precedenza solo quando il livello di compatibilità è 110 o superiore:  
  
-   **fn:contains**.  
  
-   **fn:concat**.  
  
-   gli operatori di confronto e **ordinare in base a** clausola  
  
 **Nuovo comportamento dipende dello spazio dei nomi predefinito URI per le funzioni**  
  
 Le funzioni seguenti dimostrano il nuovo comportamento descritto in precedenza solo quando l'URI dello spazio dei nomi predefinito corrisponde allo spazio dei nomi nell'indicazione finale, vale a dire [ http://www.w3.org/2005/xpath-functions ](http://www.w3.org/2005/xpath-functions). Quando il livello di compatibilità è impostato su 110 o su un valore superiore, per impostazione predefinita [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] associa lo spazio dei nomi della funzione predefinita a questo spazio dei nomi. Tuttavia, queste funzioni dimostrano il nuovo comportamento quando questo spazio dei nomi viene usato indipendentemente dal livello di compatibilità.  
  
-   **fn:string-length**  
  
-   **fn:substring**  
  
##  <a name="KJKatmai"></a> Modifiche di rilievo in SQL Server 2008 o SQL Server 2008 R2  
 In questa sezione si illustrano le modifiche di rilievo introdotte in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Nessuna modifica è stata introdotta in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
### <a name="collations"></a>Regole di confronto  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|Nuove regole di confronto|In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] sono state introdotte nuove regole di confronto completamente allineate a quelle disponibili in Windows Server 2008. Queste 80 nuove regole di confronto presentano miglioramenti nell'aspetto linguistico e sono state segnalate con i riferimenti di versione *_100. Se si scelgono nuove regole di confronto per il server o il database, è necessario tenere presente che esiste la possibilità che non vengano riconosciute dai client con versioni di driver client precedenti. Le regole di confronto non riconosciute possono determinare la restituzione di errori da parte dell'applicazione. Prendere in considerazione le soluzioni seguenti:<br /><br /> Aggiornare il sistema operativo client affinché vengano aggiornate le regole di confronto del sistema sottostanti.<br /><br /> Se nel client è installato software client del database, è possibile applicare un aggiornamento dei servizi a tale software.<br /><br /> Scegliere regole di confronto esistenti di cui viene eseguito il mapping a una tabella codici nel client.|  
  
### <a name="common-language-runtime-clr"></a>Common Language Runtime (CLR)  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|Assembly CLR|Quando un database viene aggiornato a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], viene automaticamente installato l'assembly `Microsoft.SqlServer.Types` per il supporto dei nuovi tipi di dati. Le regole di Preparazione aggiornamento rilevano qualsiasi tipo di utente o assembly con nomi in conflitto. Viene quindi indicato di rinominare gli assembly in conflitto, nonché di rinominare qualsiasi tipo in conflitto o di usare nomi in due parti nel codice per fare riferimento al tipo di utente preesistente.<br /><br /> Se un aggiornamento del database rileva un assembly utente con nome in conflitto, rinominerà automaticamente l'assembly e metterà il database in modalità sospetta.<br /><br /> Se durante l'aggiornamento esiste un utente con nome in conflitto, non viene eseguita alcuna operazione. Dopo l'aggiornamento, esisteranno sia il tipo di utente obsoleto che il nuovo tipo di sistema. Il tipo di utente sarà disponibile solo tramite nomi in due parti.|  
|Assembly CLR|Con [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] viene installato .NET Framework 3.5 SP1, che consente di aggiornare le librerie nella Global Assembly Cache (GAC). Se in un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono registrate librerie non supportate, è possibile che venga arrestato il funzionamento dell'applicazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dopo l'aggiornamento a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Ciò si verifica in quanto le operazioni di gestione o aggiornamento delle librerie presenti nella GAC non determinano l'aggiornamento degli assembly che si trovano in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se un assembly è presente sia in un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sia nella GAC, le due copie relative devono corrispondere esattamente. Se non corrispondono, si verificherà un errore quando l'assembly verrà usato dalla funzionalità di integrazione con CLR di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [librerie di .NET Framework supportate](../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).<br /><br /> Dopo aver aggiornato il database, gestire o aggiornare la copia dell'assembly nei database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con l'istruzione ALTER ASSEMBLY. Per altre informazioni, vedere [articolo 949080 della Knowledge Base](https://go.microsoft.com/fwlink/?LinkId=154563).<br /><br /> Per rilevare l'eventuale uso di librerie .NET Framework non supportate nell'applicazione, eseguire la query seguente nel database:<br /><br /> `SELECT name FROM sys.assemblies WHERE clr_name LIKE '%publickeytoken=b03f5f7f11d50a3a,%';`|  
|Routine CLR|Se si usa la rappresentazione in funzioni CLR definite dall'utente, aggregazioni definite dall'utente o tipi definiti dall'utente (UDT), è possibile che nell'applicazione si verifichi l'errore 6522 dopo l'aggiornamento a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Gli scenari seguenti hanno esito positivo in [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] e negativo in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Per ogni scenario vengono fornite le soluzioni.<br /><br /> Una funzione CLR definita dall'utente, aggregazione definita dall'utente o il metodo di tipo definito dall'utente che utilizza la rappresentazione ha un parametro di tipo `nvarchar(max)`, `varchar(max)`, `varbinary(max)`, `ntext`, `text`, `image`, o un UDT di grandi dimensioni e non dispone di  **DataAccessKind. Read** attributo del metodo. Per risolvere questo problema, aggiungere il **DataAccessKind. Read** dell'attributo del metodo, ricompilare l'assembly e ridistribuire la routine e l'assembly.<br /><br /> Una funzione CLR con valori di tabella che dispone di un **Init** metodo che esegue la rappresentazione. Per risolvere questo problema, aggiungere il **DataAccessKind. Read** dell'attributo del metodo, ricompilare l'assembly e ridistribuire la routine e l'assembly.<br /><br /> Una funzione CLR con valori di tabella con una **FillRow** metodo che esegue la rappresentazione. Per risolvere questo problema, rimuovere la rappresentazione dal **FillRow** (metodo). Accedere a risorse esterne usando il **FillRow** (metodo). In alternativa, accedere a risorse esterne dal **Init** (metodo).|  
  
### <a name="dynamic-management-views"></a>DMV  
  
|visualizzazione|Descrizione|  
|----------|-----------------|  
|sys.dm_os_sys_info|Sono state rimosse le colonne cpu_ticks_in_ms e sqlserver_start_time_cpu_ticks.|  
|sys.dm_exec_query_resource_semaphoressys.dm_exec_query_memory_grants|La colonna resource_semaphore_id non è un ID univoco in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. La modifica può influire sulla risoluzione dei problemi relativi all'esecuzione di query. Per altre informazioni, vedere [DM exec_query_resource_semaphores &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql).|  
  
### <a name="errors-and-events"></a>Errori ed eventi  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|Errori di accesso|In [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] viene restituito l'errore 18452 quando viene usato un account di accesso SQL per connettersi a un server configurato per il solo uso dell'autenticazione di Windows. In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] viene invece restituito l'errore 18456.|  
  
### <a name="showplan"></a>Showplan  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|Showplan XML Schema|Una nuova **SeekPredicateNew** aggiunta dell'elemento Showplan XML schema e la sequenza xsd che lo contiene (**SqlPredicatesType**) viene convertito in un  **\<xsd: Choice >** elemento. Invece di uno o più **SeekPredicate** gli elementi, uno o più **SeekPredicateNew** elementi possono essere ora visualizzati in Showplan XML. I due elementi si escludono a vicenda. **SeekPredicate** viene mantenuto in Showplan XML schema per le versioni precedenti compatibilità; eseguire una query, tuttavia, i piani creati nel [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] può contenere il **SeekPredicateNew** elemento. Le applicazioni che prevedono per recuperare solo le **SeekPredicate** figlio dal nodo ShowPlanXML/BatchSequence/Batch/istruzioni/StmtSimple/QueryPlan/RelOp/IndexScan/SeekPredicates potrebbe non riuscire se il  **SeekPredicate** elemento non esiste. Riscrivere l'applicazione in modo che il **SeekPredicate** oppure **SeekPredicateNew** elemento in questo nodo. Per ulteriori informazioni, vedere .|  
|Showplan XML Schema|Una nuova **IndexKind** attributo viene aggiunto per il **ObjectType** tipo complesso nello schema Showplan XML. Le applicazioni che convalidano in modo esplicito i piani di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in base allo schema [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] non riusciranno.|  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|Evento ALTER_AUTHORIZATION_DATABASE DDL|Nelle [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], quando viene generato l'evento DDL ALTER_AUTHORIZATION_DATABASE, il valore 'object' viene restituito nel **ObjectType** elemento del xml EVENTDATA per questo evento quando il tipo di entità dell'entità a protezione diretta nella definizione di dati operazione Language (DDL) è un oggetto. In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] viene restituito il tipo effettivo, quale "table" o "function".|  
|CONVERT|Se uno stile non valido viene passato alla funzione CONVERT, viene restituito un errore quando il tipo di conversione è da binario a carattere o da carattere a binario. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] lo stile non valido è impostato sullo stile predefinito per conversioni da binario a carattere e da carattere a binario.|  
|Autorizzazioni GRANT/DENY/REVOKE EXECUTE per gli assembly|L'autorizzazione EXECUTE non può essere concessa, negata o revocata agli assembly. Tale autorizzazione non ha alcun effetto e ora causa un errore. È invece possibile concederla, negarla o revocarla a stored procedure o funzioni che fanno riferimento al metodo dell'assembly.|  
|Autorizzazioni GRANT/DENY/REVOKE per i tipi di sistema|Tali autorizzazioni non possono essere concesse, negate o revocate ai tipi di sistema. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] l'esecuzione di queste istruzioni ha esito positivo, ma senza alcun effetto. In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] viene restituito un errore.|  
|GROUP BY|La clausola GROUP BY non può contenere una sottoquery in un'espressione usata per l'elenco GROUP BY. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] questo era consentito. In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] viene restituito l'errore 144.<br /><br /> Ad esempio, il codice seguente avrà esito positivo in SQL Server 2005, ma esito negativo in SQL Server 2008.<br /><br /> `DECLARE @Test TABLE(a int NOT NULL);` <br /> `INSERT INTO @Test SELECT 1 union ALL SELECT 2;` <br /> `SELECT COUNT(*)` <br /> `FROM @Test` <br /> `GROUP BY CASE WHEN a IN (SELECT t.a FROM @Test AS t)` <br /> `THEN 1 ELSE 0` <br /> `END;`|  
|Clausola OUTPUT|Per impedire un comportamento non deterministico, la clausola OUTPUT non può fare riferimento a una colonna di una vista o di una funzione inline con valori di tabella se la colonna in questione viene definita mediante uno dei metodi seguenti:<br /><br /> Sottoquery.<br /><br /> Funzione definita dall'utente che esegue, o si presume esegua, l'accesso ai dati dell'utente o di sistema.<br /><br /> Colonna calcolata che contiene, nella relativa definizione, una funzione definita dall'utente che esegue l'accesso ai dati dell'utente o di sistema.<br /><br /> <br /><br /> Quando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] rileva una colonna di questo tipo nella clausola OUTPUT, viene generato l'errore 4186. Per altre informazioni, vedere [MSSQLSERVER_4186](../relational-databases/errors-events/mssqlserver-4186-database-engine-error.md).|  
|Clausola OUTPUT INTO|La tabella di destinazione della clausola OUTPUT INTO non può includere trigger abilitati.|  
|Opzione a livello di server precompute rank|Questa opzione non è supportata in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Modificare il prima possibile le applicazioni che usano questa caratteristica.|  
|READPAST - hint di tabella|Non è possibile specificare l'hint READPAST in Isolamento dello snapshot.<br /><br /> L'hint READPAST viene ignorato se l'opzione di database READ_COMMITED_SNAPSHOT o ALLOW_SNAPSHOT_ISOLATION è impostata su ON. Tuttavia, se si combina l'hint READPAST con READCOMMITTEDLOCK, il comportamento di READPAST è uguale a quello con l'hint di blocco READCOMMITTED.|  
|sp_helpuser|Sono stati modificati i nomi di colonna seguenti restituiti nel set di risultati della stored procedure sp_helpuser:<br /><br /> GroupName è ora:<br />                            RoleName<br /><br /> Nome_gruppo è ora:<br />                            Role_name<br /><br /> Group_id è ora:<br />                            Role_id<br /><br /> È ora Users_in_group:<br />                            Users_in_role|  
|Transparent Data Encryption|Transparent Data Encryption (TDE) viene eseguito al livello di I/O: la struttura della pagina non presenta crittografia in memoria e viene crittografata solo al momento della scrittura su disco della pagina. La crittografia viene applicata sia ai file di database sia ai file di log. Le applicazioni di terze parti, che non tengono conto del normale meccanismo di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per l'accesso alle pagine e che prevedono ad esempio l'analisi diretta dei file di dati e di log, non riusciranno se in un database viene usato TDE perché i dati contenuti in tali file sono crittografati. Applicazioni di questo tipo possono usare l'API di crittografia di Windows per sviluppare una soluzione per la decrittografia dei dati all'esterno di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
### <a name="xquery"></a>XQuery  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|Supporto di dati datetime|Nelle [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], i tipi di dati `xs:time`, `xs:date`, e `xs:dateTime` non è supportata sul fuso orario. Viene eseguito il mapping dei dati del fuso orario al fuso orario UTC. In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] presenta un comportamento conforme agli standard che determina le modifiche seguenti:<br /><br /> Vengono convalidati i valori senza fuso orario.<br /><br /> Viene mantenuto il fuso orario fornito o viene preservata l'assenza di un fuso orario.<br /><br /> Viene modificata la rappresentazione di archiviazione interna.<br /><br /> Viene aumentata la risoluzione dei valori archiviati.<br /><br /> Non sono consentiti anni negativi.<br /><br /> <br /><br /> Nota: Modificare le applicazioni e le espressioni XQuery per i nuovi valori di tipo di account.|  
|Espressioni XQuery e Xpath|In [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], i passaggi in un'espressione XQuery o XPath che iniziano con due punti (': ') sono consentiti. L'istruzione seguente, ad esempio, contiene un test di nome (`CTR02)` all'interno dell'espressione di percorso che inizia con due punti.<br /><br /> `SELECT FileContext.query('for n$ in //CTR return <C>{data )(n$/:CTR02)} </C>) AS Files FROM dbo.MyTable;`<br /><br /> In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] questo utilizzo non è consentito, in quanto non è conforme agli standard XML. Viene restituito l'errore 9341. Rimuovere i due punti iniziali o specificare un prefisso per il test del nome, ad esempio (n$/CTR02) o (n$/p1:CTR02).|  
  
### <a name="connecting"></a>Connecting  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|Connessione da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client usando SSL|Per connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client, le applicazioni che usano "SERVER=shortname; FORCE ENCRYPTION=true" con un certificato il cui Subjects specifichi nomi di dominio completi in passato hanno eseguito la connessione grazie a una convalida flessibile. SQL Server 2008 R2 migliora la sicurezza grazie all'applicazione di oggetti FQDN per i certificati. Per le applicazioni che si basano su una convalida flessibile è necessario eseguire una delle operazioni seguenti:<br /><br /> Usare il nome di dominio completo nella stringa di connessione.<br /><br /> -Questa opzione non richiede la ricompilazione dell'applicazione se la parola chiave SERVER della stringa di connessione viene configurata all'esterno dell'applicazione.<br /><br /> -Questa opzione non funziona per le applicazioni che dispongono di stringhe di connessione hardcoded.<br /><br /> -Questa opzione non funziona per le applicazioni che usano il mirroring del Database poiché il server con mirroring risponde con un nome semplice.|  
||Aggiungere un alias in modo da eseguire il mapping di shortname al nome di dominio completo.<br /><br /> -Questa opzione funziona anche per le applicazioni che dispongono di stringhe di connessione hardcoded.<br /><br /> -Questa opzione non funziona per le applicazioni che usano il mirroring del Database poiché il provider non cercano gli alias per i nomi partner di failover ricevuti.|  
||Ottenere un certificato emesso per shortname.<br /><br /> -Questa opzione funziona per tutte le applicazioni.|  

## <a name="Yukon"></a> Modifiche di rilievo in SQL Server 2005  

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>Vedere anche  
 [Funzionalità del motore di Database deprecate in SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)   
 [Modifiche apportate alle funzionalità del motore di Database in SQL Server 2014](../../2014/database-engine/behavior-changes-to-database-engine-features-in-sql-server-2014.md?view=sql-server-2014)   
 [Funzionalità del motore di Database non più utilizzate in SQL Server 2014](discontinued-database-engine-functionality-in-sql-server-2016.md?view=sql-server-2014)   
 [Compatibilità con le versioni precedenti del motore di database di SQL Server](sql-server-database-engine-backward-compatibility.md)   
 [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
 [Modifiche di rilievo nelle funzionalità degli strumenti di gestione in SQL Server 2014](breaking-changes-to-management-tools-features-in-sql-server-2014.md?view=sql-server-2014)  
  
