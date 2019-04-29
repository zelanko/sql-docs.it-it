---
title: Eseguire il recupero fino a un numero di sequenza del file di log (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log sequence numbers [SQL Server]
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- LSNs
- database recovery [SQL Server]
- database restores [SQL Server], point in time
ms.assetid: f7b3de5b-198d-448d-8c71-1cdd9239676c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 835057cdef6b7d2a336b64480515a5046cfde070
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62875764"
---
# <a name="recover-to-a-log-sequence-number-sql-server"></a>Recupero fino a un numero di sequenza del file di log (SQL Server)
  Le informazioni contenute in questo argomento sono rilevanti solo per i database che utilizzano il modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk.  
  
 È possibile utilizzare un numero di sequenza del file di log (LSN) per definire il punto di recupero per un'operazione di ripristino. Si tratta tuttavia di una funzionalità specializzata progettata per i fornitori di strumenti e viene utilizzata solo in rari casi.  
  
##  <a name="LSNs"></a> Panoramica dei numeri di sequenza del file di log  
 Gli LSN sono utilizzati internamente durante una sequenza RESTORE per tenere traccia del momento specifico rispetto al quale i dati sono stati ripristinati. Quando un backup viene ripristinato, i dati vengono ripristinati sull'LSN corrispondente al momento specifico di esecuzione del backup. Backup dei log e differenziali spostano il database ripristinato a un momento successivo, corrispondente a un LSN maggiore.  
  
 Ogni record presente nel log delle transazioni è identificato in modo univoco da un numero di sequenza dei file di log (LSN). Gli LSN sono ordinati in modo tale che se LSN è maggiore di LSN1, la modifica descritta dal record di log cui fa riferimento LSN2 si verifica dopo la modifica descritta dall'LSN del record di log.  
  
 L'LSN di un record di log in corrispondenza del quale si è verificato un evento significativo può essere utile per creare sequenze di ripristino corrette. Essendo ordinati, gli LSN possono essere confrontati in termini di uguaglianza e disuguaglianza, ovvero **\<**, **>**, **=**, **\<=**, **>=**. Questi confronti sono utili nella creazione di sequenze di ripristino.  
  
> [!NOTE]  
>  Gli LSN sono valori di tipo di dati `numeric`(25,0). Gli operatori matematici, ad esempio addizione o sottrazione, non sono significativi e non devono essere utilizzati con gli LSN.  
  

  
## <a name="viewing-lsns-used-by-backup-and-restore"></a>Visualizzazione degli LSN utilizzati tramite backup e ripristino  
 L'LSN di un record di log in corrispondenza del quale si è verificato un determinato evento di backup e di ripristino è visibile utilizzando una o più delle istruzioni seguenti:  
  
-   [backupset](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
-   [backupfile](/sql/relational-databases/system-tables/backupfile-transact-sql)  
  
-   [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql); [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
-   [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)  
  
-   [RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)  
  
> [!NOTE]  
>  Gli LSN sono inoltre visualizzati nel testo di alcuni messaggi.  
  
## <a name="transact-sql-syntax-for-restoring-to-an-lsn"></a>Sintassi Transact-SQL per il ripristino fino a un numero di sequenza del file di log (LSN)  
 Un'istruzione [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) consente di arrestare il processo esattamente in corrispondenza dell'LSN o immediatamente prima, come illustrato di seguito:  
  
-   Usare la clausola WITH STOPATMARK **='** lsn:_<numero_lsn>_**'**, dove lsn:*\<Numerolsn>* è una stringa che specifica che il punto di recupero corrisponde al record di log contenente l'LSN specificato.  
  
     STOPATMARK esegue il rollforward al numero di sequenza del file di log (LSN) includendo anche tale record del log.  
  
-   Usare la clausola WITH STOPBEFOREMARK **='** lsn:_<numero_lsn>_**'**, dove lsn:*\<Numerolsn>* è una stringa che specifica che il punto di recupero corrisponde al record di log immediatamente precedente a quello contenente l'LSN specificato.  
  
     Tramite STOPBEFOREMARK viene eseguito il rollforward fino all'LSN escludendo tale record di log.  
  
 In genere, viene selezionata una transazione specifica da includere o escludere. Sebbene non sia necessario, il record di log specificato è in pratica un record di commit delle transazioni.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente si presuppone che il database `AdventureWorks` sia stato modificato in modo da utilizzare il modello di recupero con registrazione completa.  
  
```  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Ripristinare un Backup del Database &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
-   [Ripristinare un database al punto di errore nel modello di recupero con registrazione completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Ripristino di un database fino a una transazione contrassegnata &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Ripristinare un database di SQL Server fino a un punto specifico &#40;Modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Applicare backup log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
