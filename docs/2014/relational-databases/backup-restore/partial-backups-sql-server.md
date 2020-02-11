---
title: Backup parziali (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 4213bcee1d17d27bf63da9eb286b21dea4cc5a02
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62921930"
---
# <a name="partial-backups-sql-server"></a>Backup parziali (SQL Server)
  Tutti i modelli di recupero di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano backup parziali, pertanto questo argomento è attinente per tutti i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I backup parziali sono tuttavia progettati per l'utilizzo con il modello di recupero con registrazione minima e consentono di migliorare la flessibilità per i backup di database di dimensioni molto grandi contenenti uno o più filegroup di sola lettura.  
  
 I backup parziali sono utili quando si desidera escludere i filegroup di sola lettura. Un *backup parziale* è simile a un backup completo del database, ma non contiene tutti i filegroup. Per un database di lettura/scrittura, un backup parziale contiene invece i dati del filegroup primario, tutti i filegroup di lettura/scrittura e uno o più file di sola lettura specificati facoltativamente. Il backup parziale di un database di sola lettura contiene esclusivamente il filegroup primario.  
  
> [!NOTE]  
>  Se un database di sola lettura diventa di lettura/scrittura dopo un backup parziale, potrebbero essere presenti filegroup secondari di lettura/scrittura non inclusi nel backup parziale. In questo caso, se si tenta di eseguire un backup parziale differenziale, l'operazione non verrà completata. Prima di poter eseguire un backup parziale differenziale del database, è necessario eseguire un altro backup parziale. Il nuovo backup parziale include tutti i filegroup secondari di lettura/scrittura e può fungere da base per backup parziali differenziali.  
  
 I backup di file relativi a filegroup di sola lettura possono essere combinati con backup parziali. Per informazioni sui backup di file, vedere [Backup completi di file &#40;SQL Server&#41;](full-file-backups-sql-server.md).  
  
 Un backup parziale può essere utilizzato come *base differenziale* per backup parziali differenziali. Per altre informazioni, vedere [Backup differenziali &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
> [!NOTE]  
>  I backup parziali non sono supportati in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] né nella Creazione guidata piano di manutenzione.  
  
 **Per creare un backup parziale**  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql) (READ_WRITE_FILEGROUPS; opzione FILEGROUP, se necessario)  
  
 **Per utilizzare un backup parziale in una sequenza di ripristino**  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione minima&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione minima&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Ripristini di file &#40;modello di recupero con registrazione minima&#41;](file-restores-simple-recovery-model.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
