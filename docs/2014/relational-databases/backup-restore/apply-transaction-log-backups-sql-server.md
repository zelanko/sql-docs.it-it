---
title: Applicare backup di log delle transazioni (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], log backups
- transaction log backups [SQL Server], applying backups
- online restores [SQL Server], log backups
- transaction log backups [SQL Server], quantity needed for restore sequence
- backups [SQL Server], log backups
ms.assetid: 9b12be51-5469-46f9-8e86-e938e10aa3a1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7532f2a6f2c50f53e5af01c2cec979170b493147
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62922936"
---
# <a name="apply-transaction-log-backups-sql-server"></a>Applicazione dei backup di log delle transazioni (SQL Server)
  Le informazioni contenute in questo argomento sono rilevanti solo per il modello di recupero con registrazione completa o il modello di recupero con registrazione minima delle operazioni bulk.  
  
 In questo argomento viene descritta l'applicazione dei backup del log delle transazioni durante il ripristino di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Contenuto dell'argomento**  
  
-   [Requisiti per ripristinare i backup dei log delle transazioni](#Requirements)  
  
-   [Recupero e log delle transazioni](#RecoveryAndTlogs)  
  
-   [Utilizzo dei backup del log per eseguire il ripristino fino al momento dell'errore](#PITrestore)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="requirements-for-restoring-transaction-log-backups"></a><a name="Requirements"></a>Requisiti per il ripristino dei backup del log delle transazioni  
 Per applicare un backup del log delle transazioni devono essere soddisfatti i requisiti seguenti:  
  
-   **Numero sufficiente di backup del log per una sequenza di ripristino:** per completare una sequenza di ripristino, è necessario che sia disponibile il backup di un numero sufficiente di record del log. I backup del log necessari, incluso il [backup della parte finale del log](tail-log-backups-sql-server.md) se richiesto, devono essere disponibili prima dell'inizio della sequenza di ripristino.  
  
-   **Ordine di ripristino corretto:**  è necessario ripristinare innanzitutto il backup completo o il backup differenziale del database immediatamente precedente. Tutti i log delle transazioni creati dopo tale backup completo o differenziale devono essere ripristinati in ordine cronologico. Se uno dei backup del log delle transazioni appartenente a questa catena di log non è presente o risulta danneggiato, è possibile ripristinare soltanto i log delle transazioni antecedenti al log delle transazioni non più disponibile.  
  
-   **Database non ancora recuperato:**  non è possibile recuperare il database finché non viene applicato il log delle transazioni finale. Se si esegue il recupero del database dopo aver ripristinato uno dei backup del log delle transazioni intermedi, ovvero antecedenti all'estremità della catena di log, non sarà possibile eseguire il ripristino del database successivamente a tale punto senza riavviare l'intera sequenza di ripristino a partire dal backup completo del database.  
  
    > [!TIP]  
    >  È consigliabile ripristinare tutti i backup del log (RESTORE LOG *nome_database* WITH NORECOVERY). Dopo aver ripristinato l'ultimo backup del log, recuperare il database in un'operazione separata (RESTORE DATABASE *nome_database* WITH RECOVERY).  
  
##  <a name="recovery-and-transaction-logs"></a><a name="RecoveryAndTlogs"></a>Log delle transazioni e ripristino  
 Quando si recupera il database al termine dell'operazione di ripristino, viene eseguito il rollback di tutte le transazioni incomplete. Questa procedura è nota come *fase di rollback*. L'esecuzione del rollback è necessaria per ripristinare l'integrità del database. Dopo il rollback il database passa nello stato online, dopodiché non è possibile applicare alcun altro backup del log delle transazioni al database.  
  
 Si supponga, ad esempio, che una serie di backup del log delle transazioni includa una transazione con esecuzione prolungata. L'inizio della transazione viene registrato nel primo backup del log delle transazioni, mentre la fine della transazione viene registrata nel secondo backup del log delle transazioni. Il primo backup del log delle transazioni non include un record di un'operazione di commit o rollback. Se viene eseguita un'operazione di recupero quando è applicato il primo backup del log delle transazioni, la transazione con esecuzione prolungata verrà considerata incompleta e verrà eseguito il rollback delle modifiche dei dati registrate nel primo backup del log delle transazioni. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è possibile applicare il secondo backup del log delle transazioni dopo questo punto.  
  
> [!NOTE]  
>  In alcuni casi, durante il ripristino del log è possibile aggiungere un file in modo esplicito.  
  
##  <a name="using-log-backups-to-restore-to-the-point-of-failure"></a><a name="PITrestore"></a>Uso dei backup del log per eseguire il ripristino fino al punto di errore  
 Si osservi a titolo di esempio la sequenza di eventi seguente:  
  
|Tempo|Event|  
|----------|-----------|  
|8.00|Backup del database per creare un backup completo del database.|  
|12.00|Backup del log delle transazioni|  
|16.00|Backup del log delle transazioni|  
|18.00|Backup del database per creare un backup completo del database.|  
|20.00|Backup del log delle transazioni|  
|21.45|Si verifica un errore.|  
  
> [!NOTE]  
>  Per la spiegazione di questa sequenza esemplificativa di backup, vedere [Backup di log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md).  
  
 Per ripristinare lo stato del database corrispondente alle ore 21.45 (punto di errore), è possibile utilizzare una delle procedure alternative seguenti:  
  
 **Alternativa 1: ripristino del database dal backup completo più recente**  
  
1.  Creare un backup della parte finale del log delle transazioni attivo a partire dal momento dell'errore.  
  
2.  Non ripristinare del backup completo del database delle 18.00. Ripristinare invece il backup completo del database più recente effettuato alle 18.00, quindi applicare il backup del log effettuato alle 20.00 e il backup della parte finale del log.  
  
 **Alternativa 2: ripristino del database da un backup completo precedente**  
  
> [!NOTE]  
>  Questa procedura alternativa è utile nel caso non sia possibile utilizzare il backup completo del database effettuato alle 18.00 del backup completo del database delle 18.00. Questa procedura richiede più tempo di quello necessario per il ripristino del backup completo del database delle 18.00.  
  
1.  Creare un backup della parte finale del log delle transazioni attivo a partire dal momento dell'errore.  
  
2.  Ripristinare il backup completo del database delle 8.00, quindi ripristinare in sequenza tutti e quattro i backup del log delle transazioni. Ciò determina il rollforward di tutte le transazioni completate fino alle 21.45.  
  
     Questa procedura alternativa mostra quale sia il livello di sicurezza supplementare garantito dal mantenimento di una catena di backup del log delle transazioni eseguiti in una serie di backup completi del database.  
  
> [!NOTE]  
>  In alcuni casi è anche possibile utilizzare i log delle transazioni per ripristinare un database fino a un punto nel tempo specifico. Per altre informazioni, vedere [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 **Per applicare un backup del log delle transazioni**  
  
-   [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
 **Per eseguire il ripristino fino al punto di recupero**  
  
-   [Ripristinare un database fino al punto di errore nel modello di recupero con registrazione completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
-   [Recupero di database correlati che contengono transazioni contrassegnate](recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [Recupero fino a un numero di sequenza del file di log &#40;SQL Server&#41;](recover-to-a-log-sequence-number-sql-server.md)  
  
 **Per recuperare un database dopo il ripristino dei backup utilizzando WITH NORECOVERY**  
  
-   [Recuperare un database senza ripristino dei dati &#40;Transact-SQL&#41;](recover-a-database-without-restoring-data-transact-sql.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)  
  
  
