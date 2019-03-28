---
title: Riavviare un'operazione di ripristino interrotta (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3bce9a9d48dce2e795fee049bd9414a987314775
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529053"
---
# <a name="restart-an-interrupted-restore-operation-transact-sql"></a>Riavvio di un'operazione di ripristino interrotta (Transact-SQL)
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
 [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](complete-database-restores-full-recovery-model.md)   
 [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](complete-database-restores-simple-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
