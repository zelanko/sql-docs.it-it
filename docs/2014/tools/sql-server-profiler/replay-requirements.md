---
title: Requisiti per la riproduzione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], replaying traces
- traces [SQL Server], replaying
- replaying traces
- TSQL_Replay template [SQL Server]
ms.assetid: 0e01dfc7-84b9-47f6-8bf7-b0656df4fa7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b9da4b68bba6358ff473846fb710f8fa6454e5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62688606"
---
# <a name="replay-requirements"></a>Requisiti per la riproduzione
  Per riprodurre dati di traccia con [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] o Distributed Replay Utility, è necessario acquisire un set specifico di classi di evento e colonne nella traccia. Queste impostazioni sono abilitate per impostazione predefinita se si usa il modello di traccia **TSQL_Replay** per configurare una traccia usata successivamente per la riproduzione. In questo argomento vengono descritte queste impostazioni e altri requisiti per la riproduzione.  
  
> [!NOTE]  
>  È consigliabile utilizzare Distributed Replay Utility per riprodurre un'applicazione OLTP intensiva (con molte connessioni simultanee attive o una velocità effettiva elevata). Distributed Replay Utility può riprodurre dati di traccia da più computer, per simulare in modo migliore un carico di lavoro di importanza critica. Per altre informazioni, vedere [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md).  
  
## <a name="event-classes-required-for-replay"></a>Classi di evento necessarie per la riproduzione  
 Ai fini della riproduzione tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], è necessario acquisire nella traccia il set di classi di evento seguente, oltre ad altre classi di evento che si desidera monitorare:  
  
-   **CursorClose (** necessaria solo per la riproduzione di cursori sul lato server)  
  
-   **CursorExecute (** necessaria solo per la riproduzione di cursori sul lato server)  
  
-   **CursorOpen (** necessaria solo per la riproduzione di cursori sul lato server)  
  
-   **CursorPrepare (** necessaria solo per la riproduzione di cursori sul lato server)  
  
-   **CursorUnprepare (** necessaria solo per la riproduzione di cursori sul lato server)  
  
-   **Audit Login**  
  
-   **Audit Logout**  
  
-   **ExistingConnection**  
  
-   **RPC Output Parameter**  
  
-   **RPC:Completed**  
  
-   **RPC:Starting**  
  
-   **Exec Prepared SQL** (necessaria solo per la riproduzione di istruzioni SQL preparate sul lato server)  
  
-   **Prepare SQL** (necessaria solo per la riproduzione di istruzioni SQL preparate sul lato server)  
  
-   **SQL:BatchCompleted**  
  
-   **SQL:BatchStarting**  
  
## <a name="data-columns-required-for-replay"></a>Colonne di dati necessarie per la riproduzione  
 Per consentire la riproduzione di una traccia, è necessario acquisire le colonne di dati seguenti, insieme alle colonne di dati che si desidera monitorare:  
  
-   **Event Class**  
  
-   **EventSequence**  
  
-   **TextData**  
  
-   **Application Name**  
  
-   **LoginName**  
  
-   **DatabaseName**  
  
-   **ID database**  
  
-   **ClientProcessID**  
  
-   **HostName**  
  
-   **ServerName**  
  
-   **Binary Data**  
  
-   **SPID**  
  
-   **Start Time**  
  
-   **EndTime**  
  
-   **IsSystem**  
  
-   **NTDomainName**  
  
-   **NTUserName**  
  
-   **Errore**  
  
> [!NOTE]  
>  Usare il modello di traccia **TSQL_Replay** per le tracce che consentono di acquisire i dati per la riproduzione.  
  
## <a name="other-replay-requirements"></a>Altri requisiti per la riproduzione  
 In Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]durante la riproduzione viene verificata la presenza delle colonne e degli eventi necessari. Questa modifica contribuisce a migliorare la precisione della riproduzione e a rendere più specifica la risoluzione dei problemi di riproduzione in caso di mancanza di dati necessari. Se i dati necessari non sono disponibili in una traccia, viene restituito un errore di riproduzione e la riproduzione del file viene arrestata.  
  
 Per riprodurre una traccia in un server (destinazione) in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione, diverso dal server in cui la traccia veniva eseguita originariamente (origine), assicurarsi che siano state eseguite le operazioni seguenti:  
  
-   È necessario che tutti gli account di accesso e gli utenti inclusi nella traccia siano disponibili nella destinazione e nello stesso database dell'origine.  
  
-   È necessario che tutti gli account di accesso e gli utenti nella destinazione dispongano delle stesse autorizzazioni disponibili nell'origine.  
  
-   Tutte le password di accesso devono essere uguali a quella dell'utente che esegue la riproduzione.  
  
-   È consigliabile che gli ID di database nella destinazione e nell'origine siano uguali. In caso contrario, tuttavia, è possibile trovare una corrispondenza in base a **DatabaseName** , se presente nella traccia.  
  
-   È necessario che il database predefinito per ogni account di accesso incluso nella traccia sia impostato (nella destinazione) sul database di destinazione corrispondente. Si supponga ad esempio che la traccia da riprodurre includa attività per l'account di accesso **Fred**nel database **Fred_Db** nell'origine. Quindi nella destinazione il database predefinito per l'account **Fred**deve essere impostato sul database corrispondente a **Fred_Db** , anche se il nome del database è diverso. Per impostare il database predefinito dell'account di accesso, usare la stored procedure di sistema **sp_defaultdb** .  
  
 La riproduzione degli eventi associati ad account di accesso mancanti o non corretti genera errori di riproduzione, ma l'operazione non viene interrotta.  
  
 Per informazioni sulle autorizzazioni necessarie per riprodurre una traccia, vedere [Autorizzazioni necessarie per l'esecuzione di SQL Server Profiler](sql-server-profiler.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riprodurre una tabella di traccia &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md)   
 [Riprodurre un file di traccia &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md)   
 [Guida di riferimento alle classi di evento SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_defaultdb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-defaultdb-transact-sql)   
 [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)  
  
  
