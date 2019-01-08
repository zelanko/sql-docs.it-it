---
title: sp_helpmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepublication
- sp_helpmergepublication_TSQL
helpviewer_keywords:
- sp_helpmergepublication
ms.assetid: dfe1e1e1-9a65-406a-aced-6385a078e135
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3328facfd0f19d6fa5f5f02a614c45cd22a79f76
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754125"
---
# <a name="sphelpmergepublication-transact-sql"></a>sp_helpmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Vengono restituite informazioni su una pubblicazione di tipo merge. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpmergepublication [ [ @publication = ] 'publication' ]  
    [ , [ @found = ] 'found' OUTPUT ]  
    [ , [ @publication_id = ] 'publication_id' OUTPUT ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @publication **=** ] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione*viene **sysname**, il valore predefinito è **%**, che restituisce informazioni su tutte le pubblicazioni di tipo merge nel database corrente.  
  
 [ @found **=** ] **'***trovato***'** OUTPUT  
 Flag che indica le righe che restituiscono valori. *trovato*viene **int** e un parametro di OUTPUT con valore predefinito è NULL. **1** indica la pubblicazione è stata trovata. **0** indica la pubblicazione non è stata trovata.  
  
 [ @publication_id **=**] **'***publication_id***'** OUTPUT  
 Numero di identificazione della pubblicazione. *publication_id* viene **uniqueidentifier** e un parametro di OUTPUT con valore predefinito è NULL.  
  
 [ @reserved **=**] **'***riservato***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *riservato* viene **nvarchar(20)**, con un valore predefinito è NULL.  
  
 [ @publisher **=** ] **'***editore***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
 [@publisher_db **=** ] **'***publisher_db***'**  
 Nome del database di pubblicazione. *publisher_db* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|id|**int**|Ordine sequenziale della pubblicazione nell'elenco del set di risultati.|  
