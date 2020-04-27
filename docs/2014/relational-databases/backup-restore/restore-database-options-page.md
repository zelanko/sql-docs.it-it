---
title: Ripristina database (pagina Opzioni) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoredb.options.f1
ms.assetid: 9a75d48b-c25f-40f3-8ea1-32cfa8211754
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 266c127a8ef38a1a5701de24f9442861e604d84d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62875640"
---
# <a name="restore-database-options-page"></a>Ripristina database (pagina Opzioni)
  Usare la pagina **Opzioni** della finestra di dialogo **Ripristina database** per modificare il comportamento e il risultato dell'operazione di ripristino.  
  
 **Per utilizzare SQL Server Management Studio per il ripristino del backup di un database**  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
-   [Definizione di un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  Quando si specifica un'attività di ripristino mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è possibile generare uno script [!INCLUDE[tsql](../../includes/tsql-md.md)] corrispondente in cui siano contenute le istruzioni RESTORE relative a tale operazione di ripristino. Per generare lo script, fare clic sul pulsante **Script** , quindi selezionare una destinazione. Per informazioni sulla sintassi di RESTORE, vedere [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
## <a name="options"></a>Opzioni  
  
### <a name="restore-options"></a>Opzioni di ripristino  
 Per modificare alcuni aspetti del comportamento dell'operazione di ripristino, usare le opzioni del pannello **Opzioni di ripristino** .  
  
 **Sovrascrivi il database esistente (WITH REPLACE)**  
 L'operazione di ripristino consentirà di sovrascrivere i file di qualsiasi database che attualmente sta usando il nome di database specificato nel campo **Ripristina fino a**disponibile nella pagina [Generale](../../integration-services/general-page-of-integration-services-designers-options.md) della finestra di dialogo **Ripristina database** . I file del database esistente verranno sovrascritti anche se si ripristinano backup di un diverso database con il nome del database esistente. La selezione di questa opzione equivale all'uso dell'opzione REPLACE in un'istruzione [RESTORE](/sql/t-sql/statements/restore-statements-arguments-transact-sql) ([!INCLUDE[tsql](../../includes/tsql-md.md)]).  
  
> [!CAUTION]  
>  Utilizzare questa opzione solo dopo un'attenta valutazione. Per altre informazioni, vedere [Argomenti RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
 **Mantieni le impostazioni di replica (WITH KEEP_REPLICATION)**  
 Consente di mantenere le impostazioni di replica durante il ripristino di un database pubblicato in un server diverso da quello in cui è stato creato il database. Questa opzione è pertinente solo se è stata eseguita la replica del database al momento della creazione del backup.  
  
 Questa opzione è disponibile solo in combinazione con l'opzione **Lascia il database pronto per l'utilizzo eseguendo il rollback delle transazioni di cui non è stato eseguito il commit** (descritta più avanti in questa tabella), che equivale al ripristino di un backup con l'opzione RECOVERY.  
  
 La selezione di questa opzione equivale all'uso dell'opzione KEEP_REPLICATION in un'istruzione [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) .  
  
 Per altre informazioni, vedere [Eseguire il backup e ripristino di database replicati](../replication/administration/back-up-and-restore-replicated-databases.md).  
  
 **Limita accesso al database ripristinato (WITH RESTRICTED_USER)**  
 Consente di rendere disponibile il database ripristinato solo per i membri di **db_owner**, **dbcreator**o **sysadmin**.  
  
 La selezione di questa opzione equivale all'utilizzo dell'opzione RESTRICTED_USER in un'istruzione RESTORE.  
  
### <a name="recovery-state"></a>Stato di recupero  
 Per determinare lo stato del database dopo l'operazione di ripristino, è necessario selezionare una delle opzioni del pannello **Stato di recupero** .  
  
 **RESTORE WITH RECOVERY**  
 Consente di recuperare il database dopo il ripristino del backup finale selezionato nella griglia **Set di backup da ripristinare**della pagina [Generale](../../integration-services/general-page-of-integration-services-designers-options.md). Questa opzione è quella predefinita ed equivale all'opzione WITH RECOVERY in un'istruzione [RESTORE](/sql/t-sql/statements/restore-statements-arguments-transact-sql) ([!INCLUDE[tsql](../../includes/tsql-md.md)]).  
  
> [!NOTE]  
>  Se viene utilizzato il modello di recupero con registrazione completa o il modello di recupero con registrazione minima delle operazioni bulk, selezionare questa opzione solo se si stanno ripristinando tutti i file di log.  
  
 **RESTORE WITH NORECOVERY**  
 Il database viene lasciato nello stato di ripristino. Ciò consente di ripristinare backup aggiuntivi nel percorso di recupero corrente. Per recuperare il database, sarà necessario eseguire un'operazione di ripristino utilizzando l'opzione RESTORE WITH RECOVERY (vedere l'opzione precedente).  
  
 Questa opzione equivale all'opzione WITH NORECOVERY in un'istruzione RESTORE.  
  
 Selezionando questa opzione, l'opzione **Mantieni le impostazioni di replica** non sarà disponibile.  
  
 **RESTORE WITH STANDBY**  
 Lascia il database nello stato di standby, nel quale risulta disponibile per l'accesso limitato di sola lettura. Questa opzione equivale all'opzione WITH STANDBY in un'istruzione RESTORE.  
  
 Se si seleziona questa opzione, è necessario specificare un file standby nella casella di testo **File standby** . Il file standby consente di annullare gli effetti del recupero.  
  
 **File standby**  
 Consente di specificare un file standby. È possibile cercare il file standby oppure digitarne il percorso direttamente nella casella di testo.  
  
### <a name="tail-log-backup"></a>Backup della parte finale del log  
 Consente di specificare che il backup della parte finale del log venga eseguito insieme al ripristino del database.  
  
 **Esegui backup della parte finale del log prima del ripristino**  
 Selezionare questa casella per specificare la necessità di eseguire un backup della parte finale del log.  
  
> [!NOTE]  
>  Se per la temporizzazione selezionata nella finestra di dialogo [Cronologia di backup](backup-timeline.md) è richiesto il backup della parte finale del log, questa casella sarà selezionata e non sarà possibile modificarla.  
  
 **File di backup**  
 Specifica un file di backup per la parte finale del log. È possibile cercare il file di backup oppure immetterne il nome direttamente nella casella di testo.  
  
### <a name="server-connections"></a>Connessioni server  
 Consente di chiudere le connessioni di database esistenti.  
  
 **Chiudi connessioni esistenti**  
 Le operazioni di ripristino potrebbero non riuscire in presenza di connessioni attive al database. Selezionare l'opzione **Chiudi connessioni esistenti** per garantire che tutte le connessioni attive tra [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e il database vengano chiuse. Questa casella di controllo imposta il database sulla modalità utente singolo prima di effettuare qualsiasi operazione di ripristino e imposta il database sulla modalità multiutente al termine.  
  
### <a name="prompt"></a>Prompt  
 **Chiedi conferma prima del ripristino di ogni backup**  
 Consente di specificare che dopo il ripristino di ogni backup venga visualizzata la finestra di dialogo **Continua con il ripristino** per richiedere se continuare la sequenza di ripristino. In questa finestra di dialogo vengono visualizzati il nome del set di supporti successivo, se noto, nonché il nome e la descrizione del set di backup successivo.  
  
 Questa opzione consente di sospendere una sequenza di ripristino dopo aver ripristinato un backup e risulta particolarmente utile quando è necessario cambiare nastri per set di supporti diversi, ad esempio quando il server dispone di un solo dispositivo nastro. Quando si è pronti per procedere, fare clic su **OK**.  
  
 È possibile interrompere una sequenza di ripristino facendo clic su **No**. Tale operazione consente di lasciare il database nello stato di ripristino. A seconda delle proprie esigenze, è possibile continuare la sequenza di ripristino riprendendo dal backup successivo descritto nella finestra di dialogo **Continua con il ripristino** . La procedura di ripristino del backup successivo dipende dalla presenza o meno di dati o del log delle transazioni in tale backup, come indicato di seguito:  
  
-   Se il backup successivo è un backup completo o differenziale, usare nuovamente l'attività **Ripristina database** .  
  
-   Se il backup successivo è un backup del file, usare l'attività **Ripristina file e filegroup**. Per altre informazioni, vedere [Ripristinare file e filegroup &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md).  
  
-   Se il backup successivo è un backup del log, utilizzare l'attività **Ripristina log delle transazioni** . Per informazioni sulla ripresa di una sequenza di ripristino con il ripristino di un log delle transazioni, vedere [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Ripristino di un backup da un dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)   
 [Ripristinare un backup del log delle transazioni &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [Applicare backup del log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Ripristina database &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
