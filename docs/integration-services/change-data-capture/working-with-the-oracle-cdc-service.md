---
title: Uso del servizio Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 04be5896-2301-45f5-a8ce-5f4ef2b69aa5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1844396dfda42dd7a20292977b792dd731fbb3cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898935"
---
# <a name="working-with-the-oracle-cdc-service"></a>Utilizzo del servizio Oracle CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  In questa sezione vengono descritti alcuni concetti importanti relativi al servizio Oracle CDC. I concetti inclusi in questa sezione sono i seguenti:  
  
-   [Database MSXDBCDC](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_MSXDBCDC)  
  
     In questa sezione vengono descritte le tabelle incluse in questo database e ne viene sottolineata l'importanza per CDC.  
  
-   [Database CDC](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CDCdatabase)  
  
     In questa sezione viene fornita una breve descrizione dei database CDC. Questi database vengono creati utilizzando Oracle CDC Designer Console. Per ulteriori informazioni sui database CDC, vedere la documentazione inclusa con l'installazione di Oracle CDC Designer Console.  
  
-   [Utilizzo della riga di comando per configurare il servizio CDC](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CommandConfigCDC)  
  
     In questa sezione vengono descritti i comandi della riga di comando che è possibile utilizzare per configurare il servizio Oracle CDC.  
  
##  <a name="BKMK_MSXDBCDC"></a> Database MSXDBCDC  
 Il database MSXDBCDC (Microsoft External-Database CDC) è un database speciale necessario quando il servizio CDC per Oracle viene utilizzato con un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Non è possibile modificare il nome di questo database. Se nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] host è presente un database denominato MSXDBCDC che contiene tabelle diverse da quelle definite dal servizio CDC per Oracle, non è possibile utilizzare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] host.  
  
 Questo database viene principalmente utilizzato come:  
  
-   Registro di sistema dei servizi Oracle CDC associato a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Queste informazioni vengono utilizzate per i componenti di progettazione e configurazione del servizio e a supporto del coordinamento di più servizi CDC con lo stesso nome su nodi diversi su cui uno è quello attivo.  
  
-   Registro di sistema delle istanze di Oracle CDC contenute in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il servizio CDC che gestisce ogni istanza e la versione di configurazione utilizzata da ognuno. Queste informazioni sono equivalenti alla colonna **is_cdc_enabled** della tabella **sys.databases** del database master. Il servizio CDC analizza periodicamente la tabella **dbo.xdbcdc_databases** per identificare le modifiche apportate alla configurazione di CDC o all'elenco di istanze acquisite.  
  
