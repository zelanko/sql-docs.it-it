---
title: sys.remote_data_archive_tables (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 93dfc97acab31b5078bcba569b52c64f773c775b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945674"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>Stretch Database - viste del catalogo sys. remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni tabella remota che archivia i dati da una tabella locale abilitata per l'estensione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|L'ID oggetto della tabella locale abilitata per l'estensione.|  
|**remote_database_id**|**int**|L'identificatore di locale generato automaticamente del database remoto.|  
|**remote_table_name**|**sysname**|Il nome della tabella nel database remoto che corrisponde alla tabella locale abilitata per l'estensione.|  
|**filter_predicate**|**nvarchar(max)**|Il predicato del filtro, se presente, che identifica le righe della tabella per eseguire la migrazione. Se il valore è null, l'intera tabella è idonea per la migrazione.<br /><br /> Per altre informazioni, vedi [abilitare Stretch Database per una tabella](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) e [selezionare le righe di cui eseguire la migrazione tramite un predicato del filtro](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).|  
|**migration_direction**|**tinyint**|La direzione in cui i dati sono in corso la migrazione. I valori disponibili sono i seguenti.<br/>1 (in uscita)<br/>2 (in ingresso)|  
|**migration_direction_desc**|**nvarchar(60)**|Descrizione della direzione in cui i dati sono in corso la migrazione. I valori disponibili sono i seguenti.<br/>in uscita (1)<br/>connessioni in entrata (2)|  
|**is_migration_paused**|**bit**|Indica se è attualmente sospesa la migrazione.|  
|**is_reconciled**|**bit**| Indica se la tabella remota e la tabella di SQL Server sono sincronizzati.<br/><br/>Quando il valore di **is_reconciled** è 1 (true), la tabella remota e la tabella di SQL Server siano sincronizzati ed è possibile eseguire le query che includono i dati remoti.<br/><br/>Quando il valore di **is_reconciled** è 0 (false), la tabella remota e la tabella di SQL Server non sono sincronizzate. Le righe migrate hanno di recente da sottoporre a migrazione nuovamente. Ciò si verifica quando si ripristina il database di Azure remoto o quando si elimina manualmente le righe della tabella remota. Fino a quando non risolvere le differenze tra le tabelle, è possibile eseguire le query che includono i dati remoti. Per risolvere le differenze tra le tabelle, eseguire [sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md). |  
  
## <a name="see-also"></a>Vedere anche  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

