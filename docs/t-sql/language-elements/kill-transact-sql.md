---
title: KILL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KILL_TSQL
- KILL
dev_langs:
- TSQL
helpviewer_keywords:
- WITH STATUSONLY option
- terminating distributed transactions
- distributed transactions [SQL Server], terminating
- in-doubt transactions
- IDs [SQL Server], user processes
- ending distributed transactions [SQL Server]
- stopping distributed transactions
- session IDs [SQL Server]
- system process termination [SQL Server]
- stopping processes
- ending processes [SQL Server]
- UOW [SQL Server]
- orphaned transactions [SQL Server]
- unit of work [SQL Server]
- process termination [SQL Server]
- KILL statement
- terminating process
ms.assetid: 071cf260-c794-4b45-adc0-0e64097938c0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: be0bccac59c011fc36e8481029d9951cd36cad99
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205400"
---
# <a name="kill-transact-sql"></a>KILL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Termina un processo utente in base all'ID di sessione o all'unità di lavoro (UOW, Unit Of Work). Se all'ID di sessione o al valore UOW specificato sono associate numerose azioni di rollback, l'esecuzione dell'istruzione KILL potrebbe richiedere tempi lunghi, soprattutto quando implica il rollback di una transazione lunga.  
  
 È possibile utilizzare KILL per terminare una connessione normale, operazione che determina internamente la fine delle transazioni associate all'ID di sessione specificato. Questa istruzione può inoltre essere utilizzata per terminare transazioni distribuite orfane e in dubbio quando [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) è in uso.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server  
  
