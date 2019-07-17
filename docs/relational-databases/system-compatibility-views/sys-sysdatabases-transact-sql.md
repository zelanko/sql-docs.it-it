---
title: Sys. sysdatabases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdatabases_TSQL
- sys.sysdatabases_TSQL
- sys.sysdatabases
- sysdatabases
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdatabases compatibility view
- sysdatabases system table
ms.assetid: 60a93880-62f1-4eda-a886-f046706ba90c
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b0dab1ca5f21ced6a54192a4b0173ead68fd6f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089158"
---
# <a name="syssysdatabases-transact-sql"></a>sys.sysdatabases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene una riga per ogni database in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installazione iniziale **sysdatabases** contiene voci per il **master**, **modello**, **msdb**e **tempdb** i database.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome database|  
|**dbid**|**smallint**|ID database|  
|**sid**|**varbinary(85)**|ID di sistema del creatore del database|  
|**mode**|**smallint**|Per uso interno. Blocca un database mentre viene creato.|  
|**status**|**int**|Bit di stato, alcune delle quali possono essere impostate usando [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) come indicato:<br /><br /> 1 = **autoclose** (ALTER DATABASE)<br /><br /> 4 = **select in / bulkcopy** (ALTER DATABASE tramite SET RECOVERY)<br /><br /> 8 = **trunc. log sul chkpt** (ALTER DATABASE tramite SET RECOVERY)<br /><br /> 16 = **rilevamento pagine incomplete** (ALTER DATABASE)<br /><br /> 32 = **il caricamento**<br /><br /> 64 = **prerecupero**<br /><br /> 128 = **il ripristino**<br /><br /> 256 = **non ripristinato**<br /><br /> 512 = **offline** (ALTER DATABASE)<br /><br /> 1024 = **di sola lettura** (ALTER DATABASE)<br /><br /> 2048 = **solo per uso dbo** (ALTER DATABASE tramite SET RESTRICTED_USER)<br /><br /> 4096=SELECT **singolo utente** (ALTER DATABASE)<br /><br /> 32768 = **modalità di emergenza**<br /><br /> 65536 = **CHECKSUM** (ALTER DATABASE)<br /><br /> 4194304 = **autoshrink** (ALTER DATABASE)<br /><br /> 1073741824 = **chiusura normale**<br /><br /> È possibile attivare più bit contemporaneamente.|  
|**status2**|**int**|16384 = **ANSI null default** (ALTER DATABASE)<br /><br /> 65536 = **concatenazione di valori null** (ALTER DATABASE)<br /><br /> 131072 = **i trigger ricorsivi** (ALTER DATABASE)<br /><br /> 1048576 = **predefinito fino al cursore locale** (ALTER DATABASE)<br /><br /> 8388608 = **identificatore delimitato** (ALTER DATABASE)<br /><br /> 33554432 = **chiusura cursore su commit** (ALTER DATABASE)<br /><br /> 67108864 = **ANSI nulls** (ALTER DATABASE)<br /><br /> 268435456 = **ANSI warnings** (ALTER DATABASE)<br /><br /> 536870912 = **full-text abilitata** (impostata tramite **sp_fulltext_database**)|  
|**crdate**|**datetime**|Data di creazione|  
|**reserved**|**datetime**|Riservato per utilizzi futuri.|  
|**category**|**int**|Include una mappa di bit di informazioni utilizzate per la replica.<br /><br /> 1 = Pubblicata per una replica snapshot o transazionale.<br /><br /> 2 = Sottoscritta a una pubblicazione snapshot o transazionale.<br /><br /> 4 = Pubblicata per una replica di tipo merge.<br /><br /> 8 = Sottoscritta a una pubblicazione di tipo merge.<br /><br /> 16 = Database di distribuzione.|  
|**cmptlevel**|**tinyint**|Livello di compatibilità del database. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).|  
|**filename**|**nvarchar(260)**|Percorso del sistema operativo e nome del file primario del database.<br /><br /> **nome file** è visibile agli **dbcreator**, **sysadmin**, il proprietario del database con autorizzazioni CREATE ANY DATABASE o per gli utenti che dispongono di una delle seguenti autorizzazioni: ALTER ANY DATABASE, CREATE ANY DATABASE, CONSENTE DI VISUALIZZARE QUALSIASI DEFINIZIONE. Per restituire il percorso e nome file, eseguire una query di [sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md) vista di compatibilità o il [Sys. database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) visualizzazione.|  
|**version**|**smallint**|Numero di versione interno del codice [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con cui è stato creato il database. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
