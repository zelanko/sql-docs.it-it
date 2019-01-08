---
title: sysmergepartitioninfoview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepartitioninfoview
- sysmergepartitioninfoview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfoview view
ms.assetid: 714e2935-1bc7-4901-aea2-64b1bbda03d6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f39591079377dcfc1f357e582474f034a004af6d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816313"
---
# <a name="sysmergepartitioninfoview-transact-sql"></a>sysmergepartitioninfoview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **sysmergepartitioninfoview** Vista espone informazioni sul partizionamento per gli articoli di tabella. Questa vista è archiviata nel database di pubblicazione del server di pubblicazione e nel database di sottoscrizione del Sottoscrittore.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome dell'articolo.|  
|**type**|**tinyint**|Specifica il tipo di articolo. I possibili valori sono i seguenti:<br /><br /> **0x0a** = Table.<br /><br /> **0x20** = solo schema della procedura.<br /><br /> **0x40** = solo schema della vista o solo schema della vista indicizzata.<br /><br /> **0x80** = solo schema funzione.|  
|**objid**|**int**|Identificatore dell'oggetto pubblicato.|  
|**sync_objid**|**int**|ID di oggetto della vista che rappresenta il set di dati sincronizzato.|  
|**view_type**|**tinyint**|Tipo di vista:<br /><br /> **0** = non una vista, utilizzare tutti gli dell'oggetto di base.<br /><br /> **1** = vista permanente.<br /><br /> **2** = vista temporanea.|  
|**artid**|**uniqueidentifier**|Identificatore univoco per l'articolo specificato.|  
|**description**|**nvarchar(255)**|Breve descrizione dell'articolo.|  
|**pre_creation_command**|**tinyint**|Azione predefinita da eseguire quando viene creato l'articolo nel database di sottoscrizione:<br /><br /> **0** = Nessuna: se la tabella esiste già nel Sottoscrittore, viene eseguita alcuna azione.<br /><br /> **1** = rimozione: Elimina la tabella prima di ricrearla.<br /><br /> **2** = eliminazione specifica: esegue un'operazione di eliminazione in base alla clausola WHERE nel filtro di subset.<br /><br /> **3** = troncamento: equivale 2, ma Elimina pagine anziché righe. La clausola WHERE in questo caso non viene utilizzata.|  
|**pubid**|**uniqueidentifier**|ID della pubblicazione a cui appartiene l'articolo corrente.|  
|**nome alternativo**|**int**|Mapping di un nome alternativo per l'identificazione dell'articolo.|  
|**column_tracking**|**int**|Indica se viene implementato il rilevamento a livello di colonna per l'articolo.|  
|**status**|**tinyint**|Specifica lo stato dell'articolo. I possibili valori sono i seguenti:<br /><br /> **1** = non sincronizzato: lo script di elaborazione iniziale per pubblicare la tabella verrà eseguito alla successiva esecuzione dell'agente Snapshot.<br /><br /> **2** = attivo: lo script di elaborazione iniziale per pubblicare la tabella è stato eseguito.|  
|**conflict_table**|**sysname**|Nome della tabella locale che include i record in conflitto per l'articolo corrente. Lo scopo di questa tabella è esclusivamente informativo. Il contenuto può essere modificato o eliminato da routine di risoluzione dei conflitti personalizzate oppure direttamente dall'amministratore.|  
|**creation_script**|**nvarchar(255)**|Script per la creazione dell'articolo.|  
|**conflict_script**|**nvarchar(255)**|Script dei conflitti dell'articolo.|  
|**article_resolver**|**nvarchar(255)**|Sistema di risoluzione dei conflitti dell'articolo.|  
|**ins_conflict_proc**|**sysname**|Procedura utilizzata per scrivere le informazioni sui conflitti nella tabella con conflitti.|  
|**insert_proc**|**sysname**|Procedura utilizzata per inserire le righe durante la sincronizzazione.|  
|**update_proc**|**sysname**|Procedura utilizzata per aggiornare le righe durante la sincronizzazione.|  
|**select_proc**|**sysname**|Nome di una stored procedure generata automaticamente utilizzata dall'agente di merge per l'implementazione del blocco e l'individuazione delle righe e colonne per un articolo.|  
|**metadata_select_proc**|**sysname**|Nome della stored procedure generata automaticamente utilizzata per accedere ai metadati nelle tabelle di sistema della replica di tipo merge.|  
|**delete_proc**|**sysname**|Procedura utilizzata per eliminare le righe durante la sincronizzazione.|  
|**schema_option**|**binary(8)**|Mappa di bit dell'opzione di creazione dello schema per l'articolo specificato. Per informazioni su supportate *schema_option* valori, vedere [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|Nome della tabella creata nel Sottoscrittore.|  
|**destination_owner**|**sysname**|Nome del proprietario dell'oggetto di destinazione.|  
|**resolver_clsid**|**nvarchar(50)**|ID del sistema di risoluzione dei conflitti personalizzato. Per un gestore della logica di business questo valore è NULL.|  
|**subset_filterclause**|**nvarchar(1000)**|Clausola di filtro per l'articolo.|  
|**missing_col_count**|**int**|Numero di colonne pubblicate mancanti nell'articolo.|  
|**missing_cols**|**varbinary(128)**|Mappa di bit che descrive le colonne mancanti nell'articolo.|  
|**excluded_cols**|**varbinary(128)**|Mappa di bit delle colonne escluse dall'articolo.|  
|**excluded_col_count**|**int**|Numero di colonne escluse dall'articolo.|  
|**columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|Mappa di bit che descrive le colonne eliminate dall'articolo.|  
|**resolver_info**|**nvarchar(255)**|Archivio per informazioni aggiuntive necessarie per il sistema di risoluzione dei conflitti personalizzato.|  
|**view_sel_proc**|**nvarchar(290)**|Nome di una stored procedure utilizzata dall'agente di merge per il popolamento iniziale di un articolo in una pubblicazione filtrata in modo dinamico e per l'enumerazione delle righe modificate in qualsiasi pubblicazione filtrata.|  
|**gen_cur**|**bigint**|Genera il numero di modifica locale per la tabella di base di un articolo.|  
|**vertical_partition**|**int**|Specifica se in un articolo di tabella il filtraggio delle colonne è abilitato. **0** indica non è applicato alcun filtro verticale e pertanto pubblicate tutte le colonne.|  
|**identity_support**|**int**|Specifica se è abilitata la gestione automatica degli intervalli di valori Identity. **1** significa che degli intervalli di valori identity sono abilitato, e **0** significa che non vi sia alcuna identità di intervalli di valori supportati.|  
|**before_image_objid**|**int**|ID dell'oggetto tabella di rilevamento. La tabella di rilevamento include valori di colonna chiave specifici se per la pubblicazione sono state abilitate le ottimizzazioni delle modifiche delle partizioni.|  
|**before_view_objid**|**int**|ID di oggetto di una tabella di vista. La vista è relativa a una tabella in cui viene tenuto traccia se una riga appartiene a un Sottoscrittore specifico prima di essere eliminata o aggiornata. Valido solo se per la pubblicazione sono state abilitate le ottimizzazioni delle modifiche delle partizioni.|  
|**verify_resolver_signature**|**int**|Specifica se una firma digitale viene verificata o meno prima dell'utilizzo di un sistema di risoluzione dei conflitti in una replica di tipo merge:<br /><br /> **0** = firma non viene verificata.<br /><br /> **1** = firma viene verificata per stabilire se deriva da una fonte attendibile.|  
|**allow_interactive_resolver**|**bit**|Specifica se per un articolo l'utilizzo del sistema di risoluzione dei conflitti interattivo è attivato. **1** significa che il sistema di risoluzione interattivo può essere usato per l'articolo.|  
|**fast_multicol_updateproc**|**bit**|Specifica se l'agente di merge è stato attivato per l'applicazione di modifiche a più colonne della stessa riga tramite una sola istruzione UPDATE:<br /><br /> **0** = esegue un'istruzione UPDATE distinta per ogni colonna modificata.<br /><br /> **1** = rilasciato nell'istruzione UPDATE che fa in modo che gli aggiornamenti a più colonne in un'unica istruzione.|  
|**check_permissions**|**int**|Mappa di bit delle autorizzazioni a livello di tabella che verranno verificate quando l'agente di merge applicherà le modifiche nel server di pubblicazione. *check_permissions* può avere uno dei valori seguenti:<br /><br /> **0x00** = le autorizzazioni non vengono controllate.<br /><br /> **0x10** = controlli delle autorizzazioni nel server di pubblicazione prima che gli inserimenti vengono eseguiti in un sottoscrittore possono essere caricate.<br /><br /> **0x20** = le autorizzazioni vengono verificate nel server di pubblicazione prima gli aggiornamenti apportati nel Sottoscrittore possono essere caricati.<br /><br /> **0x40** = le autorizzazioni vengono verificate nel server di pubblicazione prima del caricamento DELETE eseguite in un sottoscrittore.|  
|**maxversion_at_cleanup**|**int**|Numero massimo di generazioni rimosse alla successiva esecuzione dell'agente di merge.|  
|**processing_order**|**int**|Indica l'ordine di elaborazione degli articoli in una pubblicazione di tipo merge. dove il valore **0** indica che l'articolo non è ordinato e gli articoli vengono elaborati in ordine dal valore più basso al più alto. Se due articoli hanno lo stesso valore, essi vengono elaborati simultaneamente. Per altre informazioni, vedere [Specificare l'ordine di elaborazione degli articoli di merge](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).|  
|**upload_options**|**tinyint**|Specifica se è possibile apportare modifiche nel Sottoscrittore o caricare modifiche dal Sottoscrittore. I possibili valori sono i seguenti.<br /><br /> **0** = non esistono restrizioni per gli aggiornamenti eseguiti nel Sottoscrittore; tutte le modifiche vengono caricate nel server di pubblicazione.<br /><br /> **1** = sono consentite modifiche nel Sottoscrittore, ma non vengono caricate nel server di pubblicazione.<br /><br /> **2** = non sono consentite modifiche nel Sottoscrittore.|  
|**published_in_tran_pub**|**bit**|Indica che un articolo in una pubblicazione di tipo merge viene pubblicato anche in una pubblicazione transazionale.<br /><br /> **0** = l'articolo non viene pubblicato in un articolo transazionale.<br /><br /> **1** = l'articolo è pubblicato anche in un articolo transazionale.|  
|**lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|ID della vista della tabella prima degli aggiornamenti.|  
|**delete_tracking**|**bit**|Specifica se le eliminazioni vengono replicate.<br /><br /> **0** = le eliminazioni non vengono replicate.<br /><br /> **1** = le eliminazioni vengono replicate, ovvero il comportamento predefinito per la replica di tipo merge.<br /><br /> Quando il valore di *delete_tracking* viene **0**, le righe eliminate nel Sottoscrittore devono essere rimosse manualmente nel server di pubblicazione e le righe eliminate nel server di pubblicazione devono essere rimosse manualmente nel Sottoscrittore.<br /><br /> Nota: Un valore pari **0** comporta non convergenza.|  
|**compensate_for_errors**|**bit**|Specifica se devono essere eseguite azioni di compensazione quando vengono rilevati errori durante la sincronizzazione.<br /><br /> **0** = Compensating le azioni vengono disabilitate.<br /><br /> **1** = le modifiche che non possono essere applicate in un sottoscrittore o un server di pubblicazione generano sempre azioni di compensazione per annullare queste modifiche, ovvero il comportamento predefinito per la replica di tipo merge.<br /><br /> Nota: Un valore pari **0** comporta non convergenza.|  
|**pub_range**|**bigint**|Dimensioni dell'intervallo di valori Identity del server di pubblicazione.|  
|**Intervallo**|**bigint**|Dimensioni dei valori Identity consecutivi che verrebbero assegnati nei Sottoscrittori durante un intervento di regolazione.|  
|**soglia**|**int**|Percentuale di soglia dell'intervallo di valori Identity.|  
|**stream_blob_columns**|**bit**|Indica se per le colonne BLOB (Binary Large Object) viene utilizzata l'ottimizzazione del flusso. **1** significa che viene eseguita l'ottimizzazione.|  
|**preserve_rowguidcol**|**bit**|Specifica se per la replica viene utilizzata una colonna rowguid esistente. Un valore pari **1** indica che viene utilizzata una colonna ROWGUIDCOL esistente. **0** significa che la replica aggiunto la colonna ROWGUIDCOL.|  
|**partition_view_id**|**int**|Identifica la vista che definisce una partizione del Sottoscrittore.|  
|**repl_view_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**partition_deleted_view_rule**|**sysname**|Istruzione utilizzata all'interno di un trigger di replica di tipo merge per recuperare l'ID di partizione per ogni riga eliminata o aggiornata in base ai relativi valori di colonna precedenti.|  
|**partition_inserted_view_rule**|**sysname**|Istruzione utilizzata all'interno di un trigger di replica di tipo merge per recuperare l'ID di partizione per ogni riga inserita o aggiornata in base ai relativi nuovi valori di colonna.|  
|**membership_eval_proc_name**|**sysname**|Il nome della procedura che restituisce l'ID di partizione correnti delle righe [MSmerge_contents &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md).|  
|**column_list**|**sysname**|Elenco separato da virgole delle colonne pubblicate in un articolo.|  
|**column_list_blob**|**sysname**|Elenco separato da virgole delle colonne pubblicate in un articolo, comprese le colonne BLOB.|  
|**expand_proc**|**sysname**|Nome della procedura che restituisce nuovamente gli ID di partizione per tutte le righe figlio di una riga padre appena inserita e per le righe padre sottoposte a modifica a livello di partizione oppure che sono state eliminate.|  
|**logical_record_parent_nickname**|**int**|Nome alternativo del padre di livello principale di un articolo specifico in un record logico.|  
|**logical_record_view**|**int**|Vista che ha come output la colonna rowguid dell'articolo padre di livello principale corrispondente a ogni colonna rowguid figlio.|  
|**logical_record_deleted_view_rule**|**sysname**|Simile a **logical_record_view**, ad eccezione del fatto che mostra le righe figlio nella tabella "eliminata" nei trigger update e delete.|  
|**logical_record_level_conflict_detection**|**bit**|Indica se è necessario rilevare i conflitti a livello di record logico oppure a livello di riga o colonna.<br /><br /> **0** = o colonna a livello di riga viene utilizzato il rilevamento dei conflitti.<br /><br /> **1** = logico viene utilizzato il rilevamento dei conflitti di record, in cui una modifica in una riga nel server di pubblicazione e modifica in una riga logica uguale record nel sottoscrittore viene gestita come un conflitto.<br /><br /> Se questo valore è 1, è possibile utilizzare solo la risoluzione dei conflitti a livello di record logico.|  
|**logical_record_level_conflict_resolution**|**bit**|Indica se è necessario risolvere i conflitti a livello di record logico oppure a livello di riga o colonna.<br /><br /> **0** = o colonna a livello di riga viene utilizzata la risoluzione.<br /><br /> **1** = In caso di conflitto, l'intero record logico prevalente sovrascrive l'intero record logico nella parte interessata.<br /><br /> È possibile utilizzare il valore 1 sia con il rilevamento a livello di record logico che con il rilevamento a livello di riga o colonna.|  
|**partition_options**|**tinyint**|Definisce il modo in cui vengono partizionati i dati nell'articolo. Ciò consente di ottimizzare le prestazioni se tutte le righe appartengono a un'unica partizione o a un'unica sottoscrizione. Il *partition_options* può essere uno dei valori seguenti.<br /><br /> **0** = il filtro dell'articolo è statico oppure non restituisce un subset univoco di dati per ogni partizione, vale a dire, una partizione "sovrapposta".<br /><br /> **1** = le partizioni sono sovrapposte e gli aggiornamenti DML apportati nel Sottoscrittore non è possibile modificare la partizione a cui appartiene una riga.<br /><br /> **2** = il filtro dell'articolo restituisce partizioni non sovrapposte, ma più sottoscrittori ricevono la stessa partizione.<br /><br /> **3** = il filtro dell'articolo restituisce partizioni non sovrapposte univoche per ogni sottoscrizione.|  
|**name**|**sysname**|Nome di una partizione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione delle partizioni di una pubblicazione di tipo Merge con filtri con parametri](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_helpmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)  
  
  
