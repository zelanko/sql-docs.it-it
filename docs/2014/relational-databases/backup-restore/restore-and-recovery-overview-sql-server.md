---
title: Panoramica del ripristino e del recupero (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring tables [SQL Server]
- backups [SQL Server], restore scenarios
- database backups [SQL Server], restore scenarios
- database restores [SQL Server]
- restoring [SQL Server]
- restores [SQL Server]
- table restores [SQL Server]
- restoring databases [SQL Server], about restoring databases
- database restores [SQL Server], scenarios
ms.assetid: e985c9a6-4230-4087-9fdb-de8571ba5a5f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2175ae19218592a2742aa1404ffa6620da333846
ms.sourcegitcommit: 5a9ec5e28543f106bf9e7aa30dd0a726bb750e25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925085"
---
# <a name="restore-and-recovery-overview-sql-server"></a>Panoramica del ripristino e del recupero (SQL Server)
  Per recuperare un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in seguito a un errore, il relativo amministratore deve ripristinare un set di backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in una sequenza di ripristino significativa e logicamente corretta. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano il ripristino di dati da backup di un intero database, di un file di dati o di una pagina di dati nelle modalità descritte di seguito:  
  
-   Database ( *ripristino di database completo*)  
  
     L'intero database viene ripristinato e recuperato e il database resta offline per la durata delle operazioni di ripristino e di recupero.  
  
-   File di dati ( *ripristino del file*)  
  
     Un file di dati o un set di file viene ripristinato e recuperato. Durante un ripristino del file, i filegroup che includono i file vengono impostati automaticamente come offline per la durata del ripristino. Qualsiasi tentativo di accedere a un filegroup offline provoca un errore.  
  
-   Pagina di dati ( *ripristino di pagina*)  
  
     Nel modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk è possibile ripristinare singoli database. Le operazioni di ripristino della pagina possono essere effettuate in qualsiasi database, indipendentemente dal numero di filegroup.  
  
 Il backup e il ripristino di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere utilizzati in tutti i sistemi operativi supportati, sia a 64 bit che a 32 bit. Per informazioni sui sistemi operativi supportati, vedere [requisiti hardware e software per l'installazione di SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). Per informazioni sul supporto dei backup di versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere la sezione "Supporto della compatibilità" di [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
 **Contenuto dell'argomento**  
  
-   [Panoramica degli scenari di ripristino](#RestoreScenariosOv)  
  
-   [Modelli di recupero e operazioni di ripristino supportate](#RMsAndSupportedRestoreOps)  
  
-   [Restrizioni relative al ripristino in base al modello di recupero con registrazione minima](#RMsimpleScenarios)  
  
-   [Ripristino in base al modello di recupero con registrazione minima delle operazioni bulk](#RMblogRestore)  
  
-   [Advisor per ripristino database (SQL Server Management Studio)](#DRA)  
  
-   [Contenuto correlato](#RelatedContent)  
  
##  <a name="overview-of-restore-scenarios"></a><a name="RestoreScenariosOv"></a> Panoramica degli scenari di ripristino  
 Uno *scenario di ripristino* in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è il processo di ripristino dei dati da uno o più backup, seguito dal recupero del database. Gli scenari di ripristino supportati dipendono dal modello di recupero del database e dall'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Nella tabella seguente vengono descritti i possibili scenari di ripristino supportati per modelli di recupero diversi.  
  
|scenario di ripristino|Nel modello di recupero con registrazione minima|Nel modello di recupero con registrazione completa o con registrazione minima delle operazioni bulk|  
|----------------------|---------------------------------|----------------------------------------------|  
|ripristino di database completo|Si tratta della strategia di ripristino standard. Un ripristino di database completo può comportare semplicemente il ripristino e il recupero di un backup completo del database. In alternativa, tale tipo di ripristino può comportare il ripristino di un backup completo del database seguito dal ripristino e dal recupero di un backup differenziale.<br /><br /> Per altre informazioni, vedere [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](complete-database-restores-simple-recovery-model.md).|Si tratta della strategia di ripristino standard. Un ripristino di database completo comporta il ripristino di un backup completo del database e, facoltativamente, di un backup differenziale, se disponibile, seguito dal ripristino di tutti i successivi backup del log, in sequenza. Il ripristino di database completo viene completato tramite il recupero dell'ultimo backup del log e il suo ripristino (RESTORE WITH RECOVERY).<br /><br /> Per altre informazioni, vedere [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](complete-database-restores-full-recovery-model.md).|  
|File restore **\***|Consente di ripristinare uno o più file di sola lettura danneggiati senza ripristinare l'intero database. È disponibile solo se il database contiene almeno un filegroup di sola lettura.|Consente di ripristinare uno o più file, senza ripristinare l'intero database. Può essere eseguito mentre il database è offline oppure, per alcune edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mentre il database rimane online. Durante un'operazione di ripristino del file, i filegroup che includono i file che vengono ripristinati sono sempre offline.|  
|Ripristino di pagine|Non applicabile|Consente di ripristinare una o più pagine danneggiate. Può essere eseguito mentre il database è offline oppure, per alcune edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mentre il database rimane online. Durante un'operazione di ripristino della pagina, le pagine che vengono ripristinate sono sempre offline.<br /><br /> Perché la pagina sia aggiornata rispetto al file di log corrente, è necessario che sia disponibile una catena non interrotta di backup del log, fino al file di log corrente, e che i backup vengano tutti applicati.<br /><br /> Per altre informazioni, vedere [Ripristinare pagine &#40;SQL Server&#41;](restore-pages-sql-server.md).|  
|Ripristino a fasi **\***|Consente di ripristinare e recuperare il database in varie fasi a livello di filegroup, partendo dal filegroup primario e da tutti i filegroup secondari di lettura/scrittura.|Consente di ripristinare e recuperare il database in varie fasi a livello di filegroup, partendo dal filegroup primario.|  
  
 **\*** Il ripristino in linea è supportato solo nell'Enterprise Edition.  
  
 Indipendentemente dalla modalità di ripristino dei dati, prima di poter recuperare un database, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verifica che l'intero database sia logicamente consistente. Se, ad esempio, si ripristina un file, non è possibile recuperarlo e attivare la modalità online finché non è stato eseguito un rollforward sufficiente a garantirne la coerenza con il database.  
  
### <a name="advantages-of-a-file-or-page-restore"></a>Vantaggi di un ripristino del file o della pagina  
 Il ripristino e il recupero di file o pagine, anziché dell'intero database, offrono i vantaggi seguenti:  
  
-   Il ripristino di una quantità minore di dati consente di ridurre il tempo necessario per la copia e il recupero.  
  
-   Se in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si esegue un'operazione di ripristino del file o della pagina, è possibile mantenere online altri dati del database durante l'operazione di ripristino.  
  
##  <a name="recovery-models-and-supported-restore-operations"></a><a name="RMsAndSupportedRestoreOps"></a>Modelli di recupero e operazioni di ripristino supportate  
 Le operazioni di ripristino disponibili per un database variano in base al relativo modello di recupero. Nella tabella seguente vengono riepilogati i casi e la misura in cui ognuno dei modelli di recupero supporta uno scenario di ripristino specifico.  
  
|Operazione di ripristino|Modello di recupero con registrazione completa|Modello di recupero con registrazione minima delle operazioni bulk|Modello di recupero con registrazione minima|  
|-----------------------|-------------------------|---------------------------------|---------------------------|  
|Recupero dati|Recupero completo (se il log è disponibile).|Rischio parziale di perdita di dati.|Tutti i dati successivi all'ultimo backup completo o differenziale vanno perduti.|  
|Ripristino temporizzato|Qualsiasi periodo di tempo coperto dai backup del log.|Non consentito se il backup del log contiene modifiche con registrazione minima delle operazioni bulk.|Non supportato.|  
|File restore **\***|Supporto completo.|In casi specifici. **\*\***|Disponibile solo per i file secondari di sola lettura.|  
|Page restore **\***|Supporto completo.|In casi specifici. **\*\***|No.|  
|Ripristino a fasi (a livello di filegroup) **\***|Supporto completo.|In casi specifici. **\*\***|Disponibile solo per i file secondari di sola lettura.|  
  
 **\*** Disponibile solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 **\*\*** Per le condizioni necessarie, vedere la sezione relativa alle [Restrizioni relative al ripristino in base al modello di recupero con registrazione minima](#RMsimpleScenarios)più avanti in questo argomento.  
  
> [!IMPORTANT]  
>  Indipendentemente dal modello di recupero di un database, un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può essere ripristinato da una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedente a quella tramite cui è stato creato il backup.  
  
##  <a name="restore-scenarios-under-the-simple-recovery-model"></a><a name="RMsimpleScenarios"></a>Scenari di ripristino nel modello di recupero con registrazione minima  
 Il modello di recupero con registrazione minima impone le restrizioni seguenti sulle operazioni di ripristino:  
  
-   Il ripristino del file e il ripristino a fasi sono disponibili solo per gruppi di file secondari in modalità di sola lettura. Per informazioni su questi scenari di ripristino, vedere [Ripristini di file &#40;modello di recupero con registrazione minima&#41;](file-restores-simple-recovery-model.md) e [Ripristini a fasi &#40;SQL Server&#41;](piecemeal-restores-sql-server.md).  
  
-   Il ripristino della pagina non è consentito.  
  
-   Il ripristino temporizzato non è consentito.  
  
 Se una o più di queste restrizioni non sono appropriate per le proprie esigenze di recupero, valutare se utilizzare il modello di recupero con registrazione completa. Per altre informazioni, vedere [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md).  
  
> [!IMPORTANT]  
>  Indipendentemente dal modello di recupero di un database, un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può essere ripristinato da una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedente a quella tramite cui è stato creato il backup.  
  
##  <a name="restore-under-the-bulk-logged-recovery-model"></a><a name="RMblogRestore"></a> Ripristino nel modello di recupero con registrazione minima delle operazioni bulk  
 In questa sezione vengono fornite informazioni sul ripristino proprie del modello di recupero con registrazione minima delle operazioni bulk da intendersi esclusivamente come integrazione del modello di recupero con registrazione completa.  
  
> [!NOTE]  
>  Per informazioni generali sul modello di recupero con registrazione minima delle operazioni bulk, vedere [Log delle transazioni &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md).  
  
 In linea generale, il modello di recupero con registrazione minima delle operazioni bulk è simile al modello di recupero con registrazione completa e le informazioni fornite per quest'ultimo si applicano a entrambi. Tuttavia, il recupero temporizzato e il ripristino in linea sono influenzati dal modello di recupero con registrazione minima delle operazioni bulk.  
  
### <a name="restrictions-for-point-in-time-recovery"></a>Restrizioni relative al recupero temporizzato  
 Se un backup del log eseguito utilizzando il modello di recupero con registrazione minima delle operazioni bulk contiene modifiche con registrazione minima delle operazioni bulk, il recupero temporizzato non è consentito. Se si tenta di eseguire il recupero temporizzato in un backup del log che contiene modifiche con registrazione minima delle operazioni bulk, l'operazione di ripristino non verrà eseguita correttamente.  
  
### <a name="restrictions-for-online-restore"></a>Restrizioni relative al ripristino online  
 Una sequenza di ripristino in linea funziona solo se vengono soddisfatte le condizioni seguenti:  
  
-   Tutti i backup del log necessari devono essere eseguiti prima dell'avvio della sequenza di ripristino.  
  
-   È necessario eseguire un backup delle modifiche bulk prima di avviare la sequenza del ripristino online.  
  
-   Se nel database sono presenti modifiche bulk, tutti i file devono essere online o[inattivi](remove-defunct-filegroups-sql-server.md). Questo significa che non è più parte del database.  
  
 Se queste condizioni non vengono soddisfatte, la sequenza del ripristino in linea non riesce.  
  
> [!NOTE]  
>  È consigliabile passare al modello di recupero con registrazione completa prima di avviare un ripristino online. Per altre informazioni, vedere [Modelli di recupero &#40;SQL Server&#41;](recovery-models-sql-server.md).  
  
 Per informazioni su come eseguire un ripristino online, vedere [Ripristino in linea &#40;SQL Server&#41;](online-restore-sql-server.md).  
  
##  <a name="database-recovery-advisor-sql-server-management-studio"></a><a name="DRA"></a> Database Recovery Advisor (SQL Server Management Studio)  
 Tramite Database Recovery Advisor viene semplificata la costruzione di piani di ripristino mediante i quali vengono implementate ottime sequenze di ripristino corrette. Molti problemi noti di ripristino del database sono stati risolti e sono stati apportati molti miglioramenti richiesti dai clienti. Di seguito sono riportati i miglioramenti principali introdotti da Database Recovery Advisor:  
  
-   **Algoritmo del piano di ripristino:**  l'algoritmo utilizzato per costruire i piani di ripristino è stato migliorato in modo significativo, in particolare per gli scenari di ripristino complessi. Molti casi limite, inclusi gli scenari di fork nei ripristini temporizzati, vengono gestititi in modo più efficiente rispetto alle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Ripristini temporizzati:**  tramite Database Recovery Advisor viene notevolmente semplificato il ripristino di un database in un determinato momento. Tramite una cronologia di backup visiva viene migliorato in modo significativo il supporto per i ripristini temporizzati. Tramite questa cronologia visiva è possibile identificare un momento appropriato come punto di recupero di destinazione per il ripristino di un database. Tramite la cronologia viene semplificato l'attraversamento di un percorso di recupero con fork, cioè un percorso che si estende su più fork di recupero. In un piano di ripristino temporizzato specificato sono inclusi automaticamente i backup rilevanti per il ripristino al punto nel tempo previsto (data e ora). Per altre informazioni, vedere [Ripristino di un database di SQL Server fino a un punto specifico all'interno di un backup &#40;modello di recupero con registrazione completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
 Per ulteriori informazioni su Database Recovery Advisor, vedere i seguenti blog relativi alla facilità di gestione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [Recovery Advisor: pagina di introduzione](https://blogs.msdn.com/b/managingsql/archive/2011/07/13/recovery-advisor-an-introduction.aspx)  
  
-   [Recovery Advisor: Pagina relativa all'utilizzo di SSMS per creare/ripristinare backup divisi](https://docs.microsoft.com/archive/blogs/managingsql/recovery-advisor-using-ssms-to-createrestore-split-backups)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Contenuto correlato  
 No.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)  
  
  
