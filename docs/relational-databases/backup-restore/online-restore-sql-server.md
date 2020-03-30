---
title: Ripristino in linea (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- online restores [SQL Server]
- online restores [SQL Server], about online restores
ms.assetid: 7982a687-980a-4eb8-8e9f-6894148e7d8c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: e4f5817fe575422dddeedd525b077dbf643a29b2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "72908874"
---
# <a name="online-restore-sql-server"></a>Ripristino in linea (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Il ripristino in linea è supportato solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition. In questa edizione un ripristino di file, pagina o a fasi viene eseguito online per impostazione predefinita. Le informazioni contenute in questo argomento sono importanti per i database che includono più file o filegroup e, in base al modello di recupero con registrazione minima, solo per i filegroup di sola lettura.  
  
 Il ripristino di dati mentre il database è online è denominato *ripristino online*. Un database viene considerato online quando il filegroup primario è online, anche se uno o più filegroup secondari sono offline. Tutti i modelli di recupero consentono di ripristinare un file offline mentre il database è online. Il modello di recupero con registrazione completa consente inoltre di ripristinare pagine mentre il database è online.  
  
> [!NOTE]  
>  Il ripristino in linea viene eseguito in modo automatico in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise e non richiede alcun intervento dell'utente. Se non si desidera utilizzare il ripristino online, è possibile attivare la modalità offline per un database prima di avviare un'operazione di ripristino. Per ulteriori informazioni, vedere [Attivazione della modalità offline per un database o un file](#taking_db_or_file_offline)di seguito in questo argomento.  
  
 Durante un ripristino di file online, tutti i file in fase di ripristino e il relativo filegroup devono essere in modalità offline. Se uno qualsiasi di questi file è online quando viene avviata un'operazione di ripristino online, la prima istruzione di ripristino attiva la modalità offline per il filegroup di tale file. Durante un ripristino di pagina online, è invece necessario che sia in modalità offline solo la pagina.  
  
 Per qualsiasi scenario di ripristino online è necessario eseguire la procedura di base seguente:  
  
1.  Ripristinare i dati.  
  
2.  Ripristinare il log utilizzando l'opzione WITH RECOVERY per l'ultimo ripristino del log. Verrà attivata la modalità online per i dati ripristinati.  

 In alcuni casi non è possibile eseguire il rollback di una transazione di cui non è stato eseguito il commit perché i dati necessari per il rollback sono offline durante l'avvio. In tali casi, la transazione viene posticipata. Per altre informazioni, vedere [Transazioni posticipate &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).  
  
> [!NOTE]  
>  Se il database attualmente utilizza il modello di recupero con registrazione minima delle operazioni bulk, prima di avviare un'operazione di ripristino online è consigliabile passare al modello di recupero con registrazione completa. Per altre informazioni, vedere [Visualizzazione o modifica del modello di recupero di un database &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
> [!IMPORTANT]  
>  Se i backup sono stati eseguiti con più dispositivi collegati al server, è necessario che sia disponibile lo stesso numero di dispositivi durante un'operazione di ripristino online.  
  
> [!CAUTION]  
>  Quando si usano backup di snapshot, non è possibile eseguire un **ripristino in linea**. Per altre informazioni sul **backup di snapshot**, vedere [Backup di snapshot di file per i file di database in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
## <a name="log-backups-for-online-restore"></a>Backup del log per il ripristino online  
 In un ripristino online il punto di recupero corrisponde all'ultimo punto in cui è stata attivata la modalità offline o impostata l'autorizzazione di sola lettura per i dati in fase di ripristino. I backup del log delle transazioni fino a tale punto di recupero incluso devono essere tutti disponibili. In genere, è necessario eseguire un backup del log dopo tale punto in modo da includere il punto di recupero per il file. L'unica eccezione si verifica durante un ripristino online di dati di sola lettura da un backup dei dati che è stato eseguito dopo l'impostazione dell'autorizzazione di sola lettura. In tal caso, non è necessario che sia disponibile un backup del log.  
  
 In genere, è possibile eseguire backup del log delle transazioni mentre il database è online, anche dopo l'avvio della sequenza di ripristino. Il momento in cui deve essere eseguito l'ultimo backup del log dipende dalle proprietà del file in fase di ripristino:  
  
-   Per un file di sola lettura online, è possibile eseguire l'ultimo backup del log necessario per l'operazione di recupero durante la prima sequenza di ripristino o prima di essa. Per un filegroup di sola lettura, i backup del log potrebbero non essere necessari se è stato eseguito un backup dei dati o differenziale dopo l'impostazione dell'autorizzazione di sola lettura.  
  
    > [!NOTE]  
    >  Le informazioni sopra riportate sono valide anche per i file offline.  
  
-   Un caso a parte riguarda un file di lettura/scrittura che era online quando è stata eseguita la prima istruzione di ripristino e per cui è stata attivata automaticamente la modalità offline da tale istruzione. In questo caso, è necessario eseguire un backup del log durante la prima *sequenza di ripristino* (sequenza di una o più istruzioni RESTORE per il ripristino, il rollforward e il recupero dei dati). In genere, questo backup del log deve essere eseguito dopo il ripristino di tutti i backup completi e prima del recupero dei dati. Se, tuttavia, esistono più backup di file per un filegroup specifico, il punto minimo del backup del log corrisponde al momento successivo all'attivazione della modalità offline per il filegroup. Questo backup del log successivo al ripristino dei dati include il punto in cui è stata attivata la modalità offline per il file ed è necessario perché il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] non può utilizzare log online per un ripristino online.  
  
    > [!NOTE]  
    >  In alternativa, è possibile attivare manualmente la modalità offline per il file prima di eseguire la sequenza di ripristino. Per ulteriori informazioni, vedere "Attivazione della modalità offline per un database o un file" di seguito in questo argomento.  
  
##  <a name="taking-a-database-or-file-offline"></a><a name="taking_db_or_file_offline"></a> Attivazione della modalità offline per un database o un file  
 Se non si desidera utilizzare il ripristino online, è possibile attivare la modalità offline per il database prima di avviare la sequenza di ripristino utilizzando una delle modalità seguenti:  
  
-   Con qualsiasi modello di recupero è possibile attivare la modalità offline per il database utilizzando l'istruzione [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) seguente:  
  
     ALTER DATABASE *nome_database* SET OFFLINE  
  
-   In alternativa, se si utilizza il modello di recupero con registrazione completa, è possibile forzare un ripristino di file o pagina offline utilizzando l'istruzione [BACKUP LOG](../../t-sql/statements/backup-transact-sql.md) seguente per attivare lo stato di ripristino per il database:  
  
     BACKUP LOG *nome_database* WITH NORECOVERY.  
  
 Fino a quando il database rimane in modalità offline, tutti i ripristini eseguiti sono di tipo offline.  
  
## <a name="examples"></a>Esempi  
  
> [!NOTE]  
>  La sintassi di una sequenza di ripristino online è la stessa di una sequenza di ripristino offline.  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di un database &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Esempio: Ripristino a fasi di alcuni filegroup &#40;Modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di lettura/scrittura &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Ripristino di file e filegroup &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Ripristinare pagine &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)  
  
-   [Gestione della tabella suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
-   [Recuperare un database senza ripristino dei dati &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
-   [Rimuovere filegroup inattivi &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristini di file &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Ripristini di file &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Ripristino di pagine &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
  
  
