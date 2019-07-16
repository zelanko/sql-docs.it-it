---
title: sys.availability_replicas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_replicas_TSQL
- availability_replicas
- sys.availability_replicas
- sys.availability_replicas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_replicas catalog view
ms.assetid: 0a06e9b6-a1e4-4293-867b-5c3f5a8ff62c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6623d6b95dfe0ebd4e45b13d190d8176bcab1a3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942611"
---
# <a name="sysavailabilityreplicas-transact-sql"></a>sys.availability_replicas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Restituisce una riga per ognuna delle repliche di disponibilità che appartiene a un gruppo di disponibilità Always On nel cluster di failover WSFC.  
  
Se l'istanza del server locale non è in grado di comunicare con il cluster di failover WSFC, ad esempio perché il cluster non è attivo o perché è stato perso il quorum, vengono restituite solo le righe delle repliche di disponibilità locali. Tali righe conterranno solo le colonne di dati memorizzate nella cache dei metadati in locale.  
  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|ID univoco della replica.|  
|**group_id**|**uniqueidentifier**|ID univoco del gruppo di disponibilità a cui appartiene la replica.|  
|**replica_metadata_id**|**int**|ID dell'oggetto di metadati locale per le repliche di disponibilità nel motore di database.|  
|**replica_server_name**|**nvarchar(256)**|Nome del server dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita la replica corrente e, per un'istanza non predefinita, il nome dell'istanza.|  
|**owner_sid**|**varbinary(85)**|ID di sicurezza (SID) registrato nell'istanza del server per il proprietario esterno della replica di disponibilità.<br /><br /> NULL per le repliche di disponibilità non locali.|  
|**endpoint_url**|**nvarchar(128)**|Rappresentazione di stringa dell'endpoint del mirroring di database specificato dall'utente usato dalle connessioni tra repliche primarie e secondarie per la sincronizzazione dei dati. Per informazioni sulla sintassi degli URL dell'endpoint, vedere [Specificare l'URL dell'endpoint quando si aggiunge o si modifica una replica di disponibilità &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).<br /><br /> NULL = Impossibile comunicare con il cluster di failover WSFC.<br /><br /> Per modificare questo endpoint, utilizzare l'opzione ENDPOINT_URL del [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione.|  
|**availability_mode**|**tinyint**|Modalità di disponibilità della replica. I valori possibili sono:<br /><br /> 0 &#124; commit asincrono. La replica primaria può eseguire il commit delle transazioni senza attendere che la replica secondaria salvi il log su disco.<br /><br /> 1 &#124; commit sincrono. La replica primaria attende che la replica secondaria salvi la transazione su disco prima di eseguirne il commit.<br /><br />4 &#124; solo configurazione. La replica primaria invia i metadati di configurazione gruppo di disponibilità alla replica in modo sincrono. I dati utente non viene trasmesso alla replica. Disponibile in SQL Server 2017 da CU1 e versioni successive.<br /><br /> Per altre informazioni, vedere [Modalità di disponibilità &#40;gruppi di disponibilità Always On&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).|  
|**availability_mode_desc**|**nvarchar(60)**|Descrizione della **disponibilità\_modalità**, uno di:<br /><br /> ASINCRONO\_COMMIT<br /><br /> SINCRONO\_COMMIT<br /><br /> CONFIGURAZIONE\_SOLO<br /><br /> Per modificare questa modalità di disponibilità di una replica di disponibilità, utilizzare l'opzione AVAILABILITY_MODE del [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione.<br/><br>Non è possibile modificare la modalità di disponibilità di una replica alla configurazione\_ONLY. Non è possibile modificare una configurazione\_replica solo in una replica primaria o secondaria. |  
|**failover\_mode**|**tinyint**|Il [modalità di failover](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) della replica di disponibilità, uno di:<br /><br /> 0 &#124; failover automatico. La replica è una destinazione potenziale per i failover automatici.  Failover automatico è supportato solo se la modalità di disponibilità è impostata su commit sincrono (**disponibilità\_modalità** = 1) e la replica di disponibilità è attualmente sincronizzata.<br /><br /> 1 &#124; failover manuale. Un failover in una replica secondaria impostata sul failover manuale deve essere avviato manualmente dall'amministratore del database. Il tipo di failover eseguito dipenderà dalla sincronizzazione della replica secondaria, come segue:<br /><br /> Se la replica di disponibilità non è sincronizzata o è ancora in fase di sincronizzazione, è possibile eseguire solo il failover forzato (con la possibile perdita di dati).<br /><br /> Se la modalità di disponibilità è impostata su commit sincrono (**disponibilità\_modalità** = 1) e la replica di disponibilità è attualmente sincronizzato, manuale il failover senza perdita di dati può verificarsi.<br /><br /> Per visualizzare un rollup dello stato di sincronizzazione di database di ogni database di disponibilità in una replica di disponibilità, usare il **sincronizzazione\_health** e **sincronizzazione\_integrità\_desc** le colonne delle [sys.dm_hadr_availability_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md) vista a gestione dinamica. Tramite il rollup vengono presi in considerazione lo stato di sincronizzazione di ogni database di disponibilità e la modalità di disponibilità della relativa replica di disponibilità.<br /><br /> **Nota:** Per visualizzare l'integrità della sincronizzazione di un database di disponibilità, eseguire una query di **sincronizzazione\_stato** e **sincronizzazione\_integrità** colonne del [DM hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) vista a gestione dinamica.|  
|**failover\_mode\_desc**|**nvarchar(60)**|Descrizione della **failover\_modalità**, uno di:<br /><br /> MANUAL<br /><br /> AUTOMATIC<br /><br /> Per modificare la modalità di failover, usare il FAILOVER\_opzione della modalità di [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione.|  
|**session\_timeout**|**int**|Periodo di timeout in secondi. Il periodo di timeout è il tempo di attesa massimo rispettato dalla replica per la ricezione di un messaggio da un'altra replica, prima di considerare la connessione tra la replica primaria e secondaria non riuscita. Il timeout della sessione rileva se le repliche secondarie sono connesse alla replica primaria.<br /><br /> Se viene rilevata una connessione non riuscita con una replica secondaria, la replica primaria considera la replica secondaria come non\_SYNCHRONIZED. Se viene rilevata una connessione non riuscita con una replica primaria, una replica secondaria tenta di riconnettersi.<br /><br /> **Nota:** I timeout della sessione non provocano failover automatici.<br /><br /> Per modificare questo valore, usare l'opzione SESSION_TIMEOUT del [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione.|  
|**primario\_ruolo\_Consenti\_connessioni**|**tinyint**|Specifica se la disponibilità consente tutte le connessioni o solo connessioni di lettura e scrittura. I valori possibili sono:<br /><br /> 2 = Tutte (impostazione predefinita)<br /><br /> 3 = lettura e scrittura|  
|**primario\_ruolo\_consentire\_connessioni\_desc**|**nvarchar(60)**|Descrizione della **primari\_ruolo\_consentono\_connessioni**, uno di:<br /><br /> ALL<br /><br /> LEGGERE\_SCRIVERE|  
|**secondari\_ruolo\_Consenti\_connessioni**|**tinyint**|Specifica se una replica di disponibilità che esegue il ruolo secondario, ovvero una replica secondaria, può accettare connessioni dai client. I valori possibili sono:<br /><br /> 0 = No. Non è consentita alcuna connessione ai database nella replica secondaria e i database non sono disponibili per l'accesso in lettura. Questa è l'impostazione predefinita.<br /><br /> 1 = Sola lettura. Sono consentite solo le connessioni di sola lettura ai database nella replica secondaria. Tutti i database nella replica sono disponibili per l'accesso in lettura.<br /><br /> 2 = Tutte. Sono consentite tutte le connessioni ai database nella replica secondaria per l'accesso in sola lettura.<br /><br /> Per altre informazioni, vedere [Repliche secondarie attive: Repliche secondarie leggibili &#40;Gruppi di disponibilità Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).|  
|**secondary_role_allow_connections_desc**|**nvarchar(60)**|Descrizione della **secondary_role_allow_connections**, uno di:<br /><br /> No<br /><br /> READ_ONLY<br /><br /> ALL|  
|**create_date**|**datetime**|Data di creazione della replica.<br /><br /> NULL = La replica non risiede nell'istanza del server.|  
|**modify_date**|**datetime**|Data dell'ultima modifica apportata alla replica.<br /><br /> NULL = La replica non risiede nell'istanza del server.|  
|**backup_priority**|**int**|Rappresenta la priorità specificata dall'utente per l'esecuzione dei backup nella replica rispetto alle altre repliche nello stesso gruppo di disponibilità. Il valore è un numero intero compreso nell'intervallo 0-100.<br /><br /> Per altre informazioni, vedere [Repliche secondarie attive: Backup su repliche secondarie &#40;Gruppi di disponibilità Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**read_only_routing_url**|**nvarchar(256)**|Endpoint di connettività (URL) della replica di disponibilità di sola lettura. Per altre informazioni, vedere [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md).|  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW ANY DEFINITION nell'istanza del server.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
