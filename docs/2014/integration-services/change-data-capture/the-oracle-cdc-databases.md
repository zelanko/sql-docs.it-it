---
title: Database Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a96486e9-f79b-4b24-bfaf-56203dd0e435
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7e35293fb7f59475ebdcfea70c1b27d4798e3b93
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370173"
---
# <a name="the-oracle-cdc-databases"></a>Database Oracle CDC
  Un'istanza di Oracle CDC è associata a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dallo stesso nome nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione. Questo database è denominato database Oracle CDC o CDC.  
  
 Il database CDC viene creato e configurato utilizzando la Oracle CDC Designer Console e contiene gli elementi seguenti:  
  
-   Uno schema `cdc` creato abilitando il database per SQL Server CDC.  
  
-   Un set di tabelle **cdc.xdbcdc_xxxx** utilizzate dall'istanza di Oracle CDC.  
  
-   Un set di tabelle mirror vuote con le definizioni delle tabelle acquisite nel database Oracle di origine.  
  
-   Un set di tabelle delle modifiche e funzioni di accesso alle modifiche generate dal meccanismo di SQL Server CDC e identiche a quelle utilizzate nel normale SQL Server CDC non Oracle.  
  
 Lo schema `cdc` è inizialmente accessibile solo ai membri del ruolo predefinito del database **dbowne** . L'accesso alle tabelle delle modifiche e alle funzioni di modifica è determinato dallo stesso modello di sicurezza di SQL Server CDC. Per altre informazioni sul modello di sicurezza, vedere [Modello di sicurezza](https://go.microsoft.com/fwlink/?LinkId=231151).  
  
## <a name="creating-the-cdc-database"></a>Creazione del database CDC  
 Nella maggior parte dei casi, il database CDC viene creato utilizzando la console di progettazione di CDC, ma può anche essere creato con uno script di distribuzione CDC generato utilizzando CDC Designer Console. L'amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può modificare le impostazioni del database se necessario, per elementi quali l'archiviazione, la sicurezza o la disponibilità.  
  
 Per altre informazioni sull'utilizzo di CDC Designer Console per creare le tabelle di database e gli script necessari, vedere [Utilizzare la New Instance Wizard](use-the-new-instance-wizard.md).  
  
## <a name="cdc-database-user-roles"></a>Ruoli utente del database CDC  
 Quando un database CDC viene creato e abilitato per CDC, un utente del database denominato **cdc_service** viene creato nel database CDC e associato all'account di accesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con cui è stato configurato il servizio Oracle CDC. Questo utente viene impostato come membro dei ruoli del database **db_datareader**, **db_datawriter**e **db_ddladmin** . Se l'account di accesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è anche associato all'utente `dbo` , l'utente **cdc_service** non viene creato.  
  
 Questa assegnazione di ruolo consente al servizio Oracle CDC di aggiornare le tabelle in base allo schema `cdc` con i dati acquisiti e le informazioni di controllo.  
  
 Quando viene creato un database CDC e vengono impostate le tabelle Oracle dell'origine CDC, il proprietario del database CDC può concedere l'autorizzazione SELECT delle tabelle mirror e definire ruoli di controllo di SQL Server CDC per controllare chi accede ai dati delle modifiche.  
  
## <a name="mirror-tables"></a>Tabelle mirror  
 Per ogni tabella acquisita, \<nome-schema>\<.nome-tabella>, nel database di origine Oracle, viene creata una tabella vuota analoga nel database CDC, con lo stesso nome di schema e di tabella. Non è possibile acquisire tabelle di origine Oracle con il nome di schema `cdc` (senza distinzione tra maiuscole e minuscole) perché lo schema `cdc` in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è riservato a SQL Server CDC.  
  
 Le tabelle mirror sono vuote; in esse non vengono archiviati dati. Vengono utilizzate per abilitare l'infrastruttura di SQL Server CDC standard utilizzata dall'istanza di Oracle CDC. Per evitare l'inserimento o l'aggiornamento di dati nelle tabelle mirror, tutte le operazioni UPDATE, DELETE e INSERT sono negate per PUBLIC. Ciò impedisce la modifica delle tabelle.  
  
