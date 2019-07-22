---
title: Gestire e monitorare la ricerca full-text per un'istanza del server | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], about
- full-text search [SQL Server], server management
ms.assetid: 2733ed78-6d33-4bf9-94da-60c3141b87c8
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68d1ea1ee1adc7c5126606bd0cf72ca8e54a725c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132263"
---
# <a name="manage-and-monitor-full-text-search-for-a-server-instance"></a>Gestione e monitoraggio della ricerca full-text per un'istanza del server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  L'amministrazione full-text per un'istanza del server include:  
  
-   Attività di gestione del sistema quali la gestione del servizio dell'utilità di avvio di FDHOST (MSSQLFDLauncher), il riavvio del processo host del daemon di filtri se si modificano le credenziali dell'account del servizio, la configurazione delle proprietà full-text del server e il backup dei cataloghi full-text. A livello di server, ad esempio, è possibile specificare un linguaggio full-text predefinito che differisce dal linguaggio predefinito dell'istanza del server nel suo complesso.  
  
-   Configurazione dei componenti linguistici full-text (word breaker e stemmer, file del thesaurus ed elenchi di parole non significative).  
  
-   Configurazione di un database utente per la ricerca full-text. Include la creazione di uno o più cataloghi full-text per il database e la definizione di un indice full-text in ciascuna tabella o vista indicizzata in cui eseguire query full-text.  
  
##  <a name="props"></a> Visualizzazione e modifica delle proprietà del server per la ricerca full-text  
 È possibile visualizzare le proprietà full-text di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-view-and-change-server-properties-for-full-text-search"></a>Per visualizzare e modificare le proprietà del server per la ricerca full-text  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Proprietà server** fare clic sulla pagina **Avanzate** per visualizzare le informazioni del server sulla ricerca full-text. Le proprietà full-text sono le seguenti:  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    -   **Lingua predefinita full-text**  
  
         Specifica una lingua predefinita per le colonne con indicizzazione full-text. L'analisi linguistica dei dati con indicizzazione full-text dipende dalla lingua dei dati. Il valore predefinito per questa opzione corrisponde alla lingua impostata per il server. Per la lingua corrispondente all'impostazione visualizzata, vedere [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
    -   **Opzione di aggiornamento full-text**  
  
         Questa proprietà del server consente di controllare il modo in cui viene eseguita la migrazione degli indici full-text durante l'aggiornamento di un database da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a una versione successiva. Questa proprietà si applica ai casi in cui viene eseguito l'aggiornamento tramite il collegamento di un database, il ripristino di un backup di database o di un backup di file oppure la copia del database tramite la Copia guidata database.  
  
         Sono disponibili le alternative seguenti:  
  
         **Importa**  
         I cataloghi full-text vengono importati. In genere, l'importazione è molto più veloce della ricompilazione. Se ad esempio si utilizza solo una CPU, l'importazione è di circa 10 volte più veloce della ricompilazione. Tuttavia, un catalogo full-text importato non utilizza i word breaker nuovi e migliorati introdotti in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], pertanto potrebbe essere necessario ricompilare i cataloghi full-text.  
  
        > [!NOTE]  
        >  La ricompilazione può essere eseguita in modalità a thread multipli e, nel caso in cui siano disponibili più di 10 CPU, può risultare più veloce dell'importazione se si consente alla ricompilazione di utilizzare tutte le CPU.  
  
         Se un catalogo full-text non è disponibile, gli indici full-text associati vengono ricreati. Questa opzione è disponibile solo per i database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
         **Ricompilazione**  
         I cataloghi full-text vengono ricompilati utilizzando i nuovi word breaker ottimizzati. La ricompilazione degli indici può richiedere tempo e dopo l'aggiornamento potrebbe essere necessaria una quantità significativa di CPU e di memoria.  
  
         **Reimposta**  
         I cataloghi full-text vengono ripristinati. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] I file del catalogo full-text vengono rimossi, ma i metadati per i cataloghi e per gli indici full-text vengono mantenuti. Dopo l'aggiornamento, in tutti gli indici full-text il rilevamento delle modifiche viene disabilitato e le ricerche per indicizzazione non vengono avviate automaticamente. Il catalogo resterà vuoto fino a quando non si eseguirà manualmente un popolamento completo al termine dell'aggiornamento.  
  
         Per informazioni sulla scelta dell'opzione di aggiornamento full-text, vedere[Aggiornare la ricerca full-text](../../relational-databases/search/upgrade-full-text-search.md).  
  
        > [!NOTE]  
        >  L'opzione di aggiornamento full-text può anche essere impostata con l'azione [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)**upgrade_option** .  
  
##  <a name="metadata"></a> Visualizzazione di proprietà server full-text aggiuntive  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] È possibile usare le funzioni per ottenere il valore di varie proprietà a livello server della ricerca full-text. Queste informazioni sono utili per l'amministrazione e la risoluzione dei problemi relativi alla ricerca full-text.  
  
 Nella tabella seguente solo elencate le proprietà full-text di un'istanza del server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] correlate.  
  
|Proprietà|Descrizione|Funzione|  
|--------------|-----------------|--------------|  
|**IsFullTextInstalled**|Indica se il componente full-text viene installato o meno con l'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[FULLTEXTSERVICEPROPERTY](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)<br /><br /> [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)|  
||||  
|**LoadOSResources**|Indica se i word breaker e i filtri del sistema operativo sono registrati e utilizzati in questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|FULLTEXTSERVICEPROPERTY|  
|**VerifySignature**|Specifica se il motore di ricerca full-text deve caricare solo i file binari firmati.|FULLTEXTSERVICEPROPERTY|  
  
##  <a name="monitor"></a> Monitoraggio dell'attività di ricerca full-text  
 Numerose funzioni e viste a gestione dinamica consentono di monitorare l'attività di ricerca full-text in un'istanza del server.  
  
 **Per visualizzare informazioni sui cataloghi full-text con un'attività di popolamento in corso**  
  
-   [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
  
 **Per visualizzare l'attività corrente di un processo host del daemon di filtri**  
  
-   [sys.dm_fts_fdhosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
  
 **Per visualizzare informazioni sui popolamenti di indice in corso**  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
 **Per visualizzare i buffer di memoria in un pool di memoria utilizzati come parte di una ricerca per indicizzazione o di un intervallo di ricerche per indicizzazione**  
  
-   [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
  
 **Per visualizzare i pool di memoria condivisi disponibili per il componente gatherer full-text per una ricerca per indicizzazione o un intervallo di ricerche per indicizzazione**  
  
-   [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
 **Per visualizzare informazioni su ogni batch di indicizzazione full-text**  
  
-   [sys.dm_fts_outstanding_batches &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
  
 **Per visualizzare informazioni sugli intervalli specifici correlati a un popolamento in corso**  
  
-   [sys.dm_fts_population_ranges &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
  
  
