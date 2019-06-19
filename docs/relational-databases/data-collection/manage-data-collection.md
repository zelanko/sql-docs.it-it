---
title: Gestire la raccolta di dati | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
keywords:
- Raccolta dati
helpviewer_keywords:
- data collection [SQL Server]
- data collector [SQL Server], Transact-SQL
- data collector [SQL Server], SQL Server Management Studio
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 023d0f1e720965725438682ce7df8b035d43620f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63051808"
---
# <a name="manage-data-collection"></a>Gestire raccolta dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 Usare le stored procedure e le funzioni di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] per gestire aspetti diversi della raccolta dati, ad esempio l'abilitazione o la disabilitazione della raccolta dati, la modifica della configurazione di un set di raccolta o la visualizzazione di dati nel data warehouse di gestione.  
  
## <a name="manage-data-collection-using-ssms"></a>Gestire la raccolta di dati mediante SSMS  
 In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eseguire le seguenti attività legate all'agente di raccolta dati usando Esplora oggetti:  
  
-   [Configurazione del data warehouse di gestione &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [Configurare le proprietà di un agente di raccolta dati](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)  
  
-   [Abilitazione o disabilitazione della raccolta dati](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [Avviare o arrestare un set di raccolta](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [Utilizzo di SQL Server Profiler per creare un set di raccolta Traccia SQL &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/use-sql-server-profiler-to-create-a-sql-trace-collection-set.md)  
  
-   [Visualizzazione dei log dei set di raccolta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-collection-set-logs-sql-server-management-studio.md)  
  
-   [Visualizzazione o modifica delle pianificazioni dei set di raccolta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [Visualizzare un report sui set di raccolta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
## <a name="manage-data-collection-using-transact-sql"></a>Gestire la raccolta dati mediante Transact-SQL  
 L'agente di raccolta dati fornisce una vasta raccolta di stored procedure che è possibile utilizzare per eseguire qualsiasi attività relative alla raccolta dati. Ad esempio, con [!INCLUDE[tsql](../../includes/tsql-md.md)]è possibile eseguire le attività indicate di seguito:  
  
-   [Configurazione dei parametri per la raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md)  
  
-   [Abilitazione o disabilitazione della raccolta dati](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [Avviare o arrestare un set di raccolta](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [Creazione di un set di raccolta personalizzato che utilizza il tipo agente di raccolta Query T-SQL generico &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)  
  
-   [Aggiunta di un elemento della raccolta a un set di raccolta &#40;Transact-SQL&#41;](../../relational-databases/data-collection/add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 Sono inoltre disponibili funzioni e viste che è possibile utilizzare per ottenere dati di configurazione per i database msdb e del data warehouse di gestione, dati del log di esecuzione e dati archiviati nel data warehouse di gestione.  
  
 È possibile utilizzare le stored procedure, le funzioni e le viste fornite per creare i propri scenari di raccolta dati end-to-end.  
  
>**IMPORTANTE!!** A differenza delle normali stored procedure, le stored procedure dell'agente di raccolta dati utilizzano parametri fortemente tipizzati e non supportano la conversione automatica del tipo di dati. Se tali parametri non vengono chiamati con i tipi di dati corretti per i parametri di input, come indicato nella descrizione dell'argomento, la stored procedure restituisce un errore.  
  
 Usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare ed eseguire gli esempi di codice forniti. Per altre informazioni, vedere [Esplora oggetti](../../ssms/object/object-explorer.md). In alternativa, è possibile creare la query con un editor qualsiasi e salvarla in un file di testo con estensione sql. È possibile eseguire la query dal prompt dei comandi di Windows mediante l'utilità **sqlcmd** . Per altre informazioni, vedere [Usare l'utilità sqlcmd](../../relational-databases/scripting/sqlcmd-use-the-utility.md).  
  
### <a name="stored-procedures-and-views"></a>Stored procedure e viste  
 **Utilizzo dell'agente di raccolta dati**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare l'agente di raccolta dati.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)|Abilitare l'agente di raccolta dati|  
|[sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)|Disabilitare l'agente di raccolta dati.|  
  
 **Utilizzo dei set di raccolta**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare i set di raccolta.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_run_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)|Eseguire un set di raccolta su richiesta.|  
|[sp_syscollector_start_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md)|Avviare un set di raccolta.|  
|[sp_syscollector_stop_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)|Arresto di un set di raccolta.|  
|[sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)|Creare un set di raccolta.|  
|[sp_syscollector_delete_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql.md)|Eliminare un set di raccolta.|  
|[sp_syscollector_update_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql.md)|Modificare la configurazione di un set di raccolta.|  
|[sp_syscollector_upload_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql.md)|Caricare i dati relativi a un set di raccolta nel data warehouse di gestione. Si tratta infatti di un caricamento su richiesta.|  
  
 **Utilizzo di elementi della raccolta**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare gli elementi della raccolta.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)|Creare un elemento della raccolta.|  
|[sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)|Eliminare un elemento della raccolta.|  
|[sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)|Caricare un elemento della raccolta.|  
  
 **Utilizzo dei tipi di agente di raccolta**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare i tipi di agente di raccolta.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_create_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql.md)|Creare un tipo di agente di raccolta.|  
|[sp_syscollector_update_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql.md)|Aggiornare un tipo di agente di raccolta.|  
|[sp_syscollector_delete_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql.md)|Eliminare un tipo di agente di raccolta.|  
  
 **Come ottenere informazioni sulla configurazione**  
  
 Nella tabella seguente vengono descritte le viste che è possibile utilizzare per ottenere informazioni di configurazione e dati del log di esecuzione.  
  
|Nome della vista|Descrizione|  
|---------------|-----------------|  
|[syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|Ottenere la configurazione dell'agente di raccolta dati.|  
|[syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|Ottenere informazioni su un elemento della raccolta.|  
|[syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|Ottenere informazioni su un set di raccolta.|  
|[syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|Ottenere informazioni sul tipo di agente di raccolta.|  
|[syscollector_execution_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|Ottenere informazioni sul set di raccolta ed esecuzione del pacchetto.|  
|[syscollector_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)|Ottenere informazioni sull'esecuzione dell'attività.|  
|[syscollector_execution_log_full &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|Ottenere informazioni quando il log di esecuzione è pieno.|  
  
 **Configurazione dell'accesso al data warehouse di gestione.**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per configurare l'accesso al data warehouse di gestione.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_set_warehouse_database_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)|Specificare il nome del database definito nella stringa di connessione per il data warehouse di gestione.|  
|[sp_syscollector_set_warehouse_instance_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)|Specificare l'istanza definita nella stringa di connessione per il data warehouse di gestione.|  
  
 **Configurazione del data warehouse di gestione.**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare la configurazione del data warehouse di gestione.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[core.sp_create_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql.md)|Creare uno snapshot di raccolta nel data warehouse di gestione.|  
|[core.sp_update_data_source &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql.md)|Aggiornare l'origine dati per la raccolta dati.|  
|[core.sp_add_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql.md)|Aggiungere un tipo di agente di raccolta al data warehouse di gestione.|  
|[core.sp_remove_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql.md)|Rimuovere un tipo di agente di raccolta dal data warehouse di gestione.|  
|[core.sp_purge_data &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql.md)|Eliminare dati dal data warehouse di gestione.|  
  
 **Utilizzo dei pacchetti di caricamento**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare i pacchetti di caricamento.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)|Configurare il numero di tentativi di caricamento dei dati.|  
|[sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)|Specificare l'archiviazione temporanea dei dati tra i tentativi di caricamento.|  
  
 **Utilizzo del log di esecuzione della raccolta dati**  
  
 Nella tabella seguente vengono descritte le stored procedure che è possibile eseguire per utilizzare il log di esecuzione della raccolta dati.  
  
|Nome della stored procedure|Descrizione|  
|--------------------|-----------------|  
|[sp_syscollector_delete_execution_log_tree &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql.md)|Eliminare voci relative al set di raccolta dal log di esecuzione.|  
  
### <a name="functions"></a>Funzioni  
 Nella tabella seguente vengono descritte le funzioni che è possibile utilizzare per ottenere informazioni di esecuzione e di traccia.  
  
|Nome funzione|Descrizione|  
|-------------------|-----------------|  
|[fn_syscollector_get_execution_details &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md)|Ottenere dati del log di esecuzione [!INCLUDE[ssIS](../../includes/ssis-md.md)] relativi a un pacchetto specifico.|  
|[fn_syscollector_get_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql.md)|Ottenere statistiche di esecuzione relative a un set di raccolta o un pacchetto. Tali informazioni comprendono gli errori registrati.|  
|[snapshots.fn_trace_getdata &#40;Transact-SQL&#41;](../../relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql.md)|Ottenere gli eventi registrati quando viene utilizzato il tipo di agente di raccolta Traccia SQL generico per raccogliere dati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire una stored procedure](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)   
 [Utilizzo di SQL Server Management Studio](https://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)  
  
  
