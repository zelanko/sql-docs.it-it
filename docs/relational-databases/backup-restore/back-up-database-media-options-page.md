---
title: Backup database (pagina Opzioni supporti) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- swb.backupdatabase.mediaoptions.f1
- sql13.swb.backupdatabase.mediaoptions.f1
ms.assetid: eff36228-710c-4ed5-9af5-95859575dc0f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: efbd8b811b9dda44a4cc4609704291b9469edec3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "70155556"
---
# <a name="back-up-database-media-options-page"></a>Backup database (pagina Opzioni multimediali)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Usare la pagina  **Opzioni multimediali** della finestra di dialogo **Backup database** per visualizzare o modificare le opzioni multimediali del database.  
  
 **Per creare un backup utilizzando SQL Server Management Studio**  
  
-   [Creazione di un backup completo del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Creare un backup differenziale del database &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  È possibile definire un piano di manutenzione database per creare backup di database. Per altre informazioni, vedere [Piani di manutenzione](../../relational-databases/maintenance-plans/maintenance-plans.md) e [Usare la Creazione guidata piano di manutenzione](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
> [!NOTE]  
>  Quando si specifica un'attività di backup usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è possibile generare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) corrispondente facendo clic sul pulsante **Script** e selezionando una destinazione per lo script.  
  
## <a name="options"></a>Opzioni  
  
### <a name="overwrite-media"></a>Sovrascrivi supporti  
 Le opzioni del pannello **Sovrascrivi supporti** controllano la modalità di scrittura del backup nei supporti. Se è stato selezionato un URL (Archiviazione di Azure) come destinazione di backup nella pagina Generale della finestra di dialogo Backup database, le opzioni nella sezione Sovrascrivi supporti sono disabilitate. È possibile sovrascrivere un backup usando **BACKUP TO URL. WITH FORMAT** (istruzione Transact-SQL). Per altre informazioni, vedere [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  

 L'opzione **Sovrascrivi supporti** è disabilitata se è stato selezionato **URL** come destinazione di backup nella pagina **Generale**.
  
 Solo l'opzione **Esegui backup in un nuovo set di supporti e cancella tutti i set di backup esistenti** è supportata con le opzioni di crittografia. Se si selezionano le opzioni nella sezione **Esegui backup nel set di supporti esistente**, le opzioni di crittografia nella pagina **Opzioni di backup** saranno disabilitate.  
  
> [!NOTE]  
>  Per informazioni sui set di supporti, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
**Esegui backup nel set di supporti esistente**: Consente di eseguire il backup del database in un set di supporti esistente. Selezionando questa opzione, vengono attivate tre opzioni.  
  
 Scegliere una delle opzioni seguenti:  
  
 - **Accoda al set di backup esistente**: Consente di accodare il set di backup a quello dei supporti esistente e di mantenere tutti i backup precedenti.  
  
 - **Sovrascrivi tutti i set di backup esistenti**: Consente di sostituire un eventuale backup precedente nei set di supporti esistenti con quello corrente.  
  
 - **Controlla nome set di supporti e scadenza set di backup**: Facoltativa. Se si esegue il backup in un set di supporti esistente, consente di richiedere che durante l'operazione di backup vengano verificati il nome e la data di scadenza dei set di backup.  
  
 - **Nome set di supporti**:  Facoltativa. Se l'opzione **Controlla nome set di supporti e scadenza set di backup** è selezionata, consente di specificare il nome del set di supporti da usare per l'operazione di backup.  
  
 - **Esegui backup in un nuovo set di supporti e cancella tutti i set di backup esistenti**:  Consente di utilizzare un nuovo set di supporti, cancellando i set di backup precedenti.  
  
 Se si seleziona questa opzione, verranno attivate le opzioni seguenti:  
  
 - **Nome nuovo set di supporti**: Facoltativa. Consente di immettere un nuovo nome per il set di supporti.  
  
 - **Descrizione nuovo set di supporti**:  Facoltativa. Consente di immettere una descrizione significativa del nuovo set di supporti. La descrizione deve essere sufficientemente specifica da indicare il contenuto in modo accurato.  
  
### <a name="reliability"></a>Affidabilità  
 Le opzioni del pannello **Log delle transazioni** controllano la gestione degli errori da parte dell'operazione di backup.  
  
 - **Verifica backup al termine**:  Consente di verificare che il set di backup sia completo e che tutti i volumi siano leggibili.  
  
 - **Esegui checksum prima della scrittura nei supporti**: Consente di verificare i checksum prima di scrivere nei supporti di backup. La selezione di questa opzione equivale a specificare l'opzione CHECKSUM nell'istruzione BACKUP di [!INCLUDE[tsql](../../includes/tsql-md.md)]. L'opzione può determinare un aumento del carico di lavoro e una riduzione della velocità effettiva dell'operazione di backup. Per informazioni sui checksum di backup, vedere [Possibili errori relativi ai supporti durante il backup e il ripristino &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 - **Continua in caso di errori**: L'operazione di backup deve continuare anche se si verificano errori.  
  
### <a name="transaction-log"></a>Log delle transazioni  
 Le opzioni del pannello **Log delle transazioni** controllano il comportamento del backup del log delle transazioni. Tali opzioni sono rilevanti solo nel modello di recupero con registrazione completa o nel modello di recupero con registrazione minima delle operazioni bulk. Sono attivate solo se l'opzione **Log delle transazioni** è stata selezionata nel campo **Tipo backup** disponibile nella pagina [Generale](../../relational-databases/backup-restore/back-up-database-general-page.md) della finestra di dialogo **Backup database**.  
  
> [!NOTE]  
>  Per informazioni sui backup del log delle transazioni, vedere [Backup di log delle transazioni &#40; SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 **Tronca il log delle transazioni**  
 Consente di eseguire il backup del log delle transazioni e di troncarlo per liberare spazio per i log. Il database rimane online. Questa è l'opzione predefinita.  
  
 **Esegui backup della parte finale del log e lascia il database in stato di ripristino**  
 Consente di eseguire il backup della parte finale del log lasciando il database in stato di ripristino. Questa opzione crea un *backup della parte finale del log*, che consente di eseguire il backup dei log non ancora sottoposti a questa procedura (il log attivo), in genere per la preparazione del ripristino di un database. Il database non sarà disponibile per gli utenti finché non viene ripristinato completamente.  
  
 La selezione di questa opzione equivale a specificare l'opzione WITH NO_TRUNCATE, NORECOVERY in un'istruzione [BACKUP](../../t-sql/statements/backup-transact-sql.md) ([!INCLUDE[tsql](../../includes/tsql-md.md)]). Per altre informazioni, vedere [Backup della parte finale del log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
### <a name="tape-drive"></a>Unità nastro  
 Le opzioni del pannello **Unità nastro** controllano la gestione dei nastri durante l'operazione di backup. Queste opzioni sono attivate solo se l'opzione **Nastro** è stata selezionata nel campo **Destinazione** disponibile nella pagina [Generale](../../relational-databases/backup-restore/back-up-database-general-page.md) della finestra di dialogo **Backup database**.  
  
> [!NOTE]  
>  Per informazioni sull'uso dei dispositivi nastro, vedere [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 - **Scarica nastro al termine del backup**: Consente di scaricare il nastro al termine del backup.  
  
 - **Riavvolgi il nastro prima di scaricarlo**: Consente di rilasciare e riavvolgere il nastro prima di scaricarlo. Questa opzione è abilitata solo se è selezionata l'opzione **Scarica nastro al termine del backup** .  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Backup di un log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Backup di file e filegroup &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Esecuzione del backup del log delle transazioni quando il database è danneggiato &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
