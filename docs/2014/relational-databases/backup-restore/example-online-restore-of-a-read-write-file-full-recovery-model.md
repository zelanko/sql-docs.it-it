---
title: 'Esempio: Ripristino online di un File di lettura / scrittura (modello di recupero con registrazione completa) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- online restores [SQL Server], full recovery model
- restore sequences [SQL Server], online
ms.assetid: 0dbeda81-1464-44ba-9011-914900096368
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 45056586be543894c714f4005ba84826aa856674
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62876068"
---
# <a name="example-online-restore-of-a-read-write-file-full-recovery-model"></a>Esempio: Ripristino online di un file di lettura/scrittura (modello di recupero con registrazione completa)
  Le informazioni contenute in questo argomento interessano i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] basati sul modello di recupero con registrazione completa che includono più file o filegroup.  
  
 In questo esempio un database denominato `adb`, che utilizza il modello di recupero con registrazione completa, contiene tre filegroup. Il filegroup `A` è in lettura/scrittura, mentre i filegroup `B` e `C` sono di sola lettura. Inizialmente, tutti i filegroup sono online.  
  
 Il file `a1` del filegroup `A` è danneggiato e l'amministratore del database decide di ripristinarlo, mantenendo online il database.  
  
> [!NOTE]  
>  Il modello di recupero con registrazione minima non consente il ripristino online di dati di lettura/scrittura.  
  
## <a name="restore-sequences"></a>Sequenze di ripristino  
  
> [!NOTE]  
>  La sintassi di una sequenza di ripristino online è la stessa di una sequenza di ripristino offline.  
  
1.  Ripristino in linea del file `a1`.  
  
    ```  
    RESTORE DATABASE adb FILE='a1' FROM backup   
    WITH NORECOVERY;  
    ```  
  
     A questo punto lo stato del file a1 è RESTORING e il filegroup A è offline.  
  
2.  Al termine del ripristino del file, l'amministratore del database esegue un nuovo backup del log per garantire l'acquisizione del punto in cui il file è passato offline.  
  
    ```  
    BACKUP LOG adb TO log_backup3;   
    ```  
  
3.  Ripristino online dei backup del log.  
  
     L'amministratore ripristina tutti i backup del log a partire dal backup del file ripristinato fino all'ultimo backup del log (*log_backup3*, eseguito nel passaggio 2). Una volta ripristinato l'ultimo backup, viene recuperato il database.  
  
    ```  
    RESTORE LOG adb FROM log_backup1 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup2 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY;  
    RESTORE LOG adb WITH RECOVERY;  
    ```  
  
     Il file `a1` è ora online.  
  
## <a name="additional-examples"></a>Esempi aggiuntivi  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione minima&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione minima&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;Modello di recupero con registrazione minima&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;Modello di recupero con registrazione completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristino online &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [Applicazione dei backup di log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
