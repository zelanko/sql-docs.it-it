---
title: IHpublications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublications_TSQL
- IHpublications
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublications system table
ms.assetid: b519a101-fa53-44be-bd55-6ea79245b5d1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 227762e4fbc71d58641aa5f67ec975df9df08360
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802783"
---
# <a name="ihpublications-transact-sql"></a>IHpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **IHpublications** tabella di sistema contiene una riga per ogni pubblicazione non SQL Server usando il server di distribuzione corrente. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**pubid**|**int**|Colonna Identity che include un ID univoco per la pubblicazione.|  
|**name**|**sysname**|Nome univoco associato alla pubblicazione.|  
|**repl_freq**|**tinyint**|Frequenza della replica:<br /><br /> **0** = basata sulle transazioni.<br /><br /> **1** = aggiornamento di tabella pianificato.|  
|**status**|**tinyint**|Stato della pubblicazione. I possibili valori sono i seguenti.<br /><br /> **0** = inattiva.<br /><br /> **1** = attivo.|  
|**sync_method**|**tinyint**|Metodo di sincronizzazione:<br /><br /> **1** = copia bulk di carattere.<br /><br /> **4** = Concurrent_c, che significa che viene utilizzata la copia bulk di carattere ma durante lo snapshot le tabelle non vengono bloccate.|  
|**snapshot_jobid**|**binary**|ID dell'attività pianificata.|  
|**enabled_for_internet**|**bit**|Indica se i file di sincronizzazione per la pubblicazione vengono esposti a Internet tramite FTP e altri servizi, dove **1** significa che sono accessibili da Internet.|  
|**immediate_sync_ready**|**bit**|Indica se i file di sincronizzazione sono disponibili, in cui **1** significa che sono disponibili. *Non è supportata per la pubblicazione non SQL.*|  
|**allow_queued_tran**|**bit**|Specifica se disabilitare l'inserimento in coda delle modifiche apportate nel Sottoscrittore finché non è possibile applicarle al server di pubblicazione. Se **1**, vengono messe in coda le modifiche del sottoscrittore. *Non è supportata per la pubblicazione non SQL.*|  
|**allow_sync_tran**|**bit**|Specifica se è consentito creare sottoscrizioni ad aggiornamento immediato per la pubblicazione. **1** significa che le sottoscrizioni ad aggiornamento immediato sono consentite. *Non è supportata per la pubblicazione non SQL.*|  
|**autogen_sync_procs**|**bit**|Specifica se la stored procedure di sincronizzazione per sottoscrizioni ad aggiornamento immediato viene generata nel server di pubblicazione. **1** indica che viene generato nel server di pubblicazione. *Non è supportata per la pubblicazione non SQL.*|  
|**snapshot_in_defaultfolder**|**bit**|Specifica se i file di snapshot sono archiviati nella cartella predefinita. Se **0**, i file di snapshot sono stati archiviati nel percorso alternativo specificato da *alternate_snapshot_folder*. Se **1**, i file di snapshot sono disponibili nella cartella predefinita.|  
|**alt_snapshot_folder**|**nvarchar(510)**|Specifica la posizione della cartella alternativa per lo snapshot.|  
|**pre_snapshot_script**|**nvarchar(510)**|Specifica un puntatore a un **con estensione SQL** percorso dei file. L'agente di distribuzione esegue lo script pre-snapshot prima dell'esecuzione degli script di oggetti replicati in fase di applicazione di uno snapshot in un Sottoscrittore.|  
|**post_snapshot_script**|**nvarchar(510)**|Specifica un puntatore a un **con estensione SQL** percorso dei file. L'agente di distribuzione esegue lo script post-snapshot dopo l'applicazione di tutti gli altri script di oggetti replicati e dei dati durante una sincronizzazione iniziale.|  
|**compress_snapshot**|**bit**|Specifica che lo snapshot che viene scritto il *alt_snapshot_folder* posizione deve essere compresso nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. **0** specifica che lo snapshot verrà compresso non.|  
|**ftp_address**|**sysname**|Indirizzo di rete del servizio FTP per il server di distribuzione. Specifica la posizione in cui i file di snapshot della pubblicazione possono essere prelevati dall'agente di distribuzione.|  
|**ftp_port**|**int**|Numero di porta del servizio FTP per il server di distribuzione. Specifica la posizione in cui i file di snapshot della pubblicazione possono essere prelevati dall'agente di distribuzione.|  
|**ftp_subdirectory**|**nvarchar(510)**|Specifica la posizione in cui i file di snapshot possono essere prelevati dall'agente di distribuzione se la pubblicazione supporta la propagazione degli snapshot tramite FTP.|  
|**ftp_login**|**nvarchar(256)**|Nome utente utilizzato per la connessione al servizio FTP.|  
|**ftp_password**|**nvarchar(1048)**|Password dell'utente utilizzata per la connessione al servizio FTP.|  
|**allow_dts**|**bit**|Specifica che la pubblicazione supporta le trasformazioni di dati. **1** specifica che le trasformazioni DTS sono consentite. *Non è supportata per la pubblicazione non SQL.*|  
|**allow_anonymous**|**bit**|Indica se le sottoscrizioni anonime sono consentite per la pubblicazione in cui **1** indica che essi sono consentite.|  
|**centralized_conflicts**|**bit**|Specifica se i record dei conflitti vengono archiviati nel server di pubblicazione:<br /><br /> **0** = i record dei conflitti vengono archiviati sia il server di pubblicazione e nel Sottoscrittore che ha causato il conflitto.<br /><br /> **1** = i record dei conflitti vengono archiviati nel server di pubblicazione.<br /><br /> *Non è supportata per la pubblicazione non SQL.*|  
|**conflict_retention**|**int**|Specifica il periodo di memorizzazione dei conflitti, espresso in giorni. *Non è supportata per la pubblicazione non SQL.*|  
|**conflict_policy**|**int**|Specifica i criteri di risoluzione dei conflitti adottati quando viene utilizzata l'opzione per Sottoscrittori ad aggiornamento in coda. I possibili valori sono i seguenti:<br /><br /> **1** = prevale il server di pubblicazione.<br /><br /> **2** = prevale il sottoscrittore.<br /><br /> **3** = sottoscrizione viene reinizializzata.<br /><br /> *Non è supportata per la pubblicazione non SQL.*|  
|**queue_type**|**int**|Specifica il tipo di coda da utilizzare. I possibili valori sono i seguenti:<br /><br /> **1** = msmq, ovvero Usa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Accodamento per archiviare le transazioni.<br /><br /> **2** = sql, che usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per archiviare le transazioni.<br /><br /> Questa colonna non viene utilizzata da non -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione.<br /><br /> Nota: L'utilizzo del servizio di accodamento messaggi [!INCLUDE[msCoName](../../includes/msconame-md.md)] è deprecato e non è più supportato.<br /><br /> *Questa colonna non è supportata per la pubblicazione non SQL.*|  
|**ad_guidname**|**sysname**|Specifica se la pubblicazione è pubblicata in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. Un valido identificatore univoco globale (GUID) specifica che la pubblicazione è pubblicata nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory e il GUID è l'oggetto di pubblicazione di Active Directory corrispondente **objectGUID**. Se il valore è NULL, la pubblicazione non è pubblicata in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory. *Non è supportata per la pubblicazione non SQL.*|  
|**backward_comp_level**|**int**|Livello di compatibilità del database. I possibili valori sono i seguenti:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> *Non è supportata per la pubblicazione non SQL.*|  
|**description**|**nvarchar(255)**|Voce descrittiva della pubblicazione.|  
|**independent_agent**|**bit**|Specifica se per la pubblicazione è disponibile un agente di distribuzione autonomo.<br /><br /> **0** = la pubblicazione utilizza un agente di distribuzione condiviso, e ogni coppia database del server di pubblicazione/sottoscrittore del database ha un solo agente condiviso.<br /><br /> **1** = è disponibile un agente di distribuzione autonomo per la pubblicazione.|  
|**immediate_sync**|**bit**|Indica se i file di sincronizzazione vengono creati o ricreati ogni volta che viene eseguito l'agente Snapshot, dove **1** significa che vengono creati ogni volta che viene eseguito l'agente.|  
|**allow_push**|**bit**|Indica se le sottoscrizioni push sono consentite per la pubblicazione in cui **1** indica che essi sono consentite.|  
|**allow_pull**|**bit**|Indica se sono consentite sottoscrizioni pull sulla pubblicazione, dove **1** indica che essi sono consentite.|  
|**conservazione**|**int**|Quantità di modifiche, espressa in ore, da salvare per la pubblicazione specificata.|  
|**allow_subscription_copy**|**bit**|Specifica se la funzionalità che consente di copiare i database di sottoscrizione che sottoscrivono la pubblicazione è abilitata. **1** significa che la copia è consentita.|  
|**allow_initialize_from_backup**|**bit**|Specifica se i Sottoscrittori possono inizializzare una sottoscrizione di questa pubblicazione da un backup anziché da uno snapshot iniziale. **1** significa che le sottoscrizioni possono essere inizializzate da un backup, e **0** indica che essi non è possibile. Per altre informazioni, vedere [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md). *Non è supportata per la pubblicazione non SQL.*|  
|**min_autonosync_lsn**|**binary(1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|Indica se per la pubblicazione è supportata la replica dello schema. **1** indica che le istruzioni DDL eseguite nel server di pubblicazione vengono replicate, e **0** indica che le istruzioni DDL non vengono replicate. Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md). *Non è supportata per la pubblicazione non SQL.*|  
|**options**|**int**|Mappa di bit che specifica opzioni di pubblicazione aggiuntive. I possibili valori delle opzioni bit per bit sono i seguenti:<br /><br /> **0x1** : abilitato per la replica peer-to-peer.<br /><br /> **0x2** -pubblicare solo modifiche locali.<br /><br /> **0x4** : abilitato per i sottoscrittori non SQL Server.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [syspublications &#40;vista di sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)   
 [syspublications &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syspublications-transact-sql.md)  
  
  
