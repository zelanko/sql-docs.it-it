---
title: Ripristini di database completi (modello di recupero con registrazione completa) | Microsoft Docs
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
- restoring [SQL Server], database
- full recovery model [SQL Server], performing restores
- log backups [SQL Server[
ms.assetid: 5b4c471c-b972-498e-aba9-92cf7a0ea881
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cb523d8e9b1dbbb136475d0aa739491935f755ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922158"
---
# <a name="complete-database-restores-full-recovery-model"></a>Ripristini di database completi (modello di recupero con registrazione completa)
  L'obiettivo di un ripristino completo del database è il ripristino dell'intero database. L'intero database è offline per la tutta la durata del ripristino. Prima che sia possibile portare online una o più parti del database, tutti i dati vengono recuperati fino a un punto coerente in cui tutte le parti del database sono aggiornate allo stesso punto nel tempo e non sono presenti transazioni di cui non è stato eseguito il commit.  
  
 Dopo aver ripristinato uno o più backup dei dati, è necessario ripristinare tutti i backup del log delle transazioni successivi nel modello di recupero con registrazione completa, quindi recuperare il database. È possibile ripristinare un database in un *punto di recupero* specifico all'interno di uno di questi backup del log. Tale punto di recupero può corrispondere a una data e un'ora specifiche, a una transazione contrassegnata o a un numero di sequenza del file di log (LSN).  
  
 Durante il ripristino di un database, in particolare nel modello di recupero con registrazione completa o in quello con registrazione minima delle operazioni bulk, si consiglia di utilizzare una sola sequenza di ripristino. Una *sequenza di ripristino* è costituita da una o più operazioni di ripristino che gestiscono lo spostamento dei dati attraverso una o più fasi del ripristino.  
  
> [!IMPORTANT]  
>  È consigliabile evitare di collegare o ripristinare database provenienti da origini sconosciute o non attendibili. Questi database potrebbero contenere malware che può eseguire codice [!INCLUDE[tsql](../../includes/tsql-md.md)] indesiderato o causare errori modificando lo schema o la struttura fisica di database. Prima di usare un database da un'origine sconosciuta o non attendibile, eseguire [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) sul database in un server non di produzione ed esaminare anche il codice contenuto nel database, ad esempio le stored procedure o altro codice definito dall'utente.  
  
 **Contenuto dell'argomento**  
  
-   [Ripristino di un database fino al momento dell'errore](#PointOfFailure)  
  
-   [Ripristino di un database fino a un punto all'interno di un backup del log](#PointWithinBackup)  
  
-   [Attività correlate](#RelatedTasks)  
  
> [!NOTE]  
>  Per informazioni sul supporto dei backup di versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere la sezione "Supporto della compatibilità" di [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
##  <a name="PointOfFailure"></a> Ripristino di un database fino al momento dell'errore  
 Il recupero dello stato di un database fino al momento dell'errore in genere include i passaggi seguenti:  
  
1.  Eseguire il backup del log delle transazioni attive (noto anche come parte finale del log). In questo modo viene creato un backup della parte finale del log. Se il log delle transazioni attivo non è disponibile, tutte le transazioni in quella parte del log vengono perdute.  
  
    > [!IMPORTANT]  
    >  Nel modello di recupero con registrazione minima delle operazioni bulk, per eseguire il backup di un log che contiene operazioni bulk registrate è necessario disporre dell'accesso a tutti i file di dati del database. Se i file di dati non sono accessibili, non è possibile eseguire il backup del log delle transazioni. In questo caso, è necessario ripetere manualmente tutte le modifiche apportate a partire dall'ultimo backup del log.  
  
     Per altre informazioni, vedere [Backup della parte finale del log &#40;SQL Server&#41;](tail-log-backups-sql-server.md).  
  
2.  Ripristinare il backup completo del database più recente senza recuperare il database (RESTORE DATABASE *_database* FROM *_backup* WITH NORECOVERY).  
  
3.  Se sono presenti backup differenziali, ripristinare il più recente senza recuperare il database (RESTORE DATABASE *nome_database* FROM *dispositivo_backup_differenziale* WITH NORECOVERY).  
  
     In questo modo viene ridotto il numero di backup del log da ripristinare.  
  
4.  Ripristinare i log in sequenza con NORECOVERY a partire dal primo backup del log delle transazioni creato dopo il backup appena ripristinato.  
  
5.  Recuperare il database (RESTORE DATABASE *nome_database* WITH RECOVERY). In alternativa, è possibile eseguire questo passaggio insieme al ripristino dell'ultimo backup del log.  
  
 Nella figura seguente è illustrata tale sequenza di ripristino. Dopo il verificarsi di un errore (1) viene creato un backup della parte finale del log (2). Successivamente, il database viene ripristinato fino al momento dell'errore. L'operazione comporta il ripristino di un backup del database, di un successivo backup differenziale e di tutti i backup del log eseguiti dopo il backup differenziale, incluso il backup della parte finale del log.  
  
 ![Ripristino di database completo fino al momento in cui si è verificato un errore](../../database-engine/media/bnrr-rmfull1-db-failure-pt.gif "Ripristino di database completo fino al momento in cui si è verificato un errore")  
  
> [!NOTE]  
>  Se si ripristina un backup del database in un'istanza del server diversa, vedere [Copiare database tramite backup e ripristino](../databases/copy-databases-with-backup-and-restore.md).  
  
###  <a name="TsqlSyntax"></a> Sintassi Transact-SQL di base per RESTORE  
 La sintassi di base [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] per la sequenza di ripristino nell'illustrazione precedente è la seguente:  
  
1.  RESTORE DATABASE *database* FROM *full database backup* WITH NORECOVERY;  
  
2.  RESTORE DATABASE *database* FROM *backup_differenziale_completo* WITH NORECOVERY;  
  
3.  RESTORE LOG *database* FROM *backup_log* WITH NORECOVERY;  
  
     Ripetere questo passaggio di ripristino del log per ogni ulteriore backup del log.  
  
4.  RESTORE DATABASE *database* WITH RECOVERY;  
  
###  <a name="ExampleToPoFTsql"></a> Esempio: ripristino fino al momento dell'errore (Transact-SQL)  
 Nell'esempio [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente vengono illustrate le opzioni fondamentali di una sequenza di ripristino del database fino al momento dell'errore. Nell'esempio viene creato un backup della parte finale del log del database. Vengono quindi ripristinati un backup completo del database e un backup del log, quindi il backup della parte finale del log. Il database viene infine recuperato in un passaggio finale separato.  
  
> [!NOTE]  
>  Questo esempio u un backup del database e un backup del log creati nella sezione "Backup del database nel modello di recupero con registrazione completa" di [Backup completo del database &#40;SQL Server&#41;](full-database-backups-sql-server.md). Il database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] è stato impostato per l'utilizzo del modello di recupero con registrazione completa prima del backup del database.  
  
```  
USE master;  
--Create tail-log backup.  
BACKUP LOG AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorksFullRM.bak'    
   WITH NORECOVERY;   
GO  
--Restore the full database backup (from backup set 1).  
RESTORE DATABASE AdventureWorks2012   
  FROM DISK = 'Z:\SQLServerBackups\AdventureWorksFullRM.bak'   
  WITH FILE=1,   
    NORECOVERY;  
  
--Restore the regular log backup (from backup set 2).  
RESTORE LOG AdventureWorks2012   
  FROM DISK = 'Z:\SQLServerBackups\AdventureWorksFullRM.bak'   
  WITH FILE=2,   
    NORECOVERY;  
  
--Restore the tail-log backup (from backup set 3).  
RESTORE LOG AdventureWorks2012   
  FROM DISK = 'Z:\SQLServerBackups\AdventureWorksFullRM.bak'  
  WITH FILE=3,   
    NORECOVERY;  
GO  
--recover the database:  
RESTORE DATABASE AdventureWorks2012 WITH RECOVERY;  
GO  
```  
  
##  <a name="PointWithinBackup"></a> Ripristino di un database fino a un punto all'interno di un backup del log  
 Nel modello di recupero con registrazione completa, un ripristino del database completo può essere generalmente recuperato in un punto nel tempo, in una transazione contrassegnata o in un LSN all'interno di un backup del log. Quando si utilizza il modello di recupero con registrazione minima delle operazioni bulk, se il backup del log contiene modifiche con registrazione minima delle operazioni bulk, il recupero temporizzato non è tuttavia possibile.  
  
### <a name="sample-point-in-time-restore-scenarios"></a>Scenari di ripristino temporizzato di esempio  
 Nell'esempio seguente viene illustrato un sistema di database di importanza critica per le strategie aziendali per il quale è necessaria la creazione di un backup completo del database ogni notte a mezzanotte, di un backup differenziale del database ogni ora da lunedì a sabato e di backup del log delle transazioni ogni 10 minuti per tutto il giorno. Per ripristinare lo stato in cui si trovava il database alle 05.19 di mercoledì, eseguire le operazioni seguenti:  
  
1.  Ripristinare il backup completo del database creato martedì a mezzanotte.  
  
2.  Ripristinare il backup differenziale del database creato alle 5:00 di mercoledì.  
  
3.  Applicare il backup del log delle transazioni creato alle 5:10 di mercoledì.  
  
4.  Applicare il backup del log delle transazioni creato alle 05.20 di mercoledì, specificando che il processo di recupero si applica solo alle transazioni avvenute prima delle 05.19.  
  
 In alternativa, se è necessario ripristinare lo stato del database alle 03.04 di giovedì, ma il backup differenziale del database creato alle 03.00 di giovedì non è disponibile, eseguire le operazioni seguenti:  
  
1.  Ripristinare il backup del database creato mercoledì a mezzanotte.  
  
2.  Ripristinare il backup differenziale del database creato alle 02.00 di giovedì.  
  
3.  Applicare tutti i backup del log delle transazioni creati dalle 02.10 alle 3:00 di giovedì.  
  
4.  Applicare il backup del log delle transazioni creato alle 03.10 di giovedì, arrestando il processo di recupero alle 3:04.  
  
> [!NOTE]  
>  Per un esempio di ripristino temporizzato, vedere [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per ripristinare un backup completo del database**  
  
-   [Ripristinare un Backup del Database &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
 **Per ripristinare un backup differenziale del database**  
  
-   [Ripristinare un backup differenziale del database &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
 **Per ripristinare un backup del log delle transazioni**  
  
-   [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
 **Per ripristinare un backup utilizzando SMO (SQL Server Management Objects)**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  
 **Per ripristinare un database fino a un punto all'interno di un backup del log**  
  
-   [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   [Recupero di database correlati che contengono transazioni contrassegnate](recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [Recupero fino a un numero di sequenza del file di log &#40;SQL Server&#41;](recover-to-a-log-sequence-number-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Applicare backup del log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [Backup completo del database &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [Backup differenziali &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
