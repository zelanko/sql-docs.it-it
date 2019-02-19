---
title: sp_changepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5cdd5f3b4c4c1dd8ddac0df34423834c3b09b839
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131241"
---
# <a name="spchangepublication-transact-sql"></a>sp_changepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di modificare le proprietà di una pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_changepublication [ [ @publication = ] 'publication' ]  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication =** ] **'**_pubblicazione_**'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@property =** ] **'**_proprietà_**'**  
 Proprietà della pubblicazione da modificare. *proprietà* viene **nvarchar(255**.  
  
 [  **@value =** ] **'**_valore_**'**  
 Nuovo valore della proprietà. *valore* viene **nvarchar(255**, con un valore predefinito è NULL.  
  
 Nella tabella seguente vengono descritte le proprietà della pubblicazione che è possibile modificare e le limitazioni previste per i valori di tali proprietà.  
  
|Proprietà|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|È possibile creare sottoscrizioni anonime per la pubblicazione specificata, e *immediate_sync* deve essere anche **true**. Non è possibile modificare questa proprietà per pubblicazioni peer-to-peer.|  
||**false**|Non è consentito creare sottoscrizioni anonime per la pubblicazione specificata. Non è possibile modificare questa proprietà per pubblicazioni peer-to-peer.|  
|**allow_initialize_from_backup**|**true**|I Sottoscrittori possono inizializzare una sottoscrizione di questa pubblicazione da un backup anziché da uno snapshot iniziale. Questa proprietà non può essere modificata per non -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pubblicazioni.|  
||**false**|I Sottoscrittori devono utilizzare lo snapshot iniziale. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**allow_partition_switch**|**true**|ISTRUZIONE ALTER TABLE... Istruzioni SWITCH possono essere eseguite sul database pubblicato. Per altre informazioni, vedere [Replicare tabelle e indici partizionati](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**false**|ISTRUZIONE ALTER TABLE... Istruzioni SWITCH non possono essere eseguite sul database pubblicato.|  
|**allow_pull**|**true**|È consentita la creazione di sottoscrizioni pull per la pubblicazione specificata. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|Non è consentita la creazione di sottoscrizioni pull per la pubblicazione specificata. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**allow_push**|**true**|È consentita la creazione di sottoscrizioni push per la pubblicazione specificata.|  
||**false**|Non è consentita la creazione di sottoscrizioni push per la pubblicazione specificata.|  
|**allow_subscription_copy**|**true**|Attiva la funzionalità che consente di copiare i database che sottoscrivono la pubblicazione. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|Disabilita la funzionalità che consente di copiare i database che sottoscrivono la pubblicazione. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**alt_snapshot_folder**||Posizione della cartella alternativa per lo snapshot.|  
|**centralized_conflicts**|**true**|I record con conflitti vengono archiviati nel server di pubblicazione. È possibile modificare questa proprietà solo se non esistono sottoscrizioni attive. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|I record dei conflitti vengono archiviati sia nel server di pubblicazione che nel Sottoscrittore che ha causato il conflitto. È possibile modificare questa proprietà solo se non esistono sottoscrizioni attive. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**compress_snapshot**|**true**|Lo snapshot in una cartella snapshot alternativa viene compresso nel formato di file CAB. Non è possibile comprimere lo snapshot all'interno della cartella snapshot predefinita.|  
||**false**|Lo snapshot non viene compresso, come previsto dall'impostazione predefinita per la replica.|  
|**conflict_policy**|**wins pub**|Criteri di risoluzione dei conflitti per Sottoscrittori aggiornabili in base a cui prevale il server di pubblicazione. È possibile modificare questa proprietà solo se non esistono sottoscrizioni attive. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
||**sub reinit**|Criterio di risoluzione dei conflitti per Sottoscrittori aggiornabili in base a cui la sottoscrizione deve essere reinizializzata se si verifica un conflitto. È possibile modificare questa proprietà solo se non esistono sottoscrizioni attive. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
||**Sub wins**|Criteri di risoluzione dei conflitti per Sottoscrittori aggiornabili in base a cui prevale il Sottoscrittore. È possibile modificare questa proprietà solo se non esistono sottoscrizioni attive. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**conflict_retention**||**int** che specifica il periodo di memorizzazione dei conflitti, in giorni. L'impostazione predefinita è 14 giorni. **0** significa che non è necessaria alcuna operazione di pulizia dei conflitti. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**description**||Voce facoltativa di descrizione della pubblicazione.|  
|**enabled_for_het_sub**|**true**|Abilita il supporto dei Sottoscrittori non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella pubblicazione. **enabled_for_het_sub** non può essere modificata quando sono presenti sottoscrizioni della pubblicazione. Potrebbe essere necessario eseguire [replica Stored procedure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) ai fini della conformità con i requisiti seguenti prima di impostare **enabled_for_het_sub** su true:<br /> - **allow_queued_tran** deve essere **false**.<br /> - **allow_sync_tran** deve essere **false**.<br /> Modificando **enabled_for_het_sub** al **true** potrebbe modificare le impostazioni di pubblicazione esistenti. Per altre informazioni, vedere [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|La pubblicazione non supporta Sottoscrittori non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**enabled_for_internet**|**true**|La pubblicazione è abilitata per Internet ed è possibile utilizzare FTP (File Transfer Protocol) per il trasferimento dei file di snapshot in un Sottoscrittore. I file di sincronizzazione per la pubblicazione vengono inseriti nella directory seguente: C:\Programmi\Microsoft SQL Server\MSSQL\Repldata\Ftp. *ftp_address* non può essere NULL. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**false**|La pubblicazione non è abilitata per Internet. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**enabled_for_p2p**|**true**|La pubblicazione supporta la replica peer-to-peer. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /> Per impostare **enabled_for_p2p** al **true**, si applicano le restrizioni seguenti:<br /> - **allow_anonymous** deve essere **false**<br /> - **allow_dts** deve essere **false**.<br /> - **allow_initialize_from_backup** deve essere **true**<br /> - **allow_queued_tran** deve essere **false**.<br /> - **allow_sync_tran** deve essere **false**.<br /> - **enabled_for_het_sub** deve essere **false**.<br /> - **independent_agent** deve essere **true**.<br /> - **repl_freq** deve essere **continua**.<br /> - **replicate_ddl** deve essere **1**.|  
||**false**|La pubblicazione non supporta la replica peer-to-peer. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_address**||Percorso accessibile tramite FTP dei file di snapshot della pubblicazione. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_login**||Nome utente utilizzato per la connessione al servizio FTP. Il valore ANONYMOUS è supportato. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_password**||Password del nome utente utilizzato per la connessione al servizio FTP. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_port**||Numero di porta del servizio FTP per il server di distribuzione. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ftp_subdirectory**||Specifica la posizione in cui vengono creati i file di snapshot se la pubblicazione supporta la propagazione di snapshot tramite FTP. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**immediate_sync**|**true**|I file di sincronizzazione della pubblicazione vengono creati o ricreati a ogni esecuzione dell'agente snapshot. Se l'esecuzione dell'agente snapshot è stata completata una volta prima della sottoscrizione, i Sottoscrittori possono ricevere i file di sincronizzazione immediatamente dopo la sottoscrizione. Le nuove sottoscrizioni ricevono i file di sottoscrizione più recenti generati dall'ultima esecuzione dell'agente snapshot. *independent_agent* deve essere inoltre **true**. Vedere la sezione Osservazioni di seguito per altre informazioni **immediate_sync**.|  
||**false**|I file di sincronizzazione vengono creati solo se esistono nuove sottoscrizioni. I Sottoscrittori ricevono i file di sincronizzazione dopo la sottoscrizione solo se l'agente snapshot è stato avviato e completato.|  
|**independent_agent**|**true**|Per la pubblicazione viene utilizzato un agente di distribuzione dedicato.|  
||**false**|Per la pubblicazione viene utilizzato un agente di distribuzione condiviso e a ogni coppia database di pubblicazione/database di sottoscrizione è associato un agente condiviso.|  
|**p2p_continue_onconflict**|**true**|L'agente di distribuzione continua a elaborare le modifiche quando viene rilevato un conflitto.<br /> **Attenzione:** È consigliabile usare il valore predefinito di `FALSE`. Quando questa opzione è impostata su `TRUE`, l'agente di distribuzione tenta di eseguire la convergenza dei dati nella topologia applicando la riga in conflitto dal nodo con l'ID di origine più elevato. Questo metodo non garantisce la convergenza. Dopo il rilevamento di un conflitto, è necessario assicurarsi che la topologia sia coerente. Per ulteriori informazioni, vedere la sezione relativa alla gestione dei conflitti in [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
||**false**|L'agente di distribuzione arresta l'elaborazione delle modifiche quando viene rilevato un conflitto.|  
|**post_snapshot_script**||Specifica il percorso di un file script [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguito dall'agente di distribuzione dopo l'applicazione di tutti gli altri dati e script di oggetti replicati durante una sincronizzazione iniziale.|  
|**pre_snapshot_script**||Specifica il percorso di un file script [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguito dall'agente di distribuzione prima dell'applicazione di tutti gli altri dati e script di oggetti replicati durante una sincronizzazione iniziale.|  
|**publish_to_ActiveDirectory**|**true**|Questo parametro è deprecato ed è supportato solo per compatibilità con gli script di versioni precedenti. Non è più possibile aggiungere informazioni di pubblicazione in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.|  
||**false**|Rimuove le informazioni sulla pubblicazione da Active Directory.|  
|**queue_type**|**sql**|Consente di utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'archiviazione delle transazioni. È possibile modificare questa proprietà solo se non esistono sottoscrizioni attive.<br /><br /> Nota: L'utilizzo di MSMQ ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing) non è più supportato. Se si specifica un valore di **msmq** per *valore* provoca un errore.|  
|**repl_freq**|**continua**|Pubblica l'output di tutte le transazioni basate su log.|  
||**Snapshot**|Pubblica solo gli eventi di sincronizzazione pianificati.|  
|**replicate_ddl**|**1**|Le istruzioni DDL (Data Definition Language) eseguite nel server di pubblicazione vengono replicate. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
||**0**|Non viene eseguita la replica delle istruzioni DDL. Non è possibile modificare questa proprietà per pubblicazioni non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La replica delle modifiche dello schema non può essere disabilitata in caso di utilizzo della replica peer-to-peer.|  
|**replicate_partition_switch**|**true**|ISTRUZIONE ALTER TABLE... Istruzioni SWITCH eseguite sul database pubblicato devono essere replicate ai sottoscrittori. Questa opzione è valida solo se *allow_partition_switch* è impostata su TRUE. Per altre informazioni, vedere [Replicare tabelle e indici partizionati](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).|  
||**false**|ISTRUZIONE ALTER TABLE... Le istruzioni SWITCH non devono essere replicate nei Sottoscrittori.|  
|**conservazione**||**int** che rappresenta il periodo di memorizzazione, espresso in ore, per attività di sottoscrizione. Se una sottoscrizione non viene attivata entro il periodo di memorizzazione, viene rimossa.|  
|**snapshot_in_defaultfolder**|**true**|I file di snapshot sono memorizzati nella cartella snapshot predefinita. Se *alt_snapshot_folder*viene anche specificato, i file di snapshot vengono archiviati in entrambe le predefinito e una posizione alternativa.|  
||**false**|File di snapshot sono archiviati nella posizione alternativa specificata da *alt_snapshot_folder*.|  
|**status**|**Attiva**|I dati della pubblicazione risultano immediatamente disponibili per i Sottoscrittori quando viene creata la pubblicazione. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
||**inattivo**|I dati della pubblicazione non sono disponibili per i Sottoscrittori quando viene creata la pubblicazione. Questa proprietà non è supportata per server di pubblicazione Oracle.|  
|**sync_method**|**native**|Consente di utilizzare l'output generato dal programma per la copia bulk in modalità nativa per tutte le tabelle durante la sincronizzazione delle sottoscrizioni.|  
||**character**|Consente di utilizzare l'output generato dal programma per la copia bulk in modalità carattere per tutte le tabelle durante la sincronizzazione delle sottoscrizioni.|  
||**simultanee**|Consente di utilizzare l'output generato dal programma per la copia bulk in modalità nativa per tutte le tabelle, senza tuttavia bloccare le tabelle durante il processo di generazione dello snapshot. Questa proprietà non è valida per la replica snapshot.|  
||**concurrent_c**|Consente di utilizzare l'output generato dal programma per la copia bulk in modalità carattere per tutte le tabelle, senza tuttavia bloccare le tabelle durante il processo di generazione dello snapshot. Questa proprietà non è valida per la replica snapshot.|  
|**ID attività**||Questa proprietà è deprecata e non è più supportata.|  
|**allow_drop**|**true**|Abilita `DROP TABLE` DLL il supporto per gli articoli che fanno parte della replica transazionale. Versione minima supportata: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2 o versione successiva e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] il Service Pack 1 o versione successiva. Riferimenti aggiuntivi: [KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**false**|Disabilita `DROP TABLE` DLL il supporto per gli articoli che fanno parte della replica transazionale. Questo è il **predefinito** valore per questa proprietà.|
|**NULL** (impostazione predefinita)||Restituisce l'elenco di valori supportati per *proprietà*.|  
  
[  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Segnala che l'azione eseguita da questa stored procedure potrebbe invalidare uno snapshot esistente. *force_invalidate_snapshot* è un **bit**, il valore predefinito è **0**.  
  - **0** specifica che le modifiche apportate all'articolo non invalidano lo snapshot non è valido. Se la stored procedure rileva che la modifica richiede un nuovo snapshot, viene generato un errore e non viene apportata alcuna modifica.  
  - **1** specifica che le modifiche apportate all'articolo possono invalidare lo snapshot non è valido. Se alcune sottoscrizioni esistenti richiedono un nuovo snapshot, questo valore consente di contrassegnare lo snapshot esistente come obsoleto e di generarne uno nuovo.   
Per informazioni sulle proprietà che richiedono la generazione di un nuovo snapshot quando vengono modificate, vedere la sezione Osservazioni.  
  
[ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Segnala che l'azione eseguita dalla stored procedure potrebbe richiedere la reinizializzazione delle sottoscrizioni esistenti. *force_reinit_subscription* è un **bit** con valore predefinito è **0**.  
  - **0** specifica che le modifiche apportate all'articolo non causano la reinizializzazione della sottoscrizione. Se la stored procedure rileva che la modifica richiede la reinizializzazione delle sottoscrizioni esistenti, viene generato un errore e non viene apportata alcuna modifica.  
  - **1** specifica che le modifiche apportate all'articolo causano la sottoscrizione esistente per la reinizializzazione e concede l'autorizzazione per la reinizializzazione della sottoscrizione.  
  
[ **@publisher**  =] **'**_editore_**'**  
 Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
  > [!NOTE]  
  >  *server di pubblicazione* non deve essere utilizzata quando si modificano le proprietà degli articoli in una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changepublication** viene utilizzata nella replica snapshot e transazionale.  
  
 Dopo aver modificato le proprietà seguenti, è necessario generare un nuovo snapshot, ed è necessario specificare un valore pari **1** per il *force_invalidate_snapshot* parametro.  
-   **alt_snapshot_folder**  
-   **compress_snapshot**  
-   **enabled_for_het_sub**  
-   **ftp_address**  
-   **ftp_login**  
-   **ftp_password**  
-   **ftp_port**  
-   **ftp_subdirectory**  
-   **post_snapshot_script**  
-   **pre_snapshot_script**  
-   **snapshot_in_defaultfolder**  
-   **sync_mode**  
  
Per elencare oggetti di pubblicazione in Active Directory tramite il **publish_to_active_directory** parametro, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetto sia già stato creato in Active Directory.  
  
## <a name="impact-of-immediate-sync"></a>Impatto della sincronizzazione immediata  
 Quando sincronizzazione immediata è attiva, tutte le modifiche nel log vengono rilevate subito dopo lo snapshot iniziale viene generato anche se non sono presenti sottoscrizioni. Le modifiche registrate vengono usate quando i clienti che usano backup per aggiungere un nuovo nodo peer. Dopo aver ripristinato il backup, il peer è sincronizzato con qualsiasi altra modifica che si verificano dopo l'esecuzione del backup. Poiché i comandi vengono rilevati nel database di distribuzione, la logica di sincronizzazione può esaminare l'ultimo LSN il backup e usarlo come punto di partenza, sapendo che il comando è disponibile se è stato eseguito il backup nel periodo di memorizzazione massimo. (Il valore predefinito per il periodo di memorizzazione minimo è 0 ore e max periodo è pari a 24 ore.)  
  
 Quando la sincronizzazione immediata è disattivata, le modifiche vengono mantenute per almeno il periodo di memorizzazione minimo ed eliminate immediatamente per tutte le transazioni già replicate. Se la sincronizzazione immediata è disattivata e configurata con il periodo di memorizzazione predefinito, è probabile che le modifiche necessarie dopo l'esecuzione del backup vengano eliminate e che il nuovo nodo peer non venga inizializzato correttamente. L'unica soluzione possibile è la disattivazione della topologia. Se si attiva la sincronizzazione immediata si ottiene una maggiore flessibilità; inoltre si tratta dell'impostazione consigliata per la replica P2P.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_changepublication**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Modificare le proprietà di pubblicazioni e articoli](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
