---
title: sp_addpublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14e35b85b594cadf90a467c5017ac31033bc464b
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493963"
---
# <a name="spaddpublication-transact-sql"></a>sp_addpublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una pubblicazione snapshot o transazionale. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addpublication [ @publication = ] 'publication'  
    [ , [ @taskid = ] tasked ]  
    [ , [ @restricted = ] 'restricted' ]  
    [ , [ @sync_method = ] 'sync_method' ]  
    [ , [ @repl_freq = ] 'repl_freq' ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @status = ] 'status' ]  
    [ , [ @independent_agent = ] 'independent_agent' ]  
    [ , [ @immediate_sync = ] 'immediate_sync' ]  
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]  
    [ , [ @allow_push = ] 'allow_push'  
    [ , [ @allow_pull = ] 'allow_pull' ]  
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]  
    [ , [ @allow_sync_tran = ] 'allow_sync_tran' ]  
    [ , [ @autogen_sync_procs = ] 'autogen_sync_procs' ]  
    [ , [ @retention = ] retention ]  
    [ , [ @allow_queued_tran= ] 'allow_queued_updating' ]  
    [ , [ @snapshot_in_defaultfolder= ] 'snapshot_in_default_folder' ]  
    [ , [ @alt_snapshot_folder= ] 'alternate_snapshot_folder' ]  
    [ , [ @pre_snapshot_script= ] 'pre_snapshot_script' ]  
    [ , [ @post_snapshot_script= ] 'post_snapshot_script' ]  
    [ , [ @compress_snapshot= ] 'compress_snapshot' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port= ] ftp_port ]  
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @allow_dts = ] 'allow_dts' ]  
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]  
    [ , [ @conflict_policy = ] 'conflict_policy' ]  
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @queue_type = ] 'queue_type' ]  
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]  
    [ , [ @logreader_job_name = ] 'logreader_agent_name' ]  
    [ , [ @qreader_job_name = ] 'queue_reader_agent_name' ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @allow_initialize_from_backup = ] 'allow_initialize_from_backup' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @enabled_for_p2p = ] 'enabled_for_p2p' ]  
    [ , [ @publish_local_changes_only = ] 'publish_local_changes_only' ]  
    [ , [ @enabled_for_het_sub = ] 'enabled_for_het_sub' ]  
    [ , [ @p2p_conflictdetection = ] 'p2p_conflictdetection' ]  
    [ , [ @p2p_originator_id = ] p2p_originator_id  
    [ , [ @p2p_continue_onconflict = ] 'p2p_continue_onconflict'  
    [ , [ @allow_partition_switch = ] 'allow_partition_switch'  
    [ , [ @replicate_partition_switch = ]'replicate_partition_switch'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ \@publication = ] 'publication'` È il nome della pubblicazione da creare. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito. Il nome deve essere univoco all'interno del database.  
  
`[ \@taskid = ] taskid` Supportata per compatibilità con le versioni precedenti di sola lettura. usare [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md).  
  
`[ \@restricted = ] 'restricted'` Supportata per compatibilità con le versioni precedenti di sola lettura. usare *default_access*.  
  
`[ \@sync_method = ] _'sync_method'` È la modalità di sincronizzazione. *sync_method* viene **nvarchar(13)**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**native**|Genera l'output in modalità nativa del programma per la copia bulk per tutte le tabelle. *Non supportato per il server di pubblicazione Oracle*.|  
|**character**|Genera l'output in modalità carattere del programma per la copia bulk per tutte le tabelle. _Per un server di pubblicazione Oracle_ **carattere** _è valida solo per la replica snapshot_.|  
|**concurrent**|Genera l'output del programma per la copia bulk in modalità nativa per tutte le tabelle, senza tuttavia bloccare le tabelle durante lo snapshot. Questo valore è supportato solo per pubblicazioni transazionali. *Non supportato per il server di pubblicazione Oracle*.|  
|**concurrent_c**|Genera l'output del programma per la copia bulk in modalità carattere per tutte le tabelle, senza tuttavia bloccare le tabelle durante lo snapshot. Questo valore è supportato solo per pubblicazioni transazionali.|  
|**Snapshot del database**|Genera output del programma in modalità nativa per la copia bulk di tutte le tabelle da uno snapshot del database. Gli snapshot del database non sono disponibili in tutte le edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|**caratteri di snapshot del database**|Genera output del programma in modalità carattere per la copia bulk di tutte le tabelle da uno snapshot del database. Gli snapshot del database non sono disponibili in tutte le edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).|  
|NULL (predefinito)|Per impostazione predefinita **nativi** per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione. Per non -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione, il valore predefinito è **carattere** quando il valore di *repl_freq* viene **Snapshot** e di ottenere **concurrent_c** tutti gli altri casi.|  
  
`[ \@repl_freq = ] 'repl_freq'` È il tipo di frequenza di replica *repl_freq* viene **nvarchar(10)**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Continua** (impostazione predefinita)|Il server di pubblicazione genera l'output per tutte le transazioni basate su log. Per non -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli editori, ciò richiede che *sync_method* essere impostata su **concurrent_c**.|  
|**snapshot**|Il server di pubblicazione genera solo gli eventi di sincronizzazione pianificati. Per non -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli editori, ciò richiede che *sync_method* essere impostata su **carattere**.|  
  
`[ \@description = ] 'description'` È una descrizione facoltativa per la pubblicazione. *Descrizione* viene **nvarchar(255**, con un valore predefinito è NULL.  
  
`[ \@status = ] 'status'` Specifica se i dati della pubblicazione sono disponibili. *lo stato* viene **nvarchar(8)**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**active**|I dati della pubblicazione risultano immediatamente disponibili per i Sottoscrittori.|  
|**inattivo** (impostazione predefinita)|I dati della pubblicazione non sono disponibili per i Sottoscrittori quando viene creata la pubblicazione (è possibile creare una sottoscrizione, che tuttavia non viene elaborata).|  
  
 *Non supportato per il server di pubblicazione Oracle*.  
  
`[ \@independent_agent = ] 'independent_agent'` Specifica se è disponibile un agente di distribuzione autonomo per questa pubblicazione. *independent_agent* viene **nvarchar(5**, con un valore predefinito è FALSE. Se **true**, è disponibile un agente di distribuzione autonomo per la pubblicazione. Se **false**, la pubblicazione utilizza un agente di distribuzione condiviso, e ogni coppia database del server di pubblicazione/sottoscrittore del database ha un solo agente condiviso.  
  
`[ \@immediate_sync = ] 'immediate_synchronization'` Specifica se i file di sincronizzazione per la pubblicazione vengono creati ogni volta che viene eseguito l'agente Snapshot. *solo quando independent_agent* viene **nvarchar(5**, con un valore predefinito è FALSE. Se **true**, i file di sincronizzazione vengono creati o ricreati ogni volta che viene eseguito l'agente Snapshot. Se l'esecuzione dell'agente snapshot viene completata prima della creazione della sottoscrizione, i Sottoscrittori possono ricevere i file di sincronizzazione immediatamente. Le nuove sottoscrizioni ricevono i file di sottoscrizione più recenti generati dall'ultima esecuzione dell'agente snapshot. *independent_agent* deve essere **true** per *solo quando independent_agent* essere **true**. Se **false**, i file di sincronizzazione vengono creati solo se esistono nuove sottoscrizioni. È necessario chiamare [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) per ogni sottoscrizione quando si aggiunge in modo incrementale un nuovo articolo a una pubblicazione esistente. I Sottoscrittori ricevono i file di sincronizzazione dopo la sottoscrizione solo se gli agenti snapshot sono stati avviati e completati.  
  
`[ \@enabled_for_internet = ] 'enabled_for_internet'` Specifica se la pubblicazione è abilitata per Internet e determina se è possibile utilizzare il protocollo di trasferimento di file (FTP) per trasferire i file di snapshot in un sottoscrittore. *enabled_for_internet* viene **nvarchar(5**, con un valore predefinito è FALSE. Se **true**, i file di sincronizzazione per la pubblicazione vengono inseriti nella directory C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\repldata\ftp. La directory Ftp deve essere creata dall'utente.  
  
`[ \@allow_push = ] 'allow_push'` Specifica se è possano creare sottoscrizioni push per la pubblicazione specificata. *allow_push* viene **nvarchar(5**, valore predefinito è TRUE, che consente le sottoscrizioni push nella pubblicazione.  
  
`[ \@allow_pull = ] 'allow_pull'` Specifica se è possano creare sottoscrizioni pull per la pubblicazione specificata. *allow_pull* viene **nvarchar(5**, con un valore predefinito è FALSE. Se **false**, per la pubblicazione non sono consentite sottoscrizioni pull.  
  
`[ \@allow_anonymous = ] 'allow_anonymous'` Specifica se è possano creare sottoscrizioni anonime per la pubblicazione specificata. *allow_anonymous* viene **nvarchar(5**, con un valore predefinito è FALSE. Se **true**, *solo quando independent_agent* deve anche essere impostata su **true**. Se **false**, per la pubblicazione non sono consentite sottoscrizioni anonime.  
  
`[ \@allow_sync_tran = ] 'allow_sync_tran'` Specifica se le sottoscrizioni ad aggiornamento immediato sono consentite nella pubblicazione. *allow_sync_tran* viene **nvarchar(5**, con un valore predefinito è FALSE. **true** viene *non è supportata per server di pubblicazione Oracle*.  
  
`[ \@autogen_sync_procs = ] 'autogen_sync_procs'` Specifica se la stored procedure di sincronizzazione per sottoscrizioni aggiornabili viene generata nel server di pubblicazione. *autogen_sync_procs* viene **nvarchar(5**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**true**|Questo valore viene impostato automaticamente quando sono abilitate le sottoscrizioni aggiornabili.|  
|**false**|Questo valore viene impostato automaticamente quando non sono abilitate le sottoscrizioni aggiornabili oppure per server di pubblicazione Oracle.|  
|NULL (predefinito)|Per impostazione predefinita **true** quando le sottoscrizioni aggiornabili è abilitata e alla **false** quando le sottoscrizioni ad aggiornamento non è abilitato.|  
  
> [!NOTE]  
>  Valore fornito dall'utente *autogen_sync_procs*verrà ignorato in base ai valori specificati per *allow_queued_tran* e *allow_sync_tran*.  
  
`[ \@retention = ] retention` È il periodo di conservazione in ore, per attività di sottoscrizione. *conservazione* viene **int**, con un valore predefinito è 336 ore. Se una sottoscrizione non viene attivata entro il periodo di memorizzazione, scade e viene rimossa. Il valore di questo parametro può essere maggiore del periodo di memorizzazione massimo del database di distribuzione utilizzato dal server di pubblicazione. Se **0**, noto delle sottoscrizioni della pubblicazione non scadono mai e rimosse dall'agente di pulizia di sottoscrizione scaduta.  
  
`[ \@allow_queued_tran = ] 'allow_queued_updating'` Abilita o disabilita l'accodamento delle modifiche nel Sottoscrittore finché possono essere applicate nel server di pubblicazione. *allow_queued_updating* viene **nvarchar(5** con valore predefinito è FALSE. Se **false**, le modifiche del sottoscrittore non vengono inserite in coda. **true** viene *non è supportata per server di pubblicazione Oracle*.  
  
`[ \@snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'` Specifica se i file di snapshot sono archiviati nella cartella predefinita. *snapshot_in_default_folder* viene **nvarchar(5** con valore predefinito è TRUE. Se **true**, i file di snapshot sono disponibili nella cartella predefinita. Se **false**, i file di snapshot sono stati archiviati nel percorso alternativo specificato da *alternate_snapshot_folder*. Le posizioni alternative possono essere un altro server, un'unità di rete oppure un supporto rimovibile, ad esempio un CD o un disco rimovibile. È inoltre possibile archiviare i file di snapshot in un sito FTP in modo che possano essere successivamente recuperati dal Sottoscrittore. Si noti che questo parametro può essere true e un percorso non è stato  **\@alt_snapshot_folder** parametro. Tale combinazione indica che i file di snapshot vengono archiviati sia nella posizione predefinita che in posizioni alternative.  
  
`[ \@alt_snapshot_folder = ] 'alternate_snapshot_folder'` Specifica il percorso della cartella alternativa per lo snapshot. *alternate_snapshot_folder* viene **nvarchar(255** con valore predefinito è NULL.  
  
`[ \@pre_snapshot_script = ] 'pre_snapshot_script'` Specifica un puntatore a un **con estensione SQL** percorso dei file. *pre_snapshot_script* viene **nvarchar(255,** con valore predefinito è NULL. L'agente di distribuzione esegue lo script pre-snapshot prima dell'esecuzione di tutti gli script di oggetti replicati durante l'applicazione di uno snapshot in un Sottoscrittore. Lo script viene eseguito nel contesto di sicurezza utilizzato dall'agente di distribuzione per la connessione al database di sottoscrizione.  
  
`[ \@post_snapshot_script = ] 'post_snapshot_script'` Specifica un puntatore a un **con estensione SQL** percorso dei file. *post_snapshot_script* viene **nvarchar(255**, con un valore predefinito è NULL. L'agente di distribuzione esegue lo script post-snapshot dopo l'applicazione di tutti gli altri dati e script di oggetti replicati durante una sincronizzazione iniziale. Lo script viene eseguito nel contesto di sicurezza utilizzato dall'agente di distribuzione per la connessione al database di sottoscrizione.  
  
`[ \@compress_snapshot = ] 'compress_snapshot'` Specifica che lo snapshot che viene scritto il  **\@alt_snapshot_folder** posizione deve essere compresso nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. *compress_snapshot* viene **nvarchar(5**, con un valore predefinito è FALSE. **false** specifica che non lo snapshot verrà compresso; **true** specifica che lo snapshot verrà compresso. I file di snapshot con una dimensione superiore a 2 gigabyte (GB) non possono essere compressi. I file di snapshot compressi vengono decompressi nella posizione in cui viene eseguito l'agente di distribuzione. Per le sottoscrizioni pull in genere vengono utilizzati snapshot compressi in modo che i file vengano decompressi nel Sottoscrittore. Non è possibile comprimere lo snapshot all'interno della cartella predefinita.  
  
`[ \@ftp_address = ] 'ftp_address'` È l'indirizzo di rete del servizio FTP per il server di distribuzione. *ftp_address* viene **sysname**, con un valore predefinito è NULL. Specifica la posizione in cui i file di snapshot della pubblicazione possono essere prelevati dall'agente di distribuzione o di merge di un Sottoscrittore. Poiché questa proprietà viene archiviata per ogni pubblicazione, ogni pubblicazione può essere associato un diverso *ftp_address*. La pubblicazione deve supportare la propagazione di snapshot tramite FTP.  
  
`[ \@ftp_port = ] ftp_port` È il numero di porta del servizio FTP per il server di distribuzione. *ftp_port* viene **int**, con un valore predefinito è 21. Specifica la posizione dei file di snapshot della pubblicazione, dove i file possono essere prelevati dall'agente di distribuzione o di merge di un Sottoscrittore. Poiché questa proprietà viene archiviata per ogni pubblicazione, ogni pubblicazione può avere un proprio *ftp_port*.  
  
`[ \@ftp_subdirectory = ] 'ftp_subdirectory'` Specifica in cui i file di snapshot saranno disponibili per l'agente di distribuzione o dell'agente di Merge del sottoscrittore per prelevare se la pubblicazione supporta la propagazione di snapshot tramite FTP. *ftp_subdirectory* viene **nvarchar(255**, con un valore predefinito è NULL. Poiché questa proprietà viene archiviata per ogni pubblicazione, ogni pubblicazione può avere un proprio *ftp_subdirctory* oppure scegliere di non utilizzare una sottodirectory con un valore NULL.  
  
`[ \@ftp_login = ] 'ftp_login'` È il nome utente usato per connettersi al servizio FTP. *ftp_login* viene **sysname**, predefinito è anonimo.  
  
`[ \@ftp_password = ] 'ftp_password'` Password utente utilizzata per connettersi al servizio FTP. *ftp_password* viene **sysname**, con un valore predefinito è NULL.  
  
`[ \@allow_dts = ] 'allow_dts'` Specifica che la pubblicazione consente le trasformazioni dei dati. Quando si crea una sottoscrizione, è possibile specificare un pacchetto DTS. *allow_transformable_subscriptions* viene **nvarchar(5** con un valore predefinito è FALSE, che non consente trasformazioni DTS. Quando *allow_dts* è true, *sync_method* deve essere impostato su **carattere** oppure **concurrent_c**.  
  
 **true** viene *non è supportata per server di pubblicazione Oracle*.  
  
`[ \@allow_subscription_copy = ] 'allow_subscription_copy'` Abilita o disabilita la possibilità di copiare i database di sottoscrizione che sottoscrivono la pubblicazione. *allow_subscription_copy* viene**nvarchar(5**, con un valore predefinito è FALSE.  
  
`[ \@conflict_policy = ] 'conflict_policy'` Specifica i criteri di risoluzione dei conflitti adottati quando viene utilizzata l'opzione per sottoscrittori ad aggiornamento in coda. *conflict_policy* viene **nvarchar(100)** con valore predefinito è NULL, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**wins pub**|Prevale il server di pubblicazione.|  
|**sub reinit**|Reinizializzare la sottoscrizione.|  
|**Sub wins**|Prevale il Sottoscrittore.|  
|NULL (predefinito)|Se NULL e la pubblicazione è una pubblicazione snapshot, i criteri predefiniti diventano **sub reinit**. Se NULL e la pubblicazione non è una pubblicazione snapshot, il valore predefinito diventa **wins pub**.|  
  
 *Non supportato per il server di pubblicazione Oracle*.  
  
`[ \@centralized_conflicts = ] 'centralized_conflicts'` Specifica se i record con conflitti vengono archiviati nel server di pubblicazione. *centralized_conflicts* viene **nvarchar(5**, con un valore predefinito è TRUE. Se **true**, i record con conflitti vengono archiviati nel server di pubblicazione. Se **false**, i record con conflitti vengono archiviati sia il server di pubblicazione e nel Sottoscrittore che ha causato il conflitto. *Non supportato per il server di pubblicazione Oracle*.  
  
`[ \@conflict_retention = ] conflict_retention` Specifica il periodo di memorizzazione dei conflitti, in giorni. Si tratta del periodo di tempo durante il quale i metadati dei conflitti rimangono archiviati per la replica transazionale peer-to-peer e le sottoscrizioni ad aggiornamento in coda. *conflict_retention* viene **int**, con un valore predefinito è 14. *Non supportato per il server di pubblicazione Oracle*.  
  
`[ \@queue_type = ] 'queue_type'` Specifica il tipo di coda viene utilizzato. *queue_type* viene **nvarchar(10)**, con un valore predefinito è NULL, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**sql**|Consente di utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'archiviazione delle transazioni.|  
|NULL (predefinito)|Per impostazione predefinita **sql**, che consente di utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per archiviare le transazioni.|  
  
> [!NOTE]  
>  L'utilizzo di MSMQ ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing) non è più supportato. Se si specifica un valore di **msmq** genererà un avviso e replica imposterà automaticamente il valore su **sql**.  
  
 *Non supportato per il server di pubblicazione Oracle*.  
  
`[ \@add_to_active_directory = ] 'add\to_active_directory'` Questo parametro è stato deprecato ed è supportato solo per la compatibilità con le versioni precedenti di script. Non è più possibile aggiungere informazioni di pubblicazione in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.  
  
`[ \@logreader_job_name = ] 'logreader_agent_name'` È il nome di un processo dell'agente esistente. *logreader_agent_name* viene **sysname**, con un valore predefinito NULL. Questo parametro viene specificato solo quando l'agente di lettura log utilizzerà un processo esistente anziché uno nuovo.  
  
`[ \@qreader_job_name = ] 'queue_reader_agent_name'` È il nome di un processo dell'agente esistente. *queue_reader_agent_name* viene **sysname**, con un valore predefinito NULL. Questo parametro viene specificato solo quando l'agente di lettura coda utilizzerà un processo esistente anziché uno nuovo.  
  
`[ \@publisher = ] 'publisher'` Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzato durante l'aggiunta di una pubblicazione per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
`[ \@allow_initialize_from_backup = ] 'allow_initialize_from_backup'` Indica se i sottoscrittori possono inizializzare una sottoscrizione per questa pubblicazione da un backup anziché da uno snapshot iniziale. *allow_initialize_from_backup* viene **nvarchar(5**, i possibili valori sono i seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**true**|Abilita l'inizializzazione da un backup.|  
|**false**|Disabilita l'inizializzazione da un backup.|  
|NULL (predefinito)|Per impostazione predefinita **true** per una pubblicazione in una topologia di replica peer-to-peer e **false** per tutte le altre pubblicazioni.|  
  
 Per altre informazioni, vedere [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!WARNING]  
>  Per evitare la mancanza di dati del Sottoscrittore, quando si utilizza **sp_addpublication** con `@allow_initialize_from_backup = N'true'`, utilizzare sempre `@immediate_sync = N'true'`.  
  
`[ \@replicate_ddl = ] replicate_ddl` Indica se la replica dello schema è supportata per la pubblicazione. *replicate_ddl* viene **int**, il valore predefinito è **1** per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione e **0** per non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione. **1** indica che vengono replicate istruzioni di data definition language (DDL) eseguite nel server di pubblicazione, e **0** indica che le istruzioni DDL non vengono replicate. *La replica dello schema non è supportata per server di pubblicazione Oracle.* Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Il  *\@replicate_ddl* parametro viene rispettato quando un'istruzione DDL aggiunge una colonna. Il  *\@replicate_ddl* parametro viene ignorato quando un'istruzione DDL modifica o elimina una colonna per i motivi seguenti.  
  
-   Quando viene eliminata una colonna, è necessario aggiornare sysarticlecolumns per evitare che le nuove istruzioni DML dall'inclusione della colonna eliminata causando l'esito negativo dell'agente di distribuzione. Il  *\@replicate_ddl* parametro viene ignorato perché la replica deve replicare sempre la modifica dello schema.  
  
-   Quando una colonna viene modificata, è probabile che venga modificato il tipo di dati di origine o il supporto dei valori Null, di conseguenza le istruzioni DML contengono un valore che potrebbe non essere compatibile con la tabella nel Sottoscrittore. Tali istruzioni DML potrebbero determinare la mancata esecuzione dell'agente di distribuzione. Il  *\@replicate_ddl* parametro viene ignorato perché la replica deve replicare sempre la modifica dello schema.  
  
-   Quando un'istruzione DDL aggiunge una nuova colonna, sysarticlecolumns non include la nuova colonna. Le istruzioni DML non tenteranno di replicare i dati per la nuova colonna. Il parametro viene rispettato perché la replica o la non replica di DDL è accettabile.  
  
`[ \@enabled_for_p2p = ] 'enabled_for_p2p'` Consente la pubblicazione da usare in una topologia di replica peer-to-peer. *enabled_for_p2p* viene **nvarchar(5**, con un valore predefinito è FALSE. **true** indica che la pubblicazione supporta la replica peer-to-peer. Quando si impostano *enabled_for_p2p* al **true**, si applicano le restrizioni seguenti:  
  
-   *allow_anonymous* deve essere **false**.  
  
-   *allow_dts* deve essere **false**.  
  
-   *allow_initialize_from_backup* deve essere **true**.  
  
-   *allow_queued_tran* deve essere **false**.  
  
-   *allow_sync_tran* deve essere **false**.  
  
-   *conflict_policy* deve essere **false**.  
  
-   *independent_agent* deve essere **true**.  
  
-   *repl_freq* deve essere **continua**.  
  
-   *replicate_ddl* deve essere **1**.  
  
 Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
`[ \@publish_local_changes_only = ] 'publish_local_changes_only'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ \@enabled_for_het_sub = ] 'enabled_for_het_sub'` Consente la pubblicazione per il supporto non -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori. *enabled_for_het_sub* viene **nvarchar(5** con valore predefinito è false. Un valore pari **true** significa che la pubblicazione supporti non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori. Quando *enabled_for_het_sub* viene **true**, si applicano le restrizioni seguenti:  
  
-   *allow_initialize_from_backup* deve essere **false**.  
  
-   *allow_push* deve essere **true**.  
  
-   *allow_queued_tran* deve essere **false**.  
  
-   *allow_subscription_copy* deve essere **false**.  
  
-   *allow_sync_tran* deve essere **false**.  
  
-   *autogen_sync_procs* deve essere **false**.  
  
-   *conflict_policy* deve essere NULL.  
  
-   *enabled_for_internet* deve essere **false**.  
  
-   *enabled_for_p2p* deve essere **false**.  
  
-   *ftp_address* deve essere NULL.  
  
-   *ftp_subdirectory* deve essere NULL.  
  
-   *ftp_password* deve essere NULL.  
  
-   *pre_snapshot_script* deve essere NULL.  
  
-   *post_snapshot_script* deve essere NULL.  
  
-   *replicate_ddl* deve essere 0.  
  
-   *qreader_job_name* deve essere NULL.  
  
-   *queue_type* deve essere NULL.  
  
-   *sync_method* non può essere **nativo** oppure **simultanee**.  
  
 Per altre informazioni, vedere [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
`[ \@p2p_conflictdetection = ] 'p2p_conflictdetection'` Abilita l'agente di distribuzione rilevare i conflitti se la pubblicazione è abilitata per la replica peer-to-peer. *p2p_conflictdetection* viene **nvarchar(5** con valore predefinito è true. Per altre informazioni, vedere [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
`[ \@p2p_originator_id = ] p2p_originator_id` Specifica un ID per un nodo in una topologia peer-to-peer. *p2p_originator_id* viene **int**, con un valore predefinito è NULL. Questo ID viene utilizzato per il rilevamento dei conflitti se *p2p_conflictdetection* è impostata su TRUE. Specificare un ID positivo diverso da zero che non sia mai stato utilizzato nella topologia. Per un elenco di ID che sono già stati utilizzati, eseguire [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).  
  
`[ \@p2p_continue_onconflict = ] 'p2p_continue_onconflict'` Determina se l'agente di distribuzione continua a elaborare le modifiche apportate dopo che è stato rilevato un conflitto. *p2p_continue_onconflict* viene **nvarchar(5** con valore predefinito è false.  
  
> [!CAUTION]  
>  È consigliabile utilizzare il valore predefinito FALSE. Quando questa opzione è impostata su TRUE, l'agente di distribuzione tenta di garantire la convergenza dei dati nella topologia applicando la riga in conflitto dal nodo con ID di origine maggiore. Questo metodo non garantisce la convergenza. Dopo il rilevamento di un conflitto, è necessario assicurarsi che la topologia sia coerente. Per ulteriori informazioni, vedere la sezione relativa alla gestione dei conflitti in [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
  
`[ \@allow_partition_switch = ] 'allow_partition_switch'` Specifica se ALTER TABLE... Istruzioni SWITCH possono essere eseguite sul database pubblicato. *allow_partition_switch* viene **nvarchar(5** con valore predefinito è false. Per altre informazioni, vedere [Replicare tabelle e indici partizionati](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
`[ \@replicate_partition_switch = ] 'replicate_partition_switch'` Specifica se ALTER TABLE... Istruzioni SWITCH eseguite sul database pubblicato devono essere replicate ai sottoscrittori. *replicate_partition_switch* viene **nvarchar(5** con valore predefinito è false. Questa opzione è valida solo se *allow_partition_switch* è impostata su TRUE.  

## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addpublication** viene utilizzata nella replica snapshot e transazionale.  
  
 Se esistono più pubblicazioni che pubblicano lo stesso oggetto di database, solo per le pubblicazioni con un *replicate_ddl* pari a **1** replicherà ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION, e Istruzioni ALTER TRIGGER DDL. Una istruzione ALTER TABLE DROP COLUMN DDL verrà tuttavia replicata da tutte le pubblicazioni che stanno pubblicando la colonna eliminata.  
  
 La replica DDL abilitato (*replicate_ddl* = **1**) per una pubblicazione, affinché le DDL da non replicare le modifiche della pubblicazione [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) devono essere eseguite prima di tutto per impostare *replicate_ddl* al **0**. Dopo le istruzioni DDL da non replicare, [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) può essere eseguito nuovamente per riattivare la replica DDL.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addpublication**. Gli account di accesso con autenticazione di Windows devono disporre di un account utente nel database che rappresenta il proprio account utente di Windows. Un account utente che rappresenta un gruppo di Windows non è sufficiente.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
