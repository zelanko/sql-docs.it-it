---
title: Riavviare un ripristino interrotto (Transact-SQL)
description: Questo esempio illustra come riavviare un'operazione di ripristino interrotta in SQL Server usando Transact-SQL.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- interrupted restore operation
- restoring databases [SQL Server], restarting interrupted operation
- resetting options changed after backup
- database restores [SQL Server], restarting interrupted operation
- restarting interrupted restore operation
- restoring interrupted operation [SQL Server]
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
author: cawrites
ms.author: chadam
ms.openlocfilehash: f2c70762e4e68081fc63930b1140ba904a5ca565
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129141"
---
# <a name="restart-an-interrupted-restore-operation-transact-sql"></a>Riavvio di un'operazione di ripristino interrotta (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In questo argomento viene descritta la procedura per il riavvio di un'operazione di ripristino interrotta.  
  
### <a name="to-restart-an-interrupted-restore-operation"></a>Per riavviare un'operazione di ripristino interrotta  
  
1.  Eseguire nuovamente l'istruzione RESTORE interrotta, specificando:  
  
    -   Le stesse clausole utilizzate nell'istruzione RESTORE originale.  
  
    -   La clausola RESTART.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene riavviata un'operazione di ripristino interrotta.  
  
```sql  
-- Restore a full database backup of the AdventureWorks database.  
RESTORE DATABASE AdventureWorks  
   FROM DISK = 'C:\AdventureWorks.bck'  
GO  
-- The restore operation halted prematurely.  
-- Repeat the original RESTORE statement specifying WITH RESTART.  
RESTORE DATABASE AdventureWorks   
   FROM DISK = 'C:\AdventureWorks.bck'  
   WITH RESTART  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