-   Mantenere le stored procedure di proprietà di **sysadmin**che consentono di creare e gestire le istanze di CDC. Si tratta di procedure di sistema simili a quelle utilizzate per l'implementazione della funzionalità CDC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="creating-the-msxdbcdc-database"></a>Creazione del database MSXDBCDC  
 È necessario creare un database MSXDBCDC prima di definire il servizio Oracle CDC. È possibile creare un solo database MSXDBCDC in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il database MSXDBCDC viene creato quando si prepara un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per Oracle CDC. A tale scopo, è possibile utilizzare la console di configurazione del servizio Oracle CDC oppure eseguire uno script d creazione generato tramite Oracle CDC Service Configuration Console.  
  
 Il proprietario di questo database è l'amministratore del servizio Oracle CDC che può controllare tutte le istanze di Oracle CDC ospitate nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Vedere anche:**  
  
 [Procedura di preparazione di SQL Server per CDC](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
### <a name="the-msxdbcdc-database-tables"></a>Tabelle del database MSXDBCDC  
 In questa sezione vengono descritte le tabelle del database MSXDBCDC seguenti.  
  
-   [dbo.xdbcdc_trace](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_trace)  
  
-   [dbo.xdbcdc_databases](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_databases)  
  
-   [dbo.xdbcdc_services](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_services)  
  
###  <a name="BKMK_dboxdbcdc_trace"></a> dbo.xdbcdc_trace  
 In questa tabella vengono archiviate le informazioni relative al servizio Oracle CDC. Le informazioni archiviate in questa tabella includono modifiche allo stato rilevanti e record di traccia.  
  
 Il servizio Oracle CDC scrive i record degli errori e alcuni dei record di informazioni sia nel registro eventi di Windows sia nella tabella di traccia. Qualora la tabella di traccia non risulti accessibile, le informazioni degli errori sono accessibili dal registro eventi.  
  
 Di seguito vengono descritti gli elementi inclusi nella tabella **dbo.xdbcdc_trace** .  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|TIMESTAMP|Timestamp UTC esatto della scrittura del record di traccia.|  
|tipo|Contiene uno dei valori seguenti.<br /><br /> errore<br /><br /> INFO<br /><br /> traccia|  
|node|Nome del nodo in cui è stato scritto il record.|  
|status|Codice di stato utilizzato dalla tabella dello stato.|  
|sub_status|Codice di stato secondario utilizzato dalla tabella dello stato.|  
|status_message|Messaggio di stato utilizzato dalla tabella dello stato.|  
|origine|Nome del componente di Oracle CDC che ha prodotto il record di traccia.|  
|text_data|Dati di testo aggiuntivi per i casi in cui l'errore o il record di traccia contiene un payload testuale.|  
|binary_data|Dati binari aggiuntivi per i casi in cui l'errore o il record di traccia contiene un payload binario.|  
  
 L'istanza di Oracle CDC eliminerà righe della tabella di traccia obsolete in base ai criteri di conservazione delle tabelle di modifica.  
  
###  <a name="BKMK_dboxdbcdc_databases"></a> dbo.xdbcdc_databases  
 Questa tabella contiene i nomi del servizio CDC per i database Oracle CDC nell'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ogni database corrisponde a un'istanza di Oracle CDC. Il servizio Oracle CDC utilizza questa tabella per determinare quali istanze avviare o arrestare e quali riconfigurare.  
  
 Nella tabella seguente vengono descritti gli elementi inclusi nella tabella **dbo.xdbcdc_databases** .  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|NAME|Nome del database Oracle nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|config_version|Timestamp (UTC) per l'ultima modifica della tabella **xdbcdc_config** del database CDC corrispondente o timestamp (UTC) per la riga corrente di questa tabella.<br /><br /> Il trigger UPDATE applica un valore di GETUTCDATE () per questo elemento. Tramite**config_version** il servizio CDC identifica l'istanza di CDC che deve essere controllata per la modifica della configurazione o per l'abilitazione o la disabilitazione.|  
|cdc_service_name|Tramite questo elemento è possibile determinare quale servizio Oracle CDC gestisce il database Oracle selezionato.|  
|enabled|Indica se l'istanza di Oracle CDC è attiva (1) o disabilitata (0). All'avvio del servizio Oracle CDC verranno avviate solo le istanze contrassegnate come abilitate (1).<br /><br /> **Nota**: un'istanza di Oracle CDC può essere disabilitata in seguito a un errore non ripetibile. In questo caso, è necessario riavviare manualmente l'istanza dopo avere risolto l'errore.|  
  
###  <a name="BKMK_dboxdbcdc_services"></a> dbo.xdbcdc_services  
 In questa tabella sono elencati i servizi CDC associati all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] host. Questa tabella viene utilizzata da CDC Designer Console per determinare l'elenco di servizi CDC configurati per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] locale. Viene inoltre utilizzata dal servizio CDC per garantire che solo un servizio Windows in esecuzione gestisca un determinato nome di servizio CDC.  
  
 Di seguito vengono descritti gli elementi dello stato di acquisizione inclusi nella tabella **dbo.xdbcdc_databases** .  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|cdc_service_name|Nome del servizio Oracle CDC (nome del servizio Windows).|  
