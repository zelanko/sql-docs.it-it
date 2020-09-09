---
description: restorefile (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 366c6bd83e46b2a8586590552bfd05e2975b9e04
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547016"
---
# <a name="restorefile-transact-sql"></a>restorefile (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una riga per ogni file ripristinato, compresi i file ripristinati in modo indiretto in base al nome del filegroup. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Numero di identificazione univoco che identifica l'operazione di ripristino corrispondente. Fa riferimento a **restorehistory (restore_history_id)**.|  
|**file_number**|**numerico (10, 0)**|Numero di identificazione del file ripristinato. Deve essere univoco in ogni database. Può essere NULL.<br /><br /> Quando un database viene ripristinato come snapshot di database, questo valore viene popolato nello stesso modo previsto per un ripristino completo.|  
|**destination_phys_drive**|**nvarchar(260)**|Unità o partizione in cui è stato ripristinato il file Può essere NULL.<br /><br /> Quando un database viene ripristinato come snapshot di database, questo valore viene popolato nello stesso modo previsto per un ripristino completo.|  
|**destination_phys_name**|**nvarchar(260)**|Nome del file senza l'indicazione dell'unità o partizione in cui è stato ripristinato il file Può essere NULL.<br /><br /> Quando un database viene ripristinato come snapshot di database, questo valore viene popolato nello stesso modo previsto per un ripristino completo.|  
  
## <a name="remarks"></a>Osservazioni  
 Per ridurre il numero di righe in questa tabella e in altre tabelle di backup e di cronologia, eseguire la [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) stored procedure.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di backup e ripristino &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefilegroup &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [restorehistory &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
