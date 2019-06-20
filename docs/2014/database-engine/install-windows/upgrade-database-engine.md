---
title: Aggiornare il motore di database | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84f032e89730aa9828dada1208c6d794db97260b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774975"
---
# <a name="upgrade-database-engine"></a>Aggiornare il motore di database
  In questo argomento vengono fornite le informazioni necessarie per la preparazione e la comprensione del processo di aggiornamento, ovvero:  
  
-   Problemi di aggiornamento noti.  
  
-   Considerazioni e attività preliminari all'aggiornamento.  
  
-   Collegamenti ad argomenti contenenti le procedure per l'aggiornamento del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Collegamenti ad argomenti contenenti le procedure per la migrazione dei database a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Considerazioni sui cluster di failover.  
  
-   Considerazioni e attività successive all'aggiornamento.  
  
## <a name="known-upgrade-issues"></a>Problemi di aggiornamento noti  
 Prima di aggiornare il [!INCLUDE[ssDE](../../includes/ssde-md.md)], esaminare [Compatibilità con le versioni precedenti del Motore di database di SQL Server](../sql-server-database-engine-backward-compatibility.md). Per informazioni sugli scenari di aggiornamento supportati e sui problemi noti, vedere [Aggiornamenti di versione ed edizione supportati](supported-version-and-edition-upgrades.md). Per informazioni sulla compatibilità con le versioni precedenti di altri componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Compatibilità con le versioni precedenti](../../getting-started/backward-compatibility.md).  
  
> [!IMPORTANT]  
>  Prima di eseguire l'aggiornamento da un'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'altra, verificare che le funzionalità attualmente in uso siano supportate nell'edizione a cui si desidera eseguire l'aggiornamento.  
  
> [!NOTE]  
>  Quando esegue l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition, scegliere tra Enterprise Edition: licenze basate su core ed Enterprise Edition. Queste due edizioni differiscono solo per le modalità di gestione delle licenze. Per altre informazioni, vedere [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
## <a name="pre-upgrade-checklist"></a>Elenco di controllo preliminare all'aggiornamento  
 L'aggiornamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una versione precedente è supportato solo dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . È inoltre possibile eseguire la migrazione dei database da versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La migrazione può essere eseguita da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'altra nello stesso computer o da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer diverso. Le opzioni di migrazione includono l'utilizzo della Copia guidata database, delle funzionalità di backup e ripristino, dell'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], nonché dei metodi per importare ed esportare globalmente.  
  
 Prima di aggiornare il [!INCLUDE[ssDE](../../includes/ssde-md.md)], vedere gli argomenti seguenti:  
  
