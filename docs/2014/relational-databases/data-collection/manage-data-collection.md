---
title: Gestire la raccolta di dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
- data collector [SQL Server], Transact-SQL
- data collector [SQL Server], SQL Server Management Studio
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 543f972f5c5805bb1508b6a256f7a7ed3a2aaa3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918593"
---
# <a name="manage-data-collection"></a>Gestire raccolta dati
  È possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] stored procedure e funzioni per gestire aspetti diversi della raccolta dati, ad esempio l'abilitazione o disabilitazione della raccolta di dati, la modifica di una raccolta di set di configurazione o la visualizzazione dei dati nel data warehouse di gestione .  
  
## <a name="manage-data-collection-by-using-sql-server-management-studio"></a>Gestire la raccolta dati tramite SQL Server Management Studio  
 In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è possibile eseguire le seguenti attività legate all'agente di raccolta dati utilizzando Esplora oggetti:  
  
-   [Configurazione del data warehouse di gestione &#40;SQL Server Management Studio&#41;](configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [Configurare le proprietà di un agente di raccolta dati](configure-properties-of-a-data-collector.md)  
  
-   [Abilitazione o disabilitazione della raccolta dati](data-collection.md)  
  
-   [Avviare o arrestare un set di raccolta](start-or-stop-a-collection-set.md)  
  
-   [Utilizzo di SQL Server Profiler per creare un set di raccolta Traccia SQL &#40;SQL Server Management Studio&#41;](use-sql-server-profiler-to-create-a-sql-trace-collection-set.md)  
  
-   [Visualizzazione dei log dei set di raccolta &#40;SQL Server Management Studio&#41;](view-collection-set-logs-sql-server-management-studio.md)  
  
-   [Visualizzazione o modifica delle pianificazioni dei set di raccolta &#40;SQL Server Management Studio&#41;](view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [Visualizzare un report sui set di raccolta &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
## <a name="manage-data-collection-by-using-transact-sql"></a>Gestione della raccolta dati tramite Transact-SQL  
 L'agente di raccolta dati fornisce una vasta raccolta di stored procedure che è possibile utilizzare per eseguire qualsiasi attività relative alla raccolta dati. Ad esempio, con [!INCLUDE[tsql](../../includes/tsql-md.md)]è possibile eseguire le attività indicate di seguito:  
  
-   [Configurazione dei parametri per la raccolta dati &#40;Transact-SQL&#41;](configure-data-collection-parameters-transact-sql.md)  
  
-   [Abilitazione o disabilitazione della raccolta dati](data-collection.md)  
  
-   [Avviare o arrestare un set di raccolta](start-or-stop-a-collection-set.md)  
  
-   [Creazione di un set di raccolta personalizzato che utilizza il tipo agente di raccolta Query T-SQL generico &#40;Transact-SQL&#41;](create-custom-collection-set-generic-t-sql-query-collector-type.md)  
  
-   [Aggiunta di un elemento della raccolta a un set di raccolta &#40;Transact-SQL&#41;](add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 Sono inoltre disponibili funzioni e viste che è possibile utilizzare per ottenere dati di configurazione per i database msdb e del data warehouse di gestione, dati del log di esecuzione e dati archiviati nel data warehouse di gestione.  
  
 È possibile utilizzare le stored procedure, le funzioni e le viste fornite per creare i propri scenari di raccolta dati end-to-end.  
  
> [!IMPORTANT]  
>  A differenza delle normali stored procedure, le stored procedure dell'agente di raccolta dati utilizzano parametri fortemente tipizzati e non supportano la conversione automatica del tipo di dati. Se tali parametri non vengono chiamati con i tipi di dati corretti per i parametri di input, come indicato nella descrizione dell'argomento, la stored procedure restituisce un errore.  
  
 È possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare ed eseguire gli esempi di codice forniti. Per altre informazioni, vedere [Esplora oggetti](../../ssms/object/object-explorer.md). In alternativa, è possibile creare la query con un editor qualsiasi e salvarla in un file di testo con estensione sql. È possibile eseguire la query dal prompt dei comandi di Windows mediante l'utilità `sqlcmd`. Per altre informazioni, vedere [Usare l'utilità sqlcmd](../scripting/sqlcmd-use-the-utility.md).  
  
### <a name="stored-procedures-and-views"></a>Stored procedure e viste  
 **Utilizzo dell'agente di raccolta dati**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare l'agente di raccolta dati.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql)|Abilitare l'agente di raccolta dati|  
|[sp_syscollector_disable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql)|Disabilitare l'agente di raccolta dati.|  
  
 **Utilizzo dei set di raccolta**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare i set di raccolta.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_run_collection_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql)|Eseguire un set di raccolta su richiesta.|  
|[sp_syscollector_start_collection_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql)|Avviare un set di raccolta.|  
|[sp_syscollector_stop_collection_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql)|Arresto di un set di raccolta.|  
|[sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql)|Creare un set di raccolta.|  
|[sp_syscollector_delete_collection_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql)|Eliminare un set di raccolta.|  
|[sp_syscollector_update_collection_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql)|Modificare la configurazione di un set di raccolta.|  
|[sp_syscollector_upload_collection_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql)|Caricare i dati relativi a un set di raccolta nel data warehouse di gestione. Si tratta infatti di un caricamento su richiesta.|  
  
 **Utilizzo di elementi della raccolta**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare gli elementi della raccolta.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql)|Creare un elemento della raccolta.|  
|[sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql)|Eliminare un elemento della raccolta.|  
|[sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql)|Caricare un elemento della raccolta.|  
  
 **Utilizzo dei tipi di agente di raccolta**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare i tipi di agente di raccolta.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_create_collector_type &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql)|Creare un tipo di agente di raccolta.|  
|[sp_syscollector_update_collector_type &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql)|Aggiornare un tipo di agente di raccolta.|  
|[sp_syscollector_delete_collector_type &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql)|Eliminare un tipo di agente di raccolta.|  
  
 **Come ottenere informazioni sulla configurazione**  
  
 Nella tabella seguente vengono descritte le viste che è possibile utilizzare per ottenere informazioni di configurazione e dati del log di esecuzione.  
  
|Nome della vista|Descrizione|  
|---------------|-----------------|  
|[syscollector_config_store &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-config-store-transact-sql)|Ottenere la configurazione dell'agente di raccolta dati.|  
|[syscollector_collection_items &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-collection-items-transact-sql)|Ottenere informazioni su un elemento della raccolta.|  
|[syscollector_collection_sets &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql)|Ottenere informazioni su un set di raccolta.|  
|[syscollector_collector_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-collector-types-transact-sql)|Ottenere informazioni sul tipo di agente di raccolta.|  
|[syscollector_execution_log &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-execution-log-transact-sql)|Ottenere informazioni sul set di raccolta ed esecuzione del pacchetto.|  
|[syscollector_execution_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql)|Ottenere informazioni sull'esecuzione dell'attività.|  
|[syscollector_execution_log_full &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql)|Ottenere informazioni quando il log di esecuzione è pieno.|  
  
 **Configurazione dell'accesso al data warehouse di gestione.**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per configurare l'accesso al data warehouse di gestione.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_set_warehouse_database_name &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql)|Specificare il nome del database definito nella stringa di connessione per il data warehouse di gestione.|  
|[sp_syscollector_set_warehouse_instance_name &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql)|Specificare l'istanza definita nella stringa di connessione per il data warehouse di gestione.|  
  
 **Configurazione del data warehouse di gestione.**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare la configurazione del data warehouse di gestione.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[core.sp_create_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql)|Creare uno snapshot di raccolta nel data warehouse di gestione.|  
|[core.sp_update_data_source &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql)|Aggiornare l'origine dati per la raccolta dati.|  
|[core.sp_add_collector_type &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql)|Aggiungere un tipo di agente di raccolta al data warehouse di gestione.|  
|[core.sp_remove_collector_type &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql)|Rimuovere un tipo di agente di raccolta dal data warehouse di gestione.|  
|[core.sp_purge_data &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql)|Eliminare dati dal data warehouse di gestione.|  
  
 **Utilizzo dei pacchetti di caricamento**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare i pacchetti di caricamento.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql)|Configurare il numero di tentativi di caricamento dei dati.|  
