---
title: Ripristini a fasi (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- partial updates [SQL Server]
- staged restores [SQL Server]
- piecemeal restores [SQL Server]
- restoring [SQL Server], piecemeal restore scenario
ms.assetid: 208f55e0-0762-4cfb-85c4-d36a76ea0f5b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 481146623145c2abc6e3e9c8ed5b971f614979e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62640819"
---
# <a name="piecemeal-restores-sql-server"></a>Ripristini a fasi (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Le informazioni contenute in questo argomento sono rilevanti solo per i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition (ripristino in linea) o Standard Edition (ripristino non in linea) che contengono più file o filegroup e, nel modello semplice, solo per i filegroup di sola lettura.  
  
 Per informazioni sui ripristini a fasi e tabelle ottimizzate per la memoria, vedere [Backup e ripristino a fasi di database con tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md).  
  
 Il*ripristino a fasi* consente di ripristinare e recuperare a fasi i database in cui sono inclusi più filegroup. e comprende una serie di sequenze di ripristino, a partire dal filegroup primario e, in alcuni casi, da uno o più filegroup secondari. Permette inoltre di gestire i controlli per assicurarsi che il database sia sempre coerente. Dopo il completamento della sequenza di ripristino, i file recuperati, se validi e coerenti con il database, possono essere portati online direttamente.  
  
 Il ripristino a fasi può essere utilizzato con tutti i modelli di recupero, tuttavia la massima flessibilità si ottiene con i modelli di recupero con registrazione completa o con registrazione minima delle operazioni bulk, piuttosto che con il modello di recupero con registrazione minima.  
  
 Ogni ripristino a fasi inizia con una sequenza di ripristino iniziale detta *sequenza di ripristino parziale*. Come minimo, la sequenza di ripristino parziale ripristina e recupera il filegroup primario e, nel modello di recupero con registrazione minima, tutti i filegroup di lettura/scrittura. Durante la sequenza di ripristino a fasi, è necessario che l'intero database venga portato offline. Quindi, il database è online e i filegroup ripristinati sono disponibili. Tuttavia, tutti i filegroup non ripristinati rimangono offline e non sono accessibili. I filegroup offline possono comunque essere ripristinati e portati online successivamente tramite un ripristino di file.  
  
 Indipendentemente dal modello di recupero utilizzato dal database, la sequenza di ripristino parziale inizia con un'istruzione RESTORE DATABASE che consente di ripristinare un backup completo e di specificare l'opzione PARTIAL. L'opzione PARTIAL avvia sempre un nuovo ripristino a fasi. Pertanto, è necessario specificare PARTIAL solo una volta nell'istruzione iniziale della sequenza di ripristino parziale. Quando la sequenza di ripristino parziale termina e il database viene portato online, lo stato dei file rimanenti diventa "recupero in sospeso" in quanto il loro recupero è stato posticipato.  
  
 Successivamente, un ripristino a fasi include in genere una o più sequenze di ripristino, dette *sequenze di ripristino dei filegroup*. È possibile attendere il periodo di tempo desiderato prima di eseguire una sequenza di ripristino dei filegroup specifica. Ogni sequenza di ripristino dei filegroup ripristina e recupera uno o più filegroup offline rispetto a un punto coerente con il database. Momento di esecuzione e numero delle sequenze di ripristino dei filegroup dipendono dall'obiettivo del recupero, dal numero di filegroup offline che si desidera ripristinare e dal numero di tali filegroup ripristinati per ogni sequenza di ripristino dei filegroup.  
  
 I requisiti esatti per l'esecuzione di un ripristino a fasi dipendono dal modello di recupero del database. Per ulteriori informazioni, vedere "Ripristino a fasi nel modello di recupero con registrazione minima" e "Ripristino a fasi nel modello di recupero con registrazione completa" di seguito in questo argomento.  
  
## <a name="piecemeal-restore-scenarios"></a>Scenari di ripristino a fasi  
 Tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano il ripristino a fasi offline. In Enterprise Edition, un ripristino a fasi può essere online oppure offline. Le implicazioni del ripristino a fasi offline e online sono le seguenti:  
  
-   Scenari di ripristino a fasi offline  
  
     In un ripristino a fasi offline, il database è online dopo la sequenza di ripristino parziale. I filegroup non ancora ripristinati rimangono offline, ma possono essere ripristinati secondo le esigenze dopo aver portato il database offline.  
  
-   Scenari di ripristino a fasi online  
  
     In un ripristino a fasi online, dopo la sequenza di ripristino parziale, il database è online e il filegroup primario è disponibile insieme ad eventuali filegroup secondari recuperati. I filegroup non ancora ripristinati rimangono offline, ma è possibile ripristinarli in base alle necessità mentre il database rimane online.  
  
     Il ripristino a fasi online può coinvolgere le transazioni posticipate. Quando è stato ripristinato un solo subset di filegroup, le transazioni nel database che dipendono dai filegroup online possono diventare posticipate. Si tratta di una situazione comune, in quanto l'intero database deve essere coerente. Per altre informazioni, vedere [Transazioni posticipate &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).  
  
-   [!INCLUDE[hek_1](../../includes/hek-1-md.md)] scenario di ripristino a fasi  
  
     Per informazioni sui ripristini a fasi di database OLTP in memoria, vedere [Backup e ripristino a fasi di database con tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md).  
  
## <a name="restrictions"></a>Restrictions  
 Se una sequenza di ripristino parziale esclude qualsiasi filegroup [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) , il ripristino temporizzato non è supportato. È possibile forzare la continuazione della sequenza di ripristino. Tuttavia i filegroup FILESTREAM omessi dall'istruzione RESTORE non potranno mai più essere ripristinati. Per forzare un ripristino temporizzato, specificare l'opzione CONTINUE_AFTER_ERROR insieme all'opzione STOPAT, STOPATMARK o STOPBEFOREMARK che è necessario specificare anche nelle istruzioni RESTORE LOG successive. Se si specifica CONTINUE_AFTER_ERROR, la sequenza di ripristino parziale ha esito positivo e il filegroup FILESTREAM non può più essere recuperato.  
  
## <a name="piecemeal-restore-under-the-simple-recovery-model"></a>Ripristino a fasi nel modello di recupero con registrazione minima  
 Nel modello di recupero con registrazione minima la sequenza del ripristino a fasi deve iniziare con un backup completo o parziale del database. Quindi, se il backup ripristinato è una base differenziale, ripristinare il backup differenziale più recente.  
  
 Durante la prima sequenza di ripristino parziale, se si ripristina solo un subset di filegroup di lettura/scrittura, qualsiasi filegroup non ripristinato diventa non attivo quando si recupera il database parzialmente ripristinato. L'omissione di un filegroup di lettura/scrittura dalla sequenza di ripristino parziale è adeguata solo nei casi seguenti:  
  
-   Si desidera che i filegroup non ripristinati diventino inattivi.  
  
-   La sequenza di ripristino arriverà a un punto di recupero in corrispondenza del quale ogni filegroup non ripristinato è diventato di sola lettura, è stato eliminato o è inattivo (durante un ripristino precedente nella sequenza di ripristino parziale).  
  
-   Il backup completo è stato eseguito mentre il database utilizzava il modello di recupero con registrazione minima, ma il punto di recupero si trova in corrispondenza di un punto nel tempo in cui il database utilizza il modello di recupero con registrazione completa. Per ulteriori informazioni, vedere "Esecuzione di un ripristino a fasi di un database il cui modello di recupero è passato da semplice a completo" di seguito in questo argomento.  
  
### <a name="requirements-for-piecemeal-restore-under-the-simple-recovery-model"></a>Requisiti per il ripristino a fasi nel modello di recupero con registrazione minima  
 Nel modello di recupero con registrazione minima, la fase iniziale ripristina e recupera il filegroup primario e tutti i filegroup secondari di lettura/scrittura. Dopo il completamento della fase iniziale, i file recuperati, se validi e consistenti con il database, possono essere portati online direttamente.  
  
 Quindi, è possibile ripristinare i filegroup di sola lettura in una o più fasi aggiuntive.  
  
 Il ripristino a fasi è disponibile per un filegroup secondario di sola lettura solo se sono vere le condizioni seguenti:  
  
-   Il filegroup era di sola lettura quando ne è stato eseguito il backup.  
  
-   Il filegroup è rimasto di sola lettura (mantenendolo coerente dal punto di vista logico con il filegroup primario).  
  
 Per eseguire un ripristino a fasi, è necessario seguire le linee guida seguenti:  
  
-   Un set completo di backup per il ripristino a fasi di un database con modello di recupero con registrazione minima deve contenere gli elementi seguenti:  
  
    -   Un backup del database parziale o completo che contiene il filegroup primario e tutti i filegroup che erano di lettura/scrittura al momento del backup.  
  
    -   Un backup di ogni file di sola lettura.  
  
-   Perché il backup di un file di sola lettura sia coerente con il filegroup primario, è necessario che il filegroup secondario sia stato di sola lettura dal momento dell'esecuzione del backup fino al completamento del backup che contiene il filegroup primario. È possibile utilizzare backup differenziali dei file, a condizione che siano stati creati dopo che il filegroup è diventato di sola lettura.  
  
### <a name="piecemeal-restore-stages-simple-recovery-model"></a>Fasi del ripristino a fasi (modello di recupero con registrazione minima  
 Lo scenario del ripristino a fasi include le fasi seguenti:  
  
-   Fase iniziale (ripristino e recupero del filegroup primario e di tutti i filegroup di lettura/scrittura)  
  
     Nella fase iniziale viene eseguito un ripristino parziale, ovvero la sequenza di ripristino parziale ripristina il filegroup primario, tutti i filegroup secondari di lettura/scrittura e (facoltativamente) alcuni dei filegroup di sola lettura. Durante la fase iniziale, è necessario che l'intero database venga portato offline. Dopo la fase iniziale, il database è online e i filegroup ripristinati sono disponibili. Tuttavia, eventuali filegroup di sola lettura non ancora ripristinati rimangono offline.  
  
     La prima istruzione RESTORE nella fase iniziale deve eseguire le operazioni seguenti:  
  
    -   Utilizzare un backup parziale o completo del database che contiene il filegroup primario e tutti i filegroup che erano di lettura/scrittura al momento del backup. In genere una sequenza di ripristino parziale viene avviata tramite il ripristino di un backup parziale.  
  
    -   Specificare l'opzione PARTIAL che indica l'inizio di un ripristino a fasi.  
  
    > [!NOTE]  
    >  L'opzione PARTIAL consente di eseguire i controlli di sicurezza tramite cui viene assicurato che il database risultante è adatto per essere utilizzato come database di produzione.  
  
    -   Specificare l'opzione READ_WRITE_FILEGROUPS nel caso di un backup completo del database.  
  
-   Mentre il database è online, è possibile utilizzare uno o più ripristini dei file online per ripristinare e recuperare i file di sola lettura offline che erano di sola lettura al momento del backup. Il momento in cui eseguire i ripristini dei file online dipende da quando si desidera che i dati siano online.  
  
     La necessità di ripristinare i dati in un file dipende dagli elementi seguenti:  
  
    -   I file di sola lettura validi consistenti con il database possono essere portati online direttamente recuperandoli senza ripristinare alcun dato.  
  
    -   I file danneggiati o inconsistenti con il database devono essere ripristinati prima che siano recuperati.  
  
### <a name="examples"></a>Esempi  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="piecemeal-restore-under-the-full-recovery-model"></a>Ripristino a fasi nel modello di recupero con registrazione completa  
 Nel modello di recupero con registrazione completa o nel modello di recupero con registrazione minima delle operazioni bulk, il ripristino a fasi è disponibile per qualsiasi database che contiene più filegroup, ed è possibile ripristinare un database rispetto a qualsiasi punto nel tempo. Le sequenze di ripristino di un ripristino a fasi funzionano nel modo seguente:  
  
-   sequenza di ripristino parziale  
  
     La sequenza di ripristino parziale ripristina il filegroup primario e, facoltativamente, alcuni dei filegroup secondari.  
  
     La prima istruzione RESTORE DATABASE deve eseguire le operazioni seguenti:  
  
    -   Specificare l'opzione PARTIAL. Questo indica l'avvio di un ripristino a fasi.  
  
    -   Utilizzare un backup completo del database che contiene il filegroup primario. In genere una sequenza di ripristino parziale viene avviata tramite il ripristino di un backup parziale.  
  
    -   Per eseguire il ripristino rispetto a un punto nel tempo specifico, è necessario impostare il tempo nella sequenza di ripristino parziale. Ogni passaggio successivo della sequenza di ripristino deve specificare lo stesso punto nel tempo.  
  
-   Le sequenze di ripristino dei filegroup portano online filegroup aggiuntivi rispetto a un punto coerente con il database.  
  
     In Enterprise Edition, qualsiasi filegroup secondario offline può essere ripristinato e recuperato mentre il database rimane online. Se un file di sola lettura specifico è coerente con il database e non è danneggiato, non è necessario ripristinarlo. Per altre informazioni, vedere [Recuperare un database senza il ripristino dei dati &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
### <a name="applying-log-backups"></a>Applicazione dei backup del log  
 Se un filegroup di sola lettura è stato tale fin da prima della creazione del backup del file, l'applicazione dei backup del log al filegroup non è necessaria e non viene eseguita dal ripristino del file. Se il filegroup è di lettura/scrittura, per aggiornare il filegroup rispetto al file di log attuale è necessario che venga applicata una catena ininterrotta di backup del log all'ultimo ripristino completo o differenziale.  
  
### <a name="examples"></a>Esempi  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
## <a name="performing-a-piecemeal-restore-of-a-database-whose-recovery-model-has-been-switched-from-simple-to-full"></a>Esecuzione di un ripristino a fasi di un database il cui modello di recupero è passato da semplice a completo  
 È possibile eseguire un ripristino a fasi di un database che è passato dal modello di recupero con registrazione minima al modello di recupero con registrazione completa a partire dal momento del backup completo o parziale del database. Ad esempio, si prenda in considerazione un database per cui vengono eseguiti i passaggi seguenti:  
  
1.  Creare un backup parziale (backup_1) di un database con modello di recupero con registrazione minima.  
  
2.  Dopo un determinato intervallo di tempo, passare al modello di recupero con registrazione completa.  
  
3.  Creare un backup differenziale.  
  
4.  Avviare l'esecuzione dei backup del log.  
  
 La sequenza seguente è pertanto valida:  
  
1.  Un ripristino parziale che omette alcuni filegroup secondari.  
  
2.  Un ripristino differenziale, seguito da eventuali altri ripristini necessari.  
  
3.  Successivamente, un ripristino del file di un filegroup secondario di lettura/scrittura WITH NORECOVERY dal backup parziale backup_1  
  
4.  Il backup differenziale seguito da tutti i backup ripristinati durante la sequenza del ripristino a fasi originale per ripristinare i dati fino al punto di recupero originale.  
  
## <a name="see-also"></a>Vedere anche  
 [Applicare backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Ripristinare un database di SQL Server fino a un punto specifico &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Pianificare ed eseguire sequenze di ripristino &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
