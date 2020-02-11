---
title: Visualizzare o modificare processi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 87e5644329742712e112fd3df97f601838f7faea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245515"
---
# <a name="view-or-modify-jobs"></a>Visualizzare o modificare processi
  È possibile visualizzare tutti i processi creati. Dopo l'esecuzione di un processo, è inoltre possibile visualizzarne la cronologia. Ciò consente di verificare quando un processo è stato eseguito, lo stato dell'intero processo e lo stato di ogni relativo passaggio. È inoltre possibile verificare se in precedenza si sono verificati errori nel processo, l'ultima volta che il processo è stato completato e l'output creato a ogni esecuzione del processo. I membri del ruolo predefinito del server **sysadmin** possono visualizzare o modificare qualsiasi processo, indipendentemente dal proprietario.  
  
> [!NOTE]  
>  Affinché sia disponibile una cronologia processo, è necessario che il processo sia stato eseguito almeno una volta. È possibile limitare le dimensioni totali del log di cronologia processo e le dimensioni di ogni processo.  
  
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
  
 Per ulteriori informazioni, vedere [sp_purge_jobhistory &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql).  
  
 I membri del ruolo predefinito del server **sysadmin** possono visualizzare la definizione o la cronologia nonché modificare qualsiasi processo.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|||  
|-|-|  
|**Descrizione**|**Argomento**|  
|Descrive la procedura per la visualizzazione dei processi di [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.|[View a Job](view-a-job.md)|  
|Illustra come visualizzare il log cronologia processi di [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.|[Visualizzare la cronologia processi](view-the-job-history.md)|  
|Descrive come eliminare i contenuti del log cronologia processi di [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.|[Cancellare il contenuto del log di cronologia processi](clear-the-job-history-log.md)|  
|Descrive come impostare le dimensioni massime per i log cronologia processi di [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.|[Modificare le dimensioni del log di cronologia processi](resize-the-job-history-log.md)|  
|Illustra la procedura per la modifica delle proprietà dei processi di [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.|[Modificare un processo](modify-a-job.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [dbo. sysjobhistory &#40;&#41;Transact-SQL](/sql/relational-databases/system-tables/dbo-sysjobhistory-transact-sql)  
  
  