KILL { session ID | UOW } [ WITH STATUSONLY ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
KILL 'session_id'  
[;]   
```  
  
## <a name="arguments"></a>Argomenti  
 *session ID*  
 ID di sessione del processo da terminare. *session ID* è un valore intero univoco (**int**) assegnato a ogni connessione utente al momento dell'attivazione. Il valore dell'ID di sessione rimane associato alla connessione per tutta la durata della connessione. Al termine della connessione, il valore intero viene rilasciato ed è possibile riassegnarlo a una nuova connessione.  
La query seguente consente di identificare il `session_id` che si intende eliminare:  
 ```sql  
 SELECT conn.session_id, host_name, program_name,
     nt_domain, login_name, connect_time, last_request_end_time 
FROM sys.dm_exec_sessions AS sess
JOIN sys.dm_exec_connections AS conn
    ON sess.session_id = conn.session_id;
```  
  
*UOW*  
**Si applica a**: (da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Identifica l'ID dell'unità di lavoro delle transazioni distribuite. *UOW* è un GUID che è possibile ottenere dalla colonna request_owner_guid della vista a gestione dinamica sys.dmtran_locks. È anche possibile ottenere il valore *UOW* dal log degli errori o tramite il monitoraggio MS DTC. Per ulteriori informazioni sul monitoraggio di transazioni distribuite, vedere la documentazione di MS DTC.  
  
 Usare KILL *UOW* per terminare le transazioni distribuite orfane. Queste transazioni non sono associate a un ID di sessione effettivo, ma sono invece associate in modo artificiale all'ID di sessione -2. Questo ID di sessione consente di semplificare l'identificazione delle transazioni orfane tramite l'esecuzione di una query sulla colonna dell'ID di sessione nelle viste a gestione dinamica sys.dm_tran_locks, sys.dm_exec_sessions o sys.dm_exec_requests.  
  
 WITH STATUSONLY  
 Genera un report di stato su un valore *session ID* o *UOW* specificato di cui è in corso il rollback a causa di un'istruzione KILL precedente. Il comando KILL WITH STATUSONLY non termina il processo *session ID* o *UOW* o ne esegue il rollback, ma visualizza esclusivamente lo stato corrente del rollback.  
  
## <a name="remarks"></a>Remarks  
 L'istruzione KILL viene comunemente utilizzata per terminare un processo che blocca altri processi importanti con blocchi oppure un processo che esegue una query in cui sono utilizzate risorse di sistema che è necessario liberare. I processi di sistema e i processi che eseguono una stored procedure estesa non possono essere terminati.  
  
 Eseguire l'istruzione KILL con cautela, in particolare quando sono in esecuzione processi critici. Non è possibile terminare un proprio processo ed è consigliabile non terminare i processi seguenti:  
  
-   AWAITING COMMAND  
-   CHECKPOINT SLEEP  
-   LAZY WRITER  
-   LOCK MONITOR  
-   SIGNAL HANDLER  
  
Usare @@SPID per visualizzare il valore dell'ID di sessione della sessione corrente.  
  
 Per ottenere un report dei valori di ID della sessione attiva, è possibile eseguire una query sulla colonna session_id delle viste a gestione dinamica sys.dm_tran_locks, sys.dm_exec_sessions e sys.dm_exec_requests. È inoltre possibile visualizzare la colonna SPID restituita dalla stored procedure di sistema sp_who. Se è in corso il rollback per un processo SPID specifico, nella relativa colonna cmd del set di risultati sp_who viene indicato KILLED/ROLLBACK.  
  
 Quando una determinata connessione mantiene attivo un blocco su una risorsa del database e blocca l'avanzamento di un'altra connessione, l'ID di sessione della connessione di blocco viene visualizzato nella colonna `blocking_session_id` di `sys.dm_exec_requests` o nella colonna `blk` restituita da `sp_who`.  
  
 È possibile utilizzare il comando KILL per risolvere le transazioni distribuite in dubbio. Queste sono le transazioni distribuite non risolte che si verificano in seguito a riavvii non pianificati del server di database o di MS DTC. Per altre informazioni sulla creazione di transazioni contrassegnate, vedere la sezione "Commit in due fasi" in [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="using-with-statusonly"></a>Utilizzo di WITH STATUSONLY  
 Il comando KILL WITH STATUSONLY genera un report solo se è in corso il rollback dell'ID di sessione o del valore UOW in seguito all'esecuzione di un'istruzione KILL *session ID*|*UOW* precedente. Nel report di stato è indicata la percentuale di rollback completata e il periodo di tempo rimanente, espresso in secondi, nel formato seguente:  
  
 `Spid|UOW <xxx>: Transaction rollback in progress. Estimated rollback completion: <yy>% Estimated time left: <zz> seconds`  
  
 Se quando si esegue l'istruzione KILL *session ID*|*UOW* WITH STATUSONLY l'operazione di rollback dell'ID di sessione o del valore UOW è già stata completata oppure non è in corso il rollback di tale processo, KILL *session ID*|*UOW* WITH STATUSONLY restituisce il messaggio di errore seguente:  
  
 ```
"Msg 6120, Level 16, State 1, Line 1"  
"Status report cannot be obtained. Rollback operation for Process ID <session ID> is not in progress."
```  
  
 È possibile ottenere lo stesso report di stato ripetendo la stessa istruzione KILL *session ID*|*UOW* senza usare l'opzione WITH STATUSONLY. Questa procedura non è tuttavia consigliabile. La ripetizione di un'istruzione KILL *session ID* potrebbe infatti terminare un nuovo processo se dopo il completamento del rollback l'ID di sessione viene riassegnato a una nuova attività prima dell'esecuzione della nuova istruzione KILL. L'utilizzo della clausola WITH STATUSONLY consente di evitare questo tipo di problema.  
  
## <a name="permissions"></a>Permissions  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** È richiesta l'autorizzazione ALTER ANY CONNECTION. L'autorizzazione ALTER ANY CONNECTION viene concessa mediante l'appartenenza al ruolo server predefinito sysadmin o processadmin.  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]:** È richiesta l'autorizzazione KILL DATABASE CONNECTION. L'account di accesso a livello di server principale ha l'autorizzazione KILL DATABASE CONNECTION.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-kill-to-terminate-a-session"></a>A. Utilizzo di KILL per terminare una sessione  
 Nell'esempio seguente viene illustrato come terminare l'ID di sessione `53`.  
  
```sql  
KILL 53;  
GO  
```  
  
### <a name="b-using-kill-session-id-with-statusonly-to-obtain-a-progress-report"></a>b. Utilizzo di KILL session ID WITH STATUSONLY per ottenere un report di stato  
 Nell'esempio seguente viene generato un report di stato del processo di rollback per l'ID di sessione specifico.  
  
```sql  
KILL 54;  
KILL 54 WITH STATUSONLY;  
GO  
  
--This is the progress report.  
spid 54: Transaction rollback in progress. Estimated rollback completion: 80% Estimated time left: 10 seconds.  
```  
  
### <a name="c-using-kill-to-terminate-an-orphaned-distributed-transaction"></a>C. Utilizzo di KILL per terminare una transazione distribuita orfana  
 Nell'esempio seguente viene illustrato come terminare una transazione distribuita orfana (ID di sessione = -2) con un valore *UOW* di `D5499C66-E398-45CA-BF7E-DC9C194B48CF`.  
  
```sql  
KILL 'D5499C66-E398-45CA-BF7E-DC9C194B48CF';  
```  

  
## <a name="see-also"></a>Vedere anche  
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [Funzioni predefinite &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)   
 [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  
