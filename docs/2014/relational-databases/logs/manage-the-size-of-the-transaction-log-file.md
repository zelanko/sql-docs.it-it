---
title: Gestire le dimensioni del file di log delle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 219ba0605d60bab0b13675f7f9f7ff01cace5755
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049736"
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>Gestione delle dimensioni del file di log delle transazioni
  In alcuni casi, può essere utile per ridurre o espandere fisicamente il file di log fisico del log delle transazioni di un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In questo argomento sono contenute informazioni sul monitoraggio delle dimensioni di un log delle transazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , sulla relativa compattazione, sull'aumento delle dimensioni di un file di log delle transazioni, sull'ottimizzazione del tasso di aumento del log delle transazioni di **tempdb** e sul controllo dell'aumento delle dimensioni di un file di log delle transazioni.  
  
  
##  <a name="monitor-log-space-use"></a><a name="MonitorSpaceUse"></a>Monitorare l'utilizzo dello spazio del log  
 È possibile monitorare l'utilizzo dello spazio del log mediante DBCC SQLPERF (LOGSPACE). Questo comando restituisce informazioni sulla quantità di spazio del log attualmente utilizzata e indica quando il log delle transazioni deve essere troncato. Per altre informazioni, vedere [DBCC SQLPERF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql). Per informazioni sulle dimensioni correnti di un file di log, sulle relative dimensioni massime e sull'opzione di aumento automatico delle dimensioni per il file, è anche possibile usare le colonne **size**, **max_size** e **growth** per il file di log in **sys.database_files**. Per altre informazioni, vedere [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql).  
  
> [!IMPORTANT]  
>  È consigliabile evitare l'overload del disco per il log.  
  
  
##  <a name="shrink-the-size-of-the-log-file"></a><a name="ShrinkSize"></a>Compattare le dimensioni del file di log  
 Per ridurre la dimensione fisica di un file di log fisico, è necessario ridurre il file di log. Ciò può risultare utile se si è a conoscenza del fatto che un file di log delle transazioni contiene spazio inutilizzato che non sarà più necessario. La compattazione può verificarsi solo mentre il database è online e quando almeno un file di log virtuale è disponibile. In alcuni casi, la compattazione del log potrebbe non essere possibile finché il log non viene troncato.  
  
> [!NOTE]  
>  Fattori come una transazione con esecuzione prolungata, che mantiene i file di log virtuali attivi per un lungo periodo di tempo, possono limitare in tutto o in parte la compattazione del log. Per informazioni sui fattori che possono ritardare il troncamento del log, vedere [Log delle transazioni &#40;SQL Server&#41;](the-transaction-log-sql-server.md).  
  
 Il processo di compattazione di un file di log comporta la rimozione di uno o più file di log virtuali che non contengono alcuna parte del log logico (ossia *file di log virtuali inattivi*). Quando si compatta un file di log delle transazioni, viene rimosso dalla fine del file di log un numero di file di log virtuali inattivi sufficiente a ridurre il log approssimativamente alle dimensioni di destinazione.  
  
 **Per compattare un file di log (senza compattare i file di database)**  
  
-   [DBCC SHRINKFILE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql)  
  
-   [Compattare un file](../databases/shrink-a-file.md)  
  
 **Per monitorare gli eventi di compattazione dei file di log**  
  
-   [Log File compattazione automatica classe di evento](../event-classes/log-file-auto-shrink-event-class.md).  
  
 `To monitor log space`  
  
-   [DBCC SQLPERF &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)  
  
-   [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) (Vedere le colonne **size**, **max_size** e **growth** per il file o i file di log).  
  
> [!NOTE]  
>  La compattazione dei file di log e di database può essere impostata in modo da essere eseguita automaticamente. È consigliabile tuttavia evitare di eseguire la compattazione automatica impostando la proprietà del database `autoshrink` su FALSE per impostazione predefinita. Se `autoshrink` viene impostato su TRUE, la compattazione automatica riduce le dimensioni di un file solo quando più del 25 percento dello spazio del file risulta inutilizzato. Il file viene compattato fino a quando la percentuale di spazio inutilizzato nel file non risulta pari al 25 percento oppure fino a quando il file non raggiunge le dimensioni originali, a seconda di quale tra questi due sia il valore maggiore. Per informazioni sulla modifica dell'impostazione della `autoshrink` proprietà, vedere [visualizzare o modificare le proprietà di un database](../databases/view-or-change-the-properties-of-a-database.md). utilizzare la proprietà **compattazione automatica** nella pagina **opzioni** o [Opzioni ALTER database set &#40;&#41;Transact-SQL ](/sql/t-sql/statements/alter-database-transact-sql-set-options)-utilizzare l'opzione AUTO_SHRINK.  
  
  
##  <a name="add-or-enlarge-a-log-file"></a><a name="AddOrEnlarge"></a>Aggiungere o ingrandire un file di log  
 In alternativa, è possibile guadagnare spazio aumentando le dimensioni del file di log esistente, se lo spazio è sufficiente, oppure aggiungendo un file di log al database, in genere in un disco diverso.  
  
-   Per aggiungere un file di log al database, utilizzare la clausola ADD LOG FILE dell'istruzione ALTER DATABASE. L'aggiunta di un file di log consente l'aumento delle dimensioni del log.  
  
-   Per aumentare le dimensioni del file di log, utilizzare la clausola MODIFY FILE dell'istruzione ALTER DATABASE, specificando la sintassi SIZE e MAXSIZE. Per altre informazioni, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
  
##  <a name="optimize-the-size-of-the-tempdb-transaction-log"></a><a name="tempdbOptimize"></a>Ottimizzare le dimensioni del log delle transazioni di tempdb  
 Il riavvio di un'istanza del server riporta il log delle transazioni del database **tempdb** alle dimensioni originali, antecedenti all'aumento automatico delle dimensioni. Questo può comportare una riduzione delle prestazioni del log delle transazioni di **tempdb** . Per evitare tale overhead, è possibile incrementare le dimensioni del log delle transazioni di **tempdb** dopo l'avvio o il riavvio dell'istanza del server. Per altre informazioni, vedere [tempdb Database](../databases/tempdb-database.md).  
  
  
##  <a name="control-the-growth-of-a-transaction-log-file"></a><a name="ControlGrowth"></a>Controllare la crescita di un file di log delle transazioni  
 È possibile usare l'istruzione [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql) per gestire la crescita di un file di log delle transazioni. Tenere presente quanto segue:  
  
-   Per modificare le dimensioni del file corrente in unità KB, MB, GB e TB, utilizzare l'opzione SIZE.  
  
-   Per modificare l'incremento di crescita, utilizzare l'opzione FILEGROWTH. Il valore 0 indica che l'aumento automatico delle dimensioni è disattivato e non è consentita l'allocazione di spazio aggiuntivo. Anche un piccolo aumento automatico delle dimensioni di un file di log può comportare una riduzione delle prestazioni. È consigliabile specificare un incremento di crescita per un file di log sufficientemente grande da consentire di evitare l'espansione frequente. L'incremento di crescita predefinito pari al 10% è solitamente appropriato.  
  
     Per informazioni sulla modifica della proprietà di aumento delle dimensioni dei file in un file di log, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
-   Per controllare le dimensioni massime di un file di log in unità KB, MB, GB e TB o per impostare la crescita su UNLIMITED, utilizzare l'opzione MAXSIZE.  
  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Risolvere i problemi relativi a un log delle transazioni completo &#40;Errore di SQL Server 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  
