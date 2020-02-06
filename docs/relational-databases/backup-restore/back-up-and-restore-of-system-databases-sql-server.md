---
title: 'Backup e ripristino: database di sistema'
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server], backing up and restoring
- restoring system databases [SQL Server]
- backing up [SQL Server], system databases
- database backups [SQL Server], system databases
- servers [SQL Server], backup
ms.assetid: aef0c4fa-ba67-413d-9359-1a67682fdaab
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 45bfedfe24493221570ccc1bc07202f0b4ed8b1c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "75247474"
---
# <a name="backuprestoresystemdatabases-sql-server"></a>Backup e ripristino: database di sistema (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestisce un set di database a livello di sistema, denominati*database di sistema*, fondamentali per un corretto funzionamento di un'istanza del server. Dopo ogni aggiornamento importante, è necessario eseguire il backup di numerosi database di sistema. Alcuni database di sistema di cui è necessario eseguire sempre il backup sono **msdb**, **master**e **model**. Se un database usa la replica nell'istanza del server, è necessario eseguire il backup anche di un database di sistema **distribution** . I backup di questi database di sistema consentono di ripristinare e recuperare il sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qualora si verifichi un errore a livello di sistema, ad esempio un problema che impedisce di utilizzare un disco rigido.  
  
 Nella tabella seguente è presentato un riepilogo di tutti i database di sistema.  
  
|Database di sistema|Descrizione|Necessità di backup|modello di recupero|Commenti|  
|---------------------|-----------------|---------------------------|--------------------|--------------|  
|[master](../../relational-databases/databases/master-database.md)|Nel database vengono registrate tutte le informazioni a livello di sistema relative a un sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Sì|Semplice|Eseguire il backup di **master** con la frequenza necessaria a garantire una sufficiente protezione dei dati in base alle esigenze aziendali. È consigliabile pianificare i backup con regolarità, pianificazione che è possibile integrare con backup aggiuntivi dopo un aggiornamento importante.|  
|[model](../../relational-databases/databases/model-database.md)|Modello per tutti i database creati nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sì|Configurabile dall'utente*|Eseguire il backup di **model** solo se necessario in base alle esigenze aziendali, ad esempio immediatamente dopo la personalizzazione delle opzioni del database.<br /><br /> **Procedura consigliata:** creare solo backup completi del database **model**in base alle esigenze. Poiché nel database **model** vengono apportate solo di rado lievi modifiche, il backup del log non è necessario.|  
|[msdb](../../relational-databases/databases/msdb-database.md)|Il database utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per la pianificazione di avvisi e processi e per la registrazione di operatori. **msdb** contiene anche tabelle di cronologia, ad esempio tabelle di cronologia di backup e ripristino.|Sì|Con registrazione minima (impostazione predefinita)|Eseguire il backup di **msdb** a ogni aggiornamento.|  
|[Resource](../../relational-databases/databases/resource-database.md) (RDB)|Database di sola lettura che include copie di tutti gli oggetti di sistema forniti con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|No|-|Il database **Resource** risiede nel file mssqlsystemresource.mdf, che contiene solo codice. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può quindi eseguire il backup del database **Resource** .<br /><br /> Nota: è possibile eseguire un backup basato su file o su disco del file mssqlsystemresource.mdf considerando il file un file binario (EXE) anziché un file di database. Non è tuttavia possibile utilizzare la funzionalità di ripristino di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su questi backup. Il ripristino di una copia di backup di mssqlsystemresource.mdf può essere eseguito solo manualmente, prestando attenzione a non sovrascrivere il database **Resource** corrente con una versione non aggiornata e potenzialmente non sicura.|  
|[tempdb](../../relational-databases/databases/tempdb-database.md)|Area di lavoro per il mantenimento dei set di risultati temporanei o intermedi. Questo database viene ricreato ogni volta che viene avviata un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando l'istanza del server viene chiusa, i dati inclusi in **tempdb** vengono eliminati in modo definitivo.|No|Semplice|Non è possibile eseguire il backup del database di sistema **tempdb** .|  
|[Configurare la distribuzione](../../relational-databases/replication/configure-distribution.md)|Database esistente solo se il server è configurato come server di distribuzione repliche. In questo database sono memorizzati metadati e dati della cronologia per tutti i tipi di replica, nonché transazioni per la replica transazionale.|Sì|Semplice|Per informazioni su quando eseguire il backup del database **distribution** , vedere [Eseguire il backup e ripristino di database replicati](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).|  
  
 *Per conoscere l'attuale modello di recupero del modello, vedere [Visualizzare o modificare il modello di recupero di un database &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) o [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
## <a name="limitations-on-restoring-system-databases"></a>Limitazioni sul ripristino di database di sistema  
  
-   I database di sistema possono essere ripristinati solo da backup creati nella versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguita nell'istanza del server. Per ripristinare un database di sistema in un'istanza del server eseguita in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1, ad esempio, sarà necessario utilizzare un backup del database creato dopo l'aggiornamento dell'istanza del server a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1.  
  
-   Per ripristinare un database, è necessario che l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia in esecuzione. Per l'avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario che il database **master** sia accessibile e utilizzabile almeno in parte. Se il database **master** diventa inutilizzabile, è possibile ripristinare uno stato utilizzabile del database in uno dei modi seguenti:  
  
    -   Ripristinare il database **master** da un backup del database corrente.  
  
         Se è possibile avviare l'istanza del server, dovrebbe essere possibile anche ripristinare il database **master** da un backup completo del database.  
  
    -   Ricompilare il database **master** da zero.  
  
         Se non è possibile avviare **in seguito a gravi danni al database** master [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario ricompilare il database **master**. Per altre informazioni, vedere [Ricompilare database di sistema](../../relational-databases/databases/rebuild-system-databases.md).  
  
        > [!IMPORTANT]  
        >  La ricompilazione del database **master** comporta la ricompilazione di tutti i database di sistema.  
  
-   In alcune circostanze, per i problemi relativi al recupero del database modello può essere necessario ricompilare i database di sistema o sostituire i file mdf e ldf del database modello. Per altre informazioni, vedere [Ricompilare database di sistema](../../relational-databases/databases/rebuild-system-databases.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Creazione di un backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [Ripristinare il database master &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)  
  
-   [Visualizzazione o modifica del modello di recupero di un database &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [Spostare i database di sistema](../../relational-databases/databases/move-system-databases.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Database di distribuzione](../../relational-databases/replication/distribution-database.md)   
 [Database master](../../relational-databases/databases/master-database.md)   
 [Database msdb](../../relational-databases/databases/msdb-database.md)   
 [Database model](../../relational-databases/databases/model-database.md)   
 [Database Resource](../../relational-databases/databases/resource-database.md)   
 [Database tempdb](../../relational-databases/databases/tempdb-database.md)  
  
  
