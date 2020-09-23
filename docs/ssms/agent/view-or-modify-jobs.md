---
description: Visualizzare o modificare processi
title: Visualizzare o modificare processi
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c8484cd44d40d37967b6948f667dbb78a9fe7653
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497482"
---
# <a name="view-or-modify-jobs"></a>Visualizzare o modificare processi
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte ma non tutte le funzionalità di SQL Server Agent. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

È possibile visualizzare tutti i processi creati. Dopo l'esecuzione di un processo, è inoltre possibile visualizzarne la cronologia. Ciò consente di verificare quando un processo è stato eseguito, lo stato dell'intero processo e lo stato di ogni relativo passaggio. È inoltre possibile verificare se in precedenza si sono verificati errori nel processo, l'ultima volta che il processo è stato completato e l'output creato a ogni esecuzione del processo. I membri del ruolo predefinito del server **sysadmin** possono visualizzare o modificare qualsiasi processo, indipendentemente dal proprietario.  
  
> [!NOTE]  
> Affinché sia disponibile una cronologia processo, è necessario che il processo sia stato eseguito almeno una volta. È possibile limitare le dimensioni totali del log di cronologia processo e le dimensioni di ogni processo.  
  
È infine possibile modificare un processo in modo da soddisfare nuovi requisiti. È possibile ad esempio modificare:  
  
-   Opzioni di risposta  
  
-   Pianificazioni  
  
-   Passaggi di processo  
  
-   Proprietario  
  
-   Categoria di processo  
  
-   Server di destinazione (solo processi multiserver)  
  
Per verificare che le modifiche ai processi multiserver siano operative, è necessario inviare le modifiche all'elenco di download, in modo da consentire ai server di destinazione di scaricare nuovamente il processo aggiornato. Per garantire che i server di destinazione dispongano delle definizioni di processo più aggiornate, inviare un'istruzione INSERT dopo l'aggiornamento del processo multiserver, come illustrato di seguito:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Per altre informazioni, vedere [sp_purge_jobhistory (Transact-SQL)](https://msdn.microsoft.com/237f9bad-636d-4262-9bfb-66c034a43e88).  
  
I membri del ruolo predefinito del server **sysadmin** possono visualizzare la definizione o la cronologia nonché modificare qualsiasi processo.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione|Argomento|  
|-|-|  
|Descrive la procedura per la visualizzazione dei processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[View a Job](../../ssms/agent/view-a-job.md)|  
|Illustra come visualizzare il log cronologia processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Visualizzare la cronologia processi](../../ssms/agent/view-the-job-history.md)|  
|Descrive come eliminare i contenuti del log cronologia processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Cancellare il contenuto del log di cronologia processi](../../ssms/agent/clear-the-job-history-log.md)|  
|Descrive come impostare le dimensioni massime per i log cronologia processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Modificare le dimensioni del log di cronologia processi](../../ssms/agent/resize-the-job-history-log.md)|  
|Illustra la procedura per la modifica delle proprietà dei processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Modificare un processo](../../ssms/agent/modify-a-job.md)|  
  
## <a name="see-also"></a>Vedere anche  
[sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
