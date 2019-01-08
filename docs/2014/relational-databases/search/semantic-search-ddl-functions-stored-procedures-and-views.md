---
title: DDL, funzioni, stored procedure e viste di ricerca semantica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], database objects
ms.assetid: 182f395f-3168-48a4-b723-ef4403544f9f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76ced95f53b50c0fc0402051cff35329d39ce9f0
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52530736"
---
# <a name="semantic-search-ddl-functions-stored-procedures-and-views"></a>DDL di ricerca semantica, funzioni, stored procedure e viste
  Sono elencate le istruzioni Transact-SQL e gli oggetti di database che supportano la ricerca semantica statistica in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per l'elenco di istruzioni e oggetti di database che supportano la ricerca full-text, vedere [DDL di ricerca full-text, funzioni, stored procedure e viste](../views/views.md).  
  
##  <a name="ddl"></a> Istruzioni Transact-SQL DDL (Data Definition Language)  
  
|Object|Ulteriori informazioni|  
|------------|----------------------|  
|[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)|[Abilitare la ricerca semantica in tabelle e colonne](enable-semantic-search-on-tables-and-columns.md)|  
|[CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)|[Abilitare la ricerca semantica in tabelle e colonne](enable-semantic-search-on-tables-and-columns.md)|  
  
##  <a name="func"></a> Funzioni di sistema  
  
|Object|Ulteriori informazioni|  
|------------|----------------------|  
|[semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql)|[Trovare frasi chiave nei documenti tramite la ricerca semantica](find-key-phrases-in-documents-with-semantic-search.md)|  
|[semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)|[Trovare documenti simili e correlati tramite la ricerca semantica](find-similar-and-related-documents-with-semantic-search.md)|  
|[semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)|[Trovare documenti simili e correlati tramite la ricerca semantica](find-similar-and-related-documents-with-semantic-search.md)|  
  
##  <a name="meta"></a> Funzioni per i metadati di sistema  
  
|Object|Ulteriori informazioni|  
|------------|----------------------|  
|[COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)|[Abilitare la ricerca semantica in tabelle e colonne](enable-semantic-search-on-tables-and-columns.md)|  
|[DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql)|[Abilitare la ricerca semantica in tabelle e colonne](enable-semantic-search-on-tables-and-columns.md)|  
|[FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)|[Gestire e monitorare la ricerca semantica](manage-and-monitor-semantic-search.md)|  
|[INDEXPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)|[Gestire e monitorare la ricerca semantica](manage-and-monitor-semantic-search.md)|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|[Abilitare la ricerca semantica in tabelle e colonne](enable-semantic-search-on-tables-and-columns.md)|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|[Installare e configurare la ricerca semantica](install-and-configure-semantic-search.md)|  
  
##  <a name="sproc"></a> Stored procedure di sistema  
  
|Object|Ulteriori informazioni|  
|------------|----------------------|  
|[sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql)|[Installazione e configurazione della ricerca semantica](install-and-configure-semantic-search.md)|  
|[sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql)|[Installare e configurare la ricerca semantica](install-and-configure-semantic-search.md)|  
  
##  <a name="cv"></a> Viste di sistema: viste del catalogo  
  
|Object|Ulteriori informazioni|  
|------------|----------------------|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|[Gestire e monitorare la ricerca semantica](manage-and-monitor-semantic-search.md)|  
|[sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql)|[Installare e configurare la ricerca semantica](install-and-configure-semantic-search.md)|  
|[sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql)|[Installare e configurare la ricerca semantica](install-and-configure-semantic-search.md)|  
  
##  <a name="dmv"></a> Viste di sistema: DMV  
  
|Object|Ulteriori informazioni|  
|------------|----------------------|  
|[sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)|[Gestire e monitorare la ricerca semantica](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|[Gestire e monitorare la ricerca semantica](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)|[Gestire e monitorare la ricerca semantica](manage-and-monitor-semantic-search.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire e monitorare la ricerca semantica](manage-and-monitor-semantic-search.md)  
  
  
