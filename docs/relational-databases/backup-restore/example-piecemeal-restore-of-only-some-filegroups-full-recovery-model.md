---
title: 'Ripristino a fasi: alcuni filegroup (modello di recupero con registrazione completa)'
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
ms.assetid: bced4b54-e819-472b-b784-c72e14e72a0b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3794c2453bdd541aa9bdbabe5c5d79c20a243f31
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "75243711"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-full-recovery-model"></a>Esempio: Ripristino a fasi di un numero limitato di filegroup (modello di recupero con registrazione completa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Le informazioni contenute in questo argomento interessano i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] basati sul modello di recupero con registrazione completa che includono più file o filegroup.  
  
 Una sequenza di ripristino a fasi consente di ripristinare e recuperare un database in varie fasi a livello di filegroup, a partire dal filegroup primario e tutti i filegroup secondari di lettura/scrittura.  
  
 In questo esempio un database denominato `adb`, che utilizza il modello di recupero con registrazione completa, contiene tre filegroup. Il filegroup `A` è in lettura/scrittura, mentre i filegroup `B` e `C` sono di sola lettura. Inizialmente, tutti i filegroup sono online.  
  
 Il filegroup primario e il filegroup `B` del database `adb` risultano danneggiati. Il filegroup primario è di dimensioni limitate ed è possibile ripristinarlo rapidamente. L'amministratore del database decide di ripristinare i filegroup utilizzando una sequenza di ripristino a fasi. Innanzitutto, il filegroup primario e i log delle transazioni successivi vengono ripristinati e il database recuperato.  
  
 I filegroup integri `A` e `C` includono dati di importanza critica. Verranno pertanto recuperati e resi disponibili online il più rapidamente possibile. Infine, viene ripristinato e recuperato il filegroup secondario danneggiato `B`.  
  
## <a name="restore-sequences"></a>Sequenze di ripristino:  
  
> [!NOTE]  
>  La sintassi di una sequenza di ripristino online è la stessa di una sequenza di ripristino offline.  
  
1.  Creare un backup della parte finale del log per il database `adb`. Questo passaggio è fondamentale per fare in modo che i filegroup integri `A` e `C` vengano aggiornati rispetto al punto di recupero del database.  
  
    ```  
    BACKUP LOG adb TO tailLogBackup WITH NORECOVERY  
    ```  
  
2.  Eseguire un ripristino parziale del filegroup primario.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup   
    WITH PARTIAL, NORECOVERY  
    RESTORE LOG adb FROM log_backup1 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup2 WITH NORECOVERY  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     In questa fase il filegroup primario è online. Il recupero dei file nei filegroup `A`, `B`e `C` è in sospeso e questi filegroup sono offline.  
  
3.  Eseguire un ripristino online dei filegroup `A` e `C`.  
  
     Non è necessario ripristinare questi filegroup da un backup poiché i dati in essi contenuti non sono danneggiati, ma è necessario recuperarli per attivare la modalità online.  
  
     L'amministratore del database recupera `A` e `C` immediatamente.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A', FILEGROUP='C' WITH RECOVERY  
    ```  
  
     A questo punto il filegroup primario e i filegroup `A` e `C` sono online. Il recupero dei file nel filegroup `B` è ancora in sospeso e questo filegroup è offline.  
  
4.  Eseguire un ripristino online del filegroup `B`.  

   I file nel filegroup `B` vengono ripristinati in un qualsiasi momento successivo.  
  
   > [!NOTE]  
   >  Il backup del filegroup `B` è stato eseguito dopo che il filegroup è diventato di sola lettura, quindi non è necessario eseguire il roll forward di questi file.  
  
   ```sql  
   RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY  
   ```  
  
   In questa fase tutti i filegroup sono online.  
  
## <a name="additional-examples"></a>Esempi aggiuntivi  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di lettura/scrittura &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Ripristino online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Applicare backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
