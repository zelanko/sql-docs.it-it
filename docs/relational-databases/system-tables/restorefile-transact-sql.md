---
title: restorefile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorefile
- restorefile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorefile system table
- restoring files [SQL Server], restorefile system table
- file restores [SQL Server], restorefile system table
ms.assetid: 8e40145a-8559-4abe-8e2a-39b818928009
author: stevestein
ms.author: sstein
ms.openlocfilehash: 788d0296087ee8980be0b0ecf56c43f09fb3780c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910194"
---
# <a name="restorefile-transact-sql"></a>restorefile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni file ripristinato, compresi i file ripristinati in modo indiretto in base al nome del filegroup. Questa tabella è archiviata nel **msdb** database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Numero di identificazione univoco che identifica l'operazione di ripristino corrispondente. I riferimenti **restorehistory (restore_history_id)** .|  
|**file_number**|**numeric(10,0)**|Numero di identificazione del file ripristinato. Deve essere univoco in ogni database. Può essere NULL.<br /><br /> Quando un database viene ripristinato come snapshot di database, questo valore viene popolato nello stesso modo previsto per un ripristino completo.|  
|**destination_phys_drive**|**nvarchar(260)**|Unità o partizione in cui è stato ripristinato il file Può essere NULL.<br /><br /> Quando un database viene ripristinato come snapshot di database, questo valore viene popolato nello stesso modo previsto per un ripristino completo.|  
|**destination_phys_name**|**nvarchar(260)**|Nome del file senza l'indicazione dell'unità o partizione in cui è stato ripristinato il file Può essere NULL.<br /><br /> Quando un database viene ripristinato come snapshot di database, questo valore viene popolato nello stesso modo previsto per un ripristino completo.|  
  
## <a name="remarks"></a>Note  
 Per ridurre il numero di righe in questa tabella e in altre tabelle della cronologia e backup, eseguire la [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup e ripristino di tabelle &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [restorehistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
