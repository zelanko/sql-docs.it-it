---
title: sp_helppublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
author: stevestein
ms.author: sstein
ms.openlocfilehash: 18fc2e1dfadff4e276cd40ff6d64a0aa2fc9a06e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137565"
---
# <a name="sphelppublication-transact-sql"></a>sp_helppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni su una pubblicazione. Per un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pubblicazione, questa stored procedure viene eseguita nel server di pubblicazione nel database di pubblicazione. Per una pubblicazione Oracle, questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione da visualizzare. *pubblicazione* is sysname con valore predefinito è **%** , che restituisce informazioni su tutte le pubblicazioni.  
  
`[ @found = ] 'found' OUTPUT` È un flag per indicare che restituisce righe. *trovato*viene **int** e un parametro di OUTPUT con valore predefinito è **23456**. **1** indica la pubblicazione è stata trovata. **0** indica la pubblicazione non è stata trovata.  
  
`[ @publisher = ] 'publisher'` Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* is sysname con valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere specificato quando si richiedono informazioni sulla pubblicazione da un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|pubid|**int**|ID della pubblicazione.|  
|name|**sysname**|Nome della pubblicazione.|  
|restricted|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**tinyint**|Stato corrente della pubblicazione.<br /><br /> **0** = inattiva.<br /><br /> **1** = attivo.|  
|attività||Disponibile per compatibilità con le versioni precedenti.|  
|replication frequency|**tinyint**|Tipo di frequenza della replica:<br /><br /> **0** = transazionale<br /><br /> **1** = snapshot|  
|synchronization method|**tinyint**|Modalità di sincronizzazione:<br /><br /> **0** = programma per la copia bulk in modalità nativa (**bcp** utilità)<br /><br /> **1** = copia bulk di carattere<br /><br /> **3** = simultanea, ovvero la copia bulk in modalità nativa (**bcp**utilità) viene usato ma durante lo snapshot le tabelle non vengono bloccate<br /><br /> **4** = Concurrent_c, che significa che viene utilizzata la copia bulk di carattere ma durante lo snapshot le tabelle non vengono bloccate|  
|description|**nvarchar(255)**|Descrizione facoltativa della pubblicazione.|  
|immediate_sync|**bit**|Indica se i file di sincronizzazione vengono creati o ricreati a ogni esecuzione dell'agente snapshot.|  
|enabled_for_internet|**bit**|Indica se i file di sincronizzazione della pubblicazione vengono esposti a Internet tramite FTP e altri servizi.|  
|allow_push|**bit**|Indica se per la pubblicazione sono consentite o meno sottoscrizioni push.|  
|allow_pull|**bit**|Indica se per la pubblicazione sono consentite o meno sottoscrizioni pull.|  
|allow_anonymous|**bit**|Indica se per la pubblicazione sono consentite o meno sottoscrizioni anonime.|  
|independent_agent|**bit**|Indica se per la pubblicazione è disponibile un agente di distribuzione autonomo.|  
|immediate_sync_ready|**bit**|Indica se l'agente snapshot ha generato o meno uno snapshot pronto per l'utilizzo nelle nuove sottoscrizioni. Questo parametro viene definito solo se la pubblicazione è configurata in modo che sia sempre disponibile uno snapshot per le sottoscrizioni nuove o reinizializzate.|  
|allow_sync_tran|**bit**|Indica se per la pubblicazione sono consentite sottoscrizioni ad aggiornamento immediato.|  
|autogen_sync_procs|**bit**|Indica se generare automaticamente stored procedure per il supporto di sottoscrizioni ad aggiornamento immediato.|  
|snapshot_jobid|**binary(16)**|ID dell'attività pianificata.|  
|retention|**int**|Quantità di modifiche, espresse in ore, da salvare per la pubblicazione specificata.|  
|has subscription|**bit**|Indica se esistono sottoscrizioni attive della pubblicazione. **1** significa che la pubblicazione esistono sottoscrizioni attive, e **0** significa che non esistono sottoscrizioni della pubblicazione.|  
|allow_queued_tran|**bit**|Specifica se è abilitato o meno l'inserimento in coda delle modifiche apportate nel Sottoscrittore finché non è possibile applicarle al server di pubblicazione. Se **0**, le modifiche del sottoscrittore non vengono inserite in coda.|  
|snapshot_in_defaultfolder|**bit**|Specifica se i file di snapshot sono archiviati nella cartella predefinita. Se **0**, i file di snapshot sono stati archiviati nel percorso alternativo specificato da *alternate_snapshot_folder*. Se **1**, i file di snapshot sono disponibili nella cartella predefinita.|  
|alt_snapshot_folder|**nvarchar(255)**|Specifica la posizione della cartella alternativa per lo snapshot.|  
|pre_snapshot_script|**nvarchar(255)**|Specifica un puntatore a un **con estensione SQL** percorso dei file. L'agente di distribuzione esegue lo script pre-snapshot prima dell'esecuzione di tutti gli script di oggetti replicati durante l'applicazione di uno snapshot in un Sottoscrittore.|  
|post_snapshot_script|**nvarchar(255)**|Specifica un puntatore a un **con estensione SQL** percorso dei file. L'agente di distribuzione esegue lo script post-snapshot dopo l'applicazione di tutti gli altri dati e script di oggetti replicati durante una sincronizzazione iniziale.|  
|compress_snapshot|**bit**|Specifica che lo snapshot che viene scritto il *alt_snapshot_folder* posizione deve essere compresso nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **0** specifica che lo snapshot verrà compresso non.|  
|ftp_address|**sysname**|Indirizzo di rete del servizio FTP per il server di distribuzione. Specifica la posizione in cui i file di snapshot della pubblicazione possono essere prelevati dall'agente di distribuzione o di merge di un Sottoscrittore.|  
|ftp_port|**int**|Numero di porta del servizio FTP per il server di distribuzione.|  
|ftp_subdirectory|**nvarchar(255)**|Specifica la posizione in cui i file di snapshot possono essere prelevati dall'agente di distribuzione o di merge di un Sottoscrittore se la pubblicazione supporta la propagazione degli snapshot tramite FTP.|  
|ftp_login|**sysname**|Nome utente utilizzato per la connessione al servizio FTP.|  
|allow_dts|**bit**|Specifica che la pubblicazione supporta le trasformazioni di dati. **0** specifica che le trasformazioni DTS non sono consentite.|  
|allow_subscription_copy|**bit**|Specifica se la funzionalità che consente di copiare i database di sottoscrizione che sottoscrivono la pubblicazione è abilitata. **0** significa che la copia non è consentita.|  
|centralized_conflicts|**bit**|Specifica se i record dei conflitti vengono archiviati nel server di pubblicazione:<br /><br /> **0** = i record dei conflitti vengono archiviati sia il server di pubblicazione e nel Sottoscrittore che ha causato il conflitto.<br /><br /> **1** = i record dei conflitti vengono archiviati nel server di pubblicazione.|  
|conflict_retention|**int**|Specifica il periodo di memorizzazione dei conflitti, espresso in giorni.|  
|conflict_policy|**int**|Specifica i criteri di risoluzione dei conflitti adottati quando viene utilizzata l'opzione per Sottoscrittori ad aggiornamento in coda. I possibili valori sono i seguenti:<br /><br /> **1** = prevale il server di pubblicazione.<br /><br /> **2** = prevale il sottoscrittore.<br /><br /> **3** = sottoscrizione viene reinizializzata.|  
|queue_type||Specifica il tipo di coda da utilizzare. I possibili valori sono i seguenti:<br /><br /> **MSMQ** = utilizza [!INCLUDE[msCoName](../../includes/msconame-md.md)] Accodamento per archiviare le transazioni.<br /><br /> **SQL** = utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per archiviare le transazioni.<br /><br /> Nota: Supporto per l'accodamento messaggi è stato interrotto.|  
|backward_comp_level||Livello di compatibilità del database. I possibili valori sono i seguenti:<br /><br /> **90** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|Specifica se la pubblicazione è pubblicata nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory???. Un valore pari **1** indica che viene pubblicato e il valore **0** indica che non è pubblicata.|  
|allow_initialize_from_backup|**bit**|Specifica se i Sottoscrittori possono inizializzare una sottoscrizione di questa pubblicazione da un backup anziché da uno snapshot iniziale. **1** significa che le sottoscrizioni possono essere inizializzate da un backup, e **0** indica che essi non è possibile. Per altre informazioni, vedere [inizializzare una sottoscrizione transazionale senza uno Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) una sottoscrizione transazionale senza uno snapshot.|  
|replicate_ddl|**int**|Indica se per la pubblicazione è supportata la replica dello schema. **1** indica che vengono replicate istruzioni di data definition language (DDL) eseguite nel server di pubblicazione, e **0** indica che le istruzioni DDL non vengono replicate. Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).|  
|enabled_for_p2p|**int**|Indica se la pubblicazione può essere utilizzata in una topologia di replica peer-to-peer. **1** indica che la pubblicazione supporta la replica peer-to-peer. Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
|publish_local_changes_only|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**int**|Specifica se la pubblicazione supporta Sottoscrittori non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un valore pari **1** significa che non -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono supportati i sottoscrittori. Un valore pari **0** significa che solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono supportati i sottoscrittori. Per altre informazioni, vedere [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).|  
|enabled_for_p2p_conflictdetection|**int**|Specifica se l'Agente di Distribuzione rileva i conflitti per una pubblicazione abilitata per la replica peer-to-peer. Un valore pari **1** significa che i conflitti vengono rilevati. Per altre informazioni, vedere [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|originator_id|**int**|Specifica un ID per un nodo in una topologia peer-to-peer. Questo ID viene utilizzato per il rilevamento dei conflitti se **enabled_for_p2p_conflictdetection** è impostata su **1**. Per un elenco degli ID che sono già stati utilizzati, eseguire una query sulla tabella di sistema [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) .|  
|p2p_continue_onconflict|**int**|Specifica se l'agente di distribuzione continua a elaborare le modifiche quando viene rilevato un conflitto. Un valore pari **1** significa che l'agente continua a elaborare le modifiche.<br /><br /> **\*\* Attenzione \* \***  è consigliabile usare il valore predefinito **0**. Quando questa opzione è impostata su **1**, l'agente di distribuzione tenta di eseguire la convergenza dei dati nella topologia applicando la riga in conflitto dal nodo con l'ID di origine più elevato. Questo metodo non garantisce la convergenza. Dopo il rilevamento di un conflitto, è necessario assicurarsi che la topologia sia coerente. Per ulteriori informazioni, vedere la sezione relativa alla gestione dei conflitti in [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
|allow_partition_switch|**int**|Specifica se ALTER TABLE... Istruzioni SWITCH possono essere eseguite sul database pubblicato. Per altre informazioni, vedere [Replicare tabelle e indici partizionati](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
|replicate_partition_switch|**int**|Specifica se ALTER TABLE... Istruzioni SWITCH eseguite sul database pubblicato devono essere replicate ai sottoscrittori. Questa opzione è valida solo se *allow_partition_switch* è impostata su **1**.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 sp_helppublication viene utilizzato per la replica snapshot e transazionale.  
  
 sp_helppublication restituisce informazioni su tutte le pubblicazioni di proprietà dell'utente che esegue questa procedura.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server sysadmin nel server di pubblicazione o i membri del ruolo predefinito del database db_owner nel database di pubblicazione o gli utenti nell'elenco di accesso alla pubblicazione possono eseguire sp_helppublication.  
  
 Per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione, solo i membri del ruolo di sysadmin predefinito del server nel server di distribuzione membri del ruolo predefinito del database db_owner nel database di distribuzione o gli utenti nell'elenco di accesso possono eseguire sp_helppublication.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