|cdc_service_sql_login|Nome dell'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato dal servizio Oracle CDC per la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un nuovo utente SQL denominato cdc_service viene creato e associato al nome di questo account di accesso, dopodiché viene aggiunto come membro dei ruoli predefiniti del database db_ddladmin, db_datareader e db_datawriter per ogni database CDC gestito dal servizio.|  
|ref_count|Tramite questo elemento viene contato il numero di computer in cui è installato lo stesso servizio Oracle CDC. A ogni aggiunta di un servizio Oracle CDC con lo stesso nome il conteggio aumenta, mentre diminuisce alla rimozione di un servizio. Quando il conteggio raggiunge lo zero, questa riga viene eliminata.|  
|active_service_node|Nome del nodo Windows che attualmente gestisce il servizio CDC. Quando il servizio viene arrestato correttamente, questa colonna viene impostata su null, per indicare che non vi sono più servizi attivi.|  
|active_service_heartbeat|Tramite questo elemento si tiene traccia del servizio CDC corrente per determinare se è ancora attivo.<br /><br /> Questo elemento viene aggiornato con il timestamp UTC del database corrente per il servizio CDC attivo a intervalli regolari. L'intervallo predefinito è 30 secondi, anche se può essere configurato.<br /><br /> Quando un servizio CDC in sospeso rileva che l'heartbeat non è stato aggiornato dopo il superamento dell'intervallo configurato, il servizio in sospeso tenta di assumere il ruolo del servizio CDC attivo.|  
|opzioni|Questo elemento specifica le opzioni secondarie, ad esempio traccia o ottimizzazione. Presenta il formato **name[=value][; ]**. La stringa delle opzioni utilizza la stessa semantica della stringa di connessione ODBC. Se l'opzione è Boolean (con un valore yes/no), il valore può includere solo il nome.<br /><br /> trace può avere i valori seguenti.<br /><br /> **true**<br /><br /> **on**<br /><br /> **false**<br /><br /> **off**<br /><br /> **\<nome classe[,nome classe>]**<br /><br /> <br /><br /> Il valore predefinito è **false**.<br /><br /> **service_heartbeat_interval** è l'intervallo di tempo (in secondi) entro il quale il servizio può aggiornare la colonna active_service_heartbeat. Il valore predefinito è **30**. Il valore massimo è **3600**.<br /><br /> **service_config_polling_interval** è l'intervallo di polling (in secondi) entro il quale il servizio CDC deve individuare eventuali modifiche apportate alla configurazione. Il valore predefinito è **30**. Il valore massimo è **3600**.<br /><br /> **sql_command_timeout** è il timeout comando che funziona con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il valore predefinito è **1**. Il valore massimo è **3600**.|  
||  
  
### <a name="the-msxdbcdc-database-stored-procedures"></a>Stored procedure del database MSXDBCDC  
 In questa sezione vengono descritte le stored procedure del database MSXDBCDC seguenti.  
  
-   [dbo.xcbcdc_reset_db(Database Name)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxcbcdc_reset_db)  
  
