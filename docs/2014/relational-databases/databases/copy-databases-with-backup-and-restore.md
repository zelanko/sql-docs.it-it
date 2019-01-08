---
title: Copiare database tramite backup e ripristino | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], back up and restore
- restoring databases [SQL Server], previous SQL Server versions
- database restores [SQL Server], copying databases
- restoring databases [SQL Server], onto another server instance
- restoring [SQL Server], onto another server instance
- backing up databases [SQL Server], copying databases
- database backups [SQL Server], copying databases
ms.assetid: b93e9701-72a0-408e-958c-dc196872c040
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a35156a465e521ceea60fa090142836da6a4c1a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52787833"
---
# <a name="copy-databases-with-backup-and-restore"></a>Copiare database tramite backup e ripristino
  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è possibile creare un nuovo database ripristinando un backup di un database utente creato tramite [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versione successiva. Tuttavia, i backup di **master**, **model** e **msdb** creati con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non possono essere ripristinati da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Inoltre, i backup di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non possono essere ripristinati da una qualsiasi versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] viene utilizzato un percorso predefinito diverso rispetto alle versioni precedenti. Pertanto, per ripristinare i backup di un database creato nel percorso predefinito di versioni precedenti, è necessario utilizzare l'opzione MOVE. Per informazioni sul nuovo percorso predefinito, vedere [Percorsi dei file per le istanze predefinite e denominate di SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md). Per altre informazioni sullo spostamento dei file di database, vedere "Spostamento dei file di database" di seguito in questo argomento.  
  
## <a name="general-steps-for-using-backup-and-restore-to-copy-a-database"></a>Procedura generale per l'utilizzo di operazioni di backup e ripristino per copiare un database  
 Quando si utilizza un'operazione di backup e ripristino per copiare un database in un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i computer di origine e di destinazione possono utilizzare qualsiasi piattaforma sulla quale viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Di seguito sono indicati i passaggi fondamentali:  
  
1.  Effettuare il backup del database di origine che può risiedere in un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive. Il computer in cui è in esecuzione questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è il *computer di origine*.  
  
2.  Nel computer in cui si desidera copiare il database (il *computer di destinazione*), connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su cui si prevede di ripristinare il database. Se necessario, sull'istanza del server di destinazione, creare gli stessi dispositivi di backup utilizzati dal backup dei database di origine.  
  
3.  Ripristinare il backup del database di origine sul computer di destinazione. Il ripristino del database determina la creazione automatica di tutti i file del database.  
  
 Negli argomenti riportati di seguito sono illustrate considerazioni aggiuntive che possono avere effetto su questo processo.  
  
## <a name="before-you-restore-database-files"></a>Operazioni preliminari al ripristino dei file di database  
 Il ripristino di un database determina la creazione automatica dei file di database necessari al database in fase di ripristino. Per impostazione predefinita, per i file creati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante il processo di ripristino vengono utilizzati gli stessi nomi e percorsi dei file di backup del database originale nel computer di origine.  
  
 Facoltativamente, quando si ripristina il database, è possibile specificare il mapping dei dispositivi, i nomi dei file oppure il percorso per il database in fase di ripristino. Tale operazione potrebbe essere necessaria nelle situazioni seguenti:  
  
-   La struttura di directory o il mapping delle unità utilizzato dal database nel computer originale non è più disponibile nell'altro computer. Si supponga, ad esempio, che nel backup sia incluso un file che, per impostazione predefinita, verrebbe ripristinato all'unità E, ma tale unità non è disponibile nel computer di destinazione.  
  
-   Lo spazio nel percorso di destinazione non è sufficiente.  
  
-   Si sta riutilizzando un nome del database già presente nella destinazione di ripristino e il nome di qualsiasi file contenuto nel database è uguale al file di database del set di backup, pertanto si verifica una delle situazioni indicate di seguito.  
  
    -   Se è possibile sovrascrivere il file di database esistente, verrà sovrascritto (ciò non influisce su un file appartenente a un nome di database diverso).  
  
    -   Se non è possibile sovrascrivere il file esistente, si verifica un errore di ripristino.  
  
 Per evitare errori e conseguenze impreviste, prima dell'operazione di ripristino, è possibile usare la [backupfile](/sql/relational-databases/system-tables/backupfile-transact-sql) tabella di cronologia per trovare i file di database e log nel backup si intende ripristinare.  
  
## <a name="moving-the-database-files"></a>Spostamento dei file di database  
 Se per i motivi elencati in precedenza non è possibile ripristinare i file di backup del database nel computer di destinazione, sarà necessario spostare i file in un nuovo percorso mano a mano che vengono ripristinati, Ad esempio:  
  
