---
title: Change Data Capture e altre funzionalità di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 87fcd7656ff1e86522e4ea398fc49d91acde9a34
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747750"
---
# <a name="change-data-capture-and-other-sql-server-features"></a>Change Data Capture e altre funzionalità di SQL Server
  In questo argomento viene descritta l'interazione tra Change Data Capture e le funzionalità seguenti:  
  
-   [Rilevamento modifiche](#ChangeTracking)  
  
-   [Mirroring del database](#DatabaseMirroring)  
  
-   [Replica transazionale](#TransReplication)  
  
-   [Ripristino o collegamento di un database abilitato per Change Data Capture](#RestoreOrAttach)  
  
##  <a name="ChangeTracking"></a> Change Tracking  
 Le funzionalità Change Data Capture e [rilevamento modifiche](about-change-tracking-sql-server.md) possono essere abilitate nello stesso database. Non richiedono considerazioni particolari. Per altre informazioni, vedere [Usare il rilevamento delle modifiche &#40;SQL Server&#41;](work-with-change-tracking-sql-server.md).  
  
##  <a name="DatabaseMirroring"></a> Mirroring del database  
 È possibile eseguire il mirroring di un database per il quale la funzionalità Change Data Capture è abilitata. Per assicurarsi che i processi di acquisizione e pulizia vengano eseguiti automaticamente dopo un failover, effettuare i passaggi seguenti:  
  
1.  Verificare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia in esecuzione nella nuova istanza del server principale.  
  
2.  Creare i processi di acquisizione e di pulizia nel nuovo database principale (il database mirror precedente). Per creare i processi, usare la stored procedure [sp_cdc_add_job](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql) .  
  
 Per visualizzare la configurazione corrente di un processo di pulizia o di acquisizione, usare la stored procedure [sys.sp_cdc_help_jobs](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql) nella nuova istanza del server principale. Per un database specificato, il processo di acquisizione viene denominato cdc.*database_name*_capture e il processo di pulizia viene denominato cdc.*database_name*_cleanup, dove *database_name* è il nome del database.  
  
 Per modificare la configurazione di un processo, usare la stored procedure [sys.sp_cdc_change_job](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql).  
  
 Per informazioni sul mirroring del database, vedere [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
##  <a name="TransReplication"></a> Transactional Replication  
 Le funzionalità Change Data Capture e replica transazionale possono coesistere nello stesso database, tuttavia il popolamento delle tabelle delle modifiche viene gestito in modo diverso se entrambe le funzionalità sono abilitate. Change Data Capture e la replica transazionale usano sempre la stessa stored procedure, [sp_replcmds](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql), per leggere le modifiche dal log delle transazioni. Quando Change Data Capture è la sola funzionalità abilitata, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent chiama `sp_replcmds`. Quando entrambe le funzionalità sono abilitate nello stesso database, l'agente di lettura Log chiama `sp_replcmds`. Questo agente popola sia le tabelle delle modifiche sia le tabelle del database di distribuzione. Per altre informazioni, vedere [Replication Log Reader Agent](../replication/agents/replication-log-reader-agent.md).  
  
 Si consideri uno scenario in cui la funzionalità Change Data Capture è abilitata nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e due tabelle sono abilitate per l'acquisizione. Per popolare le tabelle delle modifiche, il processo di acquisizione chiama `sp_replcmds`. Il database viene abilitato per la replica transazionale e viene creata una pubblicazione. L'agente di lettura log viene creato per il database e il processo di acquisizione viene eliminato. L'agente di lettura log continua ad analizzare il log dall'ultimo numero di sequenza di cui è stato eseguito il commit nella tabella delle modifiche. In questo modo, viene assicurata la coerenza dei dati nelle tabelle delle modifiche. Se la replica transazionale è disabilitata in questo database, l'agente di lettura log viene rimosso e il processo di acquisizione viene ricreato.  
  
> [!NOTE]  
>  Quando l'agente di lettura log viene utilizzato sia per Change Data Capture sia per la replica transazionale, le modifiche replicate vengono innanzitutto scritte nel database di distribuzione. Le modifiche acquisite vengono quindi scritte nelle tabelle delle modifiche. Il commit di entrambe le operazioni viene eseguito contemporaneamente. Se si verifica della latenza durante la scrittura nel database di distribuzione, si verificherà latenza prima che le modifiche vengano visualizzate nelle tabelle delle modifiche.  
  
 L'opzione **proc exec** della replica transazionale non è disponibile quando l'acquisizione dati delle modifiche è abilitata.  
  
##  <a name="RestoreOrAttach"></a> Ripristino o collegamento di un database abilitato per Change Data Capture  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene utilizzata la logica seguente per determinare se la funzionalità Change Data Capture rimane abilitata anche dopo il ripristino o il collegamento di un database:  
  
-   Se un database viene ripristinato nello stesso server con lo stesso nome di database, la funzionalità Change Data Capture rimane abilitata.  
  
-   Se un database viene ripristinato in un altro server, per impostazione predefinita la funzionalità Change Data Capture viene disabilitata e tutti i metadati correlati vengono eliminati.  
  
     Per mantenere abilitata la funzionalità Change Data Capture, utilizzare l'opzione `KEEP_CDC` durante il ripristino del database. Per ulteriori informazioni su questa opzione, vedere [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql).  
  
-   Se un database viene scollegato e collegato allo stesso o a un altro server, la funzionalità Change Data Capture rimane abilitata.  
  
-   Se un database viene collegato o ripristinato con il `KEEP_CDC` opzione in qualsiasi edizione diversa da Enterprise, l'operazione viene bloccata perché change data capture richiede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise. Viene visualizzato il messaggio di errore 934:  
  
     `SQL Server cannot load database '%.*ls' because change data capture is enabled. The currently installed edition of SQL Server does not support change data capture. Either disable change data capture in the database by using a supported edition of SQL Server, or upgrade the instance to one that supports change data capture.`  
  
 È possibile utilizzare [sys.sp_cdc_disable_db](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql) per rimuovere Change Data Capture da un database collegato o ripristinato.  
  
## <a name="change-data-capture-and-alwayson"></a>Change Data Capture e AlwaysOn  
 Quando si utilizza AlwaysOn, è consigliabile eseguire un'enumerazione delle modifiche nella replica secondaria per ridurre il carico su disco nella replica primaria.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare e monitorare Change Data Capture &#40;SQL Server&#41;](../track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
