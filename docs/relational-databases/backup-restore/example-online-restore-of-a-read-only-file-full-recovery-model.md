---
title: 'Ripristino online: file di sola lettura (modello di recupero con registrazione completa)'
description: Questo esempio illustra un ripristino in linea in SQL Server di un file di sola lettura per un database usando il modello di recupero con registrazione completa con più filegroup.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- online restores [SQL Server], full recovery model
- restore sequences [SQL Server], online
ms.assetid: 7ea2d2af-086f-48dc-9636-38dc194c7090
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 55cf92ac9a4c2324449e27840782a6930478e953
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85747772"
---
# <a name="example-online-restore-of-a-read-only-file-full-recovery-model"></a>Esempio: Ripristino online di un file di sola lettura (modello di recupero con registrazione completa)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Le informazioni contenute in questo argomento interessano i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] basati sul modello di recupero con registrazione completa che includono più file o filegroup.  
  
 In questo esempio un database denominato `adb`, che utilizza il modello di recupero con registrazione completa, contiene tre filegroup. Il filegroup `A` è in lettura/scrittura, mentre i filegroup `B` e `C` sono di sola lettura. Inizialmente, tutti i filegroup sono online.  
  
 È necessario ripristinare il file di sola lettura `b1`nel filegroup `B` del database `adb` . Dato che è stato eseguito un backup dopo che il file è diventato di sola lettura, i backup del log non sono necessari. Il filegroup `B` sarà offline per l'intera durata del ripristino, mentre la rimanente parte del database rimarrà online.  
  
## <a name="restore-sequence"></a>Sequenza di ripristino  
  
> [!NOTE]  
>  La sintassi di una sequenza di ripristino online è la stessa di una sequenza di ripristino offline.  
  
 Per ripristinare il file, l'amministratore del database utilizza la sequenza di ripristino seguente:  
  
```  
RESTORE DATABASE adb FILE='b1' FROM filegroup_B_backup  
WITH RECOVERY   
```  
  
 Il filegroup B è ora online.  
  
## <a name="additional-examples"></a>Esempi aggiuntivi  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di lettura/scrittura &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristino online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Ripristini di file &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
