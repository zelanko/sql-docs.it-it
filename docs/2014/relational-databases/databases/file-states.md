---
title: Stati dei file | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- restoring file state [SQL Server]
- verifying file states
- current file states
- verifying filegroup states
- file states [SQL Server]
- online file state
- offline file state [SQL Server]
- viewing filegroup states
- viewing file states
- suspect file state
- recovering file state [SQL Server]
- current filegroup state
- recovery pending file state [SQL Server]
- displaying file states
- states [SQL Server], files
- displaying filegroup states
- defunct file state
ms.assetid: b426474d-8954-4df0-b78b-887becfbe8d6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc37fbade038b39d6d05cb5b51ecc3e8ba405e2a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816303"
---
# <a name="file-states"></a>Stati dei file
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]lo stato di un file di database viene gestito in modo indipendente dallo stato del database. Lo stato di un file è sempre specifico, ad esempio ONLINE o OFFLINE. Per visualizzare lo stato corrente di un file, usare la vista del catalogo [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) o [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) . Se il database è offline, lo stato dei file è indicato nella vista del catalogo [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) .  
  
 Lo stato dei file di un filegroup determina la disponibilità dell'intero filegroup. Un filegroup è disponibile se tutti i file in esso inclusi sono online. Per visualizzare lo stato corrente di un filegroup, usare la vista del catalogo [sys.filegroups](/sql/relational-databases/system-catalog-views/sys-filegroups-transact-sql) . Se un filegroup è offline e si tenta di accedervi tramite un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] , l'operazione avrà esito negativo e verrà restituito un errore. Quando Query Optimizer compila i piani di query per le istruzioni SELECT, evita gli indici non cluster e le viste cluster incluse nei filegroup offline, lasciando che queste istruzioni vengano eseguite. Se tuttavia il filegroup offline contiene l'indice cluster o heap della tabella di destinazione, l'istruzione SELECT avrà esito negativo, così come tutte le istruzioni INSERT, UPDATE o DELETE che implicano la modifica di una tabella tramite un indice incluso in un filegroup offline.  
  
## <a name="file-state-definitions"></a>Definizioni degli stati del file  
 Nella tabella seguente sono riportate le definizioni degli stati del file.  
  
|State|Definizione|  
|-----------|----------------|  
|ONLINE|Il file è disponibile per tutte le operazioni. I file del filegroup primario sono sempre online se il database stesso è online. Se un file del filegroup primario non è online, il database non sarà online e gli stati dei file secondari risulteranno indefiniti.|  
|OFFLINE|Il file non è accessibile e potrebbe non essere presente sul disco. I file vengono portati offline a seguito di un'azione esplicita da parte dell'utente e rimangono tali finché l'utente non interviene.<br /><br /> **\*\* Attenzione \*\*** Un file deve essere portato offline solo se è danneggiato, ma può essere ripristinato. Per riportare online un file impostato su offline, è necessario ripristinare il file dal backup. Per altre informazioni sul ripristino di un singolo file, vedere [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).|  
|RESTORING|Il file è in fase di ripristino. Questo stato indica che è stato eseguito un comando di ripristino che interessa l'intero file e non solo una pagina e rimarrà attivo fino al completamento dell'operazione di ripristino e di recupero del file.|  
|RECOVERY PENDING|Il recupero del file è stato posticipato. Questo stato viene attivato automaticamente durante un processo di ripristino a fasi in cui il file non viene ripristinato e recuperato. Per risolvere l'errore e consentire il completamento del processo di recupero, è necessario un ulteriore intervento da parte dell'utente. Per altre informazioni, vedere [Ripristini a fasi &#40;SQL Server&#41;](../backup-restore/piecemeal-restores-sql-server.md).|  
|SUSPECT|Non è stato possibile recuperare il file durante un processo di ripristino online. Se il file è incluso nel filegroup primario, anche il database viene contrassegnato come suspect, ovvero sospetto. In caso contrario, solo il file sarà sospetto mentre il database risulterà ancora online.<br /><br /> Lo stato suspect rimarrà attivo finché il file non viene reso disponibile mediante uno dei metodi seguenti:<br /><br /> Ripristino e recupero<br /><br /> DBCC CHECKDB con REPAIR_ALLOW_DATA_LOSS|  
|DEFUNCT|Il file è stato eliminato quando non era online. Lo stato di tutti i file di un filegroup è defunct quando si rimuove un filegroup offline.|  
  
## <a name="related-content"></a>Contenuto correlato  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [Stati del database](database-states.md)  
  
 [Stati di mirroring &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
 [Filegroup e file di database](database-files-and-filegroups.md)  
  
  
