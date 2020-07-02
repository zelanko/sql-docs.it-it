---
title: logmarkhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ef8a263edfb6902cd4f050cbe27b99062e5b5c20
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750139"
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contiene una riga per ogni transazione contrassegnata di cui è stato eseguito il commit. Questa tabella è archiviata nel database **msdb** .  
  

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Database locale in cui è stata eseguita la transazione contrassegnata.|  
|**mark_name**|**nvarchar(128)**|Nome specificato dall'utente per la transazione contrassegnata.|  
|**Descrizione**|**nvarchar(255)**|Descrizione specificata dall'utente per la transazione contrassegnata. Può essere NULL.|  
|**user_name**|**nvarchar(128)**|Nome dell'utente di database che ha eseguito la transazione contrassegnata. Può essere NULL.|  
|**LSN**|**numeric(25,0)**|Numero di sequenza del log del record della transazione in cui è stato inserito il contrassegno.|  
|**mark_time**|**datetime**|Ora del commit della transazione contrassegnata (ora locale).|  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristino di un database fino a una transazione contrassegnata &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
