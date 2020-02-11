---
title: Configurare le proprietà dello snapshot (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: b03dd7f886cee5816d591034d1be63ece45d8d1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63021333"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>Configurazione delle proprietà dello snapshot (programmazione Transact-SQL della replica)
  Le proprietà dello snapshot possono essere definite e modificate a livello di programmazione tramite le stored procedure di replica. Le stored procedure utilizzate dipendono dal tipo di pubblicazione.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>Per configurare le proprietà dello snapshot durante la creazione di una pubblicazione snapshot o transazionale  
  
1.  Nel server di pubblicazione eseguire [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Specificare il nome di una **@publication**pubblicazione per, il valore **snapshot** o **Continuous** per **@repl_freq**e uno o più dei seguenti parametri correlati allo snapshot:  
  
    -   **@alt_snapshot_folder**: specificare un percorso se è possibile accedere allo snapshot per questa pubblicazione da tale percorso anziché o in aggiunta alla cartella snapshot predefinita.  
  
    -   **@compress_snapshot**-specificare il valore **true** se i file di snapshot nella cartella snapshot alternativa sono compressi nel formato di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] file CAB.  
  
    -   **@pre_snapshot_script**-specificare il nome del file e il percorso completo di un file con **estensione SQL** che verrà eseguito nel Sottoscrittore durante l'inizializzazione prima dell'applicazione dello snapshot iniziale.  
  
    -   **@post_snapshot_script**-specificare il nome del file e il percorso completo di un file con **estensione SQL** che verrà eseguito nel Sottoscrittore durante l'inizializzazione dopo l'applicazione dello snapshot iniziale.  
  
    -   **@snapshot_in_defaultfolder**: specificare il valore **false** se lo snapshot è disponibile solo in un percorso non predefinito.  
  
     Per ulteriori informazioni sulla creazione di pubblicazioni, vedere [Create a Publication](create-a-publication.md).  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>Per configurare le proprietà dello snapshot durante la creazione di una pubblicazione di tipo merge  
  
1.  Nel server di pubblicazione eseguire [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Specificare il nome di una **@publication**pubblicazione per, il valore **snapshot** o **Continuous** per **@repl_freq**e uno o più dei seguenti parametri correlati allo snapshot:  
  
    -   **@alt_snapshot_folder**: specificare un percorso se è possibile accedere allo snapshot per questa pubblicazione da tale percorso anziché o in aggiunta alla cartella snapshot predefinita.  
  
    -   **@compress_snapshot**-specificare il valore **true** se i file di snapshot nella cartella snapshot alternativa sono compressi nel formato di file CAB.  
  
    -   **@pre_snapshot_script**-specificare il nome del file e il percorso completo di un file con **estensione SQL** che verrà eseguito nel Sottoscrittore durante l'inizializzazione prima dell'applicazione dello snapshot iniziale.  
  
    -   **@post_snapshot_script**-specificare il nome del file e il percorso completo di un file con **estensione SQL** che verrà eseguito nel Sottoscrittore durante l'inizializzazione dopo l'applicazione dello snapshot iniziale.  
  
    -   **@snapshot_in_defaultfolder**: specificare il valore **false** se lo snapshot è disponibile solo in un percorso non predefinito.  
  
2.  Per ulteriori informazioni sulla creazione di pubblicazioni, vedere [Create a Publication](create-a-publication.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>Per modificare le proprietà dello snapshot di una pubblicazione snapshot o transazionale esistente  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Specificare il valore **1** per **@force_invalidate_snapshot** e uno dei valori seguenti per **@property**:  
  
    -   **alt_snapshot_folder** : specificare anche un nuovo percorso per la cartella snapshot alternativa **@value**.  
  
    -   **compress_snapshot** : specificare anche il valore **true** o **false** per **@value** per indicare se i file di snapshot nella cartella snapshot alternativa sono compressi nel formato di file CAB.  
  
    -   **pre_snapshot_script** : **@value** specificare anche il nome del file e il percorso completo di un file con **estensione SQL** che verrà eseguito nel Sottoscrittore durante l'inizializzazione prima dell'applicazione dello snapshot iniziale.  
  
    -   **post_snapshot_script** : **@value** specificare anche il nome del file e il percorso completo di un file con **estensione SQL** che verrà eseguito nel Sottoscrittore durante l'inizializzazione dopo l'applicazione dello snapshot iniziale.  
  
    -   **snapshot_in_defaultfolder** : specificare anche il valore **true** o **false** per indicare se lo snapshot è disponibile solo in un percorso non predefinito.  
  
2.  (Facoltativo) Nel database di pubblicazione del server di pubblicazione eseguire [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql). Specificare **@publication** e uno o più parametri di pianificazione o delle credenziali di sicurezza da modificare.  
  
    > [!IMPORTANT]  
    >  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
3.  Eseguire [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) dal prompt dei comandi o avviare il processo dell'agente snapshot per generare un nuovo snapshot. Per altre informazioni, vedere [Creazione e applicazione dello snapshot iniziale](../create-and-apply-the-initial-snapshot.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>Per modificare le proprietà dello snapshot di una pubblicazione di tipo merge esistente  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Specificare il valore **1** per **@force_invalidate_snapshot** e uno dei valori seguenti per **@property**:  
  
    -   **alt_snapshot_folder** : specificare anche un nuovo percorso per la cartella snapshot alternativa **@value**.  
  
    -   **compress_snapshot** : specificare anche il valore **true** o **false** per **@value** per indicare se i file di snapshot nella cartella snapshot alternativa sono compressi nel formato di file CAB.  
  
    -   **pre_snapshot_script** : **@value** specificare anche il nome del file e il percorso completo di un file con **estensione SQL** che verrà eseguito nel Sottoscrittore durante l'inizializzazione prima dell'applicazione dello snapshot iniziale.  
  
    -   **post_snapshot_script** : **@value** specificare anche il nome del file e il percorso completo di un file con **estensione SQL** che verrà eseguito nel Sottoscrittore durante l'inizializzazione dopo l'applicazione dello snapshot iniziale.  
  
    -   **snapshot_in_defaultfolder** : specificare anche il valore **true** o **false** per indicare se lo snapshot è disponibile solo in un percorso non predefinito.  
  
2.  Eseguire [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) dal prompt dei comandi o avviare il processo dell'agente snapshot per generare un nuovo snapshot. Per altre informazioni, vedere [Creazione e applicazione dello snapshot iniziale](../create-and-apply-the-initial-snapshot.md).  
  
## <a name="example"></a>Esempio  
 In questo esempio viene creata una pubblicazione che utilizza una cartella snapshot alternativa e uno snapshot compresso.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubaltsnapshot.sql#sp_mergealtsnapshot)]  
  
## <a name="see-also"></a>Vedere anche  
 [Percorsi alternativi cartella snapshot](../alternate-snapshot-folder-locations.md)   
 [Snapshot compressi](../compressed-snapshots.md)   
 [Eseguire gli script prima e dopo l'applicazione dello snapshot](../snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Trasferire snapshot tramite FTP](../transfer-snapshots-through-ftp.md)   
 [Modificare le proprietà di pubblicazioni e articoli](change-publication-and-article-properties.md)  
  
  
