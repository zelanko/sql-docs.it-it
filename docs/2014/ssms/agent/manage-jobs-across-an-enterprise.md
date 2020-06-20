---
title: Gestire i processi in un'organizzazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 385435302b2e987c86afb17eaebf90e91bc93e56
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062197"
---
# <a name="manage-jobs-across-an-enterprise"></a>Gestire i processi in un'azienda
  Se si apportano modifiche alle definizioni di processi multiserver al di fuori di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , è necessario inviare le modifiche all'elenco di download in modo che i server di destinazione possano scaricare nuovamente il processo aggiornato. Per garantire che i server di destinazione dispongano delle definizioni dei processi più aggiornate, inviare un'istruzione INSERT dopo l'aggiornamento del processo multiserver:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
 Per notificare ai server di destinazione che un processo multiserver è stato modificato, è necessario richiamare il comando precedente dopo avere utilizzato una qualsiasi delle procedure seguenti:  
  
-   [sp_add_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_update_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql)  
  
-   [sp_delete_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql)  
  
-   [sp_attach_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_detach_schedule &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql)  
  
    > [!NOTE]  
    >  Non è necessario chiamare **sp_post_msx_operation** dopo aver chiamato **sp_update_job** o **sp_delete_job**, in quanto tali stored procedure inviano automaticamente le modifiche necessarie all'elenco di download.  
  
 Di seguito sono indicate le operazioni comuni per la gestione di processi in un'organizzazione:  
  
 **Per controllare lo stato di un server di destinazione**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql)  
  
-   [Oggetti SMO (SQL Server Management Objects)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **Per modificare i server di destinazione per un processo**  
  
-   [SQL Server Management Studio](modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  
-   [Oggetti SMO (SQL Server Management Objects)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **Per modificare la posizione di un server di destinazione**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
-   [Oggetti SMO (SQL Server Management Objects)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **Per sincronizzare gli orologi dei server di destinazione**  
  
-   [SQL Server Management Studio](synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)  
  
 **Per forzare un server di destinazione a eseguire il polling del server master**  
  
-   [SQL Server Management Studio](force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di eventi](manage-events.md)  
  
  
