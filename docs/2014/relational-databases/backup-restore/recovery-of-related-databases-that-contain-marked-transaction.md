---
title: Recupero di database correlati che contengono transazioni contrassegnate | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], marks
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- transactions [SQL Server], recovering to a mark
- database recovery [SQL Server]
- marked transactions [SQL Server], restoring
- database restores [SQL Server], point in time
ms.assetid: 77a0d9c0-978a-4891-8b0d-a4256c81c3f8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 209bc81c63998cea299d2c377175955ee99470c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62875714"
---
# <a name="recovery-of-related--databases-that-contain-marked-transaction"></a>Recupero di database correlati che contengono transazioni contrassegnate
  Le informazioni contenute in questo argomento sono rilevanti solo per i database che includono transazioni contrassegnate e utilizzano il modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk.  
  
 Per informazioni sui requisiti per il ripristino fino a un punto di recupero specifico, vedere [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'inserimento di contrassegni denominati nel log delle transazioni per il recupero fino a un punto specifico. I contrassegni del log sono specifici della transazione e vengono inseriti solo se viene eseguito il commit della transazione associata. In questo modo, i contrassegni risultano legati a serie di operazioni specifiche ed è possibile eseguire il recupero includendo o escludendo le serie di operazioni desiderate.  
  
 Prima di inserire contrassegni denominati nel log delle transazioni, tenere presente quanto segue:  
  
-   I contrassegni di transazione occupano spazio nei log e pertanto è consigliabile utilizzarli esclusivamente per transazioni importanti ai fini della strategia di recupero dei database.  
  
-   Dopo il commit di una transazione contrassegnata, viene inserita una riga nella tabella [logmarkhistory](/sql/relational-databases/system-tables/logmarkhistory-transact-sql) del database **msdb**.  
  
-   Se una transazione contrassegnata si estende su più database dello stesso server di database o di server diversi, i contrassegni devono essere registrati nei log di tutti i database interessati. Per altre informazioni, vedere [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
> [!NOTE]  
>  Per informazioni sul contrassegno delle transazioni, vedere [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="transact-sql-syntax-for-inserting-named-marks-into-a-transaction-log"></a>Sintassi Transact-SQL per l'inserimento di contrassegni denominati in un log delle transazioni  
 Per inserire contrassegni nei log delle transazioni, usare l'istruzione [BEGIN TRANSACTION](/sql/t-sql/language-elements/begin-transaction-transact-sql) e la clausola WITH MARK [*description*]. Al contrassegno viene assegnato lo stesso nome della transazione. L'argomento *description* facoltativo è una descrizione testuale del contrassegno e non corrisponde al nome del contrassegno. Il nome sia della transazione sia del contrassegno creato nella seguente istruzione `BEGIN TRANSACTION` è ad esempio `Tx1`:  
  
```wmimof  
BEGIN TRANSACTION Tx1 WITH MARK 'not the mark name, just a description'    
```  
  
 Nel log delle transazioni vengono registrati il nome del contrassegno (il nome della transazione), la descrizione, il database, l'utente, le informazioni di tipo `datetime` e il numero di sequenza del file di log (LSN). Per l'identificazione univoca del contrassegno, il nome viene associato alle informazioni `datetime`.  
  
 Per informazioni sull'inserimento di un contrassegno in una transazione che si estende su più database, vedere [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="transact-sql-syntax-for-recovering-to-a-mark"></a>Sintassi Transact-SQL per il recupero fino a un contrassegno  
 Quando si specifica una transazione contrassegnata come destinazione usando un'istruzione[RESTORE LOG](/sql/t-sql/statements/restore-statements-transact-sql), è possibile usare una delle clausole seguenti per arrestare l'operazione in corrispondenza del contrassegno o immediatamente prima di esso:  
  
-   Usare la clausola WITH STOPATMARK = **»*`<mark_name>`*'** clausola per specificare che la transazione contrassegnata è il punto di ripristino.  
  
     STOPATMARK esegue il rollforward fino al contrassegno, includendovi la transazione contrassegnata.  
  
-   Usare la clausola WITH STOPBEFOREMARK = **»*`<mark_name>`*'** clausola per specificare che il record del log viene immediatamente precedente al contrassegno il punto di ripristino.  
  
     STOPBEFOREMARK esegue il rollforward fino al contrassegno, escludendo la transazione contrassegnata.  
  
 Entrambe le opzioni STOPATMARK e STOPBEFOREMARK supportano una clausola AFTER *datetime* facoltativa. Quando si usa *datetime* , non è necessario che i nomi dei contrassegni siano univoci.  
  
 Se AFTER *datetime* viene omesso, il rollforward viene arrestato in corrispondenza del primo contrassegno con il nome specificato. Se AFTER *datetime* viene specificato, il rollforward viene arrestato in corrispondenza del primo contrassegno con il nome specificato, nella data e ora indicate in *datetime*o in un momento successivo.  
  
> [!NOTE]  
>  Come per tutte le operazioni di ripristino temporizzato, il recupero fino a un contrassegno è disattivato quando nel database sono in corso operazioni con registrazione minima delle operazioni bulk.  
  
 **Per ripristinare una transazione contrassegnata**  
  
 [Ripristino di un database fino a una transazione contrassegnata &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
### <a name="preparing-the-log-backups"></a>Preparazione dei backup del log  
 In questo esempio, una strategia di backup appropriata per i database correlati potrebbe essere la seguente:  
  
1.  Utilizzare il modello di recupero con registrazione completa per entrambi i database.  
  
2.  Creare un backup completo di ogni database.  
  
     È possibile eseguire il backup dei database in sequenza o simultaneamente.  
  
3.  Prima di eseguire il backup del log delle transazioni, contrassegnare una transazione che viene eseguita in tutti i database. Per informazioni sulla creazione di transazioni contrassegnate, vedere [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
4.  Eseguire il backup del log delle transazioni in ogni database.  
  
### <a name="recovering-the-database-to-a-marked-transaction"></a>Recupero del database fino a una transazione contrassegnata  
 **Per ripristinare il backup**  
  
1.  Se possibile, creare [backup della parte finale del log](tail-log-backups-sql-server.md) per i database non danneggiati.  
  
2.  Ripristinare il backup completo più recente di ogni database.  
  
3.  Individuare la transazione contrassegnata più recente disponibile in tutti i backup del log delle transazioni. Questa informazione è archiviata nella tabella **logmarkhistory** del database **msdb** in ogni server.  
  
4.  Individuare i backup del log di tutti i database correlati che contengono questo contrassegno.  
  
5.  Ripristinare ogni backup del log fino alla transazione contrassegnata.  
  
6.  Recuperare ogni database.  
  
## <a name="see-also"></a>Vedere anche  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-transaction-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Applicare backup del log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Pianificare ed eseguire sequenze di ripristino &#40;modello di recupero con registrazione completa&#41;](plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
