---
title: 'Ripristino a fasi: modello di recupero con registrazione completa'
description: In questo esempio viene illustrato un ripristino a fasi in SQL Server di un database usando il modello di recupero con registrazione completa, a partire da un backup della parte finale del log.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: 0a84892d-2f7a-4e77-b2d0-d68b95595210
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f680bae8939aa6c4f6648c6076616564cd7d195c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737765"
---
# <a name="example-piecemeal-restore-of-database-full-recovery-model"></a>Esempio: Ripristino a fasi di un database (modello di recupero con registrazione completa)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Con una sequenza di ripristino a fasi, il database viene ripristinato e recuperato in varie fasi a livello di filegroup, partendo dal filegroup primario e da tutti i filegroup secondari in lettura/scrittura.  
  
 In questo esempio il database `adb` viene ripristinato in un nuovo computer dopo un'emergenza. Dato che il database utilizza il modello di recupero con registrazione completa, prima dell'avvio del ripristino è necessario eseguire un backup della parte finale del log per il database. Prima dell'emergenza, tutti i filegroup erano online. Il filegroup `B` è di sola lettura. Tutti i filegroup secondari devono essere ripristinati, ma il ripristino avviene in ordine di importanza: `A` (importanza massima), `C`e infine `B`. In questo esempio sono presenti quattro backup dei log, incluso il backup della parte finale del log.  
  
## <a name="tail-log-backup"></a>Backup della parte finale del log  
 Prima di ripristinare il database, è necessario che l'amministratore del database esegua il backup della parte finale del log. Dato che il database è danneggiato, la creazione di tale backup richiede l'utilizzo dell'opzione NO_TRUNCATE:  
  
```  
BACKUP LOG adb TO tailLogBackup WITH NORECOVERY, NO_TRUNCATE  
```  
  
 Il backup della parte finale del log è l'ultimo backup applicato nelle sequenze di ripristino seguenti.  
  
## <a name="restore-sequences"></a>Sequenze di ripristino  
  
> [!NOTE]  
>  La sintassi di una sequenza di ripristino online è la stessa di una sequenza di ripristino offline.  
  
1.  Ripristino parziale del filegroup primario e secondario `A`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup1   
       WITH PARTIAL, NORECOVERY  
    RESTORE DATABASE adb FILEGROUP='A' FROM backup2   
       WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
2.  Eseguire un ripristino online del filegroup `C`.  
  
     A questo punto sono online il filegroup primario e il filegroup secondario `A` . Il recupero di tutti i file nei filegroup `B` e `C` è in sospeso e i filegroup sono offline.  
  
     I messaggi relativi all'ultima istruzione `RESTORE LOG` nel passaggio 1 indicano che il rollback delle transazioni che interessano il filegroup `C` è stato posticipato, poiché tale filegroup non è disponibile. È possibile continuare a eseguire le normali operazioni, ma sono attivi blocchi da parte di queste transazioni e non sarà possibile eseguire il troncamento del log fino al completamento del rollback.  
  
     Nella seconda sequenza di ripristino l'amministratore del database ripristina il filegroup `C`:  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' FROM backup2a WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup4 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup5 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     A questo punto il filegroup primario e i filegroup `A` e `C` sono online. Il recupero dei file nel filegroup `B` è ancora in sospeso e questo filegroup è offline. Le transazioni posticipate sono state risolte e si procede al troncamento del log.  
  
3.  Eseguire un ripristino online del filegroup `B`.  

   Nella terza sequenza di ripristino l'amministratore del database ripristina il filegroup `B`. Il backup del filegroup `B` è stato eseguito dopo la sua conversione in filegroup di sola lettura. Non è pertanto necessario eseguire il roll forward del filegroup durante il recupero.  
  
   ```sql  
   RESTORE DATABASE adb FILEGROUP='B' FROM backup2b WITH RECOVERY  
   ```  
  
   In questa fase tutti i filegroup sono online.  
  
## <a name="additional-examples"></a>Esempi aggiuntivi  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di lettura/scrittura &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Ripristino online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Applicare backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
