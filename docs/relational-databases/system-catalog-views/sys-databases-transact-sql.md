---
title: sys. databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- databases
- databases_TSQL
- sys.databases
- sys.databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.databases catalog view
ms.assetid: 46c288c1-3410-4d68-a027-3bbf33239289
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a307cf2fb9747e822cc48ca4b0723aed437d4af7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74165954"
---
# <a name="sysdatabases-transact-sql"></a>sys.databases (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Contiene una riga per ogni database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Se un `ONLINE`database non è o `AUTO_CLOSE` è impostato su `ON` e il database è chiuso, i valori di alcune colonne possono essere. `NULL` Se un database è `OFFLINE`, la riga corrispondente non è visibile agli utenti con privilegi limitati. Per visualizzare la riga corrispondente se il database è `OFFLINE`, un utente deve disporre almeno dell' `ALTER ANY DATABASE` autorizzazione a livello di server oppure l' `CREATE DATABASE` autorizzazione nel `master` database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome del database univoco in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o in un server [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**database_id**|**int**|ID del database univoco in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o in un server [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**source_database_id**|**int**|Non-NULL = ID del database di origine di questo snapshot di database.<br /> NULL = Non è uno snapshot di database.|  
|**owner_sid**|**varbinary(85)**|ID di sicurezza (SID) del proprietario esterno del database, registrato nel server. Per informazioni sugli utenti che possono essere proprietari di un database, vedere la sezione **ALTER AUTHORIZATION for Databases** di [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).|  
|**create_date**|**datetime**|Data di creazione o di ridenominazione del database. Per **tempdb**, questo valore viene modificato ogni volta che il server viene riavviato.|  
|**compatibility_level**|**tinyint**|Integer corrispondente alla versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per cui è compatibile il comportamento:<br /> **Valore** &#124; **si applica a**<br /> 70 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 80 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 90 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /> 100 &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive e[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 110 &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive e[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 120 &#124; [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e versioni successive e[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 130 &#124; [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versioni successive<br /> 140 &#124; [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e versioni successive <br /> 150 &#124;[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]  |  
|**collation_name**|**sysname**|Regole di confronto per il database. Rappresentano le regole di confronto predefinite nel database.<br /> NULL = Il database non è online o l'opzione AUTO_CLOSE è impostata su ON e il database è chiuso.|  
|**user_access**|**tinyint**|Impostazione per l'accesso utente:<br /> 0 = MULTI_USER specificato<br /> 1 = SINGLE_USER specificato<br /> 2 = RESTRICTED_USER specificato|  
|**user_access_desc**|**nvarchar (60)**|Descrizione dell'impostazione per l'accesso utente.|  
|**is_read_only**|**bit**|1 = Il database è READ_ONLY<br /> 0 = Il database è READ_WRITE|  
|**is_auto_close_on**|**bit**|1 = AUTO_CLOSE è ON<br /> 0 = AUTO_CLOSE è OFF|  
|**is_auto_shrink_on**|**bit**|1 = AUTO_SHRINK è ON<br /> 0 = AUTO_SHRINK è OFF|  
|**state**|**tinyint**|**Valore &#124; si applica a**<br /> 0 = ONLINE <br /> 1 = RESTORING <br /> 2 = ripristino &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive<br /> 3 = RECOVERY_PENDING &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive<br /> 4 = SUSPECT <br /> 5 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] di emergenza e versioni successive<br /> 6 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] offline e versioni successive<br /> 7 = copia di [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] &#124;[!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /> 10 = OFFLINE_SECONDARY &#124; [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)][!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /><br /> **Nota:** Per Always On database, eseguire una `database_state` query `database_state_desc` sulle colonne o di [sys. dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).|  
|**state_desc**|**nvarchar (60)**|Descrizione dello stato del database. Vedere stato.|  
|**is_in_standby**|**bit**|Il database è di sola lettura per il log di ripristino.|  
|**is_cleanly_shutdown**|**bit**|1 = Il database è stato chiuso normalmente, recupero non necessario all'avvio<br /> 0 = Il database non è stato chiuso normalmente, recupero necessario all'avvio|  
|**is_supplemental_logging_enabled**|**bit**|1 = SUPPLEMENTAL_LOGGING è ON<br /> 0 = SUPPLEMENTAL_LOGGING è OFF|  
|**snapshot_isolation_state**|**tinyint**|Stato delle transazioni di isolamento dello snapshot consentite, in base all'impostazione ALLOW_SNAPSHOT_ISOLATION:<br /> 0 = Lo stato di isolamento dello snapshot è OFF (valore predefinito). L'isolamento dello snapshot non è consentito.<br /> 1 = Lo stato di isolamento dello snapshot è ON. L'isolamento dello snapshot è consentito.<br /> 2 = Lo stato di isolamento dello snapshot è in transizione verso lo stato OFF. Tutte le modifiche delle transazioni hanno un numero di versione. Non è possibile avviare nuove transazioni utilizzando l'isolamento dello snapshot. Il database resta in transizione verso lo stato OFF fino a quando tutte le transazioni attive al momento dell'esecuzione di ALTER DATABASE non vengono completate.<br /> 3 = Lo stato di isolamento dello snapshot è in transizione verso lo stato ON. Le modifiche delle nuove transazioni hanno un numero di versione. Le transazioni non possono utilizzare l'isolamento dello snapshot fino a quando lo stato di isolamento non diventa 1 (ON). Il database resta in transizione verso lo stato ON fino a quando tutte le transazioni di aggiornamento attive al momento dell'esecuzione di ALTER DATABASE non vengono completate.|  
|**snapshot_isolation_state_desc**|**nvarchar (60)**|Descrizione dello stato delle transazioni di isolamento dello snapshot consentite, in base all'opzione ALLOW_SNAPSHOT_ISOLATION.|  
|**is_read_committed_snapshot_on**|**bit**|1 = Opzione READ_COMMITTED_SNAPSHOT impostata su ON. Le operazioni di lettura con il livello di isolamento Read committed sono basate sulle analisi snapshot e non acquisiscono blocchi.<br /> 0 = Opzione READ_COMMITTED_SNAPSHOT impostata su OFF (impostazione predefinita). Le operazioni di lettura con il livello di isolamento Read committed utilizzano i blocchi di condivisione.|  
|**recovery_model**|**tinyint**|Modello di recupero selezionato:<br /> 1 = FULL<br /> 2 = BULK_LOGGED<br /> 3 = SIMPLE|  
|**recovery_model_desc**|**nvarchar (60)**|Descrizione del modello di recupero selezionato.|  
|**page_verify_option**|**tinyint**|Impostazione dell'opzione PAGE_VERIFY:<br /> 0 = NONE<br /> 1 = TORN_PAGE_DETECTION<br /> 2 = CHECKSUM|  
|**page_verify_option_desc**|**nvarchar (60)**|Descrizione dell'impostazione dell'opzione PAGE_VERIFY.|  
|**is_auto_create_stats_on**|**bit**|1 = AUTO_CREATE_STATISTICS è ON<br /> 0 = AUTO_CREATE_STATISTICS è OFF|  
|**is_auto_create_stats_incremental_on**|**bit**|Indica l'impostazione predefinita per l'opzione incrementale delle statistiche automatiche.<br /> 0 = Le statistiche a creazione automatica sono non incrementali<br /> 1 = Le statistiche a creazione automatica sono incrementali, se possibile<br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e versioni successive.|  
|**is_auto_update_stats_on**|**bit**|1 = AUTO_UPDATE_STATISTICS è ON<br /> 0 = AUTO_UPDATE_STATISTICS è OFF|  
|**is_auto_update_stats_async_on**|**bit**|1 = AUTO_UPDATE_STATISTICS_ASYNC è ON<br /> 0 = AUTO_UPDATE_STATISTICS_ASYNC è OFF|  
|**is_ansi_null_default_on**|**bit**|1 = ANSI_NULL_DEFAULT è ON<br /> 0 = ANSI_NULL_DEFAULT è OFF|  
|**is_ansi_nulls_on**|**bit**|1 = ANSI_NULLS è ON<br /> 0 = ANSI_NULLS è OFF|  
|**is_ansi_padding_on**|**bit**|1 = ANSI_PADDING è ON<br /> 0 = ANSI_PADDING è OFF|  
|**is_ansi_warnings_on**|**bit**|1 = ANSI_WARNINGS è ON<br /> 0 = ANSI_WARNINGS è OFF|  
|**is_arithabort_on**|**bit**|1 = ARITHABORT è ON<br /> 0 = ARITHABORT è OFF|  
|**is_concat_null_yields_null_on**|**bit**|1 = CONCAT_NULL_YIELDS_NULL è ON<br /> 0 = CONCAT_NULL_YIELDS_NULL è OFF|  
|**is_numeric_roundabort_on**|**bit**|1 = NUMERIC_ROUNDABORT è ON<br /> 0 = NUMERIC_ROUNDABORT è OFF|  
|**is_quoted_identifier_on**|**bit**|1 = QUOTED_IDENTIFIER è ON<br /> 0 = QUOTED_IDENTIFIER è OFF|  
|**is_recursive_triggers_on**|**bit**|1 = RECURSIVE_TRIGGERS è ON<br /> 0 = RECURSIVE_TRIGGERS è OFF|  
|**is_cursor_close_on_commit_on**|**bit**|1 = CURSOR_CLOSE_ON_COMMIT è ON<br /> 0 = CURSOR_CLOSE_ON_COMMIT è OFF|  
|**is_local_cursor_default**|**bit**|1 = CURSOR_DEFAULT è locale<br /> 0 = CURSOR_DEFAULT è globale|  
|**is_fulltext_enabled**|**bit**|1 = La funzionalità full-text è abilitata per il database<br /> 0 = La funzionalità full-text è disabilitata per il database|  
|**is_trustworthy_on**|**bit**|1 = Database contrassegnato come attendibile<br /> 0 = Database non contrassegnato come attendibile<br /> Per impostazione predefinita, i database ripristinati o collegati hanno la proprietà TRUSTWORTHY non abilitata.|  
|**is_db_chaining_on**|**bit**|1 = Il concatenamento della proprietà tra database è impostato su ON<br /> 0 = Il concatenamento della proprietà tra database è impostato su OFF|  
|**is_parameterization_forced**|**bit**|1 = La parametrizzazione è FORCED<br /> 0 = La parametrizzazione è SIMPLE|  
|**is_master_key_encrypted_by_server**|**bit**|1 = Il database include una chiave master crittografata<br /> 0 = Il database non include una chiave master crittografata|  
|**is_query_store_on**|**bit**|1 = l'archivio query è abilitato per il database. Controllare [sys. database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) per visualizzare lo stato dell'archivio query.<br /> 0 = l'archivio query non è abilitato<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (e versioni successive).|  
|**is_published**|**bit**|1 = Database di pubblicazione in una topologia di replica snapshot o transazionale<br /> 0 = Il database non è un database di pubblicazione|  
|**is_subscribed**|**bit**|Questa colonna non viene utilizzata. Restituirà sempre 0, indipendentemente dallo stato del sottoscrittore del database.|  
|**is_merge_published**|**bit**|1 = Database di pubblicazione in una topologia di replica di tipo merge<br /> 0 = Il database non è un database di pubblicazione in una topologia di replica di tipo merge|  
|**is_distributor**|**bit**|1 = Database di distribuzione per una topologia di replica<br /> 0 = Il database non è un database di distribuzione per una topologia di replica|  
|**is_sync_with_backup**|**bit**|1 = Database contrassegnato per la sincronizzazione della replica con backup<br /> 0 = Database non contrassegnato per la sincronizzazione della replica con backup|  
|**service_broker_guid**|**uniqueidentifier**|Identificatore di Service Broker per questo database. Utilizzato come **broker_instance** della destinazione nella tabella di routing.|  
|**is_broker_enabled**|**bit**|1 = Il broker nel database sta inviando e ricevendo messaggi.<br /> 0 = Tutti i messaggi inviati resteranno nella coda di trasmissione e i messaggi ricevuti non verranno inseriti nelle code in questo database.<br /> Per impostazione predefinita, Service Broker è disabilitato per i database ripristinati o collegati, L'eccezione è rappresentata dal mirroring del database, in cui Service Broker viene abilitato dopo il failover.|  
|**log_reuse_wait**|**tinyint**|Il riutilizzo dello spazio del log delle transazioni è attualmente in attesa di uno dei seguenti elementi a partire dall'ultimo checkpoint. Per una spiegazione più dettagliata di questi valori, vedere [il log delle transazioni](../../relational-databases/logs/the-transaction-log-sql-server.md).<br /> **Valore &#124; si applica a**<br /> 0 = Nessuno<br />   1 = Checkpoint (quando un database utilizza un modello di recupero e ha un filegroup di dati ottimizzato per la memoria, è necessario `log_reuse_wait` che la colonna indichi checkpoint o xtp_checkpoint) [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] &#124; e versioni successive<br />  2 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] backup del log e versioni successive<br />  3 = backup attivo o ripristino &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive<br />  4 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] transazioni attive e versioni successive<br />  5 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] mirroring del database e versioni successive<br />  6 = &#124; [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] di replica e versioni successive<br />  7 = Creazione di snapshot del [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] database &#124; e versioni successive<br />  8 = Analisi del log <br />  9 = una Always On replica secondaria dei gruppi di disponibilità applica i record del log delle transazioni del database a un database secondario corrispondente. &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive<br />  9 = altro (temporaneo) &#124; fino a e include[!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]<br />  10 = solo per uso interno &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive<br />  11 = solo per uso interno &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive<br /> 12 = solo per uso interno &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive<br />13 = &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] di pagina meno recente e versioni successive<br /> 14 = altri &#124; [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive<br />  16 = XTP_CHECKPOINT (quando un database utilizza un modello di recupero e ha un filegroup di dati ottimizzato per la memoria, è necessario che la colonna log_reuse_wait indichi checkpoint o xtp_checkpoint) [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] &#124; e versioni successive|  
|**log_reuse_wait_desc**|**nvarchar (60)**|La descrizione del riutilizzo dello spazio del log delle transazioni è attualmente in attesa come ultimo checkpoint.|  
|**is_date_correlation_on**|**bit**|1 = DATE_CORRELATION_OPTIMIZATION è ON<br /> 0 = DATE_CORRELATION_OPTIMIZATION è OFF|  
|**is_cdc_enabled**|**bit**|1 = Database abilitato per l'acquisizione dei dati delle modifiche. Per ulteriori informazioni, vedere [sys. sp_cdc_enable_db &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md).|  
|**is_encrypted**|**bit**|Indica se il database è crittografato (riflette l'ultimo stato impostato utilizzando la `ALTER DATABASE SET ENCRYPTION` clausola). Può avere uno dei valori seguenti:<br /> 1 = Crittografato<br /> 0 = Non crittografato<br /> Per altre informazioni sulla crittografia del database, vedere [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).<br /> Se è in corso la decrittografia del database, `is_encrypted` viene visualizzato un valore pari a 0. Per visualizzare lo stato del processo di crittografia, è possibile utilizzare la vista a gestione dinamica [sys. dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .|  
|**is_honor_broker_priority_on**|**bit**|Indica se il database rispetta le priorità di conversazione (riflette l'ultimo stato impostato utilizzando la `ALTER DATABASE SET HONOR_BROKER_PRIORITY` clausola). Può avere uno dei valori seguenti:<br /> 1 = HONOR_BROKER_PRIORITY è ON<br /> 0 = HONOR_BROKER_PRIORITY è OFF<br /> Per impostazione predefinita, la priorità del broker è disattivata per i database ripristinati o collegati.|  
|**replica_id**|**uniqueidentifier**|Identificatore univoco della replica di disponibilità di [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] locale del gruppo di disponibilità, se presente, di cui fa parte il database.<br /> NULL = il database non fa parte di una replica di disponibilità di un gruppo di disponibilità.<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**group_database_id**|**uniqueidentifier**|Identificatore univoco del database all'interno di un Always On gruppo di disponibilità, se presente, in cui il database partecipa. **group_database_id** è lo stesso per il database nella replica primaria e in ogni replica secondaria in cui il database è stato aggiunto al gruppo di disponibilità.<br /> NULL = il database non fa parte di una replica di disponibilità in alcun gruppo di disponibilità.<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**resource_pool_id**|**int**|L'ID del pool di risorse per cui è stato eseguito il mapping al database. Questa pool di risorse controlla la memoria totale disponibile alle tabelle ottimizzate per la memoria nel database.<br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e versioni successive|  
|**default_language_lcid**|**smallint**|Indica l'ID locale (LCID) della lingua predefinita di un database indipendente.<br /> **Nota:** Funge da [configurare l'opzione di configurazione del server default language](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) di `sp_configure`. Questo valore è **null** per un database non indipendente.<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_language_name**|**nvarchar(128)**|Indica la lingua predefinita di un database indipendente.<br /> Questo valore è **null** per un database non indipendente.<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_lcid**|**int**|Indica l'ID delle impostazioni locali (LCID) della lingua full-text predefinita del database indipendente.<br /> **Nota:** Funziona come impostazione predefinita per [configurare l'opzione di configurazione del server default full-text language](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) di `sp_configure`. Questo valore è **null** per un database non indipendente.<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_name**|**nvarchar(128)**|Indica la lingua full-text predefinita del database indipendente.<br /> Questo valore è **null** per un database non indipendente.<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_nested_triggers_on**|**bit**|Indica se nel database indipendente sono consentiti trigger nidificati.<br /> 0 = I trigger nidificati non sono consentiti<br /> 1 = I trigger nidificati sono consentiti<br /> **Nota:** Funge da [configurare l'opzione di configurazione del server nested triggers](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) di `sp_configure`. Questo valore è **null** per un database non indipendente. Per ulteriori informazioni, vedere [sys. configurations &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) .<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_transform_noise_words_on**|**bit**|Indica se le parole non significative devono essere trasformate nel database indipendente.<br /> 0 = Le parole non significative non devono essere trasformate.<br /> 1 = Le parole non significative devono essere trasformate.<br /> **Nota:** Funziona come [opzione di configurazione del server transform noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) di `sp_configure`. Questo valore è **null** per un database non indipendente. Per ulteriori informazioni, vedere [sys. configurations &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) .<br /> **Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive|  
|**two_digit_year_cutoff**|**smallint**|Indica un valore di un numero compreso tra 1753 e 9999 per rappresentare l'anno di cambio data per l'interpretazione degli anni a due cifre come anni a quattro cifre.<br /> **Nota:** Funziona come `sp_configure`l' [opzione di configurazione del server two digit year cutoff](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) . Questo valore è **null** per un database non indipendente. Per ulteriori informazioni, vedere [sys. configurations &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) .<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**contenimento**|**tinyint non null**|Indica lo stato di indipendenza del database.<br />  0 = L'indipendenza del database è disabilitata. **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 1 = il database è in contenuto parziale **si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive|  
|**containment_desc**|**nvarchar (60) not null**|Indica lo stato di indipendenza del database.<br /> NONE = Database legacy (zero indipendenza)<br /> PARTIAL = Database parzialmente indipendente<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**target_recovery_time_in_seconds**|**int**|Tempo stimato, in secondi, per il recupero del database. Ammette valori Null.<br /> **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability**|**int**|Impostazione di durabilità posticipata:<br /> 0 = DISABILITATO<br /> 1 = CONSENTITO<br /> 2 = FORZATA<br /> Per altre informazioni, vedere [Controllo della durabilità delle transazioni](../../relational-databases/logs/control-transaction-durability.md).<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (e versioni successive [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]) e.|  
|**delayed_durability_desc**|**nvarchar (60)**|Impostazione di durabilità posticipata:<br /> DISABLED<br /> ALLOWED<br /> FORCED<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (e versioni successive [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]) e.|  
|**is_memory_optimized_elevate_to_snapshot_on**|**bit**|Le tabelle con ottimizzazione per la memoria sono accessibili tramite l'isolamento SNAPSHOT quando l'impostazione della sessione HIGH TRANSACTION ISOLATION LEVEL è impostata su un livello di isolamento inferiore, READ COMMITTED o READ UNCOMMITTED.<br /> 1 = Il livello di isolamento minimo è SNAPSHOT.<br /> 0 = Il livello di isolamento non è elevato.|  
|**is_federation_member**|**bit**|Indica se il database è un membro di una federazione.<br /> **Si applica a**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_remote_data_archive_enabled**|**bit**|Indica se il database è allungato.<br /> 0 = il database non è abilitato per l'estensione.<br /> 1 = il database è abilitato per l'estensione.<br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versioni successive<br /> Per altre informazioni, vedere [Stretch Database](../../sql-server/stretch-database/stretch-database.md).|  
|**is_mixed_page_allocation_on**|**bit**|Indica se le tabelle e gli indici del database possono allocare pagine iniziali da extent misti.<br /> 0 = le tabelle e gli indici del database allocano sempre pagine iniziali da extent uniformi.<br /> 1 = le tabelle e gli indici del database possono allocare pagine iniziali da extent misti.<br /> **Si applica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versioni successive<br /> Per ulteriori informazioni, vedere l'opzione SET MIXED_PAGE_ALLOCATION delle [Opzioni ALTER database set &#40;&#41;Transact-SQL ](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**is_temporal_retention_enabled**|**bit**|Indica se l'attività di pulizia dei criteri di conservazione temporale è abilitata.<br /> **Si applica a**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type**|**int**|Impostazione delle regole di confronto del catalogo:<br />0 = DATABASE_DEFAULT<br />2 = SQL_Latin_1_General_CP1_CI_AS<br /> **Si applica a**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**catalog_collation_type_desc**|**nvarchar (60)**|Impostazione delle regole di confronto del catalogo:<br />DATABASE_DEFAULT<br />SQL_Latin_1_General_CP1_CI_AS<br /> **Si applica a**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|
|**is_result_set_caching_on**|**int**|1 = is_result_set_caching_on è on</br>0 = is_result_set_caching_on è disattivato</br>**Si applica a**: Azure SQL data warehouse Gen2. Quando queste funzionalità vengono implementate in tutte le aree, controllare la versione distribuita nell'istanza e le ultime note sulla versione di [Azure SQL DW](/azure/sql-data-warehouse/release-notes-10-0-10106-0) per la disponibilità delle funzionalità.|
  
## <a name="permissions"></a>Autorizzazioni

 Se il chiamante di `sys.databases` non è il proprietario del database e il database `master` non è o `tempdb`, le autorizzazioni minime necessarie per visualizzare la riga corrispondente sono `ALTER ANY DATABASE` o l' `VIEW ANY DATABASE` autorizzazione a livello di server oppure `CREATE DATABASE` l'autorizzazione nel `master` database. Il database a cui è connesso il chiamante può sempre essere visualizzato in `sys.databases`.  
  
> [!IMPORTANT]  
> Per impostazione predefinita, il ruolo public dispone `VIEW ANY DATABASE` dell'autorizzazione, consentendo a tutti gli account di accesso di visualizzare le informazioni sul database. Per bloccare un account di accesso dalla capacità di rilevare un database `REVOKE` , `VIEW ANY DATABASE` l'autorizzazione `public`o `DENY` l' `VIEW ANY DATABASE` autorizzazione per i singoli account di accesso.  
  
## <a name="azure-sql-database-remarks"></a>Osservazioni sul database SQL di Azure

In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] questa vista è disponibile nel `master` database e nei database utente. Nel `master` database, questa vista restituisce le informazioni sul `master` database e tutti i database utente nel server. In un database utente questa vista restituisce informazioni solo sul database corrente e sul database master.  
  
 Utilizzare la vista `sys.databases` nel database `master` del server del [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] in cui viene creato il nuovo database. Una volta avviata la copia del database, è `sys.databases` possibile eseguire `sys.dm_database_copies` una query sulle `master` viste e dal database del server di destinazione per recuperare ulteriori informazioni sullo stato di avanzamento della copia.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-query-the-sysdatabases-view"></a>R. Eseguire una query sulla vista sys.databases

