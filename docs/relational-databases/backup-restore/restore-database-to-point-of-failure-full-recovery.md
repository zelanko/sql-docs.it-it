---
title: Ripristinare un database fino al punto di errore - Recupero con registrazione completa | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- point of failure [SQL Server]
- restoring databases [SQL Server], point of failure
- database restores [SQL Server], point of failure
ms.assetid: 04106e18-bbf7-4a5e-a2e1-3d65319814d5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ad5b91a85db47b500d8a48d0fa3384eb65ba2a19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041540"
---
# <a name="restore-database-to-point-of-failure---full-recovery"></a>Ripristinare un database fino al punto di errore - Recupero con registrazione completa
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento vengono fornite informazioni su come eseguire il ripristino fino al punto di errore. L'argomento è rilevante solo per i database che utilizzano i modelli di recupero con registrazione completa o con registrazione minima delle operazioni bulk.  
  
### <a name="to-restore-to-the-point-of-failure"></a>Per eseguire il ripristino fino al punto di errore  
  
1.  Eseguire il backup della parte finale del log eseguendo l'istruzione [BACKUP](../../t-sql/statements/backup-transact-sql.md) di base seguente:  
  
    ```  
    BACKUP LOG <database_name> TO <backup_device>   
       WITH NORECOVERY, NO_TRUNCATE;  
    ```  
  
2.  Eseguire il ripristino di un backup completo del database eseguendo l'istruzione [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md) di base seguente:  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
3.  Facoltativamente, ripristinare un backup differenziale del database eseguendo l'istruzione RESTORE DATABASE di base seguente:  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
4.  Applicare tutti i log delle transazioni, incluso il backup della parte finale del log creato nel passaggio 1, specificando WITH NORECOVERY nell'istruzione RESTORE LOG:  
  
    ```  
    RESTORE LOG <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
5.  Recuperare il database eseguendo l'istruzione RESTORE DATABASE seguente:  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    ```  
    RESTORE DATABASE <database_name>   
       WITH RECOVERY;  
    ```  
  
## <a name="example"></a>Esempio  
 Prima che sia possibile eseguire l'esempio, è necessario completare le operazioni preliminari seguenti:  
  
1.  Il modello di recupero predefinito del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] è il modello di recupero con registrazione minima. Dato che questo modello di recupero non supporta il ripristino in corrispondenza del punto in cui si è verificato un errore, impostare [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] per usare il modello di recupero con registrazione completa eseguendo l'istruzione [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) seguente:  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
    ```  
  
2.  Creare un backup completo del database utilizzando l'istruzione BACKUP seguente:  
  
    ```  
    BACKUP DATABASE AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Data.bck';  
    ```  
  
3.  Creare un backup del log di routine:  
  
    ```  
    BACKUP LOG AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Log.bck';  
    ```  
  
 Nell'esempio seguente vengono ripristinati i backup creati in precedenza, dopo la creazione di un backup della parte finale del log del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . In questo passaggio si suppone che il disco del log sia accessibile.  
  
 Innanzitutto, nell'esempio viene creato un backup della parte finale del log del database che acquisisce il log attivo e lascia il database nello stato di ripristino. Quindi, nell'esempio viene ripristinato il backup del database e vengono applicati il backup del log di routine creato in precedenza e il backup della parte finale del log. Infine viene recuperato il database in un passaggio separato.  
  
> [!NOTE]  
>  Il comportamento predefinito consiste nel recuperare un database come parte dell'istruzione che ripristina il backup finale.  
  
```  
/* Example of restoring a to the point of failure */  
-- Step 1: Create a tail-log backup by using WITH NORECOVERY.  
BACKUP LOG AdventureWorks2012  
   TO DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 2: Restore the full database backup.  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Data.bck'  
   WITH NORECOVERY;  
GO  
-- Step 3: Restore the first transaction log backup.  
RESTORE LOG AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 4: Restore the tail-log backup.  
RESTORE LOG AdventureWorks2012  
   FROM  DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 5: Recover the database.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
