---
title: backupmediafamily (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediafamily
- backupmediafamily_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupmediafamily system table
- backup media [SQL Server], backupmediafamily system table
ms.assetid: ee16de24-3d95-4b2e-a094-78df2514d18a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6ea3fd7937447ba3ed0f3ad89965301dead772cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122875"
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Include una riga per ogni gruppo di supporti. Se un gruppo di supporti risiede in un set di supporti con mirroring, il gruppo includerà una riga distinta per ciascun mirror del set di supporti. Questa tabella è archiviata nel **msdb** database.  
    
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|Numero di identificazione univoco del set di supporti in cui è incluso il gruppo. I riferimenti **backupmediaset (media_set_id)**|  
|**family_sequence_number**|**tinyint**|Posizione del gruppo di supporti nel set di supporti.|  
|**media_family_id**|**uniqueidentifier**|Numero di identificazione univoco del gruppo di supporti. Può essere NULL.|  
|**media_count**|**int**|Numero di supporti nel gruppo. Può essere NULL.|  
|**logical_device_name**|**nvarchar(128)**|Nome di questo dispositivo di backup in **backup_devices**. Se si tratta di un dispositivo di backup temporaneo (invece di un dispositivo di backup permanente che esiste in **Sys. backup_devices**), il valore di **logical_device_name** è NULL.|  
|**physical_device_name**|**nvarchar(260)**|Nome fisico del dispositivo di backup. Può essere NULL. Questo campo viene condiviso tra processo di backup e ripristino. Può contenere il percorso di destinazione di backup originale o il percorso di origine ripristino originale. A seconda se il backup o ripristino ha avuto luogo prima di tutto in un server per un database. Si noti che i ripristini consecutivi dal file di backup stesso non aggiornerà il percorso, indipendentemente dalla relativa ubicazione in fase di ripristino. Ne consegue **physical_device_name** campo non può essere usato per visualizzare il percorso di ripristino utilizzato.|  
|**device_type**|**tinyint**|Tipo di dispositivo di backup:<br /><br /> 2 = Disco<br /><br /> 5 = Nastro<br /><br /> 7 = Dispositivo virtuale<br /><br /> 9 = archiviazione di azure<br /><br /> 105 = Dispositivo di backup permanente<br /><br /> Può essere NULL.<br /><br /> Tutti i nomi dei dispositivi permanenti e i numeri dei dispositivi sono reperibile nel **Sys. backup_devices**.|  
|**physical_block_size**|**int**|Dimensioni fisiche del blocco utilizzate per la scrittura del gruppo di supporti. Può essere NULL.|  
|**mirror**|**tinyint**|Numero di mirroring (0-3).|  
  
## <a name="remarks"></a>Note  
 RESTORE VERIFYONLY FROM *dispositivo_backup* WITH LOADHISTORY popola le colonne delle **backupmediaset** tabella con i valori appropriati dall'intestazione del set di supporti.  
  
 Per ridurre il numero di righe in questa tabella e in altre tabelle della cronologia e backup, eseguire la [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup e ripristino di tabelle &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
