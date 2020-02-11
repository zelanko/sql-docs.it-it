---
title: Ripristini di file (modello di recupero con registrazione minima) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server]
- simple recovery model [SQL Server]
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- Transact-SQL restore sequence
- restoring files [SQL Server], simple recovery model
- file restores [SQL Server], simple recovery model
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: b6d07386-7c6f-4cc6-be32-93289adbd3d6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5157fcfeb54e22c404dcba29655771a1c2034e2c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62921823"
---
# <a name="file-restores-simple-recovery-model"></a>Ripristini di file (modello di recupero con registrazione minima)
  Le informazioni contenute in questo argomento sono rilevanti solo per i database che utilizzano il modello di recupero con registrazione minima e includono almeno un filegroup secondario di sola lettura.  
  
 L'obiettivo di un ripristino di file consiste nel ripristinare uno o più file danneggiati senza ripristinare l'intero database. In base al modello di recupero con registrazione minima, i backup di file sono supportati solo per i file di sola lettura. Il filegroup primario e i filegroup secondari di lettura/scrittura vengono sempre ripristinati insieme attraverso il ripristino di un backup del database o di un backup parziale.  
  
 Gli scenari di ripristino dei file sono i seguenti:  
  
-   Ripristino di file offline  
  
     In un *ripristino di file offline*, i file o i filegroup danneggiati vengono ripristinati mentre il database è offline. Al termine della sequenza di ripristino, il database torna online.  
  
     Tutte le edizioni di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] supportano il ripristino di file offline.  
  
-   Ripristino di file online  
  
     In un *ripristino di file offline*, se il database è online al momento del ripristino, rimarrà online durante il ripristino del file. Tuttavia, durante l'operazione di ripristino, ogni filegroup nel quale viene ripristinato un file rimane offline. Al termine del recupero di tutti i file del filegroup offline, viene attivata automaticamente la modalità online per il filegroup.  
  
     Per informazioni sul supporto per il ripristino di pagine e file online, vedere [Funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Per altre informazioni sui ripristini online, vedere [Ripristino in linea &#40;SQL Server&#41;](online-restore-sql-server.md).  
  
    > [!TIP]  
    >  Se si desidera attivare la modalità offline per il database al fine di eseguire un ripristino di file, attivare la modalità offline per il database prima di avviare la sequenza di ripristino eseguendo la seguente istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) : ALTER DATABASE *nome_database* SET OFFLINE.  
  

  
##  <a name="Overview"></a>Panoramica del ripristino di file e filegroup nel modello di recupero con registrazione minima  
 Uno scenario di ripristino di file consiste in un'unica sequenza di ripristino che consente di eseguire la copia, il rollforward e il recupero dei dati appropriati come descritto di seguito:  
  
1.  Ripristinare ogni file danneggiato dal backup di file più recente.  
  
2.  Ripristinare il backup differenziale di file più recente per ogni file ripristinato e recuperare il database.  
  
### <a name="transact-sql-steps-for-file-restore-sequence-simple-recovery-model"></a>Passaggi di Transact-SQL per la sequenza di ripristino di file (modello di recupero con registrazione minima)  
 Questa sezione descrive le opzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)]RESTORE[ essenziali di ](/sql/t-sql/statements/restore-statements-transact-sql) per una semplice sequenza di ripristino di file. La sintassi e i dettagli non rilevanti sono stati omessi.  
  
 La sequenza di ripristino contiene solo due istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] . La prima istruzione esegue il ripristino di un file secondario, il file `A`, che viene ripristinato utilizzando WITH NORECOVERY. La seconda operazione ripristina altri due file, i file `B` e `C` , che vengono ripristinati utilizzando WITH RECOVERY da un diverso dispositivo di backup:  
  
1.  Ripristinare il ** file **=** di database del database _name_of_file_A_  
  
     FROM *backup_file_A*  
  
     WITH NORECOVERY **;**  
  
2.  **=** Restore *database database* _name_of_file_B_**,**_name_of_file_C_  
  
     FROM *backup_dei_file_B_e_C*  
  
     WITH RECOVERY **;**  
  
### <a name="examples"></a>Esempi  
  
-   [Esempio: Ripristino online di un file di sola lettura &#40;modello di recupero con registrazione minima&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Esempio: ripristino offline di un filegroup primario e di un altro filegroup &#40;modello di recupero con connessione completa&#41;](example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
 
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per ripristinare file e filegroup**  
  
-   [Ripristinare file e filegroup sovrascrivendo file esistenti &#40;SQL Server&#41;](restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Ripristino di file e filegroup &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
-   [Ripristino di file e filegroup &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino: interoperabilità e coesistenza &#40;SQL Server&#41;](backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Backup differenziali &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Backup completi dei file &#40;SQL Server&#41;](full-file-backups-sql-server.md)   
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](complete-database-restores-simple-recovery-model.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
