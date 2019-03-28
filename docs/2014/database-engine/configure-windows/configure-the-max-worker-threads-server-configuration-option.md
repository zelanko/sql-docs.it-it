---
title: Configurare l'opzione di configurazione del server max worker threads | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5d4aae8a264bd77d51c3365183ee510043ae814b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536073"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>Configurare l'opzione di configurazione del server max worker threads
  In questo argomento si illustra come configurare l'opzione di configurazione del server **max worker threads** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con l'opzione **max worker threads** è possibile configurare il numero di thread di lavoro disponibili per i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono utilizzati i servizi thread nativi dei sistemi operativi in modo che uno o più thread supportino ogni rete supportata simultaneamente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , che tramite un altro thread vengano gestiti i checkpoint di database e che tutti gli utenti siano gestiti da un pool di thread. Il valore predefinito per **max worker threads** è 0. In questo modo, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile configurare automaticamente il numero di thread di lavoro all'avvio. L'impostazione predefinita è la migliore per la maggior parte dei sistemi. A seconda della configurazione del sistema, tuttavia, l'impostazione di **max worker thread** su un valore specifico determina talvolta un miglioramento delle prestazioni.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione max worker threads utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la configurazione dell'opzione max worker threads](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Quando il numero effettivo di richieste di query è inferiore al valore impostato per **max worker threads**, viene assegnato un thread per la gestione di ogni richiesta. Se, tuttavia, il numero effettivo di richieste di query supera il valore impostato per **max worker threads**, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i thread di lavoro vengono riuniti in un pool. In questo modo, le richieste possono essere gestite dal primo thread di lavoro disponibile.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Questa opzione è avanzata e la relativa modifica è riservata ad amministratori di database esperti o a tecnici dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   La creazione di un pool di thread consente di ottimizzare le prestazioni quando al server è connesso un numero elevato di client. In genere viene creato un thread del sistema operativo distinto per ogni richiesta di query. In presenza, tuttavia, di centinaia di connessioni al server, l'utilizzo di un thread per ogni richiesta di query può occupare quantità elevate di risorse di sistema. L'opzione **max worker threads** consente di migliorare le prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grazie alla creazione di un pool di thread di lavoro per soddisfare una maggiore quantità di richieste di query.  
  
-   Nella tabella seguente viene mostrato il numero massimo di thread di lavoro configurato automaticamente per diverse combinazioni di CPU e versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    |Numero di CPU|computer a 32 bit|Computer a 64 bit|  
    |--------------------|----------------------|----------------------|  
    |\<= 4 processori|256|512|  
    |8 processori|288|576|  
    |16 processori|352|704|  
    |32 processori|480|960|  
    |64 processori|736|1472|  
    |128 processori|4224|4480|  
    |256 processori|8320|8576|  
  
    > [!NOTE]  
    >  Per consigli sull'uso di più di 64 CPU, vedere [Procedure consigliate per l'esecuzione di SQL Server in computer con più di 64 CPU](https://technet.microsoft.com/library/ee210547\(SQL.105\).aspx).  
  
    > [!WARNING]  
    >  Si consiglia 1024 come numero massimo di thread di lavoro per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione in un computer a 32 bit.  
  
-   Se tutti i thread di lavoro sono attivi con query a esecuzione prolungata, si potrebbe non ricevere alcuna risposta da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finché un thread di lavoro non viene completato e diventa disponibile. Anche se non si tratta di un difetto, questo comportamento può talvolta risultare indesiderato. Se non si riceve risposta da un processo e non è possibile elaborare alcuna query, connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando la connessione amministrativa dedicata (DAC) e terminare il processo. Per evitare questo problema, aumentare il numero massimo di thread di lavoro.  
  
 L'opzione di configurazione del server **max worker threads** non considera i thread che sono richiesti per tutte le attività di sistema come i gruppi di disponibilità, Service Broker, gestione blocchi e altri.  Se viene superato il numero di thread configurato, la seguente query fornirà informazioni sulle attività di sistema che hanno generato i thread aggiuntivi.  
  
```  
SELECT  
s.session_id,  
r.command,  
r.status,  
r.wait_type,  
r.scheduler_id,  
w.worker_address,  
w.is_preemptive,  
w.state,  
t.task_state,  
t.session_id,  
t.exec_context_id,  
t.request_id  
FROM sys.dm_exec_sessions AS s  
INNERJOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
WHERE s.is_user_process = 0;  
  
```  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>Per configurare l'opzione max worker threads  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Processori** .  
  
3.  Nella casella **Max worker threads** digitare oppure selezionare un valore compreso tra 128 e 32767.  
  
     L'opzione **max worker threads** consente di configurare il numero di thread di lavoro disponibili per i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'impostazione predefinita di **max worker threads** è ottimale per la maggior parte dei sistemi. A seconda della configurazione del sistema, tuttavia, l'impostazione di **max worker thread** su un valore inferiore determina talvolta un miglioramento delle prestazioni.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>Per configurare l'opzione max worker threads  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si illustra come utilizzare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per configurare l'opzione `max worker threads` su `900`.  
  
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
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: fasi successive alla configurazione dell'opzione max worker threads  
 La modifica sarà applicata immediatamente senza richiedere il riavvio del [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Connessione di diagnostica per gli amministratori di database](diagnostic-connection-for-database-administrators.md)  
  
  
