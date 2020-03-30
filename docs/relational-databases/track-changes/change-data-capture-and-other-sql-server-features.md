---
title: Change Data Capture e altre funzionalità di SQL Server
ms.custom: seo-dt-2019
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
author: rothja
ms.author: jroth
ms.openlocfilehash: e29ad6de65172b08bb3f35aa89820ca817a9e1d3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "74095291"
---
# <a name="change-data-capture-and-other-sql-server-features"></a>Change Data Capture e altre funzionalità di SQL Server
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  In questo argomento viene descritta l'interazione tra Change Data Capture e le funzionalità seguenti:  
  
-   [Change tracking](#ChangeTracking)  
  
-   [Mirroring del database](#DatabaseMirroring)  
  
-   [Replica transazionale](#TransReplication)  
  
-   [Ripristino o collegamento di un database abilitato per Change Data Capture](#RestoreOrAttach)

-   [Database indipendenti](#Contained)
  
##  <a name="change-tracking"></a><a name="ChangeTracking"></a> Rilevamento delle modifiche  
 Le funzionalità Change Data Capture e [rilevamento modifiche](../../relational-databases/track-changes/about-change-tracking-sql-server.md) possono essere abilitate nello stesso database. Non richiedono considerazioni particolari. Per altre informazioni, vedere [Usare il rilevamento delle modifiche &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md).  
  
##  <a name="database-mirroring"></a><a name="DatabaseMirroring"></a> Mirroring del database  
 È possibile eseguire il mirroring di un database per il quale la funzionalità Change Data Capture è abilitata. Per assicurarsi che i processi di acquisizione e pulizia vengano eseguiti automaticamente dopo un failover, effettuare i passaggi seguenti:  
  
1.  Verificare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia in esecuzione nella nuova istanza del server principale.  
  
2.  Creare i processi di acquisizione e di pulizia nel nuovo database principale (il database mirror precedente). Per creare i processi, usare la stored procedure [sp_cdc_add_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md) .  
  
 Per visualizzare la configurazione corrente di un processo di pulizia o di acquisizione, usare la stored procedure [sys.sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md) nella nuova istanza del server principale. Per un database specificato, il processo di acquisizione è denominato cdc.*database\_name*\_capture e il processo di pulizia è denominato cdc.*database\_name*\_cleanup, dove *database_name* è il nome del database.  
  
 Per modificare la configurazione di un processo, usare la stored procedure [sys.sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md) .  
  
 Per informazioni sul mirroring del database, vedere [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
##  <a name="transactional-replication"></a><a name="TransReplication"></a> Transactional Replication  
 Le funzionalità Change Data Capture e replica transazionale possono coesistere nello stesso database, tuttavia il popolamento delle tabelle delle modifiche viene gestito in modo diverso se entrambe le funzionalità sono abilitate. Change Data Capture e la replica transazionale usano sempre la stessa stored procedure, [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md), per leggere le modifiche dal log delle transazioni. Quando Change Data Capture è la sola funzionalità abilitata, un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent chiama **sp_replcmds**. Quando entrambe le funzionalità sono abilitate nello stesso database, l'agente di lettura log chiama **sp_replcmds**. Questo agente popola sia le tabelle delle modifiche sia le tabelle del database di distribuzione. Per altre informazioni, vedere [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md).  
  
 Si consideri uno scenario in cui la funzionalità Change Data Capture è abilitata nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e due tabelle sono abilitate per l'acquisizione. Per popolare le tabelle delle modifiche, il processo di acquisizione chiama **sp_replcmds**. Il database viene abilitato per la replica transazionale e viene creata una pubblicazione. L'agente di lettura log viene creato per il database e il processo di acquisizione viene eliminato. L'agente di lettura log continua ad analizzare il log dall'ultimo numero di sequenza di cui è stato eseguito il commit nella tabella delle modifiche. In questo modo, viene assicurata la coerenza dei dati nelle tabelle delle modifiche. Se la replica transazionale è disabilitata in questo database, l'agente di lettura log viene rimosso e il processo di acquisizione viene ricreato.  
  
> [!NOTE]  
>  Quando l'agente di lettura log viene utilizzato sia per Change Data Capture sia per la replica transazionale, le modifiche replicate vengono innanzitutto scritte nel database di distribuzione. Le modifiche acquisite vengono quindi scritte nelle tabelle delle modifiche. Il commit di entrambe le operazioni viene eseguito contemporaneamente. Se si verifica della latenza durante la scrittura nel database di distribuzione, si verificherà latenza prima che le modifiche vengano visualizzate nelle tabelle delle modifiche.  
  
 L'opzione **proc exec** della replica transazionale non è disponibile quando l'acquisizione dati delle modifiche è abilitata.  
  
##  <a name="restoring-or-attaching-a-database-enabled-for-change-data-capture"></a><a name="RestoreOrAttach"></a> Ripristino o collegamento di un database abilitato per Change Data Capture  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene utilizzata la logica seguente per determinare se la funzionalità Change Data Capture rimane abilitata anche dopo il ripristino o il collegamento di un database:  
  
-   Se un database viene ripristinato nello stesso server con lo stesso nome di database, la funzionalità Change Data Capture rimane abilitata.  
  
-   Se un database viene ripristinato in un altro server, per impostazione predefinita la funzionalità Change Data Capture viene disabilitata e tutti i metadati correlati vengono eliminati.  
  
     Per mantenere abilitata la funzionalità Change Data Capture, usare l'opzione **KEEP_CDC** durante il ripristino del database. Per ulteriori informazioni su questa opzione, vedere [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md).  
  
-   Se un database viene scollegato e collegato allo stesso o a un altro server, la funzionalità Change Data Capture rimane abilitata.  
  
-   Se un database viene collegato o ripristinato con l'opzione **KEEP_CDC** in qualsiasi edizione diversa da Standard o Enterprise, l'operazione viene bloccata perché Change Data Capture richiede le edizioni Standard o Enterprise di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Viene visualizzato il messaggio di errore 934:  
  
     `SQL Server cannot load database '%.*ls' because Change Data Capture is enabled. The currently installed edition of SQL Server does not support Change Data Capture. Either restore database without KEEP_CDC option, or upgrade the instance to one that supports Change Data Capture.`  
  
 È possibile usare [sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) per rimuovere Change Data Capture da un database collegato o ripristinato.  
  
##  <a name="contained-databases"></a><a name="Contained"></a> Database indipendenti  
 La funzionalità Change Data Capture non è supportata in [database indipendenti](../../relational-databases/databases/contained-databases.md).
  
## <a name="change-data-capture-and-always-on"></a>Change Data Capture e Always On  
 Quando si usa Always On, è consigliabile eseguire un'enumerazione delle modifiche nella replica secondaria per ridurre il carico su disco nella replica primaria.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare e monitorare Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
