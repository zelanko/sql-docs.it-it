---
title: Backup della parte finale del log (SQL Server) | Microsoft Docs
description: In SQL Server un backup della parte finale del log acquisisce qualsiasi record di log di cui non è stato eseguito il backup per prevenire perdite di dati e per mantenere intatta la catena di log.
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: backup-restore
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
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fa48e2e96c5066ee2a2bd5d2757a3ae8f669225b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85631365"
---
# <a name="tail-log-backups-sql-server"></a>Backup della parte finale del log [SQL Server]
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Le informazioni contenute in questo argomento sono rilevanti solo per il backup e il ripristino di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizzano il modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk.  
  
 Un *backup della parte finale del log* acquisisce qualsiasi record di log di cui non è stato eseguito il backup (la *parte finale del log*) per prevenire perdita di dati e mantenere intatta la catena di log. Prima che sia possibile recuperare un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel punto temporale più recente, è necessario eseguire il backup della parte finale del log delle transazioni. Il backup della parte finale del log sarà l'ultimo backup di interesse nel piano di recupero per il database.  
  
> **NOTA** Non in tutti gli scenari di ripristino è necessario un backup della parte finale del log. Se il punto di recupero è contenuto in un backup del log precedente, non è necessario un backup della parte finale del log. Non è inoltre necessario eseguire il backup della parte finale del log se il punto di recupero è incluso in un backup del log precedente o se si sta spostando o sostituendo (sovrascrivendo) il database e non è necessario ripristinarlo fino a un punto nel tempo dopo l'ultimo backup.  
  
   ##  <a name="scenarios-that-require-a-tail-log-backup"></a><a name="TailLogScenarios"></a> Scenari in cui è necessario un backup della parte finale del log  
 È consigliabile eseguire un backup della parte finale del log negli scenari seguenti:  
  
-   Se il database è online e si intende eseguire un'operazione di ripristino sul database, iniziare eseguendo il backup della parte finale del log. Per evitare un errore per un database online, è necessario usare... Opzione WITH NORECOVERY dell'istruzione [BACKUP](../../t-sql/statements/backup-transact-sql.md) di [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Se il database è offline e non si avvia e risulta necessario eseguire un'operazione di ripristino, iniziare eseguendo il backup della parte finale del log. Dato che in questo momento non può avvenire alcuna transazione, l'utilizzo di WITH NORECOVERY è facoltativo.  
  
-   Se un database è danneggiato, tentare di acquisire un backup della parte finale del log tramite l'opzione WITH CONTINUE_AFTER_ERROR dell'istruzione BACKUP.  
  
     Se il database è danneggiato, un backup della parte finale del log riuscirà solo se i file di log non sono danneggiati, il database è in uno stato che supporta il backup della parte finale del log e non include modifiche con registrazione minima delle operazioni bulk. Se non è possibile creare un backup della parte finale del log, qualsiasi transazione eseguita dopo l'ultimo backup del log andrà persa.  
  
 Nella tabella seguente vengono riepilogate le opzioni BACKUP NORECOVERY e CONTINUE_AFTER_ERROR.  
  
|Opzione BACKUP LOG|Commenti|  
|-----------------------|--------------|  
|NORECOVERY|Utilizzare NORECOVERY ogni volta che si intende procedere con un'operazione di ripristino sul database. NORECOVERY porta il database nello stato di ripristino. Questo assicura che il database non si modifichi dopo il backup della parte finale del log. Il log verrà troncato a meno che non venga specificata anche l'opzione NO_TRUNCATE o COPY_ONLY.<br /><br /> **Importante:** non usare NO_TRUNCATE, a meno che il database non sia danneggiato. Potrebbe essere necessario attivare la [modalità utente singolo](../../relational-databases/databases/set-a-database-to-single-user-mode.md) per il database per ottenere l'accesso esclusivo prima di eseguire il ripristino con NORECOVERY. Dopo il ripristino, impostare di nuovo il database sulla modalità multiutente. |  
|CONTINUE_AFTER_ERROR|Utilizzare CONTINUE_AFTER_ERROR solo se si sta eseguendo il backup della parte finale di un database danneggiato.<br /><br /> Quando si utilizza il backup della parte finale di un database danneggiato, alcuni dei metadati normalmente acquisiti nei backup dei log potrebbero essere non disponibili. Per altre informazioni, vedere [Backup della parte finale del log con metadati di backup incompleti](#IncompleteMetadata)in questo argomento.|  
  
##  <a name="tail-log-backups-that-have-incomplete-backup-metadata"></a><a name="IncompleteMetadata"></a> Backup della parte finale del log con metadati di backup incompleti  
 I backup della parte finale del log consentono di acquisire la parte finale del log anche quando il database è offline, è danneggiato oppure è privo di alcuni file di dati. Questo può causare metadati incompleti nei comandi di ripristino delle informazioni e in **msdb**. Tuttavia, solo i metadati sono incompleti. Il log acquisito è completo e utilizzabile.  
  
 Se un backup della parte finale del log include metadati incompleti, nella tabella [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)**has_incomplete_metadata** è impostato su **1**. Inoltre, nell'output di [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), **HasIncompleteMetadata** è impostato su **1**.  
  
 Se i metadati in un backup della parte finale del log sono incompleti, nella tabella [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md) mancheranno la maggioranza delle informazioni sui filegroup al momento dell'esecuzione del backup della parte finale del log. La maggioranza delle colonne della tabella **backupfilegroup** sono NULL. Le uniche colonne significative sono le seguenti:  
  
-   **backup_set_id**  
-   **filegroup_id**  
-   **type**  
-   **type_desc**  
-   **is_readonly**  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 Per creare un backup della parte finale del log, vedere [Esecuzione del backup del log delle transazioni quando il database è danneggiato &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
 Per ripristinare un backup del log delle transazioni, vedere [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
    
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Backup di sola copia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [Backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Applicare backup del log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)    
 [Architettura e gestione del log delle transazioni di SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)
  
