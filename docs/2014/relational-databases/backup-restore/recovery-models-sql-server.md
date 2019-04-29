---
title: Modelli di recupero (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 6c5b85e316c859e0b6d44fb83e3df6da2edd72ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62921766"
---
# <a name="recovery-models-sql-server"></a>Modelli di recupero (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le operazioni di backup e ripristino vengono eseguite nel contesto di un modello di recupero del database. I modelli di recupero sono progettati per controllare la manutenzione del log delle transazioni. Un *modello di recupero* è una proprietà del database che determina la modalità di registrazione delle transazioni, se è necessario e possibile eseguire il backup del log delle transazioni e quali tipi di operazioni di ripristino sono disponibili. Sono tre i modelli di recupero disponibili: con registrazione minima, con registrazione completa e con registrazione minima delle operazioni bulk. In genere, un database utilizza il modello di recupero con registrazione completa o con registrazione minima. In un database è possibile passare a un modello di recupero diverso in qualsiasi momento.  
  
 **Contenuto dell'argomento**  
  
-   [Panoramica del modello di recupero](#RMov)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="RMov"></a> Panoramica del modello di recupero  
 Nella tabella seguente vengono riepilogati i tre modelli di recupero.  
  
|modello di recupero|Descrizione|Potenziale perdita di dati|Recupero temporizzato|  
|--------------------|-----------------|------------------------|-------------------------------|  
|**Simple**|Non vengono eseguiti backup del log.<br /><br /> Lo spazio del log viene automaticamente recuperato per limitare i requisiti di spazio ed evitare la necessità di gestire lo spazio del log delle transazioni. Per informazioni sui backup di database nel modello di recupero con registrazione minima, vedere [Backup completo del database &#40;SQL Server&#41;](full-database-backups-sql-server.md).<br /><br /> Le operazioni che richiedono i backup dei log delle transazioni non sono supportate dal modello di recupero con registrazione minima. Le seguenti funzionalità non possono essere utilizzate nei modelli di recupero con registrazione minima:<br /><br /> Log shipping<br /><br /> Mirroring del database o AlwaysOn<br /><br /> Recupero dei supporti senza perdita dei dati<br /><br /> Ripristini temporizzati|Le modifiche eseguite in seguito al backup più recente non sono protette. In caso di emergenza sarà necessario applicare nuovamente tali modifiche.|Consente solo il recupero fino al momento corrispondente al termine di un backup. Per altre informazioni, vedere [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](complete-database-restores-simple-recovery-model.md).|  
|**Full**|Devono essere eseguiti backup del log.<br /><br /> Non si verifica alcuna perdita di dati dovuta a un file di dati perduto o danneggiato.<br /><br /> È possibile eseguire il recupero fino a un punto nel tempo arbitrario, ad esempio precedente all'errore dell'applicazione o dell'utente. Per informazioni sui backup di database nel modello di recupero con registrazione completa, vedere [Backup completo del database &#40;SQL Server&#41;](full-database-backups-sql-server.md) e [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](complete-database-restores-full-recovery-model.md).|In genere non sussiste alcun rischio.<br /><br /> Se la parte finale del log è danneggiata, sarà necessario ripetere le modifiche apportate dall'ultimo backup del log.|È possibile eseguire il recupero a una temporizzazione specifica, purché i backup siano completi fino a tale momento specifico. Per informazioni sull'utilizzo di backup del log per il ripristino al punto di errore, vedere [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).<br /><br /> Nota: Se si dispone di due o più database di modello di recupero full che devono essere consistenti, si potrebbe essere necessario implementare procedure speciali per verificare la recuperabilità di questi database. Per altre informazioni, vedere [Recupero di database correlati che contengono transazioni contrassegnate](recovery-of-related-databases-that-contain-marked-transaction.md).|  
|**Con registrazione minima delle operazioni bulk**|Devono essere eseguiti backup del log.<br /><br /> Complemento del modello di recupero con registrazione completa che consente operazioni di copia bulk a prestazioni elevate.<br /><br /> Riduce l'utilizzo di spazio del log tramite la registrazione minima della maggior parte delle operazioni bulk. Per informazioni sulle operazioni a cui può essere applicata la registrazione minima, vedere [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md).<br /><br /> Per informazioni sui backup di database nel modello di recupero con registrazione minima delle operazioni bulk, vedere [Backup completo del database &#40;SQL Server&#41;](full-database-backups-sql-server.md) e [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](complete-database-restores-full-recovery-model.md).|Se il log è danneggiato o sono state eseguite operazioni con registrazione minima delle operazioni bulk dopo l'ultimo backup del log, sarà necessario ripetere le modifiche apportate dall'ultimo backup del log.<br /><br /> Negli altri casi non si verifica alcuna perdita di dati.|Consente il recupero fino al momento corrispondente al termine di ogni backup. Il recupero temporizzato non è supportato.|  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Visualizzare o modificare il modello di recupero di un database &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [Risolvere i problemi relativi a un log delle transazioni completo &#40;Errore di SQL Server 9002&#41;](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="see-also"></a>Vedere anche  
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [Backup e ripristino di database SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [Automatizzazione delle attività amministrative &#40;SQL Server Agent&#41;](../../ssms/agent/sql-server-agent.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
