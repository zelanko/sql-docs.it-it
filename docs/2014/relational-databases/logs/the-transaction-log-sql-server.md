---
title: Log delle transazioni (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b4a175ad850ccbb0711a0997c3658cf01497686
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289409"
---
# <a name="the-transaction-log-sql-server"></a>Log delle transazioni (SQL Server)
  Ogni database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include un log delle transazioni in cui vengono registrate tutte le transazioni e le modifiche apportate dalle transazioni stesse al database. Per evitarne il riempimento, il log delle transazioni deve essere troncato regolarmente. Tuttavia, alcuni fattori possono posticipare il troncamento del log, pertanto è importante monitorare le dimensioni del log. Ad alcune operazioni può essere applicata la registrazione minima per ridurre l'impatto sulle dimensioni del log delle transazioni.  
  
 Il log delle transazioni è un componente fondamentale del database e, in caso di errore di sistema, può essere necessario per ripristinare la coerenza del database. Il log delle transazioni non deve mai essere eliminato o spostato, a meno che non vi sia la piena consapevolezza delle conseguenze di tale operazione.  
  
> [!NOTE]  
>  I checkpoint rappresentano i punti ottimali noti da cui avviare l'applicazione dei log delle transazioni durante il ripristino del database. Per altre informazioni, vedere [Checkpoint di database &#40;SQL Server&#41;](database-checkpoints-sql-server.md).  
  
 **Contenuto dell'argomento**  
  
-   [Vantaggi: operazioni supportate dal log delle transazioni](#Benefits)  
  
-   [Troncamento del log delle transazioni](#Truncation)  
  
-   [Fattori che possono ritardare il troncamento del log](#FactorsThatDelayTruncation)  
  
-   [Operazioni che possono essere registrate con registrazione minima](#MinimallyLogged)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="benefits-operations-supported-by-the-transaction-log"></a><a name="Benefits"></a>Vantaggi: operazioni supportate dal log delle transazioni  
 Il log delle transazioni supporta le operazioni seguenti:  
  
-   Recupero di singole transazioni.  
  
-   Recupero di tutte le transazioni incomplete all'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Rollforward di una pagina, file, filegroup o database ripristinato fino al punto in cui si è verificato l'errore.  
  
-   Supporto della replica transazionale.  
  
-   Supporto delle soluzioni di ripristino di emergenza e disponibilità elevata: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], mirroring del database e log shipping.  
  
##  <a name="transaction-log-truncation"></a><a name="Truncation"></a>Troncamento del log delle transazioni  
 Il troncamento del log libera spazio nel file di log per consentirne il riutilizzo da parte del log delle transazioni. Il troncamento del log è essenziale per evitare il riempimento del log. Il troncamento del log elimina i file di log virtuali inattivi dal log delle transazioni logico di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , liberando spazio nel log logico per il riutilizzo da parte del log delle transazioni fisico. Se un log delle transazioni non viene mai troncato, è possibile che le sue dimensioni aumentino fino a occupare tutto lo spazio su disco allocato ai file di log fisici.  
  
 Per evitare questo problema, il troncamento si verifica automaticamente dopo gli eventi riportati di seguito, a meno che tale operazione non sia stata posticipata per qualche motivo:  
  
-   Nel modello di recupero con registrazione minima, dopo un checkpoint.  
  
-   Nel modello di recupero con registrazione completa o nel modello di recupero con registrazione minima delle operazioni bulk, se si è verificato un checkpoint dal backup precedente, il troncamento si verifica dopo un backup del log (a meno che non si tratti di un backup del log di sola copia).  
  
 Per ulteriori informazioni, vedere [Fattori che possono posticipare il troncamento del log](#FactorsThatDelayTruncation)più avanti in questo argomento.  
  
> [!NOTE]  
>  Il troncamento del log non riduce le dimensioni del file di log fisico. Per ridurre le dimensioni fisiche di un file di log fisico, è necessario compattare il file di log. Per informazioni sulla compattazione del file di log fisico, vedere [Gestire le dimensioni del file di log delle transazioni](manage-the-size-of-the-transaction-log-file.md).  
  
##  <a name="factors-that-can-delay-log-truncation"></a><a name="FactorsThatDelayTruncation"></a>Fattori che possono ritardare il troncamento del log  
 Quando i record del log rimangono attivi per molto tempo il troncamento viene posticipato e il log delle transazioni potrebbe riempirsi.  
  
> [!IMPORTANT]  
>  Per informazioni su come agire quando il log delle transazioni è completo, vedere [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md).  
  
 Il troncamento del log può essere posticipato da diversi fattori. Per individuare l'eventuale condizione che impedisce il troncamento del log, eseguire una query sulle colonne **log_reuse_wait** e **log_reuse_wait_desc** della vista del catalogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) . Nella tabella seguente vengono descritti i valori di queste colonne.  
  
|Valore di log_reuse_wait|Valore di log_reuse_wait_desc|Descrizione|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|Attualmente vi sono uno o più file di log virtuali riutilizzabili.|  
|1|CHECKPOINT|Non si è verificato alcun checkpoint dall'ultimo troncamento del log oppure l'inizio del log non è stato ancora spostato oltre un file di log virtuale. (Tutti i modelli di recupero)<br /><br /> Si tratta di una motivazione comune per il posticipo del troncamento del log. Per altre informazioni, vedere [Checkpoint di database &#40;SQL Server&#41;](database-checkpoints-sql-server.md).|  
|2|LOG_BACKUP|È necessario eseguire un backup del log prima del troncamento del log delle transazioni. (Solo modelli di recupero con registrazione completa e con registrazione minima delle operazioni bulk)<br /><br /> Quando il backup del log successivo viene completato, parte dello spazio del log potrebbe divenire riutilizzabile.|  
|3|ACTIVE_BACKUP_OR_RESTORE|È in esecuzione un processo di backup o ripristino dei dati (tutti i modelli di recupero).<br /><br /> Se il troncamento del log è impedito da un backup dei dati, l'annullamento del backup può risolvere il problema immediato.|  
|4|ACTIVE_TRANSACTION|Una transazione è attiva (tutti i modelli di recupero).<br /><br /> Una transazione con esecuzione prolungata potrebbe esistere all'inizio del backup del log. In questo caso, per liberare lo spazio potrebbe essere necessario un altro backup del log. Si noti che le transazioni con esecuzione prolungata impediscono il troncamento del log in tutti i modelli di recupero, incluso il modello di recupero con registrazione minima, in cui il log delle transazioni viene in genere troncato in ogni checkpoint automatico.<br /><br /> Viene posticipata una transazione. Una *transazione posticipata* è una transazione attiva ed efficace il cui ritorno allo stato precedente è bloccato a causa di alcune risorse non disponibili. Per informazioni sulle cause delle transazioni posticipate e su come modificarne lo stato, vedere [Transazioni posticipate &#40;SQL Server&#41;](../backup-restore/deferred-transactions-sql-server.md). <br /><br />Anche le transazioni con esecuzione prolungata potrebbero riempire il log delle transazioni di tempdb. Tempdb viene usato in modo implicito dalle transazioni utente per gli oggetti interni, ad esempio tabelle di lavoro per l'ordinamento, file di lavoro per l'hashing, tabelle di lavoro di cursori e controllo delle versioni delle righe. Anche se la transazione utente include solo la lettura di dati (SELECT Querys), è possibile creare oggetti interni e utilizzarli nelle transazioni utente. In questo modo, il log delle transazioni di tempdb potrebbe riempirsi.|  
|5|DATABASE_MIRRORING|Il mirroring del database è sospeso o in modalità a prestazioni elevate, il database mirror è notevolmente in ritardo rispetto al database principale. (Solo modello di recupero con registrazione completa)<br /><br /> Per altre informazioni, vedere [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|6|REPLICA|Durante le repliche transazionali, le transazioni significative per le pubblicazioni non sono ancora state recapitate al database di distribuzione. (Solo modello di recupero con registrazione completa)<br /><br /> Per informazioni sulla replica transazionale, vedere [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md).|  
|7|DATABASE_SNAPSHOT_CREATION|Viene creato uno snapshot del database. (Tutti i modelli di recupero)<br /><br /> Si tratta di una motivazione comune, e generalmente di breve durata, per il posticipo del troncamento del log.|  
|8|LOG_SCAN|È in corso un'analisi del log. (Tutti i modelli di recupero)<br /><br /> Si tratta di una motivazione comune, e generalmente di breve durata, per il posticipo del troncamento del log.|  
|9|AVAILABILITY_REPLICA|Una replica secondaria di un gruppo di disponibilità applica i record del log delle transazioni del database a un database secondario corrispondente. (Modello di recupero con registrazione completa)<br /><br /> Per ulteriori informazioni, vedere [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|10|-|Solo per uso interno|  
|11|-|Solo per uso interno|  
|12|-|Solo per uso interno|  
|13|OLDEST_PAGE|Se un database è configurato per l'utilizzo dei checkpoint indiretti, la pagina meno recente del database potrebbe essere meno recente dell'LSN checkpoint. In questo caso, la pagina meno recente può causare il posticipo del troncamento del log. (Tutti i modelli di recupero)<br /><br /> Per informazioni sui checkpoint indiretti, vedere [Database Checkpoints &#40;SQL Server&#41;](database-checkpoints-sql-server.md).|  
|14|OTHER_TRANSIENT|Questo valore non è attualmente utilizzato.|  
|16|XTP_CHECKPOINT|Quando un database ha un filegroup ottimizzato per la memoria, il log delle transazioni potrebbe non essere troncato finché non viene attivato il checkpoint automatico [!INCLUDE[hek_2](../../includes/hek-2-md.md)], che si verifica a ogni 512 MB di aumento della dimensioni del log.<br /><br /> Nota: per troncare il log delle transazioni prima della dimensione di 512 MB, attivare manualmente il comando checkpoint nel database in questione.|  
  
##  <a name="operations-that-can-be-minimally-logged"></a><a name="MinimallyLogged"></a>Operazioni che possono essere registrate con registrazione minima  
 La*registrazione minima* implica la registrazione nel log delle transazioni delle sole informazioni necessarie per il recupero della transazione stesse senza il supporto del recupero temporizzato. In questo argomento vengono identificate le operazioni con registrazione minima nel modello di recupero con registrazione minima delle operazioni bulk nonché nel modello di recupero con registrazione minima, ad eccezione dei momenti in cui è in esecuzione un backup.  
  
> [!NOTE]  
>  La registrazione minima non è supportata dalle tabelle ottimizzate per la memoria.  
  
> [!NOTE]  
>  In base al modello di recupero con registrazione completa tutte le operazioni bulk vengono registrate per intero. È tuttavia possibile ridurre al minimo la registrazione per un set di operazioni bulk passando temporaneamente il database al modello di recupero con registrazione minima delle operazioni bulk per le operazioni bulk. La registrazione minima è più efficiente della registrazione completa e riduce la possibilità che un'operazione bulk su larga scala esaurisca lo spazio disponibile per il log delle transazioni durante una transazione bulk. Se tuttavia il database viene danneggiato o perso durante la registrazione minima, non è possibile recuperarlo fino al punto di errore.  
  
 Per le operazioni seguenti, con registrazione completa nel modello di recupero con registrazione completa, è prevista la registrazione minima nel modello di recupero con registrazione minima e in quello con registrazione minima delle operazioni bulk:  
  
-   Operazioni di importazione in blocco ([bcp](../../tools/bcp-utility.md), [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql)e [INSERT... SELECT](/sql/t-sql/statements/insert-transact-sql)). Per ulteriori informazioni sui casi in cui viene eseguita la registrazione minima di un'importazione bulk in una tabella, vedere [Prerequisites for Minimal Logging in Bulk Import](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
    > [!NOTE]  
    >  Quando la replica transazionale è abilitata, le operazioni BULK INSERT vengono registrate completamente persino nel modello di recupero con registrazione minima delle operazioni bulk.  
  
-   Operazioni SELECT [into](/sql/t-sql/queries/select-into-clause-transact-sql) .  
  
    > [!NOTE]  
    >  Quando la replica transazionale è abilitata, le operazioni SELECT INTO vengono registrate completamente persino nel modello di recupero con registrazione minima delle operazioni bulk.  
  
-   Aggiornamenti parziali a tipi di dati di valori di grandi dimensioni eseguiti mediante la clausola .WRITE nell'istruzione [UPDATE](/sql/t-sql/queries/update-transact-sql) quando si inseriscono o si aggiungono nuovi dati. Si noti che la registrazione minima non viene utilizzata per l'aggiornamento di valori esistenti. Per altre informazioni sui tipi di dati per valori di grandi dimensioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
-   [Istruzioni WRITETEXT](/sql/t-sql/queries/writetext-transact-sql) e [UPDATETEXT](/sql/t-sql/queries/updatetext-transact-sql) quando si inseriscono o accodano nuovi dati `text`nelle `ntext`colonne del `image` tipo di dati, e. Si noti che la registrazione minima non viene utilizzata per l'aggiornamento di valori esistenti.  
  
    > [!NOTE]  
    >  Poiché le istruzioni WRITETEXT e UPDATETEXT sono deprecate, è consigliabile evitare di utilizzarle nelle nuove applicazioni.  
  
-   Se il database viene impostato sul modello di recupero con registrazione minima o con registrazione delle operazioni bulk, verrà eseguita la registrazione minima di alcune operazioni DDL sugli indici indipendentemente dal fatto che l'operazione venga eseguita online o offline. Le operazioni sugli indici con registrazione minima sono le seguenti:  
  
    -   Operazioni[CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) (incluse le viste indicizzate).  
  
    -   Operazioni[ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql) REBUILD o DBCC DBREINDEX.  
  
        > [!NOTE]  
        >  Poiché l'istruzione DBCC DBREINDEX è deprecata, è consigliabile evitare di utilizzarla nelle nuove applicazioni.  
  
    -   Ricompilazione del nuovo heap DROP INDEX (se pertinente).  
  
        > [!NOTE]  
        >   Durante un'operazione [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql) per la deallocazione delle pagine di un indice viene eseguita sempre la registrazione completa.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 `Managing the transaction log`  
  
-   [Gestione delle dimensioni del file di log delle transazioni](manage-the-size-of-the-transaction-log-file.md)  
  
-   [Risolvere i problemi relativi a un log delle transazioni completo &#40;Errore di SQL Server 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
 **Backup del log delle transazioni (modello di recupero con registrazione completa)**  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **Ripristino del log delle transazioni (modello di recupero con registrazione completa)**  
  
-  [Ripristinare un backup del log delle transazioni](../backup-restore/restore-a-transaction-log-backup-sql-server.md)   
  
## <a name="see-also"></a>Vedere anche  
 [Controllare la durabilità delle transazioni](control-transaction-durability.md)   
 [Prerequisiti per la registrazione minima nell'importazione bulk](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [Backup e ripristino di database di SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Checkpoint di database &#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [Visualizzare o modificare le proprietà di un database](../databases/view-or-change-the-properties-of-a-database.md)   
 [Modelli di recupero &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)  
  
  