|[sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql)|Specificare l'archiviazione temporanea dei dati tra i tentativi di caricamento.|  
  
 **Utilizzo del log di esecuzione della raccolta dati**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare il log di esecuzione della raccolta dati.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_delete_execution_log_tree &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql)|Eliminare voci relative al set di raccolta dal log di esecuzione.|  
  
### <a name="functions"></a>Funzioni  
 Nella tabella seguente vengono descritte le funzioni che è possibile utilizzare per ottenere informazioni di esecuzione e di traccia.  
  
|Nome funzione|Descrizione|  
|-------------------|-----------------|  
|[fn_syscollector_get_execution_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql)|Ottenere dati del log di esecuzione [!INCLUDE[ssIS](../../includes/ssis-md.md)] relativi a un pacchetto specifico.|  
|[fn_syscollector_get_execution_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql)|Ottenere statistiche di esecuzione relative a un set di raccolta o un pacchetto. Tali informazioni comprendono gli errori registrati.|  
|[snapshots.fn_trace_getdata &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql)|Ottenere gli eventi registrati quando viene utilizzato il tipo di agente di raccolta Traccia SQL generico per raccogliere dati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire una stored procedure](../stored-procedures/execute-a-stored-procedure.md)   
 [Utilizzo di SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)   
 [Raccolta dati](data-collection.md)  
  
  