## <a name="access-to-change-data"></a>Accesso ai dati delle modifiche  
 Dato il modello di sicurezza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per ottenere accesso ai dati delle modifiche associati a un'istanza di acquisizione, è necessario concedere all'utente l'accesso `select` a tutte le colonne acquisite della tabella mirror associata (le autorizzazioni di accesso alle tabelle Oracle originali non forniscono accesso alle tabelle delle modifiche in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Per informazioni sul modello di sicurezza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Modello di sicurezza](https://go.microsoft.com/fwlink/?LinkId=231151).  
  
 Se, inoltre, al momento della creazione dell'istanza di acquisizione viene specificato un ruolo di controllo, il chiamante deve essere anche un membro del ruolo di controllo specificato. Le altre funzioni generali di Change Data Capture per l'accesso ai metadati sono accessibili a tutti gli utenti del database tramite il ruolo PUBLIC, sebbene l'accesso ai metadati restituiti sia in genere controllato utilizzando l'accesso SELECT alle tabelle di origine sottostanti e tramite l'appartenenza a qualsiasi ruolo di controllo definito.  
  
 È possibile leggere i dati delle modifiche chiamando funzioni speciali basate su tabelle generate dal componente SQL Server CDC alla creazione di un'istanza di acquisizione. Per altre informazioni su questa funzione, vedere [Funzioni Change Data Capture (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152).  
  
 L'accesso ai dati CDC tramite il componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CDC di origine è soggetto alle stesse regole.  
  
## <a name="the-cdc-database-tables"></a>Tabelle del database CDC  
 In questa sezione vengono descritte le tabelle seguenti del database CDC.  
  
