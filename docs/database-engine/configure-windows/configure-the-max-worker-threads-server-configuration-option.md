---
title: Configurare l'opzione di configurazione del server max worker threads | Microsoft Docs
ms.custom: ''
ms.date: 04/14/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d573bc4c8fc628bf4f1cc1fa36e50bc0e69c3202
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488330"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>Configurare l'opzione di configurazione del server max worker threads
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento si illustra come configurare l'opzione di configurazione del server **max worker threads** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con l'opzione **max worker threads** è possibile configurare il numero di thread di lavoro disponibili per i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono utilizzati i servizi thread nativi dei sistemi operativi in modo che uno o più thread supportino ogni rete supportata simultaneamente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , che tramite un altro thread vengano gestiti i checkpoint di database e che tutti gli utenti siano gestiti da un pool di thread. Il valore predefinito per **max worker threads** è 0. In questo modo, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile configurare automaticamente il numero di thread di lavoro all'avvio. L'impostazione predefinita è la migliore per la maggior parte dei sistemi. A seconda della configurazione del sistema, tuttavia, l'impostazione di **max worker thread** su un valore specifico determina talvolta un miglioramento delle prestazioni.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione max worker threads utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la configurazione dell'opzione max worker threads](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Quando il numero effettivo di richieste di query è inferiore al valore impostato per **max worker threads**, viene assegnato un thread per la gestione di ogni richiesta. Se tuttavia il numero effettivo di richieste di query supera il valore impostato per **max worker threads** (Numero massimo di thread di lavoro), in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i thread di lavoro vengono riuniti in un pool. In questo modo, le richieste possono essere gestite dal primo thread di lavoro disponibile.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
  
-   Questa opzione è avanzata e la relativa modifica è riservata ad amministratori di database esperti o a professionisti dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si sospetta la presenza di un problema di prestazioni, è poco probabile che si tratti della disponibilità dei thread di lavoro. È più probabile che la causa sia legata a I/O che determina l'attesa dei thread di lavoro. È consigliabile individuare la causa radice di un problema di prestazioni prima di modificare l'impostazione max worker threads.  
  
-   La creazione di un pool di thread consente di ottimizzare le prestazioni quando al server è connesso un numero elevato di client. In genere viene creato un thread del sistema operativo distinto per ogni richiesta di query. In presenza, tuttavia, di centinaia di connessioni al server, l'utilizzo di un thread per ogni richiesta di query può occupare quantità elevate di risorse di sistema. L'opzione **max worker threads** consente di migliorare le prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grazie alla creazione di un pool di thread di lavoro per soddisfare una maggiore quantità di richieste di query.  
  
-   La tabella seguente visualizza il numero massimo di thread di lavoro configurato automaticamente per diverse combinazioni di CPU, architettura del computer e versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando la formula: * **Numero massimo di ruoli di lavoro predefiniti* + ((* CPU logiche* - 4) * *Ruoli di lavoro per CPU*)**.  
  
    |Numero di CPU|Computer a 32 bit (fino a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])|Computer a 64 bit (fino a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1)|Computer a 64 bit (a partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)])|   
    |------------|------------|------------|------------|  
    |\< = 4|256|512|512|   
    |8|288|576|576|   
    |16|352|704|704|   
    |32|480|960|960|   
    |64|736|1472|2432|   
    |128|1248|2496|4480|   
    |256|2272|4544|8576|   
    
    Fino a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, i *Ruoli di lavoro per CPU* dipendono solo dall'architettura (a 32 bit o a 64 bit):
    
    |Numero di CPU|Computer a 32 bit <sup>1</sup>|Computer a 64 bit|   
    |------------|------------|------------|   
    |\< = 4|256|512|   
    |\> 4|256 + ((CPU logica - 4) * 8)|512 <sup>2</sup> + ((CPU logiche - 4) * 16)|   
    
    A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], i *Ruoli di lavoro per CPU* dipendono dall'architettura e dal numero di processori (compreso tra 4 e 64 o maggiore di 64):
    
    |Numero di CPU|Computer a 32 bit <sup>1</sup>|Computer a 64 bit|   
    |------------|------------|------------|   
    |\< = 4|256|512|   
    |\> 4 e \< = 64|256 + ((CPU logica - 4) * 8)|512 <sup>2</sup> + ((CPU logiche - 4) * 16)|   
    |\> 64|256 + ((CPU logica - 4) * 32)|512 <sup>2</sup> + ((CPU logiche - 4) * 32)|   
  
    <sup>1</sup> A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], non è più possibile installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un sistema operativo a 32 bit. I valori per i computer a 32 bit vengono indicati per offrire assistenza ai clienti che eseguono [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e versioni precedenti. Si consiglia 1.024 come numero massimo di thread di lavoro per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione in un computer a 32 bit.
    
    <sup>2</sup> A partire da [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] il valore *Default Max Workers* (Ruoli di lavoro massimi predefiniti) è diviso per 2 per i computer con meno di 2 GB di memoria.
  
    > [!TIP]  
    > Per consigli sull'uso di più di 64 CPU, vedere [Procedure consigliate per l'esecuzione di SQL Server in computer con più di 64 CPU](../../relational-databases/thread-and-task-architecture-guide.md#best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus).  
  
-   Se tutti i thread di lavoro sono attivi con query a esecuzione prolungata, si potrebbe non ricevere alcuna risposta da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finché un thread di lavoro non viene completato e diventa disponibile. Anche se non si tratta di un difetto, questo comportamento può talvolta risultare indesiderato. Se non si riceve risposta da un processo e non è possibile elaborare alcuna query, connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando la connessione amministrativa dedicata (DAC) e terminare il processo. Per evitare questo problema, aumentare il numero massimo di thread di lavoro.  
  
 L'opzione di configurazione del server **max worker thread** (Numero massimo di thread di lavoro) non limita tutti i thread che possono essere generati nel sistema. I thread necessari per attività come i gruppi di disponibilità, Service Broker, Gestione blocchi o altre vengono generati senza tener conto di questo limite. Se viene superato il numero di thread configurato, la query seguente fornirà informazioni sulle attività di sistema che hanno generato i thread aggiuntivi.  
  
 ```sql  
 SELECT  s.session_id, r.command, r.status,  
    r.wait_type, r.scheduler_id, w.worker_address,  
    w.is_preemptive, w.state, t.task_state,  
    t.session_id, t.exec_context_id, t.request_id  
 FROM sys.dm_exec_sessions AS s  
 INNER JOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
 INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
 INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
 WHERE s.is_user_process = 0;  
 ```  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione `RECONFIGURE`, a un utente deve essere concessa l'autorizzazione a livello di server `ALTER SETTINGS`. L'autorizzazione `ALTER SETTINGS` è assegnata implicitamente ai ruoli predefiniti del server**sysadmin** e **serveradmin**.  
  
##  <a name="using-ssmanstudiofull"></a><a name="SSMSProcedure"></a> Uso [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>Per configurare l'opzione max worker threads  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Processori** .  
  
3.  Nella casella **Max worker threads** digitare oppure selezionare un valore compreso tra 128 e 32.767.  
  
> [!TIP]
> L'opzione **max worker threads** consente di configurare il numero di thread di lavoro disponibili per i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'impostazione predefinita di **max worker threads** è ottimale per la maggior parte dei sistemi. A seconda della configurazione del sistema, tuttavia, l'impostazione di **max worker thread** su un valore inferiore determina talvolta un miglioramento delle prestazioni.
> Per altre informazioni, vedere [Indicazioni](#Recommendations), in precedenza in questo argomento.
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>Per configurare l'opzione max worker threads  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si illustra come utilizzare [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) per configurare l'opzione `max worker threads` su `900`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'max worker threads', 900 ;  
GO  
RECONFIGURE;  
GO  
```  
  
##  <a name="follow-up-after-you-configure-the-max-worker-threads-option"></a><a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione max worker threads  
 La modifica sarà applicata immediatamente dopo l'esecuzione di [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) senza richiedere il riavvio del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Connessione di diagnostica per gli amministratori di database](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  