-   [dbo.xdbcdc_disable_db(dbname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_disable_db)  
  
-   [dbo.xcbcdc_add_service(svcname,sqlusr)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxcbcdc_add_service)  
  
-   [dbo.xdbcdc_start(dbname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_start)  
  
-   [dbo.xdbcdc_stop(dbname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_stop)  
  
###  <a name="BKMK_dboxcbcdc_reset_db"></a> dbo.xcbcdc_reset_db(Database Name)  
 Tramite questa procedura è possibile cancellare i dati di un'istanza di Oracle CDC. Viene utilizzata:  
  
-   Per riavviare l'acquisizione dei dati ignorando i dati precedenti, ad esempio in seguito a un recupero del database di origine o a un periodo di inattività in cui alcuni dei log delle transazioni di Oracle non sono disponibili.  
  
-   Quando lo stato CDC risulta danneggiato, in particolare nei dati cdc.*tables.  
  
 Tramite la stored procedure **dbo.xcbcdc_reset_db** è possibile eseguire queste operazioni:  
  
-   Arrestare l'istanza di CDC, se attiva.  
  
-   Troncare le tabelle delle modifiche, la tabella **cdc_lsn_mapping** e la tabella **cdc_ddl_history** .  
  
-   Cancellare la tabella **cdc_xdbcdc_state** .  
  
-   Cancellare la colonna start_lsn per ogni riga di **cdc_change_table**.  
  
 Per poter usare la stored procedure **dbo.xcbcdc_reset_db** , l'utente deve essere un membro del ruolo del database **db_owner** per il database dell'istanza di CDC da denominare oppure un membro del ruolo predefinito del server **sysadmin** o **serveradmin** .  
  
 Per altre informazioni sulle tabelle CDC, vedere *Database CDC* nel sistema della Guida di CDC Designer Console.  
  
###  <a name="BKMK_dboxdbcdc_disable_db"></a> dbo.xdbcdc_disable_db(dbname)  
 Tramite la stored procedure **dbo.xcbcdc_disable_db** è possibile eseguire l'operazione seguente:  
  
-   Rimuovere la voce per il database CDC selezionato nella tabella MSXDBCDC.xdbcdc_databases.  
  
 Per poter usare la stored procedure **dbo.xcbcdc_disable_db** , l'utente deve essere un membro del ruolo del database **db_owner** per l'istanza di CDC da denominare oppure un membro del ruolo predefinito del server **sysadmin** o **serveradmin** .  
  
 Per ulteriori informazioni sulle tabelle CDC, vedere Database CDC nel sistema della Guida di CDC Designer Console.  
  
###  <a name="BKMK_dboxcbcdc_add_service"></a> dbo.xcbcdc_add_service(svcname,sqlusr)  
 Tramite la stored procedure **dbo.xcbcdc_add_service** è possibile aggiungere una voce alla tabella **MSXDBCDC.xdbcdc_services** e un incremento di uno alla colonna ref_count per il nome del servizio nella tabella **MSXDBCDC.xdbcdc_services** . Quando **ref_count** è pari a 0, la riga viene eliminata.  
  
 Per usare la stored procedure **dbo.xcbcdc_add_service\<nome servizio, nome utente>**, l'utente deve essere un membro del ruolo del database **db_owner** per l'istanza di CDC da rinominare oppure un membro del ruolo predefinito del server **sysadmin** o **serveradmin**.  
  
###  <a name="BKMK_dboxdbcdc_start"></a> dbo.xdbcdc_start(dbname)  
 Tramite la stored procedure **dbo.xdbcdc_start** è possibile inviare una richiesta di avvio al servizio CDC che gestisce l'istanza di CDC selezionata per avviare l'elaborazione delle modifiche.  
  
 Per poter usare la stored procedure **dbo.xcdcdc_start** , l'utente deve essere un membro del ruolo del database **db_owner** per l'istanza di CDC da denominare oppure un membro del ruolo predefinito del server **sysadmin** o **serveradmin** per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="BKMK_dboxdbcdc_stop"></a> dbo.xdbcdc_stop(dbname)  
 Tramite la stored procedure **dbo.xdbcdc_stop** è possibile inviare una richiesta di arresto al servizio CDC che gestisce l'istanza di CDC selezionata per arrestare l'elaborazione delle modifiche.  
  
 Per poter usare la stored procedure **dbo.xcdcdc_stop** , l'utente deve essere un membro del ruolo del database **db_owner** per l'istanza di CDC da denominare oppure un membro del ruolo predefinito del server **sysadmin** o **serveradmin** per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="BKMK_CDCdatabase"></a> Database CDC  
 Ogni istanza di Oracle CDC utilizzata in un servizio CDC è associata a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specifico denominato database CDC. Questo database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è ospitato nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associata a un servizio Oracle CDC.  
  
 Il database CDC contiene uno schema cdc speciale. Il servizio Oracle CDC usa questo schema con i nomi di tabella con prefisso **xdbcdc_**. Questo schema viene utilizzato a scopo di sicurezza e coerenza.  
  
 Sia i database CDC sia l'istanza di Oracle CDC vengono creati tramite Oracle CDC Designer Console. Per ulteriori informazioni sui database CDC, vedere la documentazione inclusa con l'installazione di Oracle CDC Designer Console.  
  
##  <a name="BKMK_CommandConfigCDC"></a> Utilizzo della riga di comando per configurare il servizio CDC  
 È possibile utilizzare il programma del servizio Oracle CDC (xdbcdcsvc.exe) dalla riga di comando. Il programma del servizio CDC è un file eseguibile di Windows a 32 o 64 bit nativo.  
  
 **Vedere anche**  
  
 [Procedura per l'uso dell'interfaccia della riga di comando del servizio CDC](../../integration-services/change-data-capture/how-to-use-the-cdc-service-command-line-interface.md)  
  
### <a name="service-program-commands"></a>Comandi del programma del servizio  
 In questa sezione vengono descritti i comandi da utilizzare per la configurazione del servizio CDC.  
  
-   [File di configurazione](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_config)  
  
-   [Create](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_create)  
  
-   [Elimina](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_delete)  
  
###  <a name="BKMK_config"></a> File di configurazione  
 Utilizzare `Config` per aggiornare la configurazione di un servizio Oracle CDC da uno script. Il comando può essere utilizzato per aggiornare solo parti specifiche della configurazione del servizio CDC, ad esempio solo la stringa di connessione senza conoscere la password della chiave asimmetrica. Il comando deve essere eseguito dall'amministratore di un computer. Di seguito è riportato un esempio del comando `Config` .  
  
```  
"<path>xdbcdcsvc.exe" config  
     <cdc-service-name>  
     [connect= <sql-server-connection-string>]  
     [key= <asym-key-password>]  
     [svcacct= <windows-account> <windows-password>]  
     [sqlacct= <sql-username> <sql-password>]  
  
```  
  
 Dove:  
  
 **cdc-service-name** è il nome del servizio CDC da aggiornare. Parametro obbligatorio.  
  
 **sql-server-connection-string** è la stringa di connessione da aggiornare. Se la stringa di connessione contiene spazi o virgolette, deve essere racchiusa tra virgolette doppie ("). Per le virgolette incorporate, è necessario utilizzare caratteri di escape raddoppiando le virgolette.  
  
 **asym-key-password** è la password da aggiornare.  
  
 **windows-account**e **windows-password** sono le credenziali dell'account di Windows per il servizio da aggiornare.  
  
 **sql-username**e **sql-password** sono le credenziali di autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da aggiornare. Se per sqlacct non sono stati specificati password e nome utente, la connessione tra il servizio Oracle CDC e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene effettuata tramite l'autenticazione di Windows.  
  
 **Nota**: qualsiasi parametro contenente spazi o virgolette doppie deve essere racchiuso tra virgolette doppie ("). Le virgolette doppie incorporate devono essere raddoppiate, ad esempio per usare **"A#B" D** come password immettere **""A#B"" D"**.  
  
###  <a name="BKMK_create"></a> Create  
 Utilizzare `Create` per creare un servizio Oracle CDC da uno script. Il comando deve essere eseguito dall'amministratore di un computer. Di seguito è riportato un esempio del comando `Create` :  
  
```  
"<path>xdbcdcsvc.exe" create  
     <cdc-service-name>  
     [connect= "<sql-server-connection-string>"]  
     [key= <asym-key-password>]  
     [svcacct <windows-account> <windows-password>]  
     [sqlacct <sql-username> <sql-password>]  
```  
  
 Dove:  
  
 **cdc-service-name** è il nome del servizio appena creato. Se è già presente un servizio con questo nome, viene restituito un errore. Non utilizzare nomi lunghi o nomi con spazi. I caratteri "/" e "\\" non sono caratteri validi per il nome di un servizio. Parametro obbligatorio.  
  
 **sql-server-connection-string** è la stringa di connessione da usare per connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associata al nuovo servizio Oracle CDC.  
  
 **asym-key-password** è la password che protegge la chiave asimmetrica usata per l'archiviazione delle credenziali di log mining del database di origine.  
  
 **windows-account**e **windows-password** sono il nome dell'account e la password associati al servizio Oracle CDC creato.  
  
 **sql-username**e **sql-password** sono il nome dell'account e la password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usati per la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se entrambi questi parametri sono vuoti, la connessione tra il servizio CDC per Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene effettuata utilizzando l'autenticazione di Windows.  
  
 **Nota**: qualsiasi parametro contenente spazi o virgolette doppie deve essere racchiuso tra virgolette doppie ("). Le virgolette doppie incorporate devono essere raddoppiate, ad esempio per usare **"A#B" D** come password immettere **""A#B"" D"**.  
  
###  <a name="BKMK_delete"></a> Elimina  
 Utilizzare `Delete` per eliminare il servizio Oracle CDC da uno script. Questo comando deve essere eseguito dall'amministratore di un computer. Di seguito è riportato un esempio del comando `Delete` .  
  
```  
"<path>xdbcdcsvc.exe" delete  
    <cdc-service-name>  
  
```  
  
 Dove:  
  
 **cdc-service-name** è il nome del servizio CDC da eliminare.  
  
 **Nota**: qualsiasi parametro contenente spazi o virgolette doppie deve essere racchiuso tra virgolette doppie ("). Le virgolette doppie incorporate devono essere raddoppiate, ad esempio per usare **"A#B" D** come password immettere **""A#B"" D"**.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di utilizzo dell'interfaccia della riga di comando del servizio CDC](../../integration-services/change-data-capture/how-to-use-the-cdc-service-command-line-interface.md)   
 [Procedura di preparazione di SQL Server per CDC](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
  