Nell'esempio seguente vengono restituite alcune colonne disponibili nella `sys.databases` vista.  
  
```sql  
SELECT name, user_access_desc, is_read_only, state_desc, recovery_model_desc  
FROM sys.databases;  
```  
  
### <a name="b-check-the-copying-status-in-includesssdsincludessssds-mdmd"></a>B. Verificare lo stato di copia in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]

Nell'esempio seguente viene eseguita `sys.databases` una `sys.dm_database_copies` query sulle viste e per ottenere informazioni su un'operazione di copia del database.  
  
**Si applica a**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql
-- Execute from the master database.  
SELECT a.name, a.state_desc, b.start_date, b.modify_date, b.percentage_complete  
FROM sys.databases AS a  
INNER JOIN sys.dm_database_copies AS b ON a.database_id = b.database_id  
WHERE a.state = 7;  
```

### <a name="c-check-the-temporal-retention-policy-status-in-includesssdsincludessssds-mdmd"></a>C. Verificare lo stato dei criteri di conservazione temporali in[!INCLUDE[ssSDS](../../includes/sssds-md.md)]

Nell'esempio seguente viene eseguita `sys.databases` una query su per restituire informazioni sull'abilitazione dell'attività di pulizia del periodo di memorizzazione temporale. Tenere presente che dopo l'operazione di ripristino la conservazione temporale è disabilitata per impostazione predefinita. Usare `ALTER DATABASE` per abilitarlo in modo esplicito.
  
**Si applica a**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```sql  
-- Execute from the master database.  
SELECT a.name, a.is_temporal_history_retention_enabled 
FROM sys.databases AS a;
```  
  
## <a name="next-steps"></a>Passaggi successivi

- [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)
- [sys. database_mirroring_witnesses &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)
- [sys. database_recovery_status &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-database-recovery-status-transact-sql.md)
- [Viste del catalogo di database e file &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)
- [sys. dm_database_copies &#40;database SQL di Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)  
