---
title: Risolvere i problemi relativi a un log delle transazioni completo (Errore di SQL Server 9002) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], full
- troubleshooting [SQL Server], full transaction log
- 9002 (Database Engine error)
- transaction logs [SQL Server], truncation
- backing up transaction logs [SQL Server], full logs
- transaction logs [SQL Server], full log
- full transaction logs [SQL Server]
ms.assetid: 0f23aa84-475d-40df-bed3-c923f8c1b520
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2c0dc1566693ad8d8c86d7efe47403248788b076
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144713"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>Risolvere i problemi relativi a un log delle transazioni completo (Errore di SQL Server 9002)
  In questo argomento vengono illustrate le risposte possibili a un log delle transazioni pieno e viene spiegato come evitare tale situazione in futuro. Quando il log delle transazioni è pieno, in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] viene generato un errore 9002. Il log può riempirsi quando il database è online o in stato di recupero. Se il log si riempie quando il database è online, quest'ultimo rimane online anche se potrà soltanto essere letto, non aggiornato. Se il log si riempie durante il recupero, in [!INCLUDE[ssDE](../../includes/ssde-md.md)] il database viene contrassegnato come RESOURCE PENDING. In entrambi i casi, è richiesto che l'utente intervenga per liberare spazio nel log.  
  
## <a name="responding-to-a-full-transaction-log"></a>Risposta a un log delle transazioni pieno  
 La risposta appropriata a un log delle transazioni pieno dipende in parte dalla condizione o dalle condizioni che hanno causato il riempimento del log. Per individuare la condizione che impedisce il troncamento del log in un caso specifico, usare le colonne **log_reuse_wait** e **log_reuse_wait_desc** della vista del catalogo **sys.database**. Per altre informazioni, vedere [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql). Per le descrizioni dei fattori che possono ritardare il troncamento del log, vedere [Log delle transazioni &#40;SQL Server&#41;](the-transaction-log-sql-server.md).  
  
> [!IMPORTANT]  
>  Se il database di ripristino durante l'errore 9002 si è verificato, dopo aver risolto il problema, ripristinare il database utilizzando ALTER DATABASE *database_name* SET ONLINE.  
  
 Per gestire un log delle transazioni pieno sono disponibili le soluzioni alternative seguenti:  
  
-   Esecuzione del backup del log  
  
-   Aumento dello spazio libero su disco in modo che le dimensioni del log possano aumentare automaticamente  
  
-   Spostamento del file di log in un'unità disco con spazio sufficiente  
  
-   Aumento delle dimensioni di un file di log  
  
-   Aggiunta di un file di log in un altro disco  
  
-   Completamento o termine di una transazione con esecuzione prolungata.  
  
 Queste soluzioni alternative verranno illustrate nelle sezioni successive. Scegliere la risposta più appropriata a seconda della situazione.  
  
### <a name="backing-up-the-log"></a>Backup del log  
 Nel modello di recupero con registrazione completa o nel modello di recupero con registrazione minima delle operazioni bulk, se non è stato eseguito il backup del log delle transazioni di recente, è possibile che sia il backup a impedire il troncamento del log. Se il backup del log non è mai stato eseguito, è necessario creare due backup del log per consentire a [!INCLUDE[ssDE](../../includes/ssde-md.md)] di troncare il log in corrispondenza del punto dell'ultimo backup. Il troncamento del log consente di rendere disponibile spazio per nuovi record del log. Per evitare che il log si riempia di nuovo, eseguire backup del log frequenti.  
  
 **Per creare un backup del log delle transazioni**  
  
> [!IMPORTANT]  
>  Se il database è danneggiato, vedere [Backup della parte finale del log &#40;SQL Server&#41;](../backup-restore/tail-log-backups-sql-server.md).  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>Aumento dello spazio disponibile su disco  
 Potrebbe essere possibile liberare spazio sull'unità disco contenente il file del log delle transazioni per il database, eliminando o spostando altri file. L'aumento dello spazio disponibile su disco consente al sistema di recupero di ingrandire automaticamente il file di log.  
  
### <a name="moving-the-log-file-to-a-different-disk"></a>Spostamento del file di log in un altro disco  
 Se non é possibile liberare spazio su disco sufficiente nell'unità che attualmente contiene il file di log, prendere in considerazione lo spostamento del file in un'altra unità con spazio adeguato.  
  
> [!IMPORTANT]  
>  È consigliabile non memorizzare mai file di log in file system compressi.  
  
 **Per spostare un file di log**  
  
-   [Spostare file del database](../databases/move-database-files.md)  
  
### <a name="increasing-the-size-of-a-log-file"></a>Aumento delle dimensioni di un file di log  
 Se nel disco del log è disponibile spazio, è possibile aumentare le dimensioni del file di log. La dimensione massima per i file di log è due terabyte per file di log.  
  
 **Per aumentare le dimensioni del file**  
  
 Se l'aumento automatico dimensioni è disabilitato, il database è online ed è disponibile spazio sufficiente sul disco, eseguire una delle operazioni seguenti:  
  
-   Aumentare manualmente le dimensioni del file per produrre un incremento di crescita singolo.  
  
-   Abilitare l'aumento automatico dimensioni utilizzando l'istruzione ALTER DATABASE per impostare un incremento di crescita diverso da zero per l'opzione FILEGROWTH.  
  
> [!NOTE]  
>  In entrambi i casi, se sono state raggiunte le dimensioni massime consentite correnti, aumentare il valore MAXSIZE.  
  
### <a name="adding-a-log-file-on-a-different-disk"></a>Aggiunta di un file di log in un altro disco  
 Aggiungere un nuovo file di log al database in un altro disco contenente spazio sufficiente utilizzando ALTER DATABASE <database_name> ADD LOG FILE.  
  
 **Per aggiungere un file di log**  
  
-   [Aggiungere file di dati o file di log a un database](../databases/add-data-or-log-files-to-a-database.md)  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Gestione delle dimensioni del file di log delle transazioni](manage-the-size-of-the-transaction-log-file.md)   
 [Backup di log delle transazioni &#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql)  
  
  
