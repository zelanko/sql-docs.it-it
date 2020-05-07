---
title: Compressione dei backup (SQL Server) | Microsoft Docs
description: Informazioni sulla compressione dei backup di SQL Server, tra cui le restrizioni, i compromessi a livello di prestazioni, la configurazione della compressione dei backup e il rapporto di compressione.
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], backup compression
- backup compression [SQL Server], about backup compression
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- backing up [SQL Server], backup compression
- backup compression [SQL Server]
ms.assetid: 05bc9c4f-3947-4dd4-b823-db77519bd4d2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 735a2a03b869e3171f6e974013c6822ef1c9335c
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220547"
---
# <a name="backup-compression-sql-server"></a>Compressione backup (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritta la compressione dei backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluse le restrizioni, il compromesso di prestazioni previsto dalla compressione di backup, la configurazione della compressione di backup e il rapporto di compressione.  La compressione dei backup è supportata nelle edizioni di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]: Enterprise, Standard e Developer.  Ogni edizione di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e successiva è in grado di ripristinare un backup compresso. 
 
  
##  <a name="benefits"></a><a name="Benefits"></a> Vantaggi  
  
-   Poiché le dimensioni di un backup compresso sono minori di quelle di un backup non compresso degli stessi dati, la compressione di un backup richiede una minore quantità di I/O del dispositivo e pertanto la velocità del backup aumenta in genere in modo significativo.  
  
     Per ulteriori informazioni, vedere [Impatto sulle prestazioni della compressione di backup](#PerfImpact), più avanti in questo argomento.  
  
  
##  <a name="restrictions"></a><a name="Restrictions"></a> Restrizioni  
 Ai backup compressi vengono applicate le restrizioni seguenti:  
  
-   I backup compressi e non compressi non possono coesistere in un set di supporti.  
  
-   Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è possibile leggere i backup compressi.  
  
-   NTbackups non può condividere un nastro con backup compressi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
##  <a name="performance-impact-of-compressing-backups"></a><a name="PerfImpact"></a> Impatto sulle prestazioni della compressione di backup  
 Per impostazione predefinita, la compressione aumenta significativamente l'utilizzo della CPU, il che può avere un impatto negativo sulle operazioni simultanee. Quindi potrebbe essere necessario creare backup compressi con priorità bassa in una sessione in cui l'utilizzo della CPU è limitato da[Resource Governor](../../relational-databases/resource-governor/resource-governor.md). Per ulteriori informazioni, vedere [Utilizzo di Resource Governor per limitare l'utilizzo della CPU da parte della compressione dei backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).  
  
 Per conoscere le prestazioni di I/O del backup, è possibile isolare l'I/O del backup in/da dispositivi valutando i seguenti ordinamenti di contatori delle prestazioni:  
  
-   Contatori delle prestazioni di I/O di Windows, ad esempio i contatori del disco fisico  
  
-   Contatore **Byte/sec velocità effettiva dispositivo** dell'oggetto [SQLServer:Backup Device](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)  
  
-   Contatore **Velocità effettiva backup o ripristino/sec** dell'oggetto [SQLServer:Databases](../../relational-databases/performance-monitor/sql-server-databases-object.md)  
  
 Per informazioni sui contatori di Windows, vedere la Guida di Windows. Per informazioni su come usare i contatori di SQL Server, vedere [Utilizzare oggetti di SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
   
##  <a name="calculate-the-compression-ratio-of-a-compressed-backup"></a><a name="CompressionRatio"></a> Calcolare il rapporto di compressione di un backup compresso  
 Per calcolare il rapporto di compressione di un backup, usare i valori per il backup nelle colonne **backup_size** e **compressed_backup_size** della tabella di cronologia [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) , come segue:  
  
 **backup_size**:**compressed_backup_size**  
  
 Una compressione 3:1, ad esempio, indica un risparmio approssimativo del 66% di spazio su disco. Per eseguire una query su queste colonne, è possibile utilizzare la seguente istruzione Transact-SQL:  
  
```sql  
SELECT backup_size/compressed_backup_size FROM msdb..backupset;  
```  
  
 Il rapporto di compressione di un backup compresso dipende dai dati compressi. Vari fattori possono avere un impatto sul rapporto di compressione ottenuto. Di seguito vengono indicati alcuni dei fattori principali:  
  
-   Tipo di dati.  
  
     I dati di tipo carattere vengono compressi maggiormente rispetto ad altri tipi di dati.  
  
-   Coerenza dei dati tra le righe in una pagina.  
  
     In genere, se una pagina contiene molte righe in cui un campo contiene lo stesso valore, potrebbe verificarsi una significativa compressione per tale valore. Invece, per un database che contiene dati casuali o che contiene solo una grande riga per pagina, un backup compresso avrebbe pressoché le stesse dimensioni di un backup non compresso.  
  
-   Crittografia dei dati.  
  
     I dati crittografati vengono compressi molto meno rispetto ai dati equivalenti non crittografati. Se si utilizza Transparent Data Encryption per crittografare un intero database, la compressione dei backup potrebbe non garantire una riduzione significativa, e in alcuni casi neanche minima, delle dimensioni.  
  
-   Compressione del database,  
  
     Se il database è compresso, la compressione potrebbe ridurre di poco o non ridurre le dimensioni dei backup.  
  
  
##  <a name="allocation-of-space-for-the-backup-file"></a><a name="Allocation"></a> Allocazione di spazio per il file di backup  
 Per i backup compressi le dimensioni dei file di backup finale dipende dal livello di compressione dei dati e questo valore non è noto finché l'operazione di backup non viene completata.  Per impostazione predefinita, quando si esegue il backup di un database mediante compressione, il motore di database utilizza pertanto un algoritmo di preallocazione per il file di backup. Tramite questo algoritmo viene preallocata una percentuale predefinita delle dimensioni del database per il file di backup. Se durante un'operazione di backup è necessaria una quantità di spazio maggiore, il motore di database aumenta le dimensioni del file. Se le dimensioni finali sono inferiori allo spazio allocato, al termine dell'operazione di backup il motore di database compatta il file in base alle dimensioni finali effettive del backup.  
  
 Per consentire l'aumento del file di backup solo di quanto necessario per raggiungere le relative dimensioni finali, utilizzare il flag di traccia 3042. Il flag di traccia 3042 fa in modo che durante l'operazione di backup venga ignorato l'algoritmo di preallocazione di compressione di backup predefinito. Questo flag di traccia è utile se è necessario risparmiare spazio allocando solo le dimensioni effettive necessarie per il backup compresso. L'utilizzo di questo flag di traccia può tuttavia comportare un effetto leggermente negativo sulle prestazioni, vale a dire un possibile aumento della durata dell'operazione di backup.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Configura compressione backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/configure-backup-compression-sql-server.md)  
  
-   [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
-   [Utilizzo di Resource Governor per limitare l'utilizzo della CPU da parte della compressione dei backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
  
-   [DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Flag di traccia &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
  
