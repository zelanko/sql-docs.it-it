---
title: Data warehouse di gestione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], management data warehouse
- data warehouse
- management data warehouse
ms.assetid: 9874a8b2-7ccd-494a-944c-ad33b30b5499
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 26af58e208527d155b5ddf3506be4509627c1f7e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918339"
---
# <a name="management-data-warehouse"></a>data warehouse di gestione
  Il data warehouse di gestione è un database relazionale che contiene i dati raccolti da un server che costituisce una destinazione di raccolta dati. Questi dati vengono utilizzati per generare report per i set di raccolta dati di sistema e possono essere utilizzati anche per creare report personalizzati.  
  
 L'infrastruttura dell'agente di raccolta dati definisce i processi e piani di manutenzione necessari per implementare i criteri di memorizzazione definiti dall'amministratore del database.  
  
> [!IMPORTANT]  
>  Per questa versione dell'agente di raccolta dati il data warehouse di gestione viene creato utilizzando il modello di recupero con registrazione minima per ridurre al minimo la registrazione. È necessario implementare il modello di recupero adatto per la propria organizzazione.  
  
## <a name="deploying-and-using-the-data-warehouse"></a>Distribuzione ed utilizzo del data warehouse  
 È possibile installare il data warehouse di gestione nella stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui viene eseguito l'agente di raccolta dati. Tuttavia, se le risorse del server o le prestazioni costituiscono un problema per il server che si sta monitorando, è possibile installare il data warehouse di gestione in un computer diverso.  
  
 Gli schemi richiesti e i relativi oggetti per i set di raccolta di sistema predefiniti vengono creati quando viene creato il data warehouse di gestione. Gli schemi creati sono core e snapshot. Un terzo schema, custom_snapshots, viene creato quando vengono creati set di raccolta definiti dall'utente nei quali sono inclusi elementi di raccolta che usano il tipo agente di raccolta Query T-SQL generico.  
  
###### <a name="core-schema"></a>Schema core  
 Nello schema core vengono descritte le tabelle, le stored procedure e le viste utilizzate per l'organizzazione e l'identificazione dei dati raccolti. Queste tabelle sono condivise da tutte le tabelle di dati create per singoli tipi di agente di raccolta. Tale schema è bloccato e può essere modificato esclusivamente dal proprietario del database del data warehouse di gestione. Ai nomi delle tabelle di questo schema viene aggiunto il prefisso "core".  
  
 Nella tabella seguente vengono descritte le tabelle di database dello schema core. Grazie a queste tabelle di database l'agente di raccolta dati è in grado di registrare la provenienza dei dati, da chi sono stati inseriti e quando sono stati caricati sul data warehouse.  
  
|Nome tabella|Descrizione|  
|----------------|-----------------|  
|core.performance_counter_report_group_items|Archivia informazioni sul modo in cui i report del data warehouse di gestione devono raggruppare e aggregare i contatori delle prestazioni.|  
|core.snapshots_internal|Identifica ogni nuovo snapshot. Una nuova riga viene inserita in questa tabella ogni volta che un pacchetto di caricamento inizia a caricare un nuovo batch di dati.|  
|core.snapshot_timetable_internal|Archivia informazioni sugli orari degli snapshot. L'ora dello snapshot viene archiviata in una tabella separata in quanto molti snapshot possono verificarsi quasi nello stesso momento.|  
|core.source.info_internal|In questa tabella sono archiviate informazioni sull'origine dati. La tabella viene aggiornata ogni volta che un nuovo set di raccolta comincia a caricare dati nel data warehouse.|  
|core.supported_collector_types_internal|Contiene gli ID dei tipi di agente di raccolta registrati che possono caricare dati nel data warehouse di gestione. Questa tabella viene aggiornata solo quando lo schema del warehouse viene aggiornato per supportare un nuovo tipo di agente di raccolta. Quando viene creato il data warehouse di gestione, questa tabella viene popolata con gli ID dei tipi di agente di raccolta forniti dall'agente di raccolta dati.|  
|core.wait_categories|Contiene le categorie utilizzate per raggruppare i tipi di attesa in base alla caratteristica di wait_type.|  
|core.wait_types|Contiene i tipi di attesa riconosciuti dall'agente di raccolta dati.|  
|core.purge_info_internal|Indica che è stata effettuata una richiesta per arrestare la rimozione di dati dal data warehouse di gestione.|  
  
 Le tabelle precedenti sono utilizzate con le tabelle del tipo di agente di raccolta per archiviare informazioni. Ad esempio, il tipo di agente di raccolta Traccia SQL generico utilizza le tabelle seguenti per archiviare dati di traccia:  
  
