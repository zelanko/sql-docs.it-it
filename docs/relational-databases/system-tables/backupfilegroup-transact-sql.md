---
title: backupfilegroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupfilegroup_TSQL
- backupfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], backupfilegroup system table
- backupfilegroup system table
ms.assetid: d26e8fbe-f5c5-4e10-b2bd-0d8e16ea21f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1d7cc485899a7f8173552788471ef6ec45ce49c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62645184"
---
# <a name="backupfilegroup-transact-sql"></a>backupfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni filegroup in un database al momento del backup. **backupfilegroup** viene archiviato nel **msdb** database.  
  
> [!NOTE]  
>  Il **backupfilegroup** tabella mostra la configurazione del filegroup del database, non del set di backup. Per identificare se un file è incluso nel set di backup, usare il **is_present** della colonna della [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) tabella.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Set di backup contenente questo filegroup.|  
|**name**|**sysname**|Nome del filegroup|  
|**filegroup_id**|**int**|ID del filegroup, univoco all'interno del database. Corrisponde a **data_space_id** nelle **Sys. FileGroups**.|  
|**filegroup_guid**|**uniqueidentifier**|Identificatore univoco globale per il filegroup. Può essere NULL.|  
|**type**|**char(2)**|Tipo di contenuto, può corrispondere a:<br /><br /> FG = Filegroup "Rows"<br /><br /> SL = Filegroup di log [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**type_desc**|**nvarchar(60)**|Descrizione del tipo di funzione, può corrispondere a:<br /><br /> ROWS_FILEGROUP<br /><br /> SQL_LOG_FILEGROUP|  
|**is_default**|**bit**|Il filegroup predefinito, utilizzato quando non è specificato alcun filegroup in CREATE TABLE o CREATE INDEX.|  
|**is_readonly**|**bit**|1 = Il filegroup è di sola lettura.|  
|**log_filegroup_guid**|**uniqueidentifier**|Può essere NULL.|  
  
## <a name="remarks"></a>Note  
  
> [!IMPORTANT]  
>  Lo stesso nome di filegroup può apparire in diversi database, ogni filegroup dispone tuttavia di un GUID proprio. Pertanto **(backup_set_id, filegroup_guid)** è una chiave univoca che identifica un filegroup in **backupfilegroup**.  
  
 RESTORE VERIFYONLY FROM *dispositivo_backup* WITH LOADHISTORY popola le colonne delle **backupmediaset** tabella con i valori appropriati dall'intestazione del set di supporti.  
  
 Per ridurre il numero di righe in questa tabella e in altre tabelle della cronologia e backup, eseguire la [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup e ripristino di tabelle &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
