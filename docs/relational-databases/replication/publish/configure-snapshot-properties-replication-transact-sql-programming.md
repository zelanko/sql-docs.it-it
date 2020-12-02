---
title: Configurare le proprietà dello snapshot (stored procedure di replica)
description: Utilizzare le stored procedure di replica per configurare le proprietà dello snapshot per le pubblicazioni snapshot o transazionali.
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 0f2aa6766320367af813852a2d1012ab6c7fef29
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130990"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>Configurazione delle proprietà dello snapshot (programmazione Transact-SQL della replica)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Le proprietà dello snapshot possono essere definite e modificate a livello di programmazione tramite le stored procedure di replica. Le stored procedure utilizzate dipendono dal tipo di pubblicazione.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>Per configurare le proprietà dello snapshot durante la creazione di una pubblicazione snapshot o transazionale  
  
1.  Nel server di pubblicazione eseguire [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Specificare il nome della pubblicazione per `@publication`, il valore **snapshot** o **continuous** per `@repl_freq` e uno o più parametri correlati allo snapshot seguenti:  
  
    -   `@alt_snapshot_folder`: specificare un percorso se allo snapshot di questa pubblicazione si accede da tale percorso in alternativa o in aggiunta alla cartella snapshot predefinita.    
    -   `@compress_snapshot`: specificare il valore **true** se i file di snapshot presenti nella cartella snapshot alternativa sono compressi nel formato CAB di [!INCLUDE[msCoName](../../../includes/msconame-md.md)].    
    -   `@pre_snapshot_script`: specificare il nome e il percorso completo di un file con estensione **sql** che verrà eseguito nel Sottoscrittore durante l'inizializzazione prima dell'applicazione dello snapshot iniziale.    
    -   `@post_snapshot_script`: specificare il nome e il percorso completo di un file con estensione **sql** che verrà eseguito nel Sottoscrittore durante l'inizializzazione dopo l'applicazione dello snapshot iniziale.    
    -   `@snapshot_in_defaultfolder`: specificare il valore **false** se lo snapshot è disponibile solo in un percorso non predefinito.  
  
     Per ulteriori informazioni sulla creazione di pubblicazioni, vedere [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>Per configurare le proprietà dello snapshot durante la creazione di una pubblicazione di tipo merge  
  
1.  Nel server di pubblicazione eseguire [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Specificare il nome della pubblicazione per `@publication`, il valore **snapshot** o **continuous** per `@repl_freq` e uno o più parametri correlati allo snapshot seguenti:  
  
    -   **alt_snapshot_folder**: specificare un percorso se allo snapshot di questa pubblicazione si accede da tale percorso alternativa o in aggiunta alla cartella snapshot predefinita.    
    -   `@compress_snapshot`: specificare il valore **true** se i file di snapshot presenti nella cartella snapshot alternativa sono compressi nel formato CAB.   
    -   `@pre_snapshot_script`: specificare il nome e il percorso completo di un file con estensione **sql** che verrà eseguito nel Sottoscrittore durante l'inizializzazione prima dell'applicazione dello snapshot iniziale.    
    -   `@post_snapshot_script`: specificare il nome e il percorso completo di un file con estensione **sql** che verrà eseguito nel Sottoscrittore durante l'inizializzazione dopo l'applicazione dello snapshot iniziale.    
    -   `@snapshot_in_defaultfolder`: specificare il valore **false** se lo snapshot è disponibile solo in un percorso non predefinito.  
  
2.  Per ulteriori informazioni sulla creazione di pubblicazioni, vedere [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>Per modificare le proprietà dello snapshot di una pubblicazione snapshot o transazionale esistente  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Specificare il valore **1** per `@force_invalidate_snapshot` e uno dei valori seguenti per `@property`:  
  
    -   **alt_snapshot_folder**: specificare anche un nuovo percorso della cartella snapshot alternativa per `@value`.    
    -   **compress_snapshot**: specificare anche il valore **true** o **false** per `@value` in modo da indicare se i file di snapshot presenti nella cartella snapshot alternativa sono compressi nel formato CAB.    
    -   **pre_snapshot_script**: sempre per `@value` specificare il nome e il percorso completo di un file con estensione **sql** che verrà eseguito nel Sottoscrittore durante l'inizializzazione prima dell'applicazione dello snapshot iniziale.    
    -   **post_snapshot_script**: sempre per `@value` specificare il nome e il percorso completo di un file con estensione **sql** che verrà eseguito nel Sottoscrittore durante l'inizializzazione dopo l'applicazione dello snapshot iniziale.    
    -   **snapshot_in_defaultfolder** : specificare anche il valore **true** o **false** per indicare se lo snapshot è disponibile solo in un percorso non predefinito.  
  
2.  (Facoltativo) Nel database di pubblicazione del server di pubblicazione eseguire [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md). Specificare `@publication` e uno o più parametri di pianificazione o delle credenziali di sicurezza da modificare.  
  
    > [!IMPORTANT]  
    >  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
3.  Eseguire [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) dal prompt dei comandi o avviare il processo dell'agente snapshot per generare un nuovo snapshot. Per altre informazioni, vedere [Creazione e applicazione dello snapshot iniziale](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>Per modificare le proprietà dello snapshot di una pubblicazione di tipo merge esistente  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Specificare il valore **1** per `@force_invalidate_snapshot` e uno dei valori seguenti per `@property**`:  
  
    -   **alt_snapshot_folder**: specificare anche un nuovo percorso della cartella snapshot alternativa per `@value`.    
    -   **compress_snapshot**: specificare anche il valore **true** o **false** per `@value` in modo da indicare se i file di snapshot presenti nella cartella snapshot alternativa sono compressi nel formato CAB.    
    -   **pre_snapshot_script**: sempre per `@value` specificare il nome e il percorso completo di un file con estensione **sql** che verrà eseguito nel Sottoscrittore durante l'inizializzazione prima dell'applicazione dello snapshot iniziale.    
    -   **post_snapshot_script**: sempre per `@value` specificare il nome e il percorso completo di un file con estensione **sql** che verrà eseguito nel Sottoscrittore durante l'inizializzazione dopo l'applicazione dello snapshot iniziale.    
    -   **snapshot_in_defaultfolder** : specificare anche il valore **true** o **false** per indicare se lo snapshot è disponibile solo in un percorso non predefinito.  
  
2.  Eseguire [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) dal prompt dei comandi o avviare il processo dell'agente snapshot per generare un nuovo snapshot. Per altre informazioni, vedere [Creazione e applicazione dello snapshot iniziale](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## <a name="example"></a>Esempio  
 In questo esempio viene creata una pubblicazione che utilizza una cartella snapshot alternativa e uno snapshot compresso.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare le opzioni snapshot](../../../relational-databases/replication/snapshot-options.md)   
 [Eseguire gli script prima e dopo l'applicazione dello snapshot](../../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Trasferire snapshot tramite FTP](../../../relational-databases/replication//publish/deliver-a-snapshot-through-ftp.md)   
 [Modificare le proprietà di pubblicazioni e articoli](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  