-   [Tabelle delle modifiche (_CT)](the-oracle-cdc-databases.md#bkmk_change_tables_ct)  
  
-   [cdc.lsn_time_mapping](the-oracle-cdc-databases.md#bkmk_cdclsn_time_mapping)  
  
-   [cdc.xdbcdc_config](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_config)  
  
-   [cdc.xdbcdc_state](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_state)  
  
-   [cdc.xdbcdc_trace](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_trace)  
  
-   [cdc.xdbcdc_staged_transactions](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_staged_transactions)  
  
###  <a name="BKMK_Change_Tables_CT"></a> Tabelle delle modifiche (_CT)  
 Le tabelle delle modifiche vengono create dalle tabelle mirror. Contengono i dati delle modifiche acquisiti dal database Oracle. Le tabelle sono denominate secondo la convenzione seguente:  
  
 **[cdc].[\<capture-instance>_CT]**  
  
 Quando l'acquisizione è abilitata inizialmente per la tabella `<schema-name>.<table-name>`, il nome dell'istanza di acquisizione predefinito è `<schema-name>_<table-name>`. Ad esempio, il nome dell'istanza di acquisizione predefinito per la tabella Oracle HR.EMPLOYEES è HR_EMPLOYEES e la tabella delle modifiche associata è [cdc]. [HR_EMPLOYEES_CT].  
  
 Le scritture nelle tabelle di acquisizione sono eseguite dall'istanza di Oracle CDC. Tali tabelle vengono lette utilizzando funzioni speciali con valori di tabella generate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alla creazione dell'istanza di acquisizione. Ad esempio, `fn_cdc_get_all_changes_HR_EMPLOYEES`. Per altre informazioni su queste funzioni CDC, vedere [Funzioni Change Data Capture (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=231152).  
  
###  <a name="BKMK_cdclsn_time_mapping"></a> cdc.lsn_time_mapping  
 La tabella **[cdc].[lsn_time_mapping]** viene generata dal componente SQL Server CDC. L'utilizzo di tale tabella con Oracle CDC è diverso dall'utilizzo normale.  
  
 Per Oracle CDC, i valori LSN archiviati in questa tabella sono basati sul valore System Change Number (SCN) Oracle associato alla modifica. I primi 6 byte del valore LSN sono il numero SCN Oracle originale.  
  
 Inoltre, quando si utilizza Oracle CDC, nelle colonne dell'ora (`tran_begin_time` e `tran_end_time`) viene archiviata l'ora UTC della modifica anziché l'ora locale come accade con il normale servizio SQL Server CDC. In questo modo, le modifiche dell'ora legale non influiscono sui dati archiviati in lsn_time_mapping.  
  
###  <a name="BKMK_cdcxdbcdc_config"></a> cdc.xdbcdc_config  
 In questa tabella sono contenuti i dati di configurazione per l'istanza di Oracle CDC. La tabella viene aggiornata tramite CDC Designer Console. La tabella ha una sola riga.  
  
 Nella tabella seguente sono descritte le colonne della tabella **cdc.xdbcdc_config** .  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|version|Tiene traccia della versione della configurazione dell'istanza di CDC. Viene aggiornato ogni volta che si aggiorna la tabella e ogni volta che si aggiunge una nuova istanza di acquisizione o si rimuove un'istanza di acquisizione esistente.|  
|connect_string|Stringa di connessione Oracle. Esempio di base:<br /><br /> `<server>:<port>/<instance>` (ad esempio `erp.contoso.com:1521/orcl`).<br /><br /> Nella stringa di connessione è anche possibile specificare un descrittore della connessione di rete Oracle, ad esempio `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`.<br /><br /> Se si utilizza un server di elenchi in linea o nomi TNS, la stringa di connessione può essere il nome della connessione.<br /><br /> Per altre informazioni sulle stringhe di connessione Oracle, vedere [https://go.microsoft.com/fwlink/?LinkId=231153](https://go.microsoft.com/fwlink/?LinkId=231153) per dettagli sulle stringhe di connessione al database Oracle per l'istanza di Oracle Instant Client usata dal servizio Oracle CDC.|  
|use_windows_authentication|Valore booleano che può essere:<br /><br /> **0**: Vengono forniti un nome utente di Oracle e una password per l'autenticazione (predefinito)<br /><br /> **1**: L'autenticazione di Windows viene utilizzato per connettersi al database Oracle. È possibile utilizzare questa opzione solo se il database Oracle è configurato per l'utilizzo dell'autenticazione di Windows.|  
|username|Nome dell'utente del database Oracle di log mining. È obbligatorio solo se **use_windows_authentication = 0**.|  
|password|Password dell'utente del database Oracle di log mining. È obbligatorio solo se **use_windows_authentication = 0**.|  
|transaction_staging_timeout|Tempo, in secondi, durante il quale una transazione Oracle viene mantenuta in memoria prima di essere scritta nella tabella **cdc.xdbcdc_staged_transactions** . Il valore predefinito è 120 secondi.|  
|memory_limit|Limite della quantità di memoria, in MB, che è possibile utilizzare per la memorizzazione nella cache di dati in memoria. Con un'impostazione inferiore vengono scritte più transazioni nella tabella **cdc.xdbcdc_staged_transactions** . Il valore predefinito è 50 MB.|  
|opzioni|Un elenco di opzioni nel formato nome[=valore] [; ] - viene utilizzato per specificare opzioni secondarie, ad esempio traccia o ottimizzazione. Per una descrizione delle opzioni disponibili, vedere la tabella di seguito.|  
  
 Nella tabella seguente vengono descritte le opzioni disponibili.  
  
|nome|Impostazione predefinita|Min|Max|Statico|Descrizione|  
|----------|-------------|---------|---------|------------|-----------------|  
|traccia|False|-|-|False|Valori disponibili:<br /><br /> **True**<br /><br /> **False**<br /><br /> **on**<br /><br /> **off**|  
|cdc_update_state_interval|10|1|120|False|La dimensione in Kbyte dei blocchi di memoria allocati per una transazione; una transazione può allocare più di un blocco. Vedere la colonna memory_limit nella tabella [cdc.xdbcdc_config](the-oracle-cdc-databases.md#bkmk_cdcxdbcdc_config) .|  
|target_max_batched_transactions|100|1|1000|True|Numero massimo di transazioni Oracle che è possibile elaborare come una transazione nell'aggiornamento delle tabelle SQL Server CT.|  
|target_idle_lsn_update_interval|10|0|1|False|L'intervallo, in secondi, per l'aggiornamento della tabella **lsn_time_mapping** quando nelle tabelle acquisite non è presente alcuna attività.|  
|trace_retention_period|24|1|24*31|False|Periodo di tempo, in ore, durante cui i messaggi vengono mantenuti nella tabella di traccia.|  
|sql_reconnect_interval|2|2|3600|False|Periodo di tempo, in secondi, che deve trascorrere prima della riconnessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo intervallo viene usato in aggiunta al timeout della connessione del client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|sql_reconnect_limit|-1|-1|-1|False|Numero massimo di riconnessioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il valore predefinito -1 indica che vengono effettuati tentativi di riconnessione fino all'arresto del processo.|  
|cdc_restart_limit|6|-1|3600|False|Nella maggior parte dei casi, tramite il servizio CDC un'istanza di CDC terminata in modo anomalo viene riavviata automaticamente. Con questa proprietà si definisce il numero di errori all'ora dopo i quali viene arrestato il riavvio dell'istanza. Il valore -1 indica che l'istanza deve essere sempre riavviata.<br /><br /> Dopo qualsiasi aggiornamento della tabella di configurazione, ricomincia il riavvio dell'istanza.|  
|cdc_memory_report|0|0|1000|False|Se il valore del parametro è stato modificato, nella tabella di traccia viene stampato il report della memoria dell'istanza di CDC.|  
|target_command_timeout|600|1|3600|False|Timeout del comando utilizzato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|source_character_set|-|-|-|True|Può essere impostato su una specifica codifica Oracle da utilizzare in sostituzione della tabella codici del database Oracle. Può essere utile quando l'effettiva codifica dei dati character in uso è diversa da quella espressa dalla tabella codici del database Oracle.|  
|source_error_retry_interval|30|1|3600|False|Viene utilizzato prima di ripetere il tentativo in caso di diversi errori, ad esempio un errore di connessione o una temporanea mancanza di sincronizzazione tra le tabelle di sistema.|  
|source_prefetch_size|100|1|10000|True|Dimensioni del batch di prelettura.|  
|source_max_tables_in_query|100|1|10000|True|Numero massimo di tabelle nella clausola WHERE prima di passare alla lettura del log Oracle senza l'applicazione di filtri alle tabelle.|  
|source_read_retry_interval|2|1|3600|False|Periodo di tempo di attesa dell'origine prima di tentare di leggere nuovamente i log delle transazioni Oracle al raggiungimento di EOF.|  
|source_reconnect_interval|30|1|3600|False|Tempo, in secondi, di attesa prima di tentare la riconnessione al database di origine.|  
|source_reconnect_limit|-1|-1||False|Numero massimo di riconnessioni al database di origine. Il valore predefinito -1 indica che vengono effettuati tentativi di riconnessione fino all'arresto del processo.|  
|source_command_timeout|30|1|3600|False|Timeout della connessione utilizzato con Oracle.|  
|source_connection_timeout|30|1|3600|False|Timeout della connessione utilizzato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|trace_data_errors|True|-|-|False|Proprietà di tipo Boolean. Se il valore è**True** vengono registrati gli errori di conversione dei dati e di troncamento.|  
|CDC_stop_on_breaking_schema_changes|False|-|-|False|Proprietà di tipo Boolean. Se il valore è**True** il servizio si arresta quando viene individuata una modifica di rilievo dello schema.<br /><br /> Se è**False** la tabella mirror e l'istanza di acquisizione vengono eliminate.|  
|source_oracle_home||-|-|False|Può essere impostato su un percorso Oracle Home o un nome Oracle Home specifico utilizzato dall'istanza di CDC per la connessione a Oracle.|  
  
###  <a name="BKMK_cdcxdbcdc_state"></a> cdc.xdbcdc_state  
 In questa tabella sono contenute informazioni sullo stato persistente dell'istanza di Oracle CDC. Lo stato di acquisizione viene utilizzato negli scenari di recupero e failover e per il monitoraggio dello stato.  
  
 Nella tabella seguente sono descritte le colonne della tabella **cdc.xdbcdc_state** .  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|status|Codice dello stato corrente per l'istanza di Oracle CDC corrente. Descrive lo stato corrente di CDC.|  
|sub_status|Stato di secondo livello che fornisce informazioni aggiuntive sullo stato corrente.|  
|active|Valore booleano che può essere:<br /><br /> **0**: Il processo dell'istanza di Oracle CDC non è attivo.<br /><br /> **1**: Il processo dell'istanza di Oracle CDC è attivo.|  
|errore|Valore booleano che può essere:<br /><br /> **0**: Il processo dell'istanza di Oracle CDC non è in stato di errore.<br /><br /> **1**: Istanza di Oracle CDC è in stato di errore.|  
|status_message|Stringa che fornisce una descrizione dell'errore o dello stato.|  
|TIMESTAMP|Timestamp con l'ora (UTC) dell'ultimo aggiornamento dello stato di acquisizione.|  
|active_capture_node|Nome dell'host, che può essere un nodo su un cluster, in cui sono attualmente in esecuzione il servizio Oracle CDC e l'istanza di Oracle CDC, mediante cui vengono elaborati i log delle transazioni Oracle.|  
|last_transaction_timestamp|Timestamp con l'ora (UTC) della scrittura dell'ultima transazione nelle tabelle delle modifiche.|  
|last_change_timestamp|Timestamp con l'ora (UTC) della lettura del record delle modifiche più recente dal log delle transazioni Oracle di origine. Il timestamp consente di identificare la latenza corrente del processo CDC.|  
|transaction_log_head_cn|Numero della modifica (CN) più recente letto dal log delle transazioni Oracle.|  
|transaction_log_tail_cn|Numero della modifica (CN) nel log delle transazioni Oracle in corrispondenza del quale viene riposizionata l'istanza di Oracle CDC in caso di riavvio o recupero.|  
|current_cn|Numero della modifica (CN) più recente di cui è nota la presenza nel database di origine.|  
|software_version|Versione interna del servizio Oracle CDC.|  
|completed_transactions|Numero di transazioni elaborate dall'ultima reimpostazione di CDC.|  
|written_changes|Numero di record delle modifiche scritti nelle tabelle delle modifiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|read_changes|Numero dei record delle modifiche letti dal log delle transazioni Oracle di origine.|  
|staged_transactions|Numero delle transazioni attualmente attive gestite temporaneamente nella tabella **cdc.xdbcdc_staged_transactions** .|  
  
###  <a name="BKMK_cdcxdbcdc_trace"></a> cdc.xdbcdc_trace  
 La tabella contiene informazioni sull'operazione dell'istanza di CDC. Le informazioni archiviate in questa tabella includono record di errore, modifiche rilevanti allo stato e record di traccia. Le informazioni sull'errore vengono inoltre scritte nel registro eventi di Windows per garantirne la disponibilità se la tabella **cdc.xcbcdc_trace** non è disponibile.  
  
 Nella tabella seguente vengono descritte le colonne della tabella cdc.xdbcdc_trace.  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|TIMESTAMP|Timestamp UTC esatto della scrittura del record di traccia.|  
|tipo|Contiene uno dei valori seguenti.<br /><br /> errore<br /><br /> INFO<br /><br /> traccia|  
|node|Nome del nodo in cui è stato scritto il record.|  
|status|Codice di stato utilizzato dalla tabella dello stato.|  
|sub_status|Codice di stato secondario utilizzato dalla tabella dello stato.|  
|status_message|Messaggio di stato utilizzato dalla tabella dello stato.|  
|dati|Dati aggiuntivi per i casi in cui il record di errore o di traccia contiene un payload, ad esempio un record di log danneggiato.|  
  
###  <a name="BKMK_cdcxdbcdc_staged_transactions"></a> cdc.xdbcdc_staged_transactions  
 In questa tabella vengono archiviati i record delle modifiche per le transazioni di grandi dimensioni o con esecuzione prolungata fino all'acquisizione del commit delle transazioni o dell'evento di rollback. I record del log acquisiti vengono ordinati dal servizio Oracle CDC in base all'ora dell'ultimo commit della transazione, quindi in base all'ordine cronologico per ciascuna transazione. I record del log per la stessa transazione vengono archiviati in memoria fino al termine della transazione, quindi vengono scritti nella tabella delle modifiche di destinazione o eliminati, in caso di rollback. Poiché la quantità di memoria disponibile è limitata, le transazioni di grandi dimensioni vengono scritte nella tabella **cdc.xdbcdc_staged_transactions** fino al completamento della transazione. Le transazioni vengono inoltre scritte nella tabella di staging in caso di esecuzione prolungata. Pertanto, al riavvio dell'istanza di Oracle CDC, non è necessario rileggere le modifiche precedenti dai log delle transazioni Oracle.  
  
 Nella tabella seguente sono descritte le colonne della tabella **cdc.xdbcdc_staged_transactions** .  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|transaction_id|Identificatore univoco della transazione gestita temporaneamente.|  
|seq_num|Numero di riga **xcbcdc_staged_transactions** per la transazione corrente (inizia con 0).|  
|data_start_cn|Numero della prima modifica (CN) nei dati in questa riga.|  
|data_end_cn|Numero dell'ultima modifica (CN) nei dati in questa riga.|  
|data|Modifiche gestite temporaneamente per la transazione nel formato di BLOB.|  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione Change Data Capture per Oracle di Attunity](change-data-capture-designer-for-oracle-by-attunity.md)  
  
  
