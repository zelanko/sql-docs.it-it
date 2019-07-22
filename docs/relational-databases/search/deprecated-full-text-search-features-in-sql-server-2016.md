---
title: Funzionalità deprecate della ricerca full-text in SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [full-text search]
- full-text search [SQL Server], deprecated features
- full-text queries [SQL Server], proximity
ms.assetid: ab0d799c-ba79-4459-837b-c4862730dafd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1ea901179d5011744f1b44609ccb9c19c27c514e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082908"
---
# <a name="deprecated-full-text-search-features-in-sql-server-2016"></a>Funzionalità deprecate della ricerca full-text in SQL Server 2016
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Questo argomento descrive le funzionalità deprecate della ricerca full-text ancora disponibili in SQL Server. Tali funzionalità verranno rimosse a partire da una delle prossime versioni. Non usare funzionalità deprecate nelle nuove applicazioni.  
  
È possibile monitorare l'uso delle funzionalità deprecate usando il contatore delle prestazioni dell'oggetto **SQL Server:Deprecated Features** e gli eventi di traccia. Per altre informazioni, vedere [Usare oggetti di SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
## <a name="features-no-longer-supported"></a>Funzionalità non più supportate  

  
|Funzionalità deprecata|Sostituzione|Nome funzionalità|ID funzionalità|  
|------------------------|-----------------|------------------|----------------|  
|Proprietà di FULLTEXTCATALOGPROPERTY: LogSize|Nessuna.|FULLTEXTCATALOGPROPERTY **('LogSize')**|211|  
|Proprietà di FULLTEXTSERVICEPROPERTY:<br /><br /> ConnectTimeout<br /><br /> DataTimeout|Nessuna.|FULLTEXTSERVICEPROPERTY **('ConnectTimeout')**<br /><br /> FULLTEXTSERVICEPROPERTY **('DataTimeout'** )|210<br /><br /> 209|  
|sp_fulltext_catalog|CREATE FULL CATALOG<br /><br /> ALTER FULLTEXT CATALOG<br /><br /> DROP FULLTEXT CATALOG|sp_fulltext_catalog|84|  
|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|CREATE FULL INDEX<br /><br /> ALTER FULLTEXT INDEX<br /><br /> DROP FULLTEXT INDEX|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|86<br /><br /> 87<br /><br /> 85|  
|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_tables<br /><br /> sp_help_fulltext_tables_cursor|sys.fulltext_catalogs<br /><br /> sys.fulltext_index_columns<br /><br /> sys.fulltext_indexes|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_table<br /><br /> sp_help_fulltext_tables_cursor|88<br /><br /> 203<br /><br /> 90<br /><br /> 92<br /><br /> 93<br /><br /> 91<br /><br /> 89|  
|sp_fulltext_service action values: clean_up, connect_timeout e data_timeout return zero|None|sp_fulltext_service @action=clean_up<br /><br /> sp_fulltext_service @action=connect_timeout<br /><br /> sp_fulltext_service @action=data_timeout|116<br /><br /> 117<br /><br /> 118|  
|Colonne sys.dm_fts_active_catalogs:<br /><br /> is_paused<br /><br /> previous_status<br /><br /> previous_status_description<br /><br /> row_count_in_thousands<br /><br /> status<br /><br /> status_description<br /><br /> worker_count|Nessuna.|dm_fts_active_catalogs.is_paused<br /><br /> dm_fts_active_catalogs.previous_status<br /><br /> dm_fts_active_catalogs.previous_status_description<br /><br /> dm_fts_active_catalogs.row_count_in_thousands<br /><br /> dm_fts_active_catalogs.status<br /><br /> dm_fts_active_catalogs.status_description<br /><br /> dm_fts_active_catalogs.worker_count|218<br /><br /> 221<br /><br /> 222<br /><br /> 224<br /><br /> 219<br /><br /> 220<br /><br /> 223|  
|Colonna sys.dm_fts_memory_buffers:<br /><br /> row_count|Nessuna.|dm_fts_memory_buffers.row_count|225|  
|Colonne sys.fulltext_catalogs:<br /><br /> percorso<br /><br /> data_space_id<br /><br /> colonne file_id|Nessuna.|fulltext_catalogs.path<br /><br /> fulltext_catalogs.data_space_id<br /><br /> fulltext_catalogs.file_id|215<br /><br /> 216<br /><br /> 217|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Funzionalità non supportate in una futura versione di SQL Server  
 Le funzionalità seguenti di ricerca full-text sono supportate nella versione successiva di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma in seguito verranno rimosse. La versione specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è stata determinata.  
  
 Il valore **Nome funzionalità** viene visualizzato negli eventi di traccia come nome dell'oggetto, mentre nei contatori delle prestazioni e in sys.dm_os_performance_counters viene visualizzato come nome dell'istanza. Il valore **ID funzionalità** viene visualizzato negli eventi di traccia come ID dell'oggetto.  
  
|Funzionalità deprecata|Sostituzione|Nome funzionalità|ID funzionalità|  
|------------------------|-----------------|------------------|----------------|  
|Operatore NEAR generico CONTAINS e CONTAINSTABLE:<br /><br /> {<simple_term> &#124; <prefix_term>}<br /><br /> {<br /><br /> { { NEAR &#124; ~ }    {<simple_term> &#124; <prefix_term>} } [...*n*]<br /><br /> }|Operatore NEAR personalizzato:<br /><br /> NEAR(<br /><br /> {   {<simple_term> &#124; <prefix_term>} [ ,...*n* ]<br /><br /> &#124; ( {<simple_term> &#124; <prefix_term>} [,...*n*] )<br /><br /> [,<distance> [,<order>] ]<br /><br /> }<br /><br /> )<br /><br /> <distance> ::= {*integer* &#124; **MAX**}<br /><br /> <order> ::= {TRUE &#124; **FALSE**}|FULLTEXT_OLD_NEAR_SYNTAX|247|  
|Opzione CREATE FULLTEXT CATALOG:<br /><br /> IN PATH '*rootpath*'<br /><br /> ON FILEGROUP *filegroup*|Nessuna.|CREATE FULLTEXT CATLOG IN PATH<br /><br /> nessuna.<sup>*</sup>|237<br /><br /> Nessuno.*|  
|Proprietà di DATABASEPROPERTYEX: IsFullTextEnabled|Nessuna.|DATABASEPROPERTYEX **('IsFullTextEnabled')**|202|  
|Opzione di sp_detach_db:<br /><br /> [ @keepfulltextindexfile = ] '*KeepFulltextIndexFile*'|Nessuna.|sp_detach_db @keepfulltextindexfile|226|  
|Valori azione sp_fulltext_service: resource_usage non ha nessuna funzione.|None|sp_fulltext_service @action=resource_usage|200|  
  
 &#42;L'oggetto **SQL Server:Deprecated Features** non monitora le occorrenze di CREATE FULLTEXT CATLOG ON FILEGROUP *filegroup*.  
  
  
