---
title: Backup completi del file (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- backing up [SQL Server], files or filegroups
- backups [SQL Server], files or filegroups
- full recovery model [SQL Server], full file backups
- file backups [SQL Server], full
- files [SQL Server], backing up
- filegroups [SQL Server], backing up
- file backups [SQL Server]
ms.assetid: a716bf8d-0c5a-490d-aadd-597b3b0fac0c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1d70bf0d8e99d24ee0d7ea9e046090ba4ed32453
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939620"
---
# <a name="full-file-backups-sql-server"></a>Backup completi del file (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Le informazioni contenute in questo argomento sono rilevanti per i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che includono più file o filegroup.  
  
 È possibile eseguire il backup e il ripristino dei singoli file contenuti in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Inoltre, è possibile specificare un intero filegroup anziché ogni singolo file componente. Tuttavia, se un qualsiasi file di un filegroup è offline, ad esempio perché il file è in fase di ripristino, l'intero filegroup risulterà offline e non sarà possibile eseguirne il backup.  
  
 I backup di file relativi a filegroup di sola lettura possono essere combinati con backup parziali. Nei backup parziali sono inclusi tutti i filegroup di lettura/scrittura e, facoltativamente, uno o più filegroup di sola lettura. Per altre informazioni, vedere [Backup parziali &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
 Un backup di file può fungere da *base differenziale* per backup differenziali di file. Per altre informazioni, vedere [Backup differenziali &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
> [!NOTE]  
>  I backup completi dei file in genere vengono definiti semplicemente *backup dei file*, tranne quando vengono confrontati in modo esplicito con i *backup differenziali dei file*.  
  
 **Contenuto dell'argomento:**  
  
-   [Vantaggi dei backup di file](#Benefits)  
  
-   [Svantaggi dei backup di file](#Disadvantages)  
  
-   [Panoramica dei backup di file](#Overview)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="Benefits"></a> Vantaggi dei backup di file  
 Rispetto ai backup completi del database, i backup di file offrono i seguenti vantaggi:  
  
-   L'utilizzo dei backup dei file può accelerare il processo di recupero, in quanto consente di ripristinare solo i file danneggiati, anziché l'intero database.  
  
     Se, ad esempio, un database è costituito da più file che si trovano in dischi diversi, in caso di errore di uno dei dischi sarà sufficiente ripristinare il file che si trova in tale disco. È possibile ripristinare il file danneggiato rapidamente e il tempo di recupero è minore rispetto al tempo richiesto per un intero database.  
  
-   I backup di file offrono maggiore flessibilità nella pianificazione e nella gestione dei supporti rispetto ai backup completi del database, che possono diventare poco gestibili in caso di database di dimensioni molto grandi. La maggiore flessibilità dei backup di file o filegroup risulta utile anche per database di grandi dimensioni che includono dati con caratteristiche di aggiornamento variabili.  
  
##  <a name="Disadvantages"></a> Svantaggi dei backup di file  
  
-   Lo svantaggio principale dei backup di file rispetto ai backup del database è un aumento della complessità a livello amministrativo. Il mantenimento e la registrazione di un set completo di questi backup può essere un'attività dispendiosa in termini di tempo e può richiedere uno spazio superiore a quello previsto per i backup completi del database.  
  
-   Un errore di un supporto può rendere irrecuperabile un intero database se manca un backup di un file danneggiato. È quindi necessario creare un intero set di backup di file e, nel caso del modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk, uno o più backup del log che coprano almeno l'intervallo tra il primo backup completo di file e l'ultimo backup completo di file.  
  
##  <a name="Overview"></a> Panoramica dei backup di file  
 Durante un backup completo di file viene creata una copia di backup di tutti i dati presenti in uno o più file o filegroup. Nei backup di file è contenuto, per impostazione predefinita, un numero sufficiente di record del log per il rollforward del file fino al termine dell'operazione di backup.  
  
 Il backup di un file o un filegroup di sola lettura è identico per tutti i modelli di recupero. In base al modello di recupero con registrazione completa, un intero set di backup completi di file corrisponde, insieme a un numero sufficiente di backup del log tale da coprire tutti i backup di file, a un backup completo del database.  
  
 È possibile eseguire una sola operazione di backup del file alla volta. È possibile eseguire il backup di più file durante una singola operazione, ma si tenga presente che ciò potrebbe comportare un allungamento del tempo di esecuzione del recupero quando è necessario ripristinare un singolo file, perché per individuare tale file è necessario leggere l'intero backup.  
  
> [!NOTE]  
>  Sebbene sia possibile ripristinare singoli file da un backup del database, l'individuazione e il ripristino di un file da un backup del database, anziché da un backup di file, richiedono maggior tempo.  
  
### <a name="file-backups-and-the-simple-recovery-model"></a>Backup di file e modello di recupero con registrazione minima  
 In base al modello di recupero con registrazione minima, è necessario creare una copia di backup contenente tutti i file di lettura/scrittura, al fine di garantire che il database possa essere ripristinato fino a un punto nel tempo consistente. Anziché specificare singolarmente ogni file o filegroup di lettura/scrittura, utilizzare l'opzione READ_WRITE_FILEGROUPS. Questa opzione consente di eseguire il backup di tutti i filegroup di lettura/scrittura del database. Un backup creato con l'opzione READ_WRITE_FILEGROUPS è noto come backup parziale. Per altre informazioni, vedere [Backup parziali &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
### <a name="file-backups-and-the-full-recovery-model"></a>Backup di file e modello di recupero con registrazione completa  
 In base al modello di recupero con registrazione completa, è necessario eseguire il backup del log delle transazioni indipendentemente dalla strategia di backup in uso. Un intero set di backup completi di file corrisponde, insieme a un numero sufficiente di backup del log tale da coprire tutti i backup di file dall'inizio del primo backup di file, a un backup completo del database.  
  
 Il ripristino di un database solo tramite backup di file e del log può essere un'operazione complessa. Se possibile, è quindi consigliabile eseguire un backup completo del database e far iniziare i backup del log prima del primo backup di file. Nella figura seguente viene illustrata una strategia che prevede l'esecuzione di un backup completo del database (punto t1) subito dopo la creazione del database (punto t0). Questo primo backup del database consente di avviare i backup del log delle transazioni, che vengono pianificati in modo da essere eseguiti a intervalli prestabiliti. I backup di file vengono eseguiti in base all'intervallo più appropriato alle esigenze aziendali per il database. In questa figura viene illustrato il backup in successione di ognuno dei quattro filegroup. L'ordine in cui viene eseguito il backup (A, C, B, A) è basato sulle esigenze aziendali per il database.  
  
 ![Strategia che combina backup di database, file e log](../../relational-databases/backup-restore/media/bnr-rmfull-3-fulldb-filegrps-log-backups.gif "Strategia che combina backup di database, file e log")  
  
> [!NOTE]  
>  In base al modello di recupero con registrazione completa, è necessario eseguire il rollforward del log delle transazioni durante il ripristino di un backup di file di lettura/scrittura, per garantire che il file sia consistente con la parte restante del database. Per evitare il rollforward di numerosi backup del log delle transazioni, è consigliabile utilizzare backup differenziali di file. Per altre informazioni, vedere [Backup differenziali &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per creare backup di file o filegroup**  
  
-   [Backup di file e filegroup &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
> [!NOTE]  
>  I backup di file non sono supportati dalla Creazione guidata piano di manutenzione.  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Backup e ripristino: interoperabilità e coesistenza &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Backup differenziali &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Ripristini di file &#40;modello di recupero con registrazione minima&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Ripristini di file &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Ripristino online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
