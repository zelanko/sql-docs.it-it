---
title: Ripristini di database completi (modello di recupero con registrazione minima) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- complete database restores
- database restores [SQL Server], complete database
- restoring databases [SQL Server], complete database
- simple recovery model [SQL Server]
- restoring [SQL Server], database
ms.assetid: 49828927-1727-4d1d-9ef5-3de43f68c026
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e64bf4d4642d8091cd0892283a996e7dccc56e26
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62877145"
---
# <a name="complete-database-restores-simple-recovery-model"></a>Ripristini di database completi (modello di recupero con registrazione minima)
  L'obiettivo di un ripristino completo del database è il ripristino dell'intero database. L'intero database è offline per la tutta la durata del ripristino. Prima che sia possibile portare online una o più parti del database, tutti i dati vengono recuperati fino a un punto coerente in cui tutte le parti del database sono aggiornate allo stesso punto nel tempo e non sono presenti transazioni di cui non è stato eseguito il commit.  
  
 Il modello di recupero con registrazione minima non consente di ripristinare il database fino a uno specifico punto nel tempo all'interno di un determinato backup.  
  
> [!IMPORTANT]  
>  È consigliabile evitare di collegare o ripristinare database provenienti da origini sconosciute o non attendibili. Questi database potrebbero contenere malware che può eseguire codice [!INCLUDE[tsql](../../../includes/tsql-md.md)] indesiderato o causare errori modificando lo schema o la struttura fisica di database. Prima di utilizzare un database da un'origine sconosciuta o non attendibile, eseguire [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) sul database in un server non di produzione ed esaminare il codice contenuto nel database, ad esempio le stored procedure o altro codice definito dall'utente.  
  

  
> [!NOTE]  
>  Per informazioni sul supporto dei backup di versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere la sezione "Supporto della compatibilità" di [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
##  <a name="overview-of-database-restore-under-the-simple-recovery-model"></a><a name="Overview"></a> Panoramica del ripristino del database nel modello di recupero con registrazione minima  
 Se si utilizza il modello di recupero con registrazione minima, il ripristino completo del database richiede solo una o due istruzioni [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) , a seconda che si desideri o meno ripristinare un backup differenziale del database. Se si utilizza solo un backup di database completo, ripristinare unicamente il backup più recente come illustrato nella figura seguente.  
  
 ![Ripristino solo di un backup completo del database](../../database-engine/media/bnrr-rmsimple1-fulldbbu.gif "Ripristino solo di un backup completo del database")  
  
 Se si utilizza anche un backup differenziale del database, ripristinare il backup completo del database più recente senza recuperare il database e quindi ripristinare il backup differenziale del database più recente e recuperare il database. Questo processo viene illustrato nella figura seguente.  
  
 ![Ripristino di backup completi e differenziali del database](../../database-engine/media/bnrr-rmsimple2-diffdbbu.gif "Ripristino di backup completi e differenziali del database")  
  
> [!NOTE]  
>  Se si prevede di ripristinare un backup del database in un'istanza del server diversa, vedere [Copiare database tramite backup e ripristino](../databases/copy-databases-with-backup-and-restore.md).  
  
###  <a name="basic-transact-sql-restore-syntax"></a><a name="TsqlSyntax"></a> Sintassi Transact-SQL di base per RESTORE  
 La sintassi di base di [!INCLUDE[tsql](../../../includes/tsql-md.md)][RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) per il ripristino di un backup di database completo è la seguente:  
  
 RESTORE DATABASE *nome_database* FROM *dispositivo_backup* [ WITH NORECOVERY ]  
  
> [!NOTE]  
>  Utilizzare WITH NORECOVERY se si desidera ripristinare anche un backup differenziale del database.  
  
 La sintassi di base di [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) per il ripristino di un backup del database è la seguente:  
  
 RESTORE DATABASE *nome_database* FROM *dispositivo_backup* WITH RECOVERY  
  
###  <a name="example-transact-sql"></a><a name="Example"></a> Esempio (Transact-SQL)  
 Nell'esempio seguente viene innanzitutto illustrato come utilizzare l'istruzione [BACKUP](/sql/t-sql/statements/backup-transact-sql) per creare un backup completo del database e un backup differenziale del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Questi backup vengono quindi ripristinati in sequenza. Il database è ripristinato con lo stesso stato del momento in cui è stato completato il backup differenziale del database.  
  
 Nell'esempio seguente vengono illustrate le opzioni fondamentali di una sequenza di ripristino per lo scenario di ripristino completo del database. Una *sequenza di ripristino* è costituita da una o più operazioni di ripristino che gestiscono lo spostamento dei dati attraverso una o più fasi del ripristino. La sintassi e i dettagli non rilevanti sono stati omessi. Quando si recupera un database, è consigliabile specificare in modo esplicito l'opzione RECOVERY per maggiore chiarezza, anche se si tratta dell'opzione predefinita.  
  
> [!NOTE]  
>  L'esempio inizia con un'istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) che imposta il modello di recupero su `SIMPLE`.  
  
```  
USE master;  
--Make sure the database is using the simple recovery model.  
ALTER DATABASE AdventureWorks2012 SET RECOVERY SIMPLE;  
GO  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
  WITH FORMAT;  
GO  
--Create a differential database backup.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH DIFFERENTIAL;  
GO  
--Restore the full database backup (from backup set 1).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=1, NORECOVERY;  
--Restore the differential backup (from backup set 2).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=2, RECOVERY;  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 **Per ripristinare un backup completo del database**  
  
-   [Ripristinare un backup del database nel modello di recupero con registrazione minima &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Ripristinare un backup del database &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
 **Per ripristinare un backup differenziale del database**  
  
-   [Ripristinare un backup differenziale del database &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
 **Per ripristinare un backup utilizzando SMO (SQL Server Management Objects)**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  

  
## <a name="see-also"></a>Vedi anche  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [sp_addumpdevice &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [Backup completi del database &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [Backup differenziali &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
