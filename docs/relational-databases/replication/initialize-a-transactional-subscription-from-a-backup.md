---
title: Inizializzare una sottoscrizione transazionale da un backup | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 466598ca9e7846b3b5ffbeef17987cd61233ec7a
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2019
ms.locfileid: "71251098"
---
# <a name="initialize-a-transactional-subscription-from-a-backup"></a>Inizializzare una sottoscrizione transazionale da un backup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Anche se una sottoscrizione di una pubblicazione transazionale viene in genere inizializzata con uno snapshot, è possibile inizializzarla da un backup utilizzando le stored procedure di replica. Per altre informazioni, vedere [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>Per inizializzare un Sottoscrittore transazionale da un backup  
  
1.  Per una pubblicazione esistente, assicurarsi che la pubblicazione supporti la funzionalità di inizializzazione da backup eseguendo [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) nel database di pubblicazione del server di pubblicazione. Si noti il valore di **allow_initialize_from_backup** nel set di risultati.  
  
    -   Se il valore è **1**, la pubblicazione supporta questa funzionalità.  
  
    -   Se il valore è **0**, eseguire [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) nel database di pubblicazione nel server di pubblicazione. Specificare il valore **allow_initialize_from_backup** per **@property** e il valore **true** per **@value** .  
  
2.  Per una nuova pubblicazione, eseguire [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) nel database di pubblicazione nel server di pubblicazione. Specificare il valore **true** per **allow_initialize_from_backup**. Per altre informazioni, vedere [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Per evitare la mancanza di dati del Sottoscrittore, quando si usa **sp_addpublication** o **sp_changepublication** con `@allow_initialize_from_backup = N'true'`, usare sempre `@immediate_sync = N'true'`.  
  
3.  Creare un backup del database di pubblicazione usando l'istruzione [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
4.  Ripristinare il backup nel Sottoscrittore usando l'istruzione [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
5.  Nel database di pubblicazione del server di pubblicazione eseguire la stored procedure [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Specificare i parametri seguenti:  
  
    -   **@sync_type** : valore **initialize with backup**.  
  
    -   **@backupdevicetype** : tipo di dispositivo di backup, ovvero **logical** (impostazione predefinita), **disk**o **tape**.  
  
    -   **@backupdevicename** : dispositivo di backup logica o fisica da utilizzare per il ripristino.  
  
         Per un dispositivo logico, specificare il nome del dispositivo di backup indicato durante la creazione dello stesso tramite **sp_addumpdevice** .  
  
         Per un dispositivo fisico, specificare un nome e un percorso completo di file, ad esempio `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` o `TAPE = '\\.\TAPE0'`.  
  
    -   (Facoltativo) **@password** : password specificata durante la creazione del set di backup.  
  
    -   (Facoltativo) **@mediapassword** : password specificata durante la formattazione del set di supporti.  
  
    -   (Facoltativo) **@fileidhint** : identificatore per il set di backup da ripristinare. Ad esempio, **1** indica il primo set di backup sul supporto, mentre **2** indica il secondo set di backup.  
  
    -   (Facoltativo per i dispositivi a nastro) **@unload** : specificare il valore **1** (impostazione predefinita) se il nastro deve essere scaricato dall'unità al termine del ripristino e **0** in caso contrario.  
  
6.  (Facoltativo) Per una sottoscrizione pull, eseguire [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) e [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) nel database di sottoscrizione del Sottoscrittore. Per altre informazioni, vedere [Creazione di una sottoscrizione pull](../../relational-databases/replication/create-a-pull-subscription.md).  
  
7.  (Facoltativo) Avviare l'agente di distribuzione. Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) o [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Copiare database tramite backup e ripristino](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
