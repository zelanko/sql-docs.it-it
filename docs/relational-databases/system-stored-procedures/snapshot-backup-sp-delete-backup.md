---
title: sp_delete_backup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 49eb0906a9a5af1fec2abfeec3ef58845b605e69
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67941826"
---
# <a name="sp_delete_backup-transact-sql"></a>sp_delete_backup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Elimina tutti gli snapshot e il file di backup che costituiscono un set di backup di snapshot dal database specificato. Questo stored procedure di sistema è l'unico metodo consigliato per la gestione dei set di backup di snapshot. Per altre informazioni, vedere [Backup di snapshot di file per i file di database in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *[ @backup_url =] backup_meta_file_url*  
 URL del backup da eliminare, che elimina tutti gli snapshot che comprendono il set di backup specificato, incluso il file di backup.  
  
 *[ @db_name =] database_name*  
 Nome del database contenente lo snapshot da eliminare. Quando viene specificato un nome di database, il sistema verifica che l'URL di backup fornito sia un URL di backup per il database specificato e utilizza [sp_delete_backup_file_snapshot &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) per eliminare ogni snapshot. Se non viene specificato alcun nome di database, questo controllo del database non viene eseguito.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione ALTER ANY DATABASE o l'autorizzazione ALTER per il database specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [sys. fn_db_backup_file_snapshots &#40;&#41;Transact-SQL](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
