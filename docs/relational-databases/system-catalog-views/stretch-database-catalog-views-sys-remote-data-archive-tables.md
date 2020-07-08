---
title: sys. remote_data_archive_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_tables
- sys.remote_data_archive_tables_TSQL
- remote_data_archive_tables
- remote_data_archive_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_tables catalog view
ms.assetid: 765069b7-60fd-414c-875f-3455460b75cd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: b91a01714f7c7784f5ec227362c66c9468f44df5
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053616"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_tables"></a>Viste del catalogo Stretch Database-sys. remote_data_archive_tables
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Contiene una riga per ogni tabella remota che archivia i dati da una tabella locale abilitata per l'estensione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID oggetto della tabella locale abilitata per l'estensione.|  
|**remote_database_id**|**int**|Identificatore locale generato automaticamente del database remoto.|  
|**remote_table_name**|**sysname**|Nome della tabella nel database remoto che corrisponde alla tabella locale abilitata per l'estensione.|  
|**filter_predicate**|**nvarchar(max)**|Predicato del filtro, se presente, che identifica le righe della tabella da migrare. Se il valore è null, l'intera tabella è idonea alla migrazione.<br /><br /> Per altre informazioni, vedere [abilitare stretch database per una tabella](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) e [selezionare le righe di cui eseguire la migrazione usando un predicato di filtro](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).|  
|**migration_direction**|**tinyint**|Direzione di migrazione dei dati. I valori disponibili sono i seguenti.<br/>1 (in uscita)<br/>2 (in ingresso)|  
|**migration_direction_desc**|**nvarchar(60)**|Descrizione della direzione in cui è attualmente in corso la migrazione dei dati. I valori disponibili sono i seguenti.<br/>in uscita (1)<br/>in ingresso (2)|  
|**is_migration_paused**|**bit**|Indica se la migrazione è attualmente sospesa.|  
|**is_reconciled**|**bit**| Indica se la tabella remota e la tabella SQL Server sono sincronizzate.<br/><br/>Quando il valore di **is_reconciled** è 1 (true), la tabella remota e la tabella SQL Server sono sincronizzate ed è possibile eseguire query che includono i dati remoti.<br/><br/>Quando il valore di **is_reconciled** è 0 (false), la tabella remota e la tabella SQL Server non sono sincronizzate. È necessario eseguire nuovamente la migrazione delle righe di cui è stata eseguita la migrazione. Questo errore si verifica quando si ripristina il database di Azure remoto o quando si eliminano le righe manualmente dalla tabella remota. Finché le tabelle non vengono riconciliate, non è possibile eseguire query che includono i dati remoti. Per riconciliare le tabelle, eseguire [sys. sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md). |  
  
## <a name="see-also"></a>Vedere anche  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

