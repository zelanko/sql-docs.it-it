---
title: Modelli di recupero (SQL Server) | Microsoft Docs
description: In SQL Server il modello di recupero determina la modalità di registrazione delle transazioni, se è necessario eseguire il backup del log delle transazioni e quali operazioni di ripristino sono disponibili.
ms.custom: ''
ms.date: 07/16/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- bulk-logged recovery model [SQL Server]
- recovery [SQL Server], recovery model
- restoring transaction logs [SQL Server], recovery models
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], about
- transaction log backups [SQL Server]
- simple recovery model [SQL Server]
- backups [SQL Server], recovery models
- recovery models [SQL Server]
- recovery models [SQL Server], transaction log management
- database restores [SQL Server], recovery models
- transaction log restores [SQL Server]
- logs [SQL Server], recovery models
- restoring databases [SQL Server], recovery models
- full recovery model [SQL Server]
- backing up transaction logs [SQL Server], recovery models
ms.assetid: 8cfea566-8f89-4581-b30d-c53f1f2c79eb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c7d04f6a6ed9a1e09c3ca278e1481000abc6cab8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "82180882"
---
# <a name="recovery-models-sql-server"></a>Modelli di recupero (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le operazioni di backup e ripristino vengono eseguite nel contesto di un modello di recupero del database. I modelli di recupero sono progettati per controllare la manutenzione del log delle transazioni. Un *modello di recupero* è una proprietà del database che determina la modalità di registrazione delle transazioni, se è necessario e possibile eseguire il backup del log delle transazioni e quali tipi di operazioni di ripristino sono disponibili. Sono tre i modelli di recupero disponibili: con registrazione minima, con registrazione completa e con registrazione minima delle operazioni bulk. In genere, un database utilizza il modello di recupero con registrazione completa o con registrazione minima. In un database è possibile passare a un modello di recupero diverso in qualsiasi momento.  
  
 **Contenuto dell'argomento**  
  
-   [Panoramica del modello di recupero](#RMov)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="recovery-model-overview"></a><a name="RMov"></a> Panoramica del modello di recupero  
 Nella tabella seguente vengono riepilogati i tre modelli di recupero.  
  
|modello di recupero|Descrizione|Potenziale perdita di dati|Recupero temporizzato|  
|--------------------|-----------------|------------------------|-------------------------------|  
|**Simple**|Non vengono eseguiti backup del log.<br /><br /> Lo spazio del log viene automaticamente recuperato per limitare i requisiti di spazio ed evitare la necessità di gestire lo spazio del log delle transazioni. Per informazioni sui backup di database nel modello di recupero con registrazione minima, vedere [Backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md).<br /><br /> Le operazioni che richiedono i backup dei log delle transazioni non sono supportate dal modello di recupero con registrazione minima. Le seguenti funzionalità non possono essere utilizzate nei modelli di recupero con registrazione minima:<br /><br /> \- Log shipping<br /><br /> \- Always On o mirroring del database<br /><br /> \- Recupero dei supporti senza perdita di dati<br /><br /> \- Ripristini temporizzati|Le modifiche eseguite in seguito al backup più recente non sono protette. In caso di emergenza sarà necessario applicare nuovamente tali modifiche.|Consente solo il recupero fino al momento corrispondente al termine di un backup. Per altre informazioni, vedere [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md). <br><br> Per una spiegazione più dettagliata del modello di recupero con registrazione minima, vedere [SQL Server Simple Recovery Model (modello di recupero con registrazione minima di SQL Server)](https://www.mssqltips.com/sqlservertutorial/4/sql-server-simple-recovery-model/) a cura degli esperti di [MSSQLTips!](https://www.mssqltips.com)|  
|**Completo**|Devono essere eseguiti backup del log.<br /><br /> Non si verifica alcuna perdita di dati dovuta a un file di dati perduto o danneggiato.<br /><br /> È possibile eseguire il recupero fino a un punto nel tempo arbitrario, ad esempio precedente all'errore dell'applicazione o dell'utente. Per informazioni sui backup di database nel modello di recupero con registrazione completa, vedere [Backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md) e [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md).|In genere non sussiste alcun rischio.<br /><br /> Se la parte finale del log è danneggiata, sarà necessario ripetere le modifiche apportate dall'ultimo backup del log.|È possibile eseguire il recupero a una temporizzazione specifica, purché i backup siano completi fino a tale momento specifico. Per informazioni sull'utilizzo di backup del log per il ripristino al punto di errore, vedere [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).<br /><br /> Nota: Se sono presenti due o più database in cui viene usato il modello di recupero con registrazione completa che devono essere coerenti da un punto di vista logico, potrebbe essere necessario implementare procedure speciali per verificare la recuperabilità di questi database. Per altre informazioni, vedere [Recupero di database correlati che contengono transazioni contrassegnate](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md).|  
|**Con registrazione minima delle operazioni bulk**|Devono essere eseguiti backup del log.<br /><br /> Complemento del modello di recupero con registrazione completa che consente operazioni di copia bulk a prestazioni elevate.<br /><br /> Riduce l'utilizzo di spazio del log tramite la registrazione minima della maggior parte delle operazioni bulk. Per informazioni sulle operazioni a cui può essere applicata la registrazione minima, vedere [Log delle transazioni &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).<br /><br /> I backup del log possono raggiungere dimensioni significative perché le operazioni con registrazione minima vengono acquisite nel backup del log. Per informazioni sui backup di database nel modello di recupero con registrazione minima delle operazioni bulk, vedere [Backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md) e [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md).|Se il log è danneggiato o sono state eseguite operazioni con registrazione minima delle operazioni bulk dopo l'ultimo backup del log, sarà necessario ripetere le modifiche apportate dall'ultimo backup del log.<br /><br /> Negli altri casi non si verifica alcuna perdita di dati.|Consente il recupero fino al momento corrispondente al termine di ogni backup. Il recupero temporizzato non è supportato.|  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Visualizzazione o modifica del modello di recupero di un database &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [Risolvere i problemi relativi a un log delle transazioni completo &#40;Errore di SQL Server 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="see-also"></a>Vedere anche  
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Log delle transazioni &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Automatizzazione delle attività amministrative &#40;SQL Server Agent&#41;](https://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
  
  
