---
title: Backup della parte finale del log (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], tail of log
- transaction log backups [SQL Server], tail-log backups
- NO_TRUNCATE clause
- backups [SQL Server], log backups
- tail-log backups
- backups [SQL Server], tail-log backups
ms.assetid: 313ddaf6-ec54-4a81-a104-7ffa9533ca58
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cd7c505701a4edb1f66ca516d06179b2eb1a222d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956251"
---
# <a name="tail-log-backups-sql-server"></a>Backup della parte finale del log [SQL Server]
  Le informazioni contenute in questo argomento sono rilevanti solo per il backup e il ripristino di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizzano il modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk.  
  
 Un *backup della parte finale del log* acquisisce qualsiasi record di log di cui non è stato eseguito il backup (la *parte finale del log*) per prevenire perdita di dati e mantenere intatta la catena di log. Prima che sia possibile recuperare un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel punto temporale più recente, è necessario eseguire il backup della parte finale del log delle transazioni. Il backup della parte finale del log sarà l'ultimo backup di interesse nel piano di recupero per il database.  
  
> [!NOTE]  
>  Non in tutti gli scenari di ripristino è necessario un backup della parte finale del log. Se il punto di recupero è contenuto in un backup del log precedente, non è necessario un backup della parte finale del log. Non è inoltre necessario eseguire il backup della parte finale del log se il punto di recupero è incluso in un backup del log precedente o se si sta spostando o sostituendo (sovrascrivendo) il database e non è necessario ripristinarlo fino a un punto nel tempo dopo l'ultimo backup.  
  
 
  
##  <a name="scenarios-that-require-a-tail-log-backup"></a><a name="TailLogScenarios"></a> Scenari in cui è necessario un backup della parte finale del log  
 È consigliabile eseguire un backup della parte finale del log negli scenari seguenti:  
  
-   Se il database è online e si intende eseguire un'operazione di ripristino sul database, iniziare eseguendo il backup della parte finale del log. Per evitare un errore per un database online, è necessario utilizzare... Opzione WITH NORECOVERY dell'istruzione [backup](/sql/t-sql/statements/backup-transact-sql) [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   Se il database è offline e non si avvia e risulta necessario eseguire un'operazione di ripristino, iniziare eseguendo il backup della parte finale del log. Dato che in questo momento non può avvenire alcuna transazione, l'utilizzo di WITH NORECOVERY è facoltativo.  
  
-   Se un database è danneggiato, tentare di acquisire un backup della parte finale del log tramite l'opzione WITH CONTINUE_AFTER_ERROR dell'istruzione BACKUP.  
  
     Se il database è danneggiato, un backup della parte finale del log riuscirà solo se i file di log non sono danneggiati, il database è in uno stato che supporta il backup della parte finale del log e non include modifiche con registrazione minima delle operazioni bulk. Se non è possibile creare un backup della parte finale del log, qualsiasi transazione eseguita dopo l'ultimo backup del log andrà persa.  
  
 Nella tabella seguente vengono riepilogate le opzioni BACKUP NORECOVERY e CONTINUE_AFTER_ERROR.  
  
|Opzione BACKUP LOG|Commenti|  
|-----------------------|--------------|  
|NORECOVERY|Utilizzare NORECOVERY ogni volta che si intende procedere con un'operazione di ripristino sul database. NORECOVERY porta il database nello stato di ripristino. Questo assicura che il database non si modifichi dopo il backup della parte finale del log.  Il log viene troncato a meno che non venga specificata anche l'opzione NO_TRUNCATE o COPY_ONLY.<br /><br /> Importante è consigliabile evitare di utilizzare NO_TRUNCATE, tranne quando il database è danneggiato. ** \* \* \* \* **|  
|CONTINUE_AFTER_ERROR|Utilizzare CONTINUE_AFTER_ERROR solo se si sta eseguendo il backup della parte finale di un database danneggiato.<br /><br /> Nota: quando si utilizza il backup della parte finale del log in un database danneggiato, alcuni dei metadati normalmente acquisiti nei backup del log potrebbero non essere disponibili. Per altre informazioni, vedere [Backup della parte finale del log con metadati di backup incompleti](#IncompleteMetadata) di seguito in questo argomento.|  
  
##  <a name="tail-log-backups-that-have-incomplete-backup-metadata"></a><a name="IncompleteMetadata"></a>Backup della parte finale del log con metadati di backup incompleti  
 I backup della parte finale del log consentono di acquisire la parte finale del log anche quando il database è offline, è danneggiato oppure è privo di alcuni file di dati. Questo può causare metadati incompleti nei comandi di ripristino delle informazioni e in **msdb**. Tuttavia, solo i metadati sono incompleti. Il log acquisito è completo e utilizzabile.  
  
 Se un backup della parte finale del log include metadati incompleti, nella tabella [backupset](/sql/relational-databases/system-tables/backupset-transact-sql)**has_incomplete_metadata** è impostato su **1**. Inoltre, nell'output di [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql), **HasIncompleteMetadata** è impostato su **1**.  
  
 Se i metadati in un backup della parte finale del log sono incompleti, nella tabella [backupfilegroup](/sql/relational-databases/system-tables/backupfilegroup-transact-sql) mancheranno la maggioranza delle informazioni sui filegroup al momento dell'esecuzione del backup della parte finale del log. La maggioranza delle colonne della tabella **backupfilegroup** sono NULL. Le uniche colonne significative sono le seguenti:  
  
-   **backup_set_id**  
  
-   **filegroup_id**  
  
-   **type**  
  
-   **type_desc**  
  
-   **is_readonly**  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 Per creare un backup della parte finale del log, vedere [Esecuzione del backup del log delle transazioni quando il database è danneggiato &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
 Per ripristinare un backup del log delle transazioni, vedere [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Backup e ripristino di database SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [Backup di sola copia &#40;SQL Server&#41;](copy-only-backups-sql-server.md)   
 [Backup di log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Applicare backup di log delle transazioni &#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)  
  
  
