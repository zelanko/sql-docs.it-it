---
title: sys.fn_db_backup_file_snapshots (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
author: rothja
ms.author: jroth
ms.openlocfilehash: 5159b72cb91cfdcf21129c6216cab4cf0e8d4dea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120268"
---
# <a name="sysfndbbackupfilesnapshots-transact-sql"></a>sys.fn_db_backup_file_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Restituisce gli snapshot di Azure associati con i file di database. Se il database specificato non viene trovato o se i file di database non sono archiviati nel servizio di archiviazione Blob di Microsoft Azure, viene restituita alcuna riga. Utilizzare questa funzione di sistema in combinazione con il **sp_delete_backup_file_snapshot** stored procedure per identificare ed eliminare snapshot di backup orfani di sistema. Per altre informazioni, vedere [Backup di snapshot di file per i file di database in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Database_name*  
 Il nome del database sottoposto a query. Se NULL, questa funzione viene eseguita nell'ambito del database corrente.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|file_id|**int**|ID File per il database. Non ammette i valori Null.|  
|snapshot_time|**nvarchar(260)**|Il timestamp dello snapshot perché viene restituito dall'API REST. Restituisce NULL se non esiste alcuno snapshot.|  
|snapshot_url|**nvarchar(360)**|L'URL completo per lo snapshot di file. Restituisce NULL se nessuno snapshot esiste.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE per il database.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
