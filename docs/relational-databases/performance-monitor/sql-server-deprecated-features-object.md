---
title: Oggetto Deprecated Features di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Deprecated Features
- performance counters [SQL Server], deprecated features
- deprecation [SQL Server], performance counters
- Deprecated Features object
ms.assetid: e95de9d6-c950-41cd-8aaa-be529c6de198
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 9fcb107c5ae7a22fa2705fda0580e0284940f694
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380692"
---
# <a name="sql-server-deprecated-features-object"></a>Oggetto SQL Server:Deprecated Features
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'oggetto SQLServer:Caratteristiche deprecate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce un contatore per monitorare le caratteristiche definite deprecate. In ognuno dei casi il contatore fornisce un conteggio dell'utilizzo indicante il numero di volte in cui è stata rilevata la funzionalità deprecata dall'ultimo avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Il valore di questi contatori è disponibile anche tramite l'istruzione seguente:  
  
```  
SELECT * FROM sys.dm_os_performance_counters   
WHERE object_name = 'SQLServer:Deprecated Features';  
```  

La tabella seguente descrive l'oggetto prestazione **Deprecated Features** di SQL Server.

|**Contatore SQL Server Deprecated Features**|Descrizione|  
|-------------|-----------------|  
|**Utilizzo**|Utilizzo delle funzionalità dall'ultimo avvio di SQL Server.|
  
 Nella tabella seguente vengono descritte le istanze del contatore Caratteristiche deprecate di SQL Server.  
  
