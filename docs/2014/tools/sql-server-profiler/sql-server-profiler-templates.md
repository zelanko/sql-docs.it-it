---
title: Modelli di SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- default SQL Server Profiler templates
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- predefined templates [SQL Server Profiler]
- SQL Server Profiler, templates
ms.assetid: b674e491-dc58-47a1-acdd-7028e9a201fc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5cac924e926d03dffb9116e5ce7194bb784d45fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68186148"
---
# <a name="sql-server-profiler-templates"></a>Modelli di SQL Server Profiler
  È possibile utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per creare modelli per la definizione delle classi di evento e delle colonne di dati da includere nelle tracce. Dopo aver definito e salvato il modello, è possibile eseguire una traccia per la registrazione dei dati relativi a ogni classe di evento selezionata. È possibile utilizzare un modello per più tracce. Il modello non viene eseguito direttamente.  
  
 
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] offre modelli di tracce predefiniti che consentono di configurare facilmente le classi di eventi che saranno probabilmente necessarie per tracce specifiche. Il modello Standard, ad esempio, consente di creare una traccia generica per la registrazione degli accessi, delle disconnessioni, dei batch completati e delle informazioni per la connessione. È possibile utilizzare questo modello per l'esecuzione di tracce senza modifiche oppure come punto di partenza per modelli aggiuntivi con configurazioni di evento diverse.  
  
> [!NOTE]  
>  Oltre che da modelli predefiniti, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] consente inoltre di creare le tracce da un modello vuoto, che per impostazione predefinita non include classi di eventi. L'utilizzo di un modello di traccia vuoto può essere utile quando una traccia pianificata non somiglia alle configurazioni di nessuno dei modelli predefiniti.  
  
 
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] può tracciare vari tipi di server. È ad esempio possibile tracciare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Le classi di evento che è possibile includere, tuttavia, non sono le stesse per ogni tipo di server. Pertanto, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] mantiene modelli diversi per server diversi e rende disponibile il modello specifico corrispondente al tipo server selezionato.  
  
## <a name="predefined-templates"></a>Modelli predefiniti  
 Oltre al modello Standard (predefinito), [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] include vari modelli predefiniti per il monitoraggio di determinati tipi di eventi. Nella tabella seguente vengono elencati i modelli predefiniti, il loro scopo e le classi di eventi per le quali acquisiscono informazioni.  
  
