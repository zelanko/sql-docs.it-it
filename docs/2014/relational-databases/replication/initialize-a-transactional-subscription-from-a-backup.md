---
title: Inizializzare una sottoscrizione transazionale da un backup (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1563d58f2d54f77680781e22a162112ade1658e4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85057107"
---
# <a name="initialize-a-transactional-subscription-from-a-backup-replication-transact-sql-programming"></a>Inizializzazione di una sottoscrizione transazionale da un backup (programmazione Transact-SQL della replica)
  Anche se una sottoscrizione di una pubblicazione transazionale viene in genere inizializzata con uno snapshot, è possibile inizializzarla da un backup utilizzando le stored procedure di replica. Per altre informazioni, vedere [Inizializzazione di una sottoscrizione transazionale senza uno snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>Per inizializzare un Sottoscrittore transazionale da un backup  
  
1.  Per una pubblicazione esistente, assicurarsi che la pubblicazione supporti la funzionalità di inizializzazione da backup eseguendo [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) nel database di pubblicazione del server di pubblicazione. Si noti il valore di **allow_initialize_from_backup** nel set di risultati.  
  
    -   Se il valore è **1**, la pubblicazione supporta questa funzionalità.  
  
    -   Se il valore è **0**, eseguire [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) nel database di pubblicazione nel server di pubblicazione. Specificare il valore **allow_initialize_from_backup** per ** \@ Property** e il valore `true` per ** \@ value**.  
  
2.  Per una nuova pubblicazione, eseguire [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) nel database di pubblicazione nel server di pubblicazione. Specificare il valore `true` per **allow_initialize_from_backup**. Per ulteriori informazioni, vedere la pagina relativa alla [creazione di una pubblicazione](publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Per evitare la mancanza di dati del Sottoscrittore, quando si utilizza **sp_addpublication** con `@allow_initialize_from_backup = N'true'`, utilizzare sempre `@immediate_sync = N'true'`.  
  
3.  Creare un backup del database di pubblicazione usando l'istruzione [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
4.  Ripristinare il backup nel Sottoscrittore usando l'istruzione [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
5.  Nel database di pubblicazione del server di pubblicazione eseguire la stored procedure [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Specificare i parametri seguenti:  
  
    -   ** \@ sync_type** : valore **Initialize with backup**.  
  
    -   ** \@ backupdevicetype** : tipo di dispositivo di backup, ovvero **Logical** (impostazione predefinita), **disk**o **Tape**.  
  
    -   ** \@ backupdevicename** : dispositivo di backup logico o fisico da usare per il ripristino.  
  
         Per un dispositivo logico, specificare il nome del dispositivo di backup indicato durante la creazione dello stesso tramite **sp_addumpdevice** .  
  
         Per un dispositivo fisico, specificare un nome e un percorso completo di file, ad esempio `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\BACKUP\Mybackup.dat'` o `TAPE = '\\.\TAPE0'`.  
  
    -   Opzionale ** \@ password** : password fornita al momento della creazione del set di backup.  
  
    -   Opzionale ** \@ MEDIAPASSWORD** : password specificata durante la formattazione del set di supporti.  
  
    -   Opzionale ** \@ fileidhint** : identificatore per il set di backup da ripristinare. Ad esempio, **1** indica il primo set di backup sul supporto, mentre **2** indica il secondo set di backup.  
  
    -   (Facoltativo per i dispositivi a nastro) ** \@ unload** : specificare il valore **1** (impostazione predefinita) se il nastro deve essere scaricato dall'unità al termine del ripristino e **0** se non deve essere scaricato.  
  
6.  (Facoltativo) Per una sottoscrizione pull, eseguire [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql) e [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) nel database di sottoscrizione del Sottoscrittore. Per altre informazioni, vedere [Creazione di una sottoscrizione pull](create-a-pull-subscription.md).  
  
7.  (Facoltativo) Avviare l'agente di distribuzione. Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) o [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Copiare database tramite backup e ripristino](../databases/copy-databases-with-backup-and-restore.md)   
 [Backup e ripristino di database SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
