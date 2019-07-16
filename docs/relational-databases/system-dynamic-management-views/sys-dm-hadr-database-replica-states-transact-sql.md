---
title: sys.dm_hadr_database_replica_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_states_TSQL
- sys.dm_hadr_database_states
- dm_hadr_database_states
- dm_hadr_database_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_database_replica_states dynamic management view
ms.assetid: 1a17b0c9-2535-4f3d-8013-cd0a6d08f773
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3a9395b27aa7ddf6d6fd85734da5d66a870eb634
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900605"
---
# <a name="sysdmhadrdatabasereplicastates-transact-sql"></a>sys.dm_hadr_database_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni database che partecipa a un gruppo di disponibilità Always On per il quale l'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ospita una replica di disponibilità. Questa DMV espone informazioni sullo stato sia sulle repliche primarie sia su quelle secondarie. Su una replica secondaria, questa vista restituisce una riga per ogni database secondario sull'istanza del server. Sulla replica primaria, questa vista restituisce una riga per ogni database primario e una riga aggiuntiva per il database secondario corrispondente.  
  
> [!IMPORTANT]
> A seconda dell'azione e degli stati di livello superiore, è possibile che le informazioni sullo stato del database non siano disponibili o non aggiornate. I valori hanno inoltre pertinenza esclusivamente locale. Ad esempio, nella replica primaria, il valore della **last_hardened_lsn** colonna riflette le informazioni su un determinato database secondario attualmente disponibile per la replica primaria, non il LSN finalizzato effettivo valore che la replica secondaria potrebbe disporre attualmente.  
   