|Nome modello|Scopo del modello|Classi di eventi|  
|-------------------|----------------------|-------------------|  
|SP_Counts|Acquisisce il comportamento di esecuzione delle stored procedure nel tempo.|**SP: avvio in corso**|  
|Standard|Punto di partenza generico per la creazione di una traccia. Acquisisce tutte le stored procedure e i batch di [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguiti. Utilizzabile per il monitoraggio dell'attività generale del server di database.|**Connessione di controllo**<br /><br /> **Disconnessione di controllo**<br /><br /> **ExistingConnection**<br /><br /> **RPC: completato**<br /><br /> **SQL: BatchCompleted**<br /><br /> **SQL: BatchStarting**|  
|TSQL|Acquisisce tutte le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] inviate a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dai client e l'ora dell'invio. Utilizzabile per il debug delle applicazioni client.|**Connessione di controllo**<br /><br /> **Disconnessione di controllo**<br /><br /> **ExistingConnection**<br /><br /> **RPC: avvio in corso**<br /><br /> **SQL: BatchStarting**|  
|TSQL_Duration|Acquisisce tutte le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] inviate a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dai client e il relativo tempo di esecuzione (in millisecondi), quindi le raggruppa per durata. Utilizzabile per identificare query lente.|**RPC: completato**<br /><br /> **SQL: BatchCompleted**|  
|TSQL_Grouped|Acquisisce tutte le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] inviate a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'ora dell'invio. Raggruppa le informazioni per utente o client che ha inviato l'istruzione. Utilizzabile per analizzare le query dal punto di vista di un client o utente particolare.|**Connessione di controllo**<br /><br /> **Disconnessione di controllo**<br /><br /> **ExistingConnection**<br /><br /> **RPC: avvio in corso**<br /><br /> **SQL: BatchStarting**|  
|TSQL_Locks|Acquisisce tutte le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] inviate a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dai client insieme a eventi del blocco insoliti. Utilizzabile per risolvere eventi di deadlock, di timeout di blocco e di escalation blocchi.|**Report processo bloccato**<br /><br /> **SP: StmtCompleted**<br /><br /> **SP: StmtStarting**<br /><br /> **SQL:StmtCompleted**<br /><br /> **SQL:StmtStarting**<br /><br /> **Grafico deadlock**<br /><br /> **Blocca: Annulla**<br /><br /> **Blocco: deadlock**<br /><br /> **Lock: Deadlock Chain**<br /><br /> **Lock: escalation**<br /><br /> **Lock: timeout (timeout>0)**|  
|TSQL_Replay|Acquisisce informazioni dettagliate sulle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] necessarie per l'eventuale riproduzione della traccia. Utilizzabile per eseguire l'ottimizzazione iterativa, ad esempio per test di benchmark.|**CursorClose**<br /><br /> **CursorExecute**<br /><br /> **CursorOpen**<br /><br /> **CursorPrepare**<br /><br /> **CursorUnprepare**<br /><br /> **Connessione di controllo**<br /><br /> **Disconnessione di controllo**<br /><br /> **Connessione esistente**<br /><br /> **Parametro di output RPC**<br /><br /> **RPC: completato**<br /><br /> **RPC: avvio in corso**<br /><br /> **SQL preparata per exec**<br /><br /> **Prepara SQL**<br /><br /> **SQL: BatchCompleted**<br /><br /> **SQL: BatchStarting**|  
|TSQL_SPs|Acquisisce informazioni dettagliate relative a tutte le stored procedure in esecuzione. Utilizzabile per analizzare i passaggi dei componenti delle stored procedure. Aggiungere l'evento **SP:Recompile** se si ritiene che le stored procedure vengano ricompilate.|**Connessione di controllo**<br /><br /> **Disconnessione di controllo**<br /><br /> **ExistingConnection**<br /><br /> **RPC: avvio in corso**<br /><br /> **SP: completato**<br /><br /> **SP: avvio in corso**<br /><br /> **SP: StmtStarting**<br /><br /> **SQL: BatchStarting**|  
|Ottimizzazione|Acquisisce informazioni sulle stored procedure e l'esecuzione dei batch [!INCLUDE[tsql](../../includes/tsql-md.md)] . Consente di generare un output di traccia utilizzabile in Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] come carico di lavoro per l'ottimizzazione dei database.|**RPC: completato**<br /><br /> **SP: StmtCompleted**<br /><br /> **SQL: BatchCompleted**|  
  
 Per informazioni sulle classi di evento, vedere [Guida di riferimento alle classi di evento di SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
## <a name="default-template"></a>Modello predefinito  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]designa automaticamente il modello **standard** come modello predefinito applicato a qualsiasi nuova traccia. Tuttavia è possibile modificare il modello predefinito in qualsiasi altro modello, predefinito o definito dall'utente. Per modificare il modello predefinito, selezionare la casella di controllo **Usa come modello predefinito per il tipo di server selezionato** quando si crea o modifica un modello utilizzando la scheda **Generale** della finestra di dialogo **Proprietà modello di traccia** .  
  
 Per passare alla finestra di dialogo **Proprietà modello di traccia** scegliere [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **dal menu** File **di**e quindi fare clic su **Nuovo modello** o su **Modifica modello**.  
  
> [!NOTE]  
>  Il modello predefinito è specifico per un determinato tipo di server. La modifica del modello predefinito per un tipo di server non ha effetto sul modello predefinito per gli altri tipi. Per altre informazioni sull'impostazione di un modello predefinito per un server specifico, vedere [Impostare i valori predefiniti per una definizione di traccia &#40;SQL Server Profiler&#41;](set-trace-definition-defaults-sql-server-profiler.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un modello di traccia &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)   
 [Modificare modello di traccia &#40;SQL Server Profiler&#41;](../../database-engine/modify-a-trace-template-sql-server-profiler.md)   
 [Esportare un modello di traccia &#40;SQL Server Profiler&#41;](export-a-trace-template-sql-server-profiler.md)   
 [Importare un modello di traccia &#40;SQL Server Profiler&#41;](import-a-trace-template-sql-server-profiler.md)  
  
  
