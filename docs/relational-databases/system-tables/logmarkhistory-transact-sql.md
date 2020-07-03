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
ms.openlocfilehash: 0b295105b76711e0e7305374cdd0ce380cd3abea
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890117"
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
  
  