-   Si supponga di voler ripristinare un database da backup creati nella posizione predefinita di versioni precedenti.  
  
-   Per problemi di spazio, potrebbe essere necessario ripristinare alcuni file di database nel backup in un'altra unità disco. Questa eventualità può verificarsi frequentemente, in quanto la maggior parte dei computer di un'organizzazione non ha lo stesso numero o le stesse dimensioni di unità disco o configurazioni software identiche.  
  
-   Può essere necessario creare una copia di un database esistente sullo stesso computer, a scopo di prova. In questo caso i file del database originale esistono già, quindi al momento della creazione della copia del database tramite l'operazione di ripristino sarà necessario specificare nomi di file diversi.  
  
 Per altre informazioni, vedere "Per ripristinare file e filegroup in una nuova posizione" di seguito in questo argomento.  
  
## <a name="changing-the-database-name"></a>Modifica del nome del database  
 Il nome del database può essere modificato al momento del ripristino nel computer di destinazione. Non è necessario ripristinare il database e quindi modificare il nome manualmente. Ad esempio, può risultare necessario cambiare il nome del database da **Sales** a **SalesCopy** per indicare che si tratta di una copia.  
  
 Il nome del database specificato esplicitamente al momento del ripristino viene utilizzato automaticamente come nuovo nome del database. Poiché il nome del database non esiste, viene creato un database con il nuovo nome tramite i file presenti nel backup.  
  
## <a name="when-upgrading-a-database-by-using-restore"></a>Aggiornamento di un database utilizzando il ripristino  
 Nel ripristino dei backup da una versione precedente può essere utile sapere in anticipo se il percorso (unità e directory) di ogni catalogo full-text di un backup sia esistente sul computer di destinazione. Per un elenco dei nomi logici e fisici (percorso e nome file) di ogni file in un backup, inclusi i file di catalogo, usare un'istruzione RESTORE FILELISTONLY FROM *<dispositivo_backup>*. Per altre informazioni, vedere [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql).  
  
 Se lo stesso percorso non esiste sul computer di destinazione, sono disponibili due alternative:  
  
-   Creare il mapping di unità/directory equivalente sul computer di destinazione.  
  
-   Spostare i file di catalogo in una nuova posizione durante l'operazione di ripristino, utilizzando la clausola WITH MOVE nell'istruzione RESTORE DATABASE. Per altre informazioni, vedere [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
 Per informazioni sulle opzioni alternative per l'aggiornamento degli indici full-text, vedere [Aggiornare la ricerca full-text](../search/upgrade-full-text-search.md).  
  
## <a name="database-ownership"></a>Proprietà dei database  
 Quando un database viene ripristinato in un altro computer, l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o l'utente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows che inizia l'operazione di ripristino diventa automaticamente il proprietario del nuovo database. Al momento del ripristino, l'amministratore di sistema o il nuovo proprietario del database possono modificare il proprietario del database. Per evitare ripristini non autorizzati di un database, impostare password per i supporti o i set di backup.  
  
## <a name="managing-metadata-when-restoring-to-another-server-instance"></a>Gestione dei metadati durante il ripristino di un'altra istanza del server  
 Quando si ripristina un database in un'altra istanza del server per offrire a utenti e applicazioni un sistema più coerente, può essere necessario ricreare alcuni o tutti i metadati del database, ad esempio account di accesso e processi, nell'altra istanza del server. Per altre informazioni, vedere [Gestione dei metadati quando si rende disponibile un database in un'altra istanza del server &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md).  
  
 **Per visualizzare i file di dati e i file di log in un set di backup**  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)  
  
 **Per ripristinare file e filegroup in un nuovo percorso**  
  
-   [Ripristinare file in un percorso nuovo &#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Ripristinare un Backup del Database &#40;SQL Server Management Studio&#41;](../backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **Per ripristinare file e filegroup sovrascrivendo file esistenti**  
  
-   [Ripristinare file e filegroup sovrascrivendo file esistenti &#40;SQL Server&#41;](../backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
 **Per ripristinare un database con un nuovo nome**  
  
-   [Ripristinare un Backup del Database &#40;SQL Server Management Studio&#41;](../backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **Per riavviare un'operazione di ripristino interrotta**  
  
-   [Riavviare un'operazione di ripristino interrotta &#40;Transact-SQL&#41;](../backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
 **Per modificare il proprietario di un database**  
  
-   [sp_changedbowner &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedbowner-transact-sql)  
  
 **Copiare un database usando SQL Server Management Objects (SMO)**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadFileList%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.RelocateFiles%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReplaceDatabase%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
## <a name="see-also"></a>Vedere anche  
 [Copia di database in altri server](copy-databases-to-other-servers.md)   
 [Percorsi dei file per le istanze predefinite e denominate di SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