-   Esaminare le informazioni contenute in [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Esaminare le informazioni contenute in [Check Parameters for the System Configuration Checker](check-parameters-for-the-system-configuration-checker.md).  
  
-   Esaminare le informazioni contenute in [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
-   Esaminare [Aggiornamenti di versione ed edizione supportati](supported-version-and-edition-upgrades.md).  
  
-   Esaminare [Utilizzare Preparazione aggiornamento per preparare gli aggiornamenti](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
-   Esaminare [Utilizzare l'utilità Riesecuzione distribuita per preparare gli aggiornamenti](../../sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md).  
  
-   Esaminare [Compatibilità con le versioni precedenti del Motore di database di SQL Server](../sql-server-database-engine-backward-compatibility.md).  
  
-   Esaminare [Migrare piani di query](change-the-database-compatibility-mode-and-use-the-query-store.md).  
  
 Esaminare i problemi seguenti e apportare modifiche prima di aggiornare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   In caso di aggiornamento di istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene integrato nelle relazioni MSX/TSX, aggiornare i server di destinazione prima di quelli master. In caso contrario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non sarà in grado di connettersi alle istanze master di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   In caso di aggiornamento da un'edizione a 64 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'edizione a 64 bit di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è necessario aggiornare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] prima del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Eseguire il backup di tutti i file di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dall'istanza da aggiornare, in modo che sia possibile ripristinarli se necessario.  
  
-   Eseguire i comandi DBCC (Database Console Commands) appropriati sui database da aggiornare per assicurarne la consistenza.  
  
-   Valutare lo spazio su disco necessario per l'aggiornamento dei componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , oltre ai database utente. Per informazioni sullo spazio su disco necessario per i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Requisiti di hardware e software per l’installazione di SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Verificare che i database di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esistenti, ovvero master, model, msdb e tempdb, siano configurati per l'aumento automatico delle dimensioni e dispongano di una quantità di spazio su disco sufficiente.  
  
-   Verificare che nel database master siano disponibili le informazioni di accesso per tutti i server di database. Si tratta di un elemento importante per il ripristino di un database, in quanto le informazioni di accesso al sistema risiedono nel database master.  
  
-   Disabilitare tutte le stored procedure di avvio, in quanto i servizi verranno avviati e arrestati nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in fase di aggiornamento. Le stored procedure elaborate all'avvio potrebbero bloccare il processo di aggiornamento.  
  
-   Verificare che la replica sia corrente, quindi arrestare la replica.  
  
-   Uscire da tutte le applicazioni, inclusi tutti i servizi che intrattengono dipendenze con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'aggiornamento potrebbe avere esito negativo se le applicazioni locali sono connesse all'istanza in fase di aggiornamento.  
  
-   Se si usa il mirroring del database, vedere [Riduzione al minimo del tempo di inattività per i database con mirroring quando si aggiornano le istanze del server](../database-mirroring/upgrading-mirrored-instances.md).  
  
## <a name="upgrading-the-database-engine"></a>Aggiornamento del motore di database  
 È possibile sovrascrivere un'installazione di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive con un aggiornamento della versione. Se durante l'esecuzione del programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene rilevata una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vengono aggiornati tutti i file di programma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti e tutti i dati archiviati nell'istanza precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono mantenuti. Le versioni precedenti della documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , inoltre, resteranno invariate nel computer.  
  
> [!WARNING]  
>  Quando si esegue il programma di installazione di SQL Server 2014, l'istanza di SQL Server viene arrestata e riavviata quando si eseguono i controlli di pre-aggiornamento.  
  
> [!CAUTION]  
>  Quando si aggiorna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'istanza precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene sovrascritta e non sarà più disponibile nel computer. Prima dell'aggiornamento, eseguire il backup dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e degli altri oggetti associati all'istanza precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 È possibile aggiornare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="database-compatibility-level-after-upgrade"></a>Livello di compatibilità del database dopo l'aggiornamento  
 I livelli di compatibilità del `tempdb`, `model`, `msdb` e **risorsa** database siano impostati su 120 dopo l'aggiornamento. Per il database di sistema `master` viene mantenuto il livello di compatibilità precedente l'aggiornamento.  
  
 Se il livello di compatibilità di un database utente era 100 o superiore prima dell'aggiornamento, rimane invariato dopo l'aggiornamento. Se il livello di compatibilità è 90 prima dell'aggiornamento, nel database aggiornato viene impostato su 100, ovvero sul livello di compatibilità supportato più basso in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  I nuovi database utente erediteranno il livello di compatibilità del database `model`.  
  
## <a name="migrating-databases"></a>Migrazione dei database  
 È possibile spostare database utente in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite operazioni di backup e ripristino o scollegare e collegare funzionalità in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Copiare database tramite backup e ripristino](../../relational-databases/databases/copy-databases-with-backup-and-restore.md) o [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
> [!IMPORTANT]  
>  Non è possibile spostare o copiare un database con lo stesso nome nei server di origine e di destinazione. In questo caso, verrà indicato che il database esiste già.  
  
 Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="after-upgrading-the-database-engine"></a>Operazioni successive all'aggiornamento del Motore di database  
 Al termine dell'aggiornamento del [!INCLUDE[ssDE](../../includes/ssde-md.md)], completare le operazioni seguenti:  
  
-   Registrare nuovamente i server. Per altre informazioni sulla registrazione dei server, vedere [Registrazione di server](../../ssms/register-servers/register-servers.md).  
  
-   Ripopolare cataloghi full-text per garantire la coerenza semantica nei risultati delle query.  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] offre nuovi word breaker da usare per la ricerca full-text e semantica. I word breaker vengono utilizzati sia in fase di indicizzazione che di esecuzione delle query. Se non si ricompilano i cataloghi full-text, i risultati di ricerca potrebbero risultare incoerenti. Se si esegue una query full-text che esegue la ricerca di una frase divisa in modo diverso dal word breaker in una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rispetto a quello corrente, è possibile che si verifichi il mancato recupero di una riga o documento contenente la frase. Questo problema si verifica perché le frasi indicizzate sono state divise in base a una logica diversa da quella utilizzata dalla query. Per risolvere il problema, ripopolare (ricompilare) i cataloghi full-text con i nuovi word breaker in modo che il comportamento in fase di indicizzazione e di esecuzione delle query sia lo stesso.  
  
     Per altre informazioni, vedere [sp_fulltext_catalog &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql).  
  
-   Configurare l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per ridurre la superficie di attacco di un sistema, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati e abilitati in modo selettivo i servizi e le funzionalità principali.  
  
-   Convalidare o rimuovere gli hint USE PLAN generati da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e applicati alle query su tabelle e indici partizionati.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modifica la modalità di elaborazione delle query su tabelle e indici partizionati. È possibile che le query su oggetti partizionati che usano l'hint USE PLAN per un piano generato da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] contengano un piano non valido in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Dopo avere eseguito l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è consigliabile eseguire le procedure indicate di seguito.  
  
     **Quando l'hint USE PLAN è specificato direttamente in una query:**  
  
    1.  Rimuovere l'hint USE PLAN dalla query.  
  
    2.  Testare la query.  
  
    3.  Se Query Optimizer non seleziona un piano appropriato, ottimizzare la query, quindi valutare l'opportunità di specificare l'hint USE PLAN con il piano di query desiderato.  
  
     **Quando l'hint USE PLAN è specificato in una Guida di piano:**  
  
    1.  Usare la funzione sys.fn_validate_plan_guide per verificare la validità della guida di piano. In alternativa, è possibile verificare la validità dei piani usando l'evento Plan Guide Unsuccessful in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
    2.  Se la guida di piano non è valida, eliminarla. Se Query Optimizer non seleziona un piano appropriato, ottimizzare la query, quindi valutare l'opportunità di specificare l'hint USE PLAN con il piano di query desiderato.  
  
     Un piano non valido non comporterà l'esito negativo della query quando si specifica l'hint USE PLAN in una guida di piano. Al contrario, la query verrà compilata senza usare l'hint USE PLAN.  
  
 I database contrassegnati come abilitati o disabilitati per la funzionalità full-text prima dell'aggiornamento manterranno lo stato anche in seguito all'aggiornamento. Al termine dell'aggiornamento, i cataloghi full-text verranno ricompilati e popolati automaticamente per tutti i database abilitati per la funzionalità full-text. Si tratta di un'operazione che richiede tempi lunghi e un numero elevato di risorse. Per interrompere temporaneamente l'operazione di indicizzazione full-text, eseguire l'istruzione seguente:  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 1;  
```  
  
 Per riprendere il popolamento dell'indice full-text, eseguire l'istruzione seguente:  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 0;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamenti di versione ed edizione supportati](supported-version-and-edition-upgrades.md)   
 [Uso di più versioni e istanze di SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [Compatibilità con le versioni precedenti](../../getting-started/backward-compatibility.md)   
 [Aggiornare database replicati](upgrade-replicated-databases.md)  
  
  
