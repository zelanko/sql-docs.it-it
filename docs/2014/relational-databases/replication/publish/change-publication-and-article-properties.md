---
title: Modificare le proprietà di pubblicazioni e articoli | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying article properties
- modifying publication properties
- administering replication, properties
- publications [SQL Server replication], changing properties
- articles [SQL Server replication], properties
ms.assetid: f7df51ef-c088-4efc-b247-f91fb2c6ff32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c43c81612ffd851d7ea0e0679f79f3c8fec91037
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882344"
---
# <a name="change-publication-and-article-properties"></a>Modifica delle proprietà di pubblicazioni e articoli
  Dopo aver creato una pubblicazione, è possibile modificare la maggior parte delle proprietà della pubblicazione stessa e degli articoli. In alcuni casi è necessario rigenerare lo snapshot e/o reinizializzare le sottoscrizioni. In questo argomento vengono fornite informazioni su tutte le proprietà che, se modificate, richiedono l'esecuzione di una o entrambe le azioni.  
  
## <a name="publication-properties-for-snapshot-and-transactional-replication"></a>Proprietà della pubblicazione per la replica snapshot e transazionale  
  
|Descrizione|Stored procedure|Proprietà|Requisiti|  
|-----------------|----------------------|----------------|------------------|  
|Modifica del formato snapshot.|**sp_changepublication**|**sync_method**|Nuovo snapshot.|  
|Modifica della posizione dello snapshot.|**sp_changepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|Nuovo snapshot.|  
|Modifica della posizione dello snapshot.|**sp_changedistpublisher**|**working_directory**|Nuovo snapshot.|  
|Modifica della compressione dello snapshot.|**sp_changepublication**|**compress_snapshot**|Nuovo snapshot.|  
|Modifica delle opzioni dello snapshot FTP (File Transfer Protocol).|**sp_changepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|Nuovo snapshot.|  
|Modifica della posizione dello script pre- o post-snapshot.|**sp_changepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|Nuovo snapshot (necessario anche se si modifica il contenuto dello script).<br /><br /> È necessario eseguire la reinizializzazione per applicare il nuovo script al Sottoscrittore.|  
|Abilitazione o disabilitazione del supporto per Sottoscrittori non[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|**sp_changepublication**|**is_enabled_for_het_sub**|Nuovo snapshot.|  
|Modifica del report sui conflitti per le sottoscrizioni ad aggiornamento in coda.|**sp_changepublication**|**centralized_conflicts**|È possibile modificare questa proprietà solo se non esiste alcuna sottoscrizione attiva.|  
|Modifica dei criteri di risoluzione dei conflitti per le sottoscrizioni ad aggiornamento in coda.|**sp_changepublication**|**conflict_policy**|È possibile modificare questa proprietà solo se non esiste alcuna sottoscrizione attiva.|  
  
## <a name="article-properties-for-snapshot-and-transactional-replication"></a>Proprietà degli articoli per la replica snapshot e transazionale  
  
|Descrizione|Stored procedure|Proprietà|Requisiti|  
|-----------------|----------------------|----------------|------------------|  
|Eliminazione di un articolo.|**sp_droparticle**|Tutti i parametri.|È possibile eliminare gli articoli prima di creare le sottoscrizioni. È possibile utilizzare le stored procedure per eliminare una sottoscrizione in un articolo. Se si utilizza [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], è necessario eliminare, ricreare e sincronizzare l'intera sottoscrizione. Per altre informazioni, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](add-articles-to-and-drop-articles-from-existing-publications.md).|  
|Modifica di un filtro colonne.|**sp_articlecolumn**|**\@colonna**<br /><br /> **operazione \@**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Aggiunta di un filtro di riga.|**sp_articlefilter**|Tutti i parametri.|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Eliminazione di un filtro di riga.|**sp_articlefilter**|**articolo \@**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Modifica di un filtro di riga.|**sp_articlefilter**|**\@filter_clause**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Modifica di un filtro di riga.|**sp_changearticle**|**filter**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Modifica delle opzioni dello schema.|**sp_changearticle**|**schema_option**|Nuovo snapshot.|  
|Modifica della modalità di gestione delle tabelle nel Sottoscrittore prima dell'applicazione dello snapshot.|**sp_changearticle**|**pre_creation_cmd**|Nuovo snapshot.|  
|Modifica dello stato degli articoli.|**sp_changearticle**|**status**|Nuovo snapshot.|  
|Modifica dei comandi INSERT, UPDATE o DELETE.|**sp_changearticle**|**ins_cmd**<br /><br /> **upd_cmd**<br /><br /> **del_cmd**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Modifica del nome della tabella di destinazione.|**sp_changearticle**|**dest_table**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Modifica del proprietario della tabella di destinazione (schema).|**sp_changearticle**|**destination_owner**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Modifica dei mapping dei tipi di dati (si applica solo alla pubblicazione Oracle).|**sp_changearticlecolumndatatype**|**tipo di \@**<br /><br /> **lunghezza \@**<br /><br /> **precisione \@**<br /><br /> **scalabilità \@**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
  
## <a name="publication-properties-for-merge-replication"></a>Proprietà della pubblicazione per la replica di tipo merge  
  
|Descrizione|Stored procedure|Proprietà|Requisiti|  
|-----------------|----------------------|----------------|------------------|  
|Modifica del formato dello snapshot.|**sp_changemergepublication**|**sync_mode**|Nuovo snapshot.|  
|Modifica della posizione dello snapshot.|**sp_changemergepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|Nuovo snapshot.|  
|Modifica della posizione dello snapshot.|**sp_changedistpublisher**|**working_directory**|Nuovo snapshot.|  
|Modifica della compressione dello snapshot.|**sp_changemergepublication**|**compress_snapshot**|Nuovo snapshot.|  
|Modifica delle opzioni dello snapshot FTP.|**sp_changemergepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|Nuovo snapshot.|  
|Modifica della posizione degli script pre- o post-snapshot.|**sp_changemergepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|Nuovo snapshot (necessario anche se si modifica il contenuto dello script).<br /><br /> È necessario eseguire la reinizializzazione per applicare il nuovo script al Sottoscrittore.|  
|Aggiunta di un filtro join o di un record logico.|**sp_addmergefilter**|Tutti i parametri.|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Eliminazione di un filtro join o di un record logico.|**sp_dropmergefilter**|Tutti i parametri.|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Modifica di un filtro join o di un record logico.|**sp_changemergefilter**|**Proprietà \@**<br /><br /> **\@value**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Disabilitazione dell'utilizzo di filtri con parametri (per l'abilitazione dei filtri con parametri non sono necessarie particolari azioni).|**sp_changemergepublication**|Impostazione del valore **false** per **dynamic_filters**.|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Abilitazione o disabilitazione dell'utilizzo di partizioni pre-calcolate.|**sp_changemergepublication**|**use_partition_groups**|Nuovo snapshot.|  
|Abilitazione o disabilitazione dell'ottimizzazione delle partizioni di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] .|**sp_changemergepublication**|**keep_partition_changes**|Reinizializzazione delle sottoscrizioni.|  
|Abilitazione o disabilitazione della convalida delle partizioni del Sottoscrittore.|**sp_changemergepublication**|**validate_subscriber_info**|Reinizializzazione delle sottoscrizioni.|  
|Modifica del livello di compatibilità della pubblicazione a 80sp3 o inferiore.|**sp_changemergepublication**|**publication_compatibility_level**|Nuovo snapshot.|  
  