|Istanze del contatore SQL Server Deprecated Features|Descrizione|  
|------------------------------------------------------|-----------------|  
|'#' e '##' come nomi di tabelle e stored procedure temporanee|È stato rilevato un identificatore che non contiene alcun carattere diverso da #. Usare almeno un carattere aggiuntivo. Si verifica una volta per ogni compilazione.|  
|Sintassi per la chiamata di funzioni '::'|È stata rilevata la sintassi per la chiamata di funzioni :: per una funzione con valori di tabella. Sostituirla con `SELECT column_list FROM` *< nome_funzione>*`()`. Sostituire, ad esempio, `SELECT * FROM ::fn_virtualfilestats(2,1)` con `SELECT * FROM sys.fn_virtualfilestats(2,1)`. Si verifica una volta per ogni compilazione.|  
|"\@" e nomi che iniziano con "\@\@" come identificatori [!INCLUDE[tsql](../../includes/tsql-md.md)]|È stato rilevato un identificatore che inizia con \@ o \@\@. Non usare come identificatori \@ o \@v@ o nomi che iniziano con \@\@. Si verifica una volta per ogni compilazione.|  
|ADDING TAPE DEVICE|È stata rilevata la caratteristica deprecata sp_addumpdevice'**tape**'. In alternativa, usare sp_addumpdevice'**disk**'. Si verifica una volta per ogni utilizzo.|  
|Autorizzazione ALL|Numero totale di volte in cui è stata rilevata la sintassi GRANT ALL, DENY ALL o REVOKE ALL. Modificare la sintassi in modo da negare autorizzazioni specifiche. Si verifica una volta per ogni query.|  
|ALTER DATABASE WITH TORN_PAGE_DETECTION|Numero totale di volte in cui è stata usata la funzionalità deprecata TORN_PAGE_DETECTION di ALTER DATABASE dall'avvio dell'istanza del server. Usare la sintassi PAGE_VERIFY. Si verifica una volta per ogni utilizzo in un'istruzione DDL.|  
|ALTER LOGIN WITH SET CREDENTIAL|È stata rilevata la sintassi deprecata ALTER LOGIN WITH SET CREDENTIAL o ALTER LOGIN WITH NO CREDENTIAL. Usare la sintassi ADD o DROP CREDENTIAL. Si verifica una volta per ogni compilazione.|  
|Azeri_Cyrilllic_90|L'evento si verifica una volta per ogni avvio del database e una volta per ogni utilizzo delle regole di confronto. Pianificare la modifica delle applicazioni che usano queste regole di confronto.|  
|Azeri_Latin_90|L'evento si verifica una volta per ogni avvio del database e una volta per ogni utilizzo delle regole di confronto. Pianificare la modifica delle applicazioni che usano queste regole di confronto.|  
|BACKUP DATABASE o LOG TO TAPE|È stata rilevata la funzionalità deprecata BACKUP { DATABASE &#124; LOG } TO TAPE o BACKUP { DATABASE &#124; LOG } TO *dispositivo_nastro*.<br /><br /> In alternativa, usare BACKUP { DATABASE &#124; LOG } TO DISK o BACKUP { DATABASE &#124; LOG } TO *dispositivo_disco*. Si verifica una volta per ogni utilizzo.|  
|BACKUP DATABASE o LOG WITH MEDIAPASSWORD|È stata rilevata la funzionalità deprecata BACKUP DATABASE WITH MEDIAPASSWORD o BACKUP LOG WITH MEDIAPASSWORD. Non usare WITH MEDIAPASSWORD.|  
|BACKUP DATABASE o LOG WITH PASSWORD|È stata rilevata la funzionalità deprecata BACKUP DATABASE WITH PASSWORD o BACKUP LOG WITH PASSWORD. Non usare WITH PASSWORD.|  
|COMPUTE [BY]|È stata rilevata la sintassi COMPUTE o COMPUTE BY. Riscrivere la query in modo che utilizzi GROUP BY con ROLLUP. Si verifica una volta per ogni compilazione.|  
|CREATE FULLTEXT CATLOG IN PATH|È stata rilevata un'istruzione CREATE FULLTEXT CATLOG con la clausola IN PATH. La clausola non ha alcun effetto in questa versione di SQL Server. Si verifica una volta per ogni utilizzo.|  
|CREATE TRIGGER WITH APPEND|È stata rilevata un'istruzione CREATE TRIGGER con la clausola WITH APPEND. Ricreare l'intero trigger. Si verifica una volta per ogni utilizzo in un'istruzione DDL.|  
|CREATE_DROP_DEFAULT|È stata rilevata la sintassi CREATE DEFAULT o DROP DEFAULT. Riscrivere il comando usando l'opzione DEFAULT di CREATE TABLE o ALTER TABLE. Si verifica una volta per ogni compilazione.|  
|CREATE_DROP_RULE|È stata rilevata la sintassi CREATE RULE. Riscrivere il comando usando vincoli. Si verifica una volta per ogni compilazione.|  
|Tipi di dati: text, ntext o image|Sono stati rilevati i tipi di dati **text**, **ntext**o **image** . Riscrivere le applicazioni in modo che utilizzino il tipo di dati **varchar(max)** e rimuovere la sintassi dei tipi di dati **text**, **ntext**e **image** . Si verifica una volta per ogni query.|  
||Numero totale di volte in cui il livello di compatibilità di un database è stato modificato in 80. Pianificare l'aggiornamento del database e dell'applicazione prima della versione successiva. Si verifica anche quando viene avviato un database con livello di compatibilità 80.|  
|Livello di compatibilità 100, 110 del database. 120|Numero totale di volte in cui il livello di compatibilità di un database è stato modificato. Pianificare l'aggiornamento del database e dell'applicazione per una versione successiva. Si verifica anche quando viene avviato un database con livello di compatibilità deprecato.|  
|DATABASE_MIRRORING|Rilevamento di riferimenti alla funzionalità di mirroring del database. Pianificare l'aggiornamento dei gruppi di disponibilità AlwaysOn oppure, se si esegue un'edizione di SQL Server che non supporta questi gruppi, pianificare la migrazione al log shipping.|  
|database_principal_aliases|Sono stati rilevati riferimenti alla vista deprecata sys.database_principal_aliases. Usare ruoli anziché alias. Si verifica una volta per ogni compilazione.|  
|DATABASEPROPERTY|Un'istruzione fa riferimento a DATABASEPROPERTY. Aggiornare l'istruzione DATABASEPROPERTY a DATABASEPROPERTYEX. Si verifica una volta per ogni compilazione.|  
|DATABASEPROPERTYEX('IsFullTextEnabled')|Un'istruzione fa riferimento alla proprietà DATABASEPROPERTYEX IsFullTextEnabled. Il valore di questa proprietà non ha alcun effetto. I database utente sono sempre abilitati per la ricerca full-text. Non usare questa proprietà. Si verifica una volta per ogni compilazione.|  
|DBCC [UN]PINTABLE|È stata rilevata l'istruzione DBCC PINTABLE o DBCC UNPINTABLE. Questa istruzione non ha alcun effetto e deve essere rimossa. Si verifica una volta per ogni query.|  
|DBCC DBREINDEX|È stata rilevata l'istruzione DBCC DBREINDEX. Riscrivere l'istruzione in modo che utilizzi l'opzione REBUILD di ALTER INDEX. Si verifica una volta per ogni query.|  
|DBCC INDEXDEFRAG|È stata rilevata l'istruzione DBCC INDEXDEFRAG. Riscrivere l'istruzione in modo che utilizzi l'opzione REORGANIZE di ALTER INDEX. Si verifica una volta per ogni query.|  
|DBCC SHOWCONTIG|È stata rilevata l'istruzione DBCC SHOWCONTIG. Eseguire una query su sys.dm_db_index_physical_stats per ottenere queste informazioni. Si verifica una volta per ogni query.|  
|Parola chiave DEFAULT come valore predefinito|È stata rilevata una sintassi che usano la parola chiave DEFAULT come valore predefinito. Non usare. Si verifica una volta per ogni compilazione.|  
|Algoritmo di crittografia deprecata|L'algoritmo di crittografia deprecato rc4 verrà rimosso nella prossima versione di SQL Server. Evitare di usare questa funzionalità e pianificare la modifica delle applicazioni che ne fanno uso. L'algoritmo RC4 non è sufficientemente sicuro ed è supportato solo per motivi di compatibilità con le versioni precedenti. È possibile crittografare il nuovo materiale usando RC4 o RC4_128 solo quando il livello di compatibilità del database è 90 o 100. (Non consigliato.) Usare un algoritmo più recente, ad esempio uno degli algoritmi AES. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive il materiale crittografato usando RC4 o RC4_128 può essere decrittografato in qualsiasi livello di compatibilità.|  
|Algoritmo hash deprecato|Usare gli algoritmo MD2, MD4, MD5, SHA o SHA1.|  
|Algoritmo DESX|È stata rilevata una sintassi che usano l'algoritmo di crittografia DESX. Usare un algoritmo diverso per la crittografia. Si verifica una volta per ogni compilazione.|  
|dm_fts_active_catalogs|Il contatore dm_fts_active_catalogs indica sempre 0 perché alcune colonne della vista sys.dm_fts_active_catalogs non sono deprecate. Per monitorare una colonna deprecata, utilizzare il contatore specifico della colonna, ad esempio dm_fts_active_catalogs.is_paused.|  
|dm_fts_active_catalogs.is_paused|È stata rilevata la colonna is_paused della vista a gestione dinamica [sys.dm_fts_active_catalogs](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md) . Evitare di usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|dm_fts_active_catalogs.previous_status|È stata rilevata la colonna previous_status della vista a gestione dinamica sys.dm_fts_active_catalogs. Evitare di usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|dm_fts_active_catalogs.previous_status_description|È stata rilevata la colonna previous_status_description della vista a gestione dinamica sys.dm_fts_active_catalogs. Evitare di usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|dm_fts_active_catalogs.row_count_in_thousands|È stata rilevata la colonna row_count_in_thousands della vista a gestione dinamica sys.dm_fts_active_catalogs. Evitare di usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|dm_fts_active_catalogs.status|È stata rilevata la colonna status della vista a gestione dinamica sys.dm_fts_active_catalogs. Evitare di usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|dm_fts_active_catalogs.status_description|È stata rilevata la colonna status_description della vista a gestione dinamica sys.dm_fts_active_catalogs. Evitare di usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|dm_fts_active_catalogs.worker_count|È stata rilevata la colonna worker_count della vista a gestione dinamica sys.dm_fts_active_catalogs. Evitare di usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|dm_fts_memory_buffers|Il contatore dm_fts_memory_buffers indica sempre 0 perché la maggior parte delle colonne della vista sys.dm_fts_memory_buffers non è deprecata. Per monitorare la colonna deprecata, utilizzare il contatore specifico della colonna dm_fts_memory_buffers.row_count.|  
|dm_fts_memory_buffers.row_count|È stata rilevata la colonna row_count della vista a gestione dinamica [sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md) . Evitare di usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|DROP INDEX con nome in due parti|La sintassi DROP INDEX contiene la sintassi del formato *table_name.index_name* in DROP INDEX. Sostituire con la sintassi *index_name* ON *table_name* nell'istruzione DROP INDEX. Si verifica una volta per ogni compilazione.|  
|EXT_CREATE_ALTER_SOAP_ENDPOINT|È stata rilevata l'istruzione CREATE o ALTER ENDPOINT con l'opzione FOR SOAP. I servizi Web XML nativi sono deprecati. Usare Windows Communications Foundation (WCF) o ASP.NET.|  
|EXT_endpoint_webmethods|È stata rilevata la vista sys.endpoint_webmethods. I servizi Web XML nativi sono deprecati. Usare Windows Communications Foundation (WCF) o ASP.NET.|  
|EXT_soap_endpoints|È stata rilevata la vista sys.soap_endpoints. I servizi Web XML nativi sono deprecati. Usare Windows Communications Foundation (WCF) o ASP.NET.|  
|EXTPROP_LEVEL0TYPE|È stato rilevato TYPE in level0type. Usare SCHEMA come level0type e TYPE come level1type. Si verifica una volta per ogni query.|  
|EXTPROP_LEVEL0USER|È stato rilevato level0type USER quando è specificato anche level1type. Usare USER solo come level0type per le proprietà estese direttamente in un utente. Si verifica una volta per ogni query.|  
|FASTFIRSTROW|È stata rilevata la sintassi FASTFIRSTROW. Riscrivere le istruzioni in modo che utilizzino la sintassi OPTION (FAST *n*). Si verifica una volta per ogni compilazione.|  
|FILE_ID|È stata rilevata la sintassi FILE_ID. Riscrivere le istruzioni in modo che utilizzino FILE_IDEX. Si verifica una volta per ogni compilazione.|  
|fn_get_sql|È stata compilata la funzione fn_get_sql. Utilizzare sys.dm_exec_sql_text. Si verifica una volta per ogni compilazione.|  
|fn_servershareddrives|È stata compilata la funzione fn_servershareddrives. Utilizzare sys.dm_io_cluster_shared_drives. Si verifica una volta per ogni compilazione.|  
|fn_virtualservernodes|È stata compilata la funzione fn_virtualservernodes. Utilizzare sys.dm_os_cluster_nodes. Si verifica una volta per ogni compilazione.|  
|fulltext_catalogs|Il contatore fulltext_catalogs indica sempre 0 perché alcune colonne della vista sys.fulltext_catalogs non sono deprecate. Per monitorare una colonna deprecata, utilizzare il contatore specifico della colonna, ad esempio fulltext_catalogs.data_space_id. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|fulltext_catalogs.data_space_id|È stata rilevata la colonna data_space_id della vista del catalogo [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) . Non usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|fulltext_catalogs.file_id|È stata rilevata la colonna file_id della vista del catalogo sys.fulltext_catalogs. Non usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|fulltext_catalogs.path|È stata rilevata la colonna path della vista del catalogo sys.fulltext_catalogs. Non usare questa colonna. Si verifica ogni volta che l'istanza del server rileva un riferimento alla colonna.|  
|FULLTEXTCATALOGPROPERTY('LogSize')|È stata rilevata la proprietà LogSize della funzione FULLTEXTCATALOGPROPERTY. Evitare di usare questa proprietà.|  
|FULLTEXTCATALOGPROPERTY('PopulateStatus')|È stata rilevata la proprietà PopulateStatus della funzione FULLTEXTCATALOGPROPERTY. Evitare di usare questa proprietà.|  
|FULLTEXTSERVICEPROPERTY('ConnectTimeout')|È stata rilevata la proprietà ConnectTimeout della funzione FULLTEXTCATALOGPROPERTY. Evitare di usare questa proprietà.|  
|FULLTEXTSERVICEPROPERTY('DataTimeout')|È stata rilevata la proprietà DataTimeout della funzione FULLTEXTCATALOGPROPERTY. Evitare di usare questa proprietà.|  
|FULLTEXTSERVICEPROPERTY('ResourceUsage')|È stata rilevata la proprietà ResourceUsage della funzione FULLTEXTCATALOGPROPERTY. Evitare di usare questa proprietà.|  
|GROUP BY ALL|Numero totale di volte in cui è stata rilevata la sintassi GROUP BY ALL. Modificare la sintassi per raggruppare in base a tabelle specifiche.|  
|Hindi|L'evento si verifica una volta per ogni avvio del database e una volta per ogni utilizzo delle regole di confronto. Pianificare la modifica delle applicazioni che usano queste regole di confronto. Usare Indic_General_90.|  
|Hint di tabella HOLDLOCK senza parentesi||  
|IDENTITYCOL|È stata rilevata la sintassi IDENTITYCOL. Riscrivere le istruzioni in modo che utilizzino la sintassi $identity. Si verifica una volta per ogni compilazione.|  
|Elenco di selezione di una vista indicizzata senza COUNT_BIG(\*)|L'elenco di selezione di una vista indicizzata aggregata deve contenere COUNT_BIG(\*).|  
|INDEX_OPTION|È stata rilevata la sintassi CREATE TABLE, ALTER TABLE o CREATE INDEX senza parentesi per racchiudere le opzioni. Riscrivere le istruzioni in modo che utilizzino la sintassi corrente. Si verifica una volta per ogni query.|  
|INDEXKEY_PROPERTY|È stata rilevata la sintassi INDEXKEY_PROPERTY. Riscrivere le istruzioni per eseguire query su sys.index_columns. Si verifica una volta per ogni compilazione.|  
|Hint di funzione con valori di tabella indiretti|L'applicazione indiretta, tramite una vista, di hint di tabella a una chiamata di una funzione con valori di tabella con istruzioni multiple verrà rimossa in una versione successiva di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|INSERT NULL in colonne TIMESTAMP|È stato inserito un valore NULL in una colonna TIMESTAMP. Usare un valore predefinito. Si verifica una volta per ogni compilazione.|  
|INSERT_HINTS||  
|Korean_Wansung_Unicode|L'evento si verifica una volta per ogni avvio del database e una volta per ogni utilizzo delle regole di confronto. Pianificare la modifica delle applicazioni che usano queste regole di confronto.|  
|Lithuanian_Classic|L'evento si verifica una volta per ogni avvio del database e una volta per ogni utilizzo delle regole di confronto. Pianificare la modifica delle applicazioni che usano queste regole di confronto.|  
|Macedonian|L'evento si verifica una volta per ogni avvio del database e una volta per ogni utilizzo delle regole di confronto. Pianificare la modifica delle applicazioni che usano queste regole di confronto. Usare Macedonian_FYROM_90.|  
|MODIFY FILEGROUP READONLY|È stata rilevata la sintassi MODIFY FILEGROUP READONLY. Riscrivere le istruzioni in modo che utilizzino la sintassi READ_ONLY. Si verifica una volta per ogni compilazione.|  
|MODIFY FILEGROUP READWRITE|È stata rilevata la sintassi MODIFY FILEGROUP READWRITE. Riscrivere le istruzioni in modo che utilizzino la sintassi READ_WRITE. Si verifica una volta per ogni compilazione.|  
|Nome di colonna in più di due parti|Una query usano un nome in tre o quattro parti nell'elenco di colonne. Modificare la query in modo che utilizzi nomi in due parti conformi allo standard. Si verifica una volta per ogni compilazione.|  
|Più hint di tabella senza virgola|È stato usato uno spazio come separatore tra hint di tabella. Usare una virgola. Si verifica una volta per ogni compilazione.|  
|NOLOCK o READUNCOMMITTED in UPDATE o DELETE|È stato rilevato l'hint di tabella NOLOCK o READUNCOMMITTED nella clausola FROM di un'istruzione UPDATE o DELETE. Rimuovere l'hint di tabella NOLOCK o READUNCOMMITTED dalla clausola FROM.|  
|Operatori non ANSI *= o =\* outer join|È stata rilevata un'istruzione che usa la sintassi join *= o =\* . Riscrivere le istruzioni in modo che utilizzino la sintassi join ANSI. Si verifica una volta per ogni compilazione.|  
|numbered_stored_procedures||  
|numbered_procedure_parameters|Sono stati rilevati riferimenti alla vista deprecata sys.numbered_procedure_parameters. Non usare. Si verifica una volta per ogni compilazione.|  
|numbered_procedures|Sono stati rilevati riferimenti alla vista deprecata sys.numbered_procedures. Non usare. Si verifica una volta per ogni compilazione.|  
|Oldstyle RAISEERROR|È stata rilevata la sintassi deprecata RAISERROR (formato: RAISERROR stringa di tipo integer). Riscrivere l'istruzione in modo che utilizzi la sintassi RAISERROR corrente. Si verifica una volta per ogni compilazione.|  
|OLEDB per connessioni ad hoc|SQLOLEDB non è un provider supportato. Per le connessioni ad hoc, usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.|  
|PERMISSIONS|Sono stati rilevati riferimenti alla funzione intrinseca PERMISSIONS. Eseguire una query su sys.fn_my_permissions. Si verifica una volta per ogni query.|  
|ProcNums|È stata rilevata la sintassi deprecata ProcNums. Riscrivere le istruzioni per rimuovere i riferimenti. Si verifica una volta per ogni compilazione.|  
|READTEXT|È stata rilevata la sintassi READTEXT. Riscrivere le applicazioni in modo che utilizzino il tipo di dati **varchar(max)** e rimuovere la sintassi dei tipi di dati **text** . Si verifica una volta per ogni query.|  
|RESTORE DATABASE o LOG WITH DBO_ONLY|È stata rilevata la sintassi RESTORE ... WITH DBO_ONLY. In alternativa, usare RESTORE ... RESTRICTED_USER.|  
|RESTORE DATABASE o LOG WITH MEDIAPASSWORD|È stata rilevata la sintassi RESTORE ... WITH MEDIAPASSWORD. La sintassi WITH MEDIAPASSWORD fornisce una sicurezza insufficiente e deve essere rimossa.|  
|RESTORE DATABASE o LOG WITH PASSWORD|È stata rilevata la sintassi RESTORE ... WITH PASSWORD. La sintassi WITH PASSWORD fornisce una sicurezza insufficiente e deve essere rimossa.|  
|Restituzione di risultati da un trigger|Questo evento si verifica una volta per ogni chiamata del trigger. Riscrivere il trigger in modo che non restituisca set di risultati.|  
|ROWGUIDCOL|È stata rilevata la sintassi ROWGUIDCOL. Riscrivere le istruzioni in modo che utilizzino la sintassi $rowguid. Si verifica una volta per ogni compilazione.|  
|SET ANSI_NULLS OFF|È stata rilevata la sintassi SET ANSI_NULLS OFF. Rimuovere questa sintassi deprecata. Si verifica una volta per ogni compilazione.|  
|SET ANSI_PADDING OFF|È stata rilevata la sintassi SET ANSI_PADDING OFF. Rimuovere questa sintassi deprecata. Si verifica una volta per ogni compilazione.|  
|SET CONCAT_NULL_YIELDS_NULL OFF|È stata rilevata la sintassi SET CONCAT_NULL_YIELDS_NULL OFF. Rimuovere questa sintassi deprecata. Si verifica una volta per ogni compilazione.|  
|SET DISABLE_DEF_CNST_CHK|È stata rilevata la sintassi SET DISABLE_DEF_CNST_CHK, che non ha alcun effetto. Rimuovere questa sintassi deprecata. Si verifica una volta per ogni compilazione.|  
|SET FMTONLY ON|È stata rilevata la sintassi SET FMTONLY. Rimuovere questa sintassi deprecata. Si verifica una volta per ogni compilazione.|  
|SET OFFSETS|È stata rilevata la sintassi SET OFFSETS. Rimuovere questa sintassi deprecata. Si verifica una volta per ogni compilazione.|  
|SET REMOTE_PROC_TRANSACTIONS|È stata rilevata la sintassi SET REMOTE_PROC_TRANSACTIONS. Rimuovere questa sintassi deprecata. Utilizzare server collegati e sp_serveroption.|  
|SET ROWCOUNT|È stata rilevata la sintassi SET ROWCOUNT in un'istruzione DELETE, INSERT o UPDATE. Riscrivere l'istruzione usando TOP. Si verifica una volta per ogni compilazione.|  
|SETUSER|È stata rilevata l'istruzione SET USER. In alternativa, usare la clausola EXECUTE AS. Si verifica una volta per ogni query.|  
|sp_addapprole|È stata rilevata la procedura sp_addapprole. In alternativa, usare CREATE APPLICATION ROLE. Si verifica una volta per ogni query.|  
|sp_addextendedproc|È stata rilevata la procedura sp_addextendedproc. In alternativa, usare CLR. Si verifica una volta per ogni compilazione.|  
|sp_addlogin|È stata rilevata la procedura sp_addlogin. In alternativa, usare CREATE LOGIN. Si verifica una volta per ogni query.|  
|sp_addremotelogin|È stata rilevata la procedura sp_addremotelogin. In alternativa, usare server collegati.|  
|sp_addrole|È stata rilevata la procedura sp_addrole. In alternativa, usare CREATE ROLE. Si verifica una volta per ogni query.|  
|sp_addserver|È stata rilevata la procedura sp_addserver. In alternativa, usare server collegati.|  
|sp_addtype|È stata rilevata la procedura sp_addtype. In alternativa, usare CREATE TYPE. Si verifica una volta per ogni compilazione.|  
|sp_adduser|È stata rilevata la procedura sp_adduser. In alternativa, usare CREATE USER. Si verifica una volta per ogni query.|  
|sp_approlepassword|È stata rilevata la procedura sp_approlepassword. In alternativa, usare ALTER APPLICATION ROLE. Si verifica una volta per ogni query.|  
|sp_attach_db|È stata rilevata la procedura sp_attach_db. In alternativa, usare CREATE DATABASE FOR ATTACH. Si verifica una volta per ogni query.|  
|sp_attach_single_file_db|È stata rilevata la procedura sp_single_file_db. In alternativa, usare CREATE DATABASE FOR ATTACH_REBUILD_LOG. Si verifica una volta per ogni query.|  
|sp_bindefault|È stata rilevata la procedura sp_bindefault. In alternativa, usare la parola chiave DEFAULT di ALTER TABLE o CREATE TABLE. Si verifica una volta per ogni compilazione.|  
|sp_bindrule|È stata rilevata la procedura sp_bindrule. In alternativa, usare vincoli CHECK. Si verifica una volta per ogni compilazione.|  
|sp_bindsession|È stata rilevata la procedura sp_bindsession. In alternativa, usare MARS (Multiple Active Result Set) o transazioni distribuite. Si verifica una volta per ogni compilazione.|  
|sp_certify_removable|È stata rilevata la procedura sp_certify_removable. Utilizzare sp_detach_db. Si verifica una volta per ogni query.|  
|sp_changeobjectowner|È stata rilevata la procedura sp_changeobjectowner. In alternativa, usare ALTER SCHEMA o ALTER AUTHORIZATION. Si verifica una volta per ogni query.|  
|sp_change_users_login|È stata rilevata la procedura sp_change_users_login. In alternativa, usare ALTER USER. Si verifica una volta per ogni query.|  
|sp_configure 'allow updates'|È stata rilevata l'opzione allow updates di sp_configure. Le tabelle di sistema non sono più aggiornabili. Non usare. Si verifica una volta per ogni query.|  
|sp_configure 'disallow results from triggers'|È stata rilevata l'opzione disallow result sets from triggers di sp_configure. Per impedire la restituzione di set di risultati da trigger, utilizzare sp_configure per impostare l'opzione su 1. Si verifica una volta per ogni query.|  
|sp_configure 'ft crawl bandwidth (max)'|È stata rilevata l'opzione ft crawl bandwidth (max) di sp_configure. Non usare. Si verifica una volta per ogni query.|  
|sp_configure 'ft crawl bandwidth (min)'|È stata rilevata l'opzione ft crawl bandwidth (min) di sp_configure. Non usare. Si verifica una volta per ogni query.|  
|sp_configure 'ft notify bandwidth (max)'|È stata rilevata l'opzione ft notify bandwidth (max) di sp_configure. Non usare. Si verifica una volta per ogni query.|  
|sp_configure 'ft notify bandwidth (min)'|È stata rilevata l'opzione ft notify bandwidth (min) di sp_configure. Non usare. Si verifica una volta per ogni query.|  
|sp_configure 'locks'|È stata rilevata l'opzione locks di sp_configure. I blocchi non sono più configurabili. Non usare. Si verifica una volta per ogni query.|  
|sp_configure 'open objects'|È stata rilevata l'opzione open objects di sp_configure. Il numero di oggetti aperti non è più configurabile. Non usare. Si verifica una volta per ogni query.|  
|sp_configure 'priority boost'|È stata rilevata l'opzione priority boost di sp_configure. Non usare. Si verifica una volta per ogni query. In alternativa, usare l'opzione start /high ... program.exe di Windows.|  
|sp_configure 'remote proc trans'|È stata rilevata l'opzione remote proc trans di sp_configure. Non usare. Si verifica una volta per ogni query.|  
|sp_configure 'set working set size'|È stata rilevata l'opzione set working set size di sp_configure Le dimensioni del working set non sono più configurabili. Non usare. Si verifica una volta per ogni query.|  
|sp_control_dbmasterkey_password|La stored procedure sp_control_dbmasterkey_password non controlla se una chiave master è esistente. Questo è consentito solo per la compatibilità con le versioni precedenti, ma viene visualizzato un avviso. Questo comportamento è deprecato. In una versione futura la chiave master deve esistere e la password usata nella stored procedure sp_control_dbmasterkey_password deve essere una delle password usate per crittografare la chiave master del database.|  
|sp_create_removable|È stata rilevata la procedura sp_create_removable. In alternativa, usare CREATE DATABASE. Si verifica una volta per ogni query.|  
|sp_db_vardecimal_storage_format|È stato rilevato l'utilizzo del formato di archiviazione **vardecimal** . Usare la compressione dei dati.|  
|sp_dbcmptlevel|È stata rilevata la procedura sp_dbcmptlevel. Utilizzare ALTER DATABASE ... SET COMPATIBILITY_LEVEL. Si verifica una volta per ogni query.|  
|sp_dbfixedrolepermission|È stata rilevata la procedura sp_dbfixedrolepermission. Non usare. Si verifica una volta per ogni query.|  
|sp_dboption|È stata rilevata la procedura sp_dboption. In alternativa, usare ALTER DATABASE e DATABASEPROPERTYEX. Si verifica una volta per ogni compilazione.|  
|sp_dbremove|È stata rilevata la procedura sp_dbremove. In alternativa, usare DROP DATABASE. Si verifica una volta per ogni query.|  
|sp_defaultdb|È stata rilevata la procedura sp_defaultdb. In alternativa, usare ALTER LOGIN. Si verifica una volta per ogni compilazione.|  
|sp_defaultlanguage|È stata rilevata la procedura sp_defaultlanguage. In alternativa, usare ALTER LOGIN. Si verifica una volta per ogni compilazione.|  
|sp_denylogin|È stata rilevata la procedura sp_denylogin. In alternativa, usare ALTER LOGIN DISABLE. Si verifica una volta per ogni query.|  
|sp_depends|È stata rilevata la procedura sp_depends. Utilizzare sys.dm_sql_referencing_entities e sys.dm_sql_referenced_entities. Si verifica una volta per ogni query.|  
|sp_detach_db \@keepfulltextindexfile|È stato rilevato l'argomento \@keepfulltextindexfile in un'istruzione sp_detach_db. Non usare questo argomento.|  
|sp_dropalias|È stata rilevata la procedura sp_dropalias. Sostituire gli alias con una combinazione di account utente e ruoli del database. Utilizzare sp_dropalias per rimuovere gli alias in database aggiornati. Si verifica una volta per ogni compilazione.|  
|sp_dropapprole|È stata rilevata la procedura sp_dropapprole. In alternativa, usare DROP APPLICATION ROLE. Si verifica una volta per ogni query.|  
|sp_dropextendedproc|È stata rilevata la procedura sp_dropextendedproc. In alternativa, usare CLR. Si verifica una volta per ogni compilazione.|  
|sp_droplogin|È stata rilevata la procedura sp_droplogin. In alternativa, usare DROP LOGIN. Si verifica una volta per ogni query.|  
|sp_dropremotelogin|È stata rilevata la procedura sp_dropremotelogin. In alternativa, usare server collegati.|  
|sp_droprole|È stata rilevata la procedura sp_droprole. In alternativa, usare DROP ROLE. Si verifica una volta per ogni query.|  
|sp_droptype|È stata rilevata la procedura sp_droptype. In alternativa, usare DROP TYPE.|  
|sp_dropuser|È stata rilevata la procedura sp_dropuser. In alternativa, usare DROP USER. Si verifica una volta per ogni query.|  
|sp_estimated_rowsize_reduction_for_vardecimal|È stato rilevato l'utilizzo del formato di archiviazione **vardecimal** . Utilizzare la compressione dati e sp_estimate_data_compression_savings.|  
|sp_fulltext_catalog|È stata rilevata la procedura sp_fulltext_catalog. In alternativa, usare CREATE/ALTER/DROP FULLTEXT CATALOG. Si verifica una volta per ogni compilazione.|  
|sp_fulltext_column|È stata rilevata la procedura sp_fulltext_column. In alternativa, usare ALTER FULLTEXT INDEX. Si verifica una volta per ogni compilazione.|  
|sp_fulltext_database|È stata rilevata la procedura sp_fulltext_database. In alternativa, usare ALTER DATABASE. Si verifica una volta per ogni compilazione.|  
|sp_fulltext_service \@action=clean_up|È stata rilevata l'opzione clean_up della procedura sp_fulltext_service. Si verifica una volta per ogni query.|  
|sp_fulltext_service \@action=connect_timeout|È stata rilevata l'opzione connect_timeout della procedura sp_fulltext_service. Si verifica una volta per ogni query.|  
|sp_fulltext_service \@action=data_timeout|È stata rilevata l'opzione data_timeout della procedura sp_fulltext_service. Si verifica una volta per ogni query.|  
|sp_fulltext_service \@action=resource_usage|È stata rilevata l'opzione resource_usage della procedura sp_fulltext_service. Questa opzione non ha alcuna funzione. Si verifica una volta per ogni query.|  
|sp_fulltext_table|È stata rilevata la procedura sp_fulltext_table. In alternativa, usare CREATE/ALTER/DROP FULLTEXT INDEX. Si verifica una volta per ogni compilazione.|  
|sp_getbindtoken|È stata rilevata la procedura sp_getbindtoken. In alternativa, usare MARS (Multiple Active Result Set) o transazioni distribuite. Si verifica una volta per ogni compilazione.|  
|sp_grantdbaccess|È stata rilevata la procedura sp_grantdbaccess. In alternativa, usare CREATE USER. Si verifica una volta per ogni query.|  
|sp_grantlogin|È stata rilevata la procedura sp_grantlogin. In alternativa, usare CREATE LOGIN. Si verifica una volta per ogni query.|  
|sp_help_fulltext_catalog_components|È stata rilevata la procedura sp_help_fulltext_catalog_components, Questa stored procedure restituisce righe vuote. Non usare questa procedura. Si verifica una volta per ogni compilazione.|  
|sp_help_fulltext_catalogs|È stata rilevata la procedura sp_help_fulltext_catalogs. Eseguire una query su sys.fulltext_catalogs. Si verifica una volta per ogni compilazione.|  
|sp_help_fulltext_catalogs_cursor|È stata rilevata la procedura sp_help_fulltext_catalogs_cursor. Eseguire una query su sys.fulltext_catalogs. Si verifica una volta per ogni compilazione.|  
|sp_help_fulltext_columns|È stata rilevata la procedura sp_help_fulltext_columns. Eseguire una query su sys.fulltext_index_columns. Si verifica una volta per ogni compilazione.|  
|sp_help_fulltext_columns_cursor|È stata rilevata la procedura sp_help_fulltext_columns_cursor. Eseguire una query su sys.fulltext_index_columns. Si verifica una volta per ogni compilazione.|  
|sp_help_fulltext_tables|È stata rilevata la procedura sp_help_fulltext_tables. Eseguire una query su sys.fulltext_indexes. Si verifica una volta per ogni compilazione.|  
|sp_help_fulltext_tables_cursor|È stata rilevata la procedura sp_help_fulltext_tables_cursor. Eseguire una query su sys.fulltext_indexes. Si verifica una volta per ogni compilazione.|  
|sp_helpdevice|È stata rilevata la procedura sp_helpdevice. Eseguire una query su sys.backup_devices. Si verifica una volta per ogni query.|  
|sp_helpextendedproc|È stata rilevata la procedura sp_helpextendedproc. In alternativa, usare CLR. Si verifica una volta per ogni compilazione.|  
|sp_helpremotelogin|È stata rilevata la procedura sp_helpremotelogin. In alternativa, usare server collegati.|  
|sp_indexoption|È stata rilevata la procedura sp_indexoption. In alternativa, usare ALTER INDEX. Si verifica una volta per ogni compilazione.|  
|sp_lock|È stata rilevata la procedura sp_lock. Eseguire una query su sys.dm_tran_locks. Si verifica una volta per ogni query.|  
|sp_password|È stata rilevata la procedura sp_password. In alternativa, usare ALTER LOGIN. Si verifica una volta per ogni query.|  
|sp_remoteoption|È stata rilevata la procedura sp_remoteoption. In alternativa, usare server collegati.|  
|sp_renamedb|È stata rilevata la procedura sp_renamedb. In alternativa, usare ALTER DATABASE. Si verifica una volta per ogni query.|  
|sp_resetstatus|È stata rilevata la procedura sp_resetstatus. In alternativa, usare ALTER DATABASE. Si verifica una volta per ogni query.|  
|sp_revokedbaccess|È stata rilevata la procedura sp_revokedbaccess. In alternativa, usare DROP USER. Si verifica una volta per ogni query.|  
|sp_revokelogin|È stata rilevata la procedura sp_revokelogin. In alternativa, usare DROP LOGIN. Si verifica una volta per ogni query.|  
|sp_srvrolepermission|È stata rilevata la procedura deprecata sp_srvrolepermission. Non usare. Si verifica una volta per ogni query.|  
|sp_unbindefault|È stata rilevata la procedura sp_unbindefault. In alternativa, usare la parola chiave DEFAULT nell'istruzione CREATE TABLE o ALTER TABLE. Si verifica una volta per ogni compilazione.|  
|sp_unbindrule|È stata rilevata la procedura sp_unbindrule. Usare vincoli CHECK anziché regole. Si verifica una volta per ogni compilazione.|  
|SQL_AltDiction_CP1253_CS_AS|L'evento si verifica una volta per ogni avvio del database e una volta per ogni utilizzo delle regole di confronto. Pianificare la modifica delle applicazioni che usano queste regole di confronto.|  
|Valori letterali stringa come alias di colonna|È stata rilevata una sintassi contenente una stringa usata come alias di colonna in un'istruzione SELECT, ad esempio `'string' = expression`. Non usare. Si verifica una volta per ogni compilazione.|  
|sys.sql_dependencies|Sono stati rilevati riferimenti a sys.sql_dependencies. Utilizzare sys.sql_expression_dependencies. Si verifica una volta per ogni compilazione.|  
|sysaltfiles|Sono stati rilevati riferimenti a sysaltfiles. Utilizzare sys.master_files. Si verifica una volta per ogni compilazione.|  
|syscacheobjects|Sono stati rilevati riferimenti a syscacheobjects. Utilizzare sys.dm_exec_cached_plans, sys.dm_exec_plan_attributes e sys.dm_exec_sql_text. Si verifica una volta per ogni compilazione.|  
|syscolumns|Sono stati rilevati riferimenti a syscolumns. Utilizzare sys.columns. Si verifica una volta per ogni compilazione.|  
|syscomments|Sono stati rilevati riferimenti a syscomments. Utilizzare sys.sql_modules. Si verifica una volta per ogni compilazione.|  
|sysconfigures|Sono stati rilevati riferimenti alla tabella sysconfigures. In alternativa, fare riferimento alla vista sys.sysconfigures. Si verifica una volta per ogni compilazione.|  
|sysconstraints|Sono stati rilevati riferimenti a sysconstraints. Utilizzare sys.check_constraints, sys.default_constraints, sys.key_constraints e sys.foreign_keys. Si verifica una volta per ogni compilazione.|  
|syscurconfigs|Sono stati rilevati riferimenti a syscurconfigs. Utilizzare sys.configurations. Si verifica una volta per ogni compilazione.|  
|sysdatabases|Sono stati rilevati riferimenti a sysdatabases. Utilizzare sys.databases. Si verifica una volta per ogni compilazione.|  
|sysdepends|Sono stati rilevati riferimenti a sysdepends. Utilizzare sys.sql_dependencies. Si verifica una volta per ogni compilazione.|  
|sysdevices|Sono stati rilevati riferimenti a sysdevices. Utilizzare sys.backup_devices. Si verifica una volta per ogni compilazione.|  
|sysfilegroups|Sono stati rilevati riferimenti a sysfilegroups. Utilizzare sys.filegroups. Si verifica una volta per ogni compilazione.|  
|sysfiles|Sono stati rilevati riferimenti a sysfiles. Utilizzare sys.database_files. Si verifica una volta per ogni compilazione.|  
|sysforeignkeys|Sono stati rilevati riferimenti a sysforeignkeys. Utilizzare sys.foreign_keys. Si verifica una volta per ogni compilazione.|  
|sysfulltextcatalogs|Sono stati rilevati riferimenti a sysfulltextcatalogs. Utilizzare sys.fulltext_catalogs. Si verifica una volta per ogni compilazione.|  
|sysindexes|Sono stati rilevati riferimenti a sysindexes. Utilizzare sys.indexes, sys.partitions, sys.allocation_units e sys.dm_db_partition_stats. Si verifica una volta per ogni compilazione.|  
|sysindexkeys|Sono stati rilevati riferimenti a sysindexkeys. Utilizzare sys.index_columns. Si verifica una volta per ogni compilazione.|  
|syslockinfo|Sono stati rilevati riferimenti a syslockinfo. Utilizzare sys.dm_tran_locks. Si verifica una volta per ogni compilazione.|  
|syslogins|Sono stati rilevati riferimenti a syslogins. Utilizzare sys.server_principals e sys.sql_logins. Si verifica una volta per ogni compilazione.|  
|sysmembers|Sono stati rilevati riferimenti a sysmembers. Utilizzare sys.database_role_members. Si verifica una volta per ogni compilazione.|  
|sysmessages|Sono stati rilevati riferimenti a sysmessages. Utilizzare sys.messages. Si verifica una volta per ogni compilazione.|  
|sysobjects|Sono stati rilevati riferimenti a sysobjects. Utilizzare sys.objects. Si verifica una volta per ogni compilazione.|  
|sysoledbusers|Sono stati rilevati riferimenti a sysoledbusers. Utilizzare sys.linked_logins. Si verifica una volta per ogni compilazione.|  
|sysopentapes|Sono stati rilevati riferimenti a sysopentapes. Utilizzare sys.dm_io_backup_tapes. Si verifica una volta per ogni compilazione.|  
|sysperfinfo|Sono stati rilevati riferimenti a sysperfinfo. Usare sys.dm_os_performance_counters. . Si verifica una volta per ogni compilazione.|  
|syspermissions|Sono stati rilevati riferimenti a syspermissions. Utilizzare sys.database_permissions e sys.server_permissions. Si verifica una volta per ogni compilazione.|  
|sysprocesses|Sono stati rilevati riferimenti a sysprocesses. Utilizzare sys.dm_exec_connections, sys.dm_exec_sessions e sys.dm_exec_requests. Si verifica una volta per ogni compilazione.|  
|sysprotects|Sono stati rilevati riferimenti a sysprotects. Utilizzare sys.database_permissions e sys.server_permissions. Si verifica una volta per ogni compilazione.|  
|sysreferences|Sono stati rilevati riferimenti a sysreferences. Utilizzare sys.foreign_keys. Si verifica una volta per ogni compilazione.|  
|sysremotelogins|Sono stati rilevati riferimenti a sysremotelogins. Utilizzare sys.remote_logins. Si verifica una volta per ogni compilazione.|  
|sysservers|Sono stati rilevati riferimenti a sysservers. Utilizzare sys.servers. Si verifica una volta per ogni compilazione.|  
|systypes|Sono stati rilevati riferimenti a systypes. Utilizzare sys.types. Si verifica una volta per ogni compilazione.|  
|sysusers|Sono stati rilevati riferimenti a sysusers. Utilizzare sys.database_principals. Si verifica una volta per ogni compilazione.|  
|Hint di tabella senza WITH|È stata rilevata un'istruzione che usano hint di tabella ma non la parola chiave WITH. Modificare le istruzioni in modo che includano la parola WITH. Si verifica una volta per ogni compilazione.|  
|Opzione di tabella text in row|Sono stati rilevati riferimenti all'opzione di tabella 'text in row'. Utilizzare sp_tableoption 'large value types out of row'. Si verifica una volta per ogni query.|  
|TEXTPTR|Sono stati rilevati riferimenti alla funzione TEXTPTR. Riscrivere le applicazioni in modo che utilizzino il tipo di dati **varchar(max)** e rimuovere la sintassi dei tipi di dati **text**, **ntext**e **image** . Si verifica una volta per ogni query.|  
|TEXTVALID|Sono stati rilevati riferimenti alla funzione TEXTVALID. Riscrivere le applicazioni in modo che utilizzino il tipo di dati **varchar(max)** e rimuovere la sintassi dei tipi di dati **text**, **ntext**e **image** . Si verifica una volta per ogni query.|  
|timestamp|Numero totale di volte in cui è stato rilevato il tipo di dati deprecato **timestamp** in un'istruzione DDL. In alternativa, usare il tipo di dati **rowversion** .|  
|UPDATETEXT o WRITETEXT|È stata rilevata l'istruzione UPDATETEXT o WRITETEXT. Riscrivere le applicazioni in modo che utilizzino il tipo di dati **varchar(max)** e rimuovere la sintassi dei tipi di dati **text**, **ntext**e **image** . Si verifica una volta per ogni query.|  
|USER_ID|Sono stati rilevati riferimenti alla funzione USER_ID. Usare la funzione DATABASE_PRINCIPAL_ID. Si verifica una volta per ogni compilazione.|  
|Utilizzo di OLEDB per server collegati||  
|Formato di archiviazione vardecimal|È stato rilevato l'utilizzo del formato di archiviazione **vardecimal** . Usare la compressione dei dati.|  
|XMLDATA|È stata rilevata la sintassi FOR XML. Usare la generazione XSD per le modalità RAW e AUTO. Non sono disponibili sostituzioni per la modalità esplicita. Si verifica una volta per ogni compilazione.|  
|XP_API|È stata rilevata un'istruzione di una stored procedure estesa. Non usare.|  
|xp_grantlogin|È stata rilevata la procedura xp_grantlogin. In alternativa, usare CREATE LOGIN. Si verifica una volta per ogni compilazione.|  
|xp_loginconfig|È stata rilevata la procedura xp_loginconfig. In alternativa, usare l'argomento IsIntegratedSecurityOnly di SERVERPROPERTY. Si verifica una volta per ogni query.|  
|xp_revokelogin|È stata rilevata la procedura xp_revokelogin. In alternativa, usare ALTER LOGIN DISABLE o DROP LOGIN. Si verifica una volta per ogni compilazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità del Motore di database deprecate in SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funzionalità deprecate della ricerca full-text in SQL Server 2016](../../relational-databases/search/deprecated-full-text-search-features-in-sql-server-2016.md)   
 [Classe di evento Deprecation Announcement](../../relational-databases/event-classes/deprecation-announcement-event-class.md)   
 [Classe di evento Deprecation Final Support](../../relational-databases/event-classes/deprecation-final-support-event-class.md)   
 [Funzionalità del motore di database non più usate in SQL Server 2016](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Funzionalità della ricerca full-text non più supportate in SQL Server 2016](https://msdn.microsoft.com/library/70587b3c-cc77-4681-924d-a1df7cdf1517)   
 [Utilizzare oggetti di SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md)  
  
  
