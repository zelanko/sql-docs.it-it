---
title: Eseguire il backup in un set di supporti con mirroring (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b498aaa0a5a82294bc68942a68859939aff0fb7f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67940872"
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>Backup in un set di supporti con mirroring (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questo argomento descrive come usare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)]BACKUP[ di ](../../t-sql/statements/backup-transact-sql.md) per specificare un set di supporti con mirroring durante l'esecuzione del backup di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nell'istruzione BACKUP specificare il primo mirror nella clausola TO, quindi specificare ogni mirror nella relativa clausola MIRROR TO. È necessario che le clausole TO e MIRROR TO specifichino lo stesso numero e tipo di dispositivo di backup.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato il set di supporti con mirroring indicato nella figura precedente e viene eseguito il backup del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] su entrambi i mirror.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
    FORMAT,  
    MEDIANAME = 'AdventureWorks2012Set1';  
GO  
```  
  
## <a name="related-tasks"></a>Attività correlate  
 **Per eseguire il ripristino da un backup con mirroring**  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Set di supporti di backup con mirroring &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  
