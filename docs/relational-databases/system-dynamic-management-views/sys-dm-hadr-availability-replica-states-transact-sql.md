---
title: sys.dm_hadr_availability_replica_states (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 05964e0557cb08e874424af542b8fc8a57ce0835
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900617"
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni replica locale e una riga per ogni replica remota nello stesso gruppo di disponibilità Always On di una replica locale. Ogni riga contiene informazioni sullo stato di una determinata replica.  
  
> [!IMPORTANT]  
>  Per ottenere informazioni su ogni replica in un gruppo di disponibilità, eseguire una query **sys.dm_hadr_availability_replica_states** nell'istanza del server che ospita la replica primaria. Se si eseguono query su questa DMV in un'istanza del server che ospita una replica secondaria di un gruppo di disponibilità, questa vista restituisce solo informazioni locali per il gruppo di disponibilità.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Identificatore univoco della replica.|  
|**group_id**|**uniqueidentifier**|Identificatore univoco del gruppo di disponibilità.|  
|**is_local**|**bit**|Se la replica è locale, uno di:<br /><br /> 0 = Indica una replica secondaria remota in un gruppo di disponibilità la cui replica primaria è ospitata dall'istanza del server locale. Questo valore si verifica solo sul percorso della replica primaria.<br /><br /> 1 = indica una replica locale. Sulle repliche secondarie, è l'unico valore disponibile per il gruppo di disponibilità a cui appartiene la replica.|  
|**role**|**tinyint**|Corrente [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ruolo di una replica locale o una replica remota connessa, uno di:<br /><br /> 0 = Risoluzione<br /><br /> 1 = Primaria<br /><br /> 2 = Secondaria<br /><br /> Per informazioni sui ruoli di [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], vedere [Panoramica di Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|**role_desc**|**nvarchar(60)**|Descrizione della **ruolo**, uno di:<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|Stato operativo corrente della replica, uno di:<br /><br /> 0 = Failover in sospeso<br /><br /> 1 = in sospeso<br /><br /> 2 = Online<br /><br /> 3 = non in linea<br /><br /> 4 = operazione non riuscita<br /><br /> 5 = Non completato, nessun quorum<br /><br /> Null = La replica non è locale.<br /><br /> Per altre informazioni, vedere [ruoli e stati operativi](#RolesAndOperationalStates), più avanti in questo argomento.|  
|**operational\_state\_desc**|**nvarchar(60)**|Descrizione della **operativa\_stato**, uno di:<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**ripristino\_integrità**|**tinyint**|Rollup delle **database\_stato** colonna del [DM hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) vista a gestione dinamica. Di seguito sono i valori possibili e le relative descrizioni.<br /><br /> 0: In corso.  Almeno un database unito in join nello stato di un database diverso da ONLINE (**database\_stato** è non 0).<br /><br /> 1: In linea. Tutti i database aggiunti hanno uno stato database ONLINE (**database_state** è 0).<br /><br /> NULL: **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|Descrizione della **recovery_health**, uno di:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization\_health**|**tinyint**|Riflette un rollup dello stato di sincronizzazione del database (**synchronization_state**) di tutti i database di disponibilità unita (noto anche come *repliche*) e la modalità di disponibilità del (replica modalità con commit sincrono o asincrono). Il rollup rifletterà lo stato accumulato meno integro dei database nella replica. Di seguito sono i valori possibili e le relative descrizioni.<br /><br /> 0: Non è integro.   Almeno un database di cui è stato creato un join si trova nello stato NOT SYNCHRONIZING.<br /><br /> 1: Parzialmente integro. Alcune repliche non sono nello stato di sincronizzazione di destinazione: le repliche con commit sincrono devono trovarsi nello stato Sincronizzato, mentre le repliche con commit asincrono devono trovarsi nello stato Sincronizzazione in corso.<br /><br /> 2: Integro. Tutte le repliche sono nello stato di sincronizzazione di destinazione: le repliche con commit sincrono si trovano nello stato Sincronizzato, mentre le repliche con commit asincrono si trovano nello stato Sincronizzazione in corso.|  
|**synchronization_health_desc**|**nvarchar(60)**|Descrizione della **synchronization_health**, uno di:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|Se una replica secondaria è attualmente connessa alla replica primaria. I valori possibili sono illustrati di seguito con le relative descrizioni.<br /><br /> 0: Disconnesso La risposta di una replica di disponibilità per lo stato DISCONNECTED dipende dal relativo ruolo: Nella replica primaria, se una replica secondaria è disconnessa, i database secondari sono contrassegnati come NOT SYNCHRONIZED sulla replica primaria, che attende la secondaria venga riconnessa; In una replica secondaria, dopo avere rilevato che è disconnessa, la replica secondaria tenta di riconnettersi alla replica primaria.<br /><br /> 1: Connesso.<br /><br /> Ogni replica primaria tiene traccia dello stato di connessione per ogni replica secondaria nello stesso gruppo di disponibilità. Le repliche secondarie tengono traccia dello stato di connessione della sola replica primaria.|  
|**connected_state_desc**|**nvarchar(60)**|Descrizione della **connection_state**, uno di:<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|Numero dell'ultimo errore di connessione.|  
|**last_connect_error_description**|**nvarchar(1024)**|Testo del **last_connect_error_number** messaggio.|  
|**last_connect_error_timestamp**|**datetime**|Data e ora di timestamp che indicano quando le **last_connect_error_number** si è verificato un errore.|  
  
##  <a name="RolesAndOperationalStates"></a> Ruoli e stati operativi  
 Il ruolo **ruolo**, riflette lo stato di una replica di disponibilità e lo stato operativo, **operational_state**, descrive se la replica è pronta per elaborare le richieste client per tutti i database della replica di disponibilità. Di seguito è riportato un riepilogo degli stati operativi possibili per ogni ruolo: RESOLVING, PRIMARY e SECONDARY.  
  
 **RISOLUZIONE:** Quando una replica di disponibilità è il ruolo RESOLVING, gli stati operativi possibili sono come illustrato nella tabella seguente.  
  
|Stato operativo|Descrizione|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|È in corso l'elaborazione di un comando di failover per il gruppo di disponibilità.|  
|OFFLINE|Tutti i dati di configurazione per la replica di disponibilità sono stati aggiornati sul cluster WSFC e anche nei metadati locali, ma attualmente nel gruppo di disponibilità non è presente alcuna replica primaria.|  
|FAILED|Errore di lettura nel tentativo di recuperare informazioni dal cluster WSFC.|  
|FAILED_NO_QUORUM|Il nodo WSFC locale non dispone di quorum. Si tratta di uno stato derivato.|  
  
 **PRIMARIO:** Se una replica di disponibilità esegue il ruolo primario, è attualmente la replica primaria. Gli stati operativi possibili sono come illustrato nella tabella seguente.  
  
|Stato operativo|Descrizione|  
|-----------------------|-----------------|  
|PENDING|Si tratta di uno stato temporaneo, tuttavia una replica primaria può rimanere bloccata in questo stato se i thread di lavoro non elaborano le richieste.|  
|ONLINE|La risorsa del gruppo di disponibilità è online e tutti i thread di lavoro del database sono stati prelevati.|  
|FAILED|La replica di disponibilità non è in grado di leggere e/o scrivere dal cluster WSFC.|  
  
 **DATABASE SECONDARIO:** Se una replica di disponibilità esegue il ruolo secondario, è attualmente una replica secondaria. Gli stati operativi possibili sono come illustrato nella tabella seguente.  
  
|Stato operativo|Descrizione|  
|-----------------------|-----------------|  
|ONLINE|La replica secondaria locale è connessa alla replica primaria.|  
|FAILED|La replica secondaria locale non è in grado di leggere e/o scrivere dal cluster WSFC.|  
|NULL|Su una replica primaria, questo valore viene restituito quando la riga è correlata a una replica secondaria.|  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