|NAME|**sysname**|Nome della pubblicazione.|  
|description|**nvarchar(255)**|Descrizione della pubblicazione.|  
|status|**tinyint**|Viene indicato quando i dati della pubblicazione sono disponibili.|  
|retention|**int**|Tempo per salvare i metadati delle modifiche per gli articoli nella pubblicazione. Le unità per questo periodo di tempo possono essere giorni, settimane, mesi o anni. Per informazioni sulle unità, vedere la colonna retention_period_unit.|  
|sync_mode|**tinyint**|Modalità di sincronizzazione della pubblicazione:<br /><br /> **0** = programma per la copia bulk in modalità nativa (**bcp** utilità)<br /><br /> **1** = copia bulk di carattere|  
|allow_push|**int**|Determina se è possibile creare sottoscrizioni push per la pubblicazione specificata. **0** indica che una sottoscrizione push non è consentita.|  
|allow_pull|**int**|Determina se è possibile creare sottoscrizioni pull per la pubblicazione specificata. **0** significa che una sottoscrizione pull non è consentita.|  
|allow_anonymous|**int**|Determina se è possibile creare sottoscrizioni anonime per la pubblicazione specificata. **0** significa che non è consentita una sottoscrizione anonima.|  
|centralized_conflicts|**int**|Viene determinato se i record dei conflitti vengono archiviati nel server di pubblicazione specificato:<br /><br /> **0** = i record dei conflitti vengono archiviati sia il server di pubblicazione e nel Sottoscrittore che ha causato il conflitto.<br /><br /> **1** = tutti i record dei conflitti vengono archiviati nel server di pubblicazione.|  
|priority|**float(8)**|Priorità della sottoscrizione di loopback.|  
|snapshot_ready|**tinyint**|Viene indicato se lo snapshot della pubblicazione specificata è pronto:<br /><br /> **0** = lo snapshot è pronto per l'uso.<br /><br /> **1** = lo snapshot non è pronto per l'uso.|  
|publication_type|**int**|Tipo di pubblicazione:<br /><br /> **0** = snapshot.<br /><br /> **1** = transazionale.<br /><br /> **2** = unione nell'indice.|  
|pubid|**uniqueidentifier**|Identificatore univoco della pubblicazione.|  
|snapshot_jobid|**binary(16)**|ID di processo dell'agente snapshot. Per ottenere la voce per il processo di snapshot nel [sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md) tabella di sistema, è necessario convertire questo valore esadecimale a **uniqueidentifier**.|  
|enabled_for_internet|**int**|Viene determinato se la pubblicazione è abilitata per Internet. Se **1**, i file di sincronizzazione per la pubblicazione vengono inseriti nella `C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\Ftp` directory. La directory FTP (File Transfer Protocol) deve essere creata dall'utente. Se **0**, la pubblicazione non è abilitata per l'accesso a Internet.|  
|dynamic_filter|**int**|Indica se viene utilizzato un filtro di riga con parametri. **0** significa che non viene utilizzato un filtro di riga con parametri.|  
|has_subscription|**bit**|Indica se esistono sottoscrizioni della pubblicazione. **0** significa che non sono attualmente presenti sottoscrizioni alla pubblicazione.|  
|snapshot_in_default_folder|**bit**|Viene specificato se i file di snapshot sono archiviati nella cartella predefinita.<br /><br /> Se **1**, i file di snapshot sono disponibili nella cartella predefinita.<br /><br /> Se **0**, i file di snapshot vengono archiviati nel percorso alternativo specificato da **alt_snapshot_folder**. Una posizione alternativa può essere un altro server, un'unità di rete oppure un supporto rimovibile, ad esempio un CD o un disco rimovibile. È inoltre possibile archiviare i file di snapshot in un sito FTP in modo che possano essere successivamente recuperati dal Sottoscrittore.<br /><br /> Nota: Questo parametro può essere true e un percorso non è stato **alt_snapshot_folder** parametro. Tale combinazione consente di specificare che i file di snapshot vengono archiviati sia nel percorso predefinito che in quello alternativo.|  
|alt_snapshot_folder|**nvarchar(255)**|Specifica la posizione della cartella alternativa per lo snapshot.|  
|pre_snapshot_script|**nvarchar(255)**|Specifica un puntatore a un **con estensione SQL** generare script per file che l'agente di Merge viene eseguito prima di qualsiasi di oggetti replicati durante l'applicazione dello snapshot in un sottoscrittore.|  
|post_snapshot_script|**nvarchar(255)**|Specifica un puntatore a un **con estensione SQL** che l'agente di Merge viene eseguita dopo l'altro file script di oggetti replicati e dei dati sono stati applicati durante una sincronizzazione iniziale.|  
|compress_snapshot|**bit**|Specifica che lo snapshot che viene scritto il **alt_snapshot_folder** posizione viene compresso nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB.|  
|ftp_address|**sysname**|Indirizzo di rete del servizio FTP per il database di distribuzione. Viene specificata la posizione in cui i file di snapshot della pubblicazione possono essere prelevati dall'agente di merge.|  
|ftp_port|**int**|Numero di porta del servizio FTP per il database di distribuzione. **ftp_port** ha un valore predefinito è **21**. Viene specificata la posizione in cui i file di snapshot della pubblicazione possono essere prelevati dall'agente di merge.|  
|ftp_subdirectory|**nvarchar(255)**|Viene specificata la posizione in cui i file di snapshot possono essere prelevati dall'agente di merge quando lo snapshot viene recapitato tramite FTP.|  
|ftp_login|**sysname**|Nome utente utilizzato per la connessione al servizio FTP.|  
|conflict_retention|**int**|Viene specificato il periodo di memorizzazione dei conflitti espresso in giorni. Al trascorrere del numero di giorni specificati, la riga in conflitto viene eliminata dalla tabella dei conflitti.|  
|keep_partition_changes|**int**|Specifica se viene eseguita l'ottimizzazione della sincronizzazione per la pubblicazione specificata. **keep_partition_changes** ha un valore predefinito è **0**. Un valore pari **0** significa che la sincronizzazione non è ottimizzata e le partizioni inviate a tutti i sottoscrittori vengono verificate quando si modificano i dati in una partizione.<br /><br /> **1** significa che la sincronizzazione è ottimizzata e vengono coinvolti solo i sottoscrittori con righe nella partizione modificata.<br /><br /> Nota: Per impostazione predefinita, nelle pubblicazioni di tipo merge vengono utilizzate partizioni precalcolate tramite cui viene garantito un livello di ottimizzazione maggiore rispetto a questa opzione. Per altre informazioni, vedere [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) e [Ottimizza prestazioni filtro con parametri con partizioni pre-calcolate](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).|  
|allow_subscription_copy|**int**|Specifica se la funzionalità che consente di copiare i database di sottoscrizione che sottoscrivono la pubblicazione è abilitata. Un valore pari **0** significa copia non è consentita.|  
|allow_synctoalternate|**int**|Viene specificato se è consentito l'utilizzo di un partner di sincronizzazione alternativo per la sincronizzazione con il server di pubblicazione. Un valore pari **0** indica un partner di sincronizzazione non è consentito.|  
|validate_subscriber_info|**nvarchar(500)**|Viene visualizzato un elenco delle funzioni utilizzate per il recupero delle informazioni sul Sottoscrittore e la convalida dei criteri per i filtri di riga con parametri nel Sottoscrittore. Inoltre, viene facilitata la verifica del partizionamento consistente delle informazioni a ogni operazione di unione.|  
|backward_comp_level|**int**|Livello di compatibilità del database. I possibili valori sono i seguenti:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_activedirectory|**bit**|Specifica se le informazioni sulla pubblicazione sono pubblicate in Active Directory. Un valore pari **0** significa che le informazioni di pubblicazione non sono disponibili da Active Directory.<br /><br /> Questo parametro è deprecato ed è supportato solo per compatibilità con gli script di versioni precedenti. Non è più possibile aggiungere informazioni sulla pubblicazione in Active Directory.|  
|max_concurrent_merge|**int**|Numero massimo di processi di merge simultanei. Se **0**, non sono previsti limiti al numero di processi di merge simultanei in esecuzione in un determinato momento.|  
|max_concurrent_dynamic_snapshots|**int**|Numero massimo di sessioni simultanee di snapshot dei dati filtrati eseguibili nella pubblicazione di tipo merge. Se **0**, non sono previsti limiti al numero massimo di sessioni di snapshot dei dati filtrati eseguibili contemporaneamente nella pubblicazione in un determinato momento.|  
|use_partition_groups|**int**|Viene determinato se vengono utilizzate partizioni precalcolate. Un valore pari **1** significa che partizioni precalcolate viene utilizzate.|  
|num_of_articles|**int**|Numero di articoli nella pubblicazione.|  
|replicate_ddl|**int**|Viene specificato se le modifiche dello schema apportate in tabelle pubblicate vengono replicate. Un valore pari **1** significa che le modifiche dello schema vengono replicate.|  
|publication_number|**smallint**|Numero assegnato alla pubblicazione.|  
|allow_subscriber_initiated_snapshot|**bit**|Viene determinato se il processo di generazione dello snapshot dei dati filtrati può essere avviato dai Sottoscrittori. Un valore pari **1** significa che i sottoscrittori possono avviare il processo di snapshot.|  
|allow_web_synchronization|**bit**|Viene determinato se la pubblicazione è abilitata per la sincronizzazione Web. Un valore pari **1** significa che la sincronizzazione Web è abilitata.|  
|web_synchronization_url|**nvarchar(500)**|URL Internet utilizzato per la sincronizzazione Web.|  
|allow_partition_realignment|**bit**|Viene determinato se le eliminazioni vengono inviate al Sottoscrittore quando la modifica apportata alla riga nel server di pubblicazione comporta un cambiamento di partizione. Un valore pari **1** significa che le eliminazioni vengono inviate al sottoscrittore.  Per altre informazioni, vedere [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).|  
|retention_period_unit|**tinyint**|Viene definita l'unità utilizzata per la definizione del periodo di memorizzazione. I valori possibili sono i seguenti:<br /><br /> **0** = giorno<br /><br /> **1** = Settimana<br /><br /> **2** = Mese<br /><br /> **3** = Anno|  
|has_downloadonly_articles|**bit**|Specifica se la pubblicazione include articoli di solo download. Un valore pari **1** indica che esistono articoli di solo download.|  
|decentralized_conflicts|**int**|Viene specificato se i record dei conflitti vengono archiviati nel Sottoscrittore a causa dei quali si è verificato il conflitto. Un valore pari **0** indica che i record dei conflitti non vengono archiviati nel Sottoscrittore. Il valore 1 indica che i record dei conflitti vengono archiviati nel Sottoscrittore.|  
|generation_leveling_threshold|**int**|Viene specificato il numero di modifiche contenute in una generazione. Una generazione è una raccolta di modifiche recapitate a un server di pubblicazione o a un Sottoscrittore|  
|automatic_reinitialization_policy|**bit**|Indica se le modifiche vengono caricate dal Sottoscrittore prima di una reinizializzazione automatica. Un valore pari **1** indica che le modifiche vengono caricate dal sottoscrittore prima che si verifichi una reinizializzazione automatica. Il valore 0 indica che le modifiche non vengono caricate dal Sottoscrittore prima di una reinizializzazione automatica.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 sp_helpmergepublication viene utilizzata per la replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 I membri dell'elenco di accesso a una pubblicazione possono eseguire sp_helpmergepublication per tale pubblicazione. I membri del ruolo predefinito del database db_owner nel database di pubblicazione possono eseguire sp_helpmergepublication per ottenere informazioni su tutte le pubblicazioni.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_helpmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-helpmergepublication-_1.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