-   core.source_info_internal  
  
-   core.snapshots_internal  
  
-   snapshots.trace_info  
  
-   snapshots.trace_data  
  
###### <a name="snapshots-schema"></a>Schema snapshot  
 Lo schema snapshot descrive gli oggetti necessari ad archiviare e gestire i dati raccolti dai tipi di agente di raccolta forniti. Le tabelle contenute in questo schema sono corrette, pertanto non è necessario modificarle per l'intera durata del tipo di agente di raccolta. In caso di necessità, lo schema può essere modificato esclusivamente da membri del ruolo mdw_admin. Queste tabelle sono create per archiviare i dati raccolti dai set di raccolta dati di sistema.  
  
 Nelle tabelle seguenti è illustrata una parte dello schema del data warehouse di gestione richiesta per i set di raccolta Attività server e Statistiche query.  
  
-   Tabelle delle risorse a livello di sistema  
  
    -   **snapshots.os_wait_stats**  
  
    -   **snapshots.os_latch_stats**  
  
    -   **snapshots.os_schedulers**  
  
    -   `snapshots.os_memory_clerks`  
  
    -   **snapshots.os_memory_nodes**  
  
    -   snapshots.sql_process_and_system_memory  
  
-   Attività di sistema  
  
    -   snapshots.active_sessions_and_requests  
  
-   Statistiche query  
  
    -   snapshots.query_stats  
  
-   Statistiche di I/O  
  
    -   `snapshots.io_virtual_file_stats`  
  
-   Testo e piano di query  
  
    -   snapshots.notable_query_text  
  
    -   snapshots.notable_query_plan  
  
-   Statistiche query normalizzate  
  
    -   snapshots.distinct_queries  
  
    -   snapshots.distinct_query_to_handle  
  
 **Schema custom_snapshot**  
  
 Lo schema del custom_snapshots descrive le nuove tabelle e viste create quando per creare set di raccolta definiti dall'utente vengono utilizzati tipi di agente di raccolta standard o di terze parti. Qualora un tipo di agente di raccolta richieda una nuova tabella di dati per un elemento della raccolta può creare tale tabella in questo schema. Possono aggiungere nuove tabelle in questo schema i membri del ruolo mdw_writer. Qualsiasi altra modifica allo schema può essere apportata esclusivamente dai membri del ruolo mdw_admin.  
  
 È possibile ottenere informazioni dettagliate sul contenuto e sul tipo di dati delle colonne delle tabelle di database leggendo la documentazione relativa alla stored procedure dell'agente di raccolta dati appropriata per ciascuna tabella.  
  
### <a name="best-practices"></a>Procedure consigliate  
 Quando si utilizza il data warehouse di gestione si consiglia di attenersi alle seguenti procedure:  
  
-   Non modificare i metadati di tabelle del data warehouse di gestione se non in caso di aggiunta di un nuovo tipo di agente di raccolta.  
  
-   Non modificare direttamente i dati contenuti nel data warehouse di gestione. La modifica dei dati raccolti invalida la legittimità di tali dati.  
  
-   Per accedere ai dati delle istanze e delle applicazioni, anziché utilizzare direttamente le tabelle, avvalersi delle stored procedure e delle funzioni fornite con l'agente di raccolta dati. I nomi e le definizioni delle tabelle possono cambiare, cambiano quando si aggiorna l'applicazione e potrebbero cambiare nelle versioni future.  
  
## <a name="change-history"></a>Cronologia modifiche  
  
|Contenuto aggiornato|  
|---------------------|  
|Aggiunta della tabella core.performance_counter_report_group_items alla sezione "Schema core".|  
|Aggiornamento dell'elenco di tabelle nella sezione "Schema snapshot". Aggiunta di snapshots.os_memory_clerks, snapshots.sql_process_and_system_memory e snapshots.io_virtual_file_stats. Rimozione di snapshots.os_process_memory e snapshots.distinct_query_stats.|  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure del data warehouse di gestione &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql)   
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)   
 [Raccolta dati](data-collection.md)   
 [Visualizzare un report sui set di raccolta &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
  