|Nome colonna|Tipo di dati|Descrizione (sulla replica primaria)|  
|-----------------|---------------|----------------------------------------|  
|**database_id**|**int**|Identificatore del database, univoco in un'istanza di SQL Server. Questo è lo stesso valore come visualizzato nei [Sys. Databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista del catalogo.|  
|**group_id**|**uniqueidentifier**|Identificatore del gruppo di disponibilità a cui appartiene il database.|  
|**replica_id**|**uniqueidentifier**|Identificatore della replica di disponibilità all'interno del gruppo di disponibilità.|  
|**group_database_id**|**uniqueidentifier**|Identificatore del database nel gruppo di disponibilità. L'identificatore è identico su ogni replica a cui è stato aggiunto questo database.|  
|**is_local**|**bit**|Se il database di disponibilità è locale, uno di:<br /><br /> 0 = Il database non è locale rispetto all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = Il database è locale rispetto all'istanza del server.|  
|**is_primary_replica**|**bit**|Restituisce 1 se la replica è primaria o 0 se si tratta di una replica secondaria.<br /><br />**Si applica a:**  da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] fino a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**synchronization_state**|**tinyint**|Stato di spostamento dei dati, uno dei valori seguenti.<br /><br /> 0 = non in sincronizzazione. Per un database primario, indica che il database non è pronto per la sincronizzazione del log delle transazioni con i database secondari corrispondenti. Per un database secondario, indica che il database non ha ancora avviato la sincronizzazione del log a causa di un problema di connessione, è stato sospeso o si trova in stati di transizione durante l'avvio o un cambio di ruolo.<br /><br /> 1 = sincronizzazione in corso. Per un database primario, indica che il database è pronto ad accettare una richiesta di analisi da un database secondario. Per un database secondario, indica che è in corso uno spostamento dati attivo per il database.<br /><br /> 2 = Synchronized. Un database primario risulta essere nello stato SYNCHRONIZED anziché SYNCHRONIZING. Un database secondario con commit sincrono risulta essere nello stato sincronizzato se nella cache locale il database è pronto per il failover ed è in corso la sincronizzazione.<br /><br /> 3 = ripristino. Indica la fase del processo di rollback in cui un database secondario ottiene attivamente le pagine dal database primario.<br />**Attenzione:** Quando un database in una replica secondaria è nello stato REVERTING, il failover forzato sulla replica secondaria lascia il database in uno stato in cui non può essere avviato come database primario. Il database dovrà essere riconnesso come un database secondario oppure sarà necessario applicare i nuovi record del log da un backup del log.<br /><br /> 4 = inizializzazione in corso. Indica la fase di rollback in cui il log delle transazioni necessario a un database secondario per l'intercettazione dell'LSN di rollback viene fornito e finalizzato su una replica secondaria.<br />**Attenzione:** Quando un database in una replica secondaria è nello stato INITIALIZING, il failover forzato sulla replica secondaria lascia il database in uno stato in cui non può essere avviato come database primario. Il database dovrà essere riconnesso come un database secondario oppure sarà necessario applicare i nuovi record del log da un backup del log.|  
|**synchronization_state_desc**|**nvarchar(60)**|Descrizione dello stato di spostamento dei dati, uno di:<br /><br /> NOT SYNCHRONIZING<br /><br /> SYNCHRONIZING<br /><br /> SYNCHRONIZED<br /><br /> REVERTING<br /><br /> INITIALIZING|  
|**is_commit_participant**|**bit**|0 = il commit della transazione non è sincronizzato rispetto a questo database.<br /><br /> 1 = il commit della transazione è sincronizzato rispetto a questo database.<br /><br /> Per un database in una replica di disponibilità con commit asincrono, questo valore è sempre 0.<br /><br /> Per un database in una replica di disponibilità con commit sincrono, questo valore è preciso solo nel database primario.|  
|**synchronization_health**|**tinyint**|Riflette l'intersezione dello stato di sincronizzazione di un database appartenente al gruppo di disponibilità sulla replica di disponibilità e la modalità di disponibilità della replica di disponibilità (modalità con commit sincrono o asincrono), uno del i valori seguenti.<br /><br /> 0 = non integro. Il **synchronization_state** del database è 0 (NOT SYNCHRONIZING).<br /><br /> 1 = parzialmente integro. Un database in una replica di disponibilità con commit sincrono è considerato parzialmente integro se **synchronization_state** è 1 (SYNCHRONIZING).<br /><br /> 2 = Healthy. Un database in una replica di disponibilità con commit sincrono è considerato integro se **synchronization_state** è 2 (SYNCHRONIZED) e un database in una replica di disponibilità con commit asincrono è considerato integro se **synchronization_state** è 1 (SYNCHRONIZING).|  
|**synchronization_health_desc**|**nvarchar(60)**|Descrizione del **synchronization_health** del database di disponibilità.<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**database_state**|**tinyint**|0 = Online<br /><br /> 1 = Ripristino in corso<br /><br /> 2 = Recupero in corso<br /><br /> 3 = Recupero in sospeso<br /><br /> 4 = Sospetto<br /><br /> 5 = Emergenza<br /><br /> 6 = Offline<br /><br /> **Nota:** Uguale allo **stato** colonna in sys. Databases.|  
|**database_state_desc**|**nvarchar(60)**|Descrizione del **database_state** della replica di disponibilità.<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> EMERGENCY<br /><br /> OFFLINE<br /><br /> **Nota:** Uguale allo **state_desc** colonna in sys. Databases.|  
|**is_suspended**|**bit**|Stato del database, uno di:<br /><br /> 0 = Ripreso<br /><br /> 1 = sospeso|  
|**suspend_reason**|**tinyint**|Se il database è sospeso, il motivo dello stato sospeso, uno di:<br /><br /> 0 = Azione utente<br /><br /> 1 = Sospensione da parte del partner<br /><br /> 2 = Rollforward<br /><br /> 3 = Acquisizione<br /><br /> 4 = Applicazione<br /><br /> 5 = Riavvio<br /><br /> 6 = Rollback<br /><br /> 7 = Riconvalida<br /><br /> 8 = Errore nel calcolo del punto di sincronizzazione della replica secondaria|  
|**suspend_reason_desc**|**nvarchar(60)**|Descrizione del motivo dello stato sospeso del database, uno di:<br /><br /> SUSPEND_FROM_USER = Movimento di dati sospeso manualmente dall'utente<br /><br /> SUSPEND_FROM_PARTNER = La replica di database viene sospesa dopo un failover forzato<br /><br /> SUSPEND_FROM_REDO = Si è verificato un errore durante la fase di rollforward<br /><br /> SUSPEND_FROM_APPLY = Si è verificato un errore durante la scrittura del log nel file (vedere il log degli errori)<br /><br /> SUSPEND_FROM_CAPTURE = Si è verificato un errore durante l'acquisizione del log sulla replica primaria<br /><br /> SUSPEND_FROM_RESTART = La replica di database è stata sospesa prima che il database venisse riavviato (vedere il log degli errori)<br /><br /> SUSPEND_FROM_UNDO = Si è verificato un errore durante la fase di annullamento (vedere il log degli errori)<br /><br /> SUSPEND_FROM_REVALIDATION = Rilevata la mancata corrispondenza con le modifiche al log alla riconnessione (vedere il log degli errori)<br /><br /> SUSPEND_FROM_XRF_UPDATE = Impossibile trovare il punto del log comune (vedere il log degli errori)|  
|**recovery_lsn**|**numeric(25,0)**|Nella replica primaria, la fine del log delle transazioni prima della scrittura di qualsiasi nuovo record di log da parte del database primario dopo il failover o il recupero. Se per un database secondario specificato questo valore è minore del valore LSN finale corrente (last_hardened_lsn), recovery_lsn rappresenta il valore in base al quale è necessario risincronizzare il database secondario (ripristino e reinizializzazione). Se questo valore è maggiore o uguale al valore LSN finale corrente, la risincronizzazione non è necessaria e non viene eseguita.<br /><br /> **recovery_lsn** riflette un ID di blocco di log riempito con zeri. Non si tratta di un numero di sequenza del file di log (LSN). Per informazioni sul modo in cui questo valore è derivato, vedere [informazioni sui valori delle colonne LSN](#LSNcolumns), più avanti in questo argomento.|  
|**truncation_lsn**|**numeric(25,0)**|Nella replica primaria, per il database primario, riflette l'LSN di troncamento del log minimo in tutti i database secondari corrispondenti. Se il troncamento del log locale è bloccato, ad esempio da un'operazione di backup, questo LSN potrebbe essere maggiore di quello di troncamento locale.<br /><br /> Per un database secondario specificato, riflette il punto di troncamento del database in questione.<br /><br /> **truncation_lsn** riflette un ID di blocco di log riempito con zeri. Non si tratta di un numero di sequenza del file di log (LSN).|  
|**last_sent_lsn**|**numeric(25,0)**|Identificatore del blocco di log che indica il punto fino a cui tutti i blocchi di log sono stati inviati dal database primario. ID del blocco di log successivo che verrà inviato, anziché l'ID del blocco di log inviato più di recente.<br /><br /> **last_sent_lsn** riflette un ID di blocco di log riempito con zeri, non è un numero di sequenza del file effettivo.|  
|**last_sent_time**|**datetime**|Ora di invio dell'ultimo blocco di log.|  
|**last_received_lsn**|**numeric(25,0)**|ID del blocco di log che identifica il punto fino a cui tutti i blocchi di log sono stati ricevuti dalla replica secondaria che ospita questo database secondario.<br /><br /> **last_received_lsn** riflette un ID di blocco di log riempito con zeri. Non si tratta di un numero di sequenza del file di log (LSN).|  
|**last_received_time**|**datetime**|Ora in cui è stato letto l'ID del blocco di log nell'ultimo messaggio ricevuto sulla replica secondaria.|  
|**last_hardened_lsn**|**numeric(25,0)**|Avvio del blocco del log in cui sono contenuti i record di log dell'LSN ultima finalizzazione in un database secondario.<br /><br /> In un database primario con commit asincrono o in un database con commit sincrono i cui criteri correnti si riferiscono a un ritardo, il valore è NULL. Per altri database primari con commit sincrono **last_hardened_lsn** indica il valore minimo del LSN finalizzato in tutti i database secondari.<br /><br /> **Nota: last_hardened_lsn** riflette un ID di blocco di log riempito con zeri. Non si tratta di un numero di sequenza del file di log (LSN). Per altre informazioni, vedere [informazioni sui valori delle colonne LSN](#LSNcolumns), più avanti in questo argomento.|  
|**last_hardened_time**|**datetime**|In un database secondario, ora dell'identificatore del blocco di log per l'ultimo valore LSN finale (**last_hardened_lsn**). In un database primario, riflette l'ora corrispondente all'LSN minimo finalizzato.|  
|**last_redone_lsn**|**numeric(25,0)**|Numero di sequenza del file di log (LSN) effettivo dell'ultimo record di log di cui è stato eseguito il rollforward nel database secondario. **last_redone_lsn** è sempre minore **last_hardened_lsn**.|  
|**last_redone_time**|**datetime**|Ora del rollforward dell'ultimo record di log sul database secondario.|  
|**log_send_queue_size**|**bigint**|Quantità di record di log del database primario che non è stata inviata ai database secondari, espressa in KB.|  
|**log_send_rate**|**bigint**|Media frequenza con cui i dati inviato di istanza di replica primaria durante l'ultimo periodo attivo, in kilobyte (KB) al secondo.|  
|**redo_queue_size**|**bigint**|Quantità di record di log nei file di log della replica secondaria che non sono ancora stati sottoposti a rollforward (in KB).|  
|**redo_rate**|**bigint**|Media frequenza con cui i record del log viene eseguito rollforward su un determinato database secondario, in kilobyte (KB) al secondo.|  
|**filestream_send_rate**|**bigint**|Velocità alla quale i file FILESTREAM vengono inviati alla replica secondaria (in KB/secondo).|  
|**end_of_log_lsn**|**numeric(25,0)**|Fine locale dell'LSN del log. LSN effettivo che corrisponde all'ultimo record di log nella cache di log sui database primario e secondari. Nella replica primaria, le righe secondarie riflettono la fine dell'LSN del log degli ultimi messaggi di stato inviati dalle repliche secondarie alla replica primaria.<br /><br /> **end_of_log_lsn** riflette un ID di blocco di log riempito con zeri. Non si tratta di un numero di sequenza del file di log (LSN). Per altre informazioni, vedere [informazioni sui valori delle colonne LSN](#LSNcolumns), più avanti in questo argomento.|  
|**last_commit_lsn**|**Numeric(25,0)**|Numero di sequenza del file di log effettivo che corrisponde all'ultimo record di commit nel log delle transazioni.<br /><br /> Sul database primario corrisponde all'ultimo record di commit elaborato. Nelle righe per i database secondari viene mostrato il numero di sequenza del file di log (LSN) inviato dalla replica secondaria alla replica primaria.<br /><br /> Sulla replica secondaria si tratta dell'ultimo record di commit di cui è stato eseguito il rollforward.|  
|**last_commit_time**|**datetime**|Ora che corrisponde all'ultimo record di commit.<br /><br /> Sul database secondario, l'ora equivale a quella sul database primario.<br /><br /> Sulla replica primaria ogni riga del database secondario contiene l'ora in cui la replica secondaria che ospita il database secondario ha riferito alla replica primaria. La differenza oraria tra la riga di database primario e un determinato database secondario rappresenta approssimativamente l'obiettivo punto di ripristino (RPO), presupponendo che il processo di rollforward venga intercettato e che lo stato di avanzamento sia stato riferito alla replica primaria per la replica secondaria.|  
|**low_water_mark_for_ghosts**|**bigint**|Numero a incremento progressivo costante per il database che indica un limite minimo usato dall'attività di pulizia dei record fantasma sul database primario. Se questo numero non aumenta nel tempo, implica che la pulizia dei record fantasma potrebbe non avvenire. Per decidere quali righe fantasma pulire, la replica primaria utilizza il valore minimo di questa colonna per questo database in tutte le repliche di disponibilità, inclusa quella primaria.|  
|**secondary_lag_seconds**|**bigint**|Il numero di secondi durante i quali la replica secondaria si trova dietro la replica primaria durante la sincronizzazione.<br /><br />**Si applica a:**  da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] fino a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
##  <a name="LSNcolumns"></a> Informazioni sui valori delle colonne LSN  
 I valori del **end_of_log_lsn**, **last_hardened_lsn**, **last_received_lsn**, **last_sent_lsn**, **ripristino _lsn**, e **truncation_lsn** colonne non sono numeri di sequenza effettiva del log (LSN). Ognuno di questi valori riflette invece un ID del blocco di log riempito con zeri.  
  
 **end_of_log_lsn**, **last_hardened_lsn**, e **recovery_lsn** sono LSN scaricati. Ad esempio, **last_hardened_lsn** indica l'inizio del blocco successivo oltre i blocchi già presenti su disco.  Pertanto, qualsiasi LSN < il valore di **last_hardened_lsn** è su disco.  Numero LSN che sono > = a questo valore non vengono scaricati.  
  
 Dei valori LSN restituiti da **DM hadr_database_replica_states**, solo **last_redone_lsn** è un LSN effettivo.  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
