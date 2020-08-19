---
description: sys.fn_db_backup_file_snapshots (Transact-SQL)
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
ms.openlocfilehash: 067a1d65b65c1e2cc9bde252e6f56951e87950a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427793"
---
# <a name="sysfn_db_backup_file_snapshots-transact-sql"></a>sys.fn_db_backup_file_snapshots (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Restituisce gli snapshot di Azure associati ai file di database. Se il database specificato non viene trovato o se i file di database non vengono archiviati nel servizio di archiviazione BLOB di Microsoft Azure, non viene restituita alcuna riga. Utilizzare questa funzione di sistema insieme al stored procedure **sys. sp_delete_backup_file_snapshot** System per identificare ed eliminare gli snapshot di backup orfani. Per altre informazioni, vedere [Backup di snapshot di file per i file di database in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Database_name*  
 Nome del database sottoposto a query. Se è NULL, questa funzione viene eseguita nell'ambito del database corrente.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|file_id|**int**|ID file per il database. Non ammette i valori Null.|  
|snapshot_time|**nvarchar(260)**|Timestamp dello snapshot come viene restituito dall'API REST. Restituisce NULL se non esiste alcuno snapshot.|  
|snapshot_url|**nvarchar(360)**|URL completo dello snapshot del file. Restituisce NULL se non esiste alcuno snapshot.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW DATABASE STATE per il database.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_delete_backup_file_snapshot &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
