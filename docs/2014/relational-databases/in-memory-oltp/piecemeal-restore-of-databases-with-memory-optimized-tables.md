---
title: Ripristino a fasi di database con tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 732c9721-8dd4-481d-8ff9-1feaaa63f84f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3c9ee00a81dd64ea1fa6093eaccc8d9b96e0aa59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806693"
---
# <a name="piecemeal-restore-of-databases-with-memory-optimized-tables"></a>Ripristino a fasi di database con tabelle con ottimizzazione per la memoria
  Nei database con tabelle ottimizzate per la memoria è supportato il ripristino a fasi, tranne per la restrizione descritta di seguito. Per altre informazioni sul backup e sul ripristino a fasi, vedere[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) e [Ripristini a fasi &#40;SQL Server&#41;](../backup-restore/piecemeal-restores-sql-server.md).  
  
 Il backup e ripristino di un filegroup ottimizzato per la memoria deve essere eseguito insieme al filegroup primario:  
  
-   Se si esegue il backup (o ripristino) del filegroup primario, è necessario specificare il filegroup ottimizzato per la memoria.  
  
-   Se si esegue il backup (o ripristino) del filegroup ottimizzato per la memoria, è necessario specificare il filegroup primario.  
  
 Di seguito sono riportati gli scenari principali per il backup e ripristino a fasi.  
  
-   Il backup a fasi consente di ridurre le dimensioni del backup. Di seguito alcuni esempi:  
  
    -   Configurare l'esecuzione del backup del database in ore o giorni diversi per ridurre l'impatto sul carico di lavoro. Un esempio è rappresentato da un database di dimensioni molto estese (maggiore di 1 TB) in cui non è possibile completare un backup completo del database nel tempo allocato per la manutenzione del database. In questo caso, è possibile utilizzare il backup a fasi per eseguire il backup completo del database in più backup a fasi.  
  
    -   Se un filegroup è di sola lettura, non è necessario un backup del log delle transazioni dopo essere stato contrassegnato come di sola lettura. È possibile scegliere di eseguire il backup del filegroup solo una volta dopo averlo contrassegnato come di sola lettura.  
  
-   Ripristino a fasi.  
  
    -   L'obiettivo di un ripristino a fasi è portare online le parti fondamentali del database, senza attendere tutti i dati. Un esempio è il caso in cui i dati di un database sono partizionati, in modo che le partizioni meno recenti vengono utilizzate solo raramente. È possibile eseguirne il ripristino solo in base alle esigenze. Lo stesso vale per i filegroup in cui sono contenuti, ad esempio, i dati cronologici.  
  
    -   Con la correzione della pagina, è possibile correggere i danneggiamenti di pagina ripristinando in particolare la pagina. Per altre informazioni, vedere [Ripristinare pagine &#40;SQL Server&#41;](../backup-restore/restore-pages-sql-server.md).  
  
## <a name="samples"></a>Esempi  
 Negli esempi viene utilizzato lo schema seguente:  
  
```  
CREATE DATABASE imoltp  
ON PRIMARY (name = imoltp_primary1, filename = 'c:\data\imoltp_data1.mdf')  
LOG ON (name = imoltp_log, filename = 'c:\data\imoltp_log.ldf')  
GO  
  
ALTER DATABASE imoltp ADD FILE (name = imoltp_primary2, filename = 'c:\data\imoltp_data2.ndf')  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_secondary  
ALTER DATABASE imoltp ADD FILE (name = imoltp_secondary, filename = 'c:\data\imoltp_secondary.ndf') TO FILEGROUP imoltp_secondary  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod2', filename='c:\data\imoltp_mod2') TO FILEGROUP imoltp_mod   
GO  
```  
  
### <a name="backup"></a>Backup  
 In questo esempio viene illustrato come eseguire il backup del filegroup primario e di quello ottimizzato per la memoria. È necessario specificare insieme sia il filegroup primario sia quello ottimizzato per la memoria.  
  
```  
backup database imoltp filegroup='primary', filegroup='imoltp_mod' to disk='c:\data\imoltp.dmp' with init  
```  
  
 Nell'esempio seguente viene illustrato che il funzionamento di un backup di filegroup diversi dai filegroup primari e ottimizzati per la memoria è simile ai database senza tabelle ottimizzate per la memoria. Tramite il comando riportato di seguito viene eseguito il backup del filegroup secondario  
  
```  
backup database imoltp filegroup='imoltp_secondary' to disk='c:\data\imoltp_secondary.dmp' with init  
```  
  
### <a name="restore"></a>Ripristina  
 Nell'esempio seguente viene illustrato come ripristinare insieme il filegroup primario e quello ottimizzato per la memoria.  
  
```  
restore database imoltp filegroup = 'primary', filegroup = 'imoltp_mod'   
from disk='c:\data\imoltp.dmp' with partial, norecovery  
  
--restore the transaction log  
 RESTORE LOG [imoltp] FROM DISK = N'c:\data\imoltp_log.dmp' WITH  FILE = 1,  NOUNLOAD,  STATS = 10  
GO  
```  
  
 Nell'esempio successivo viene illustrato che il funzionamento del ripristino di filegroup diversi dai filegroup primari e ottimizzati per la memoria è simile ai database senza tabelle ottimizzate per la memoria.  
  
```  
RESTORE DATABASE [imoltp] FILE = N'imoltp_secondary'   
FROM  DISK = N'c:\data\imoltp_secondary.dmp' WITH  FILE = 1,  RECOVERY,  NOUNLOAD,  STATS = 10  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup, ripristinare e recuperare tabelle con ottimizzazione per la memoria](../../database-engine/backup-restore-and-recovery-of-memory-optimized-tables.md)  
  
  