## <a name="article-properties-for-merge-replication"></a>Proprietà degli articoli per la replica di tipo merge  
  
|Descrizione|Stored procedure|Proprietà|Requisiti|  
|-----------------|----------------------|----------------|------------------|  
|Eliminazione di un articolo al quale è associato l'ultimo filtro con parametri nella pubblicazione.|**sp_dropmergearticle**|Tutti i parametri.|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Eliminazione di un articolo padre in un filtro join o in un record logico con l'effetto collaterale di eliminare il join correlato.|**sp_dropmergearticle**|Tutti i parametri.|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Eliminazione di un articolo in tutte le altre circostanze.|**sp_dropmergearticle**|Tutti i parametri.|Nuovo snapshot.|  
|Inclusione di un filtro colonna non pubblicato precedentemente.|**sp_mergearticlecolumn**|**\@colonna**<br /><br /> **operazione \@**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Aggiunta, eliminazione o modifica di un filtro di riga.|**sp_changemergearticle**|**subset_filterclause**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.<br /><br /> Se si aggiunge, elimina o modifica un filtro con parametri, le modifiche in sospeso nel Sottoscrittore non possono essere caricate nel server di pubblicazione durante la reinizializzazione. Per caricare le modifiche in sospeso, sincronizzare tutte le sottoscrizioni prima di modificare il filtro.<br /><br /> Se a un articolo non è associato alcun filtro di join, è possibile eliminarlo e aggiungerlo nuovamente con un filtro di riga diverso, evitando di dover reinizializzare l'intera sottoscrizione. Per altre informazioni sull'aggiunta e l'eliminazione di articoli, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](add-articles-to-and-drop-articles-from-existing-publications.md).|  
|Modifica delle opzioni dello schema.|**sp_changemergearticle**|**schema_option**|Nuovo snapshot.|  
|Modifica del rilevamento dal livello di colonna al livello di riga (per la modifica inversa dal livello di riga al livello di colonna non sono necessarie particolari azioni).|**sp_changemergearticle**|Impostazione del valore **false** per **column_tracking**.|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Attivazione o disattivazione del controllo delle autorizzazioni prima dell'applicazione nel server di pubblicazione delle istruzioni create nel Sottoscrittore.|**sp_changemergearticle**|**check_permissions**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
|Abilitazione o disabilitazione delle sottoscrizioni di solo download (per il passaggio alle o dalle altre opzioni di caricamento non sono necessarie particolari azioni).|**sp_changemergearticle**|Passaggio al o dal valore di **2** per **subscriber_upload_options**.|Reinizializzazione delle sottoscrizioni.|  
|Modifica del proprietario della tabella di destinazione.|**sp_changemergearticle**|**destination_owner**|Nuovo snapshot.<br /><br /> Reinizializzazione delle sottoscrizioni.|  
  
## <a name="see-also"></a>Vedere anche  
 [Domande frequenti sull'amministrazione della replica](../administration/frequently-asked-questions-for-replication-administrators.md)   
 [Creare e applicare lo snapshot](../create-and-apply-the-snapshot.md)   
 [Reinizializzare le sottoscrizioni](../reinitialize-subscriptions.md)   
 [sp_addmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)   
 [sp_articlefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql)   
 [sp_changearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)   
 [sp_changearticlecolumndatatype &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)   
 [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)   
 [sp_droparticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql)   
 [sp_dropmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql)   
 [sp_mergearticlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)  
  
  
