---
title: Backup parziali (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- partial backups [SQL Server]
- READ_WRITE_FILEGROUPS option
- database backups [SQL Server], about backing up databases
ms.assetid: fe6b6bb1-38d0-46c4-bab8-31df14e8999c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a2c265d3a373eb53b822142fa2955d07b96b88f2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68033649"
---
# <a name="partial-backups-sql-server"></a>Backup parziali (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Tutti i modelli di recupero di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano backup parziali, pertanto questo argomento è attinente per tutti i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I backup parziali sono tuttavia progettati per l'utilizzo con il modello di recupero con registrazione minima e consentono di migliorare la flessibilità per i backup di database di dimensioni molto grandi contenenti uno o più filegroup di sola lettura.  
  
 I backup parziali sono utili quando si desidera escludere i filegroup di sola lettura. Un *backup parziale* è simile a un backup completo del database, ma non contiene tutti i filegroup. Per un database di lettura/scrittura, un backup parziale contiene invece i dati del filegroup primario, tutti i filegroup di lettura/scrittura e uno o più file di sola lettura specificati facoltativamente. Il backup parziale di un database di sola lettura contiene esclusivamente il filegroup primario.  
  
> [!NOTE]  
>  Se un database di sola lettura diventa di lettura/scrittura dopo un backup parziale, potrebbero essere presenti filegroup secondari di lettura/scrittura non inclusi nel backup parziale. In questo caso, se si tenta di eseguire un backup parziale differenziale, l'operazione non verrà completata. Prima di poter eseguire un backup parziale differenziale del database, è necessario eseguire un altro backup parziale. Il nuovo backup parziale include tutti i filegroup secondari di lettura/scrittura e può fungere da base per backup parziali differenziali.  
  
 I backup di file relativi a filegroup di sola lettura possono essere combinati con backup parziali. Per informazioni sui backup di file, vedere [Backup completi di file &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md).  
  
 Un backup parziale può essere utilizzato come *base differenziale* per backup parziali differenziali. Per altre informazioni, vedere [Backup differenziali &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
> [!NOTE]  
>  I backup parziali non sono supportati in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] né nella Creazione guidata piano di manutenzione.  
  
 **Per creare un backup parziale**  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md) (READ_WRITE_FILEGROUPS; opzione FILEGROUP, se necessario)  
  
 **Per utilizzare un backup parziale in una sequenza di ripristino**  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Ripristini di file &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
