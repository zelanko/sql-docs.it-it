---
title: Modificare un processo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 614c35992be2f85ef15afd0645140746041d083d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62656384"
---
# <a name="modify-a-job"></a>Modificare un processo
  In questo argomento viene descritto come modificare le proprietà dei processi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o SQL Server Management Objects.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:** ,  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per modificare un processo tramite:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Un processo master di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non può essere destinato sia a server locali sia a server remoti.  
  
###  <a name="Security"></a> Sicurezza  
 È possibile modificare solo i processi di cui si è proprietari, a meno che non si appartenga al ruolo predefinito del server **sysadmin** . Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-modify-a-job"></a>Per modificare un processo  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ed espandere tale istanza.  
  
2.  Espandere il nodo **SQL Server Agent**e il nodo **Processi**; fare clic con il pulsante destro del mouse sul processo che si vuole modificare e scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà processo** aggiornare le proprietà, i passaggi, la pianificazione e le notifiche del processo nelle schede corrispondenti.  
  
##  <a name="TSQL"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-modify-a-job"></a>Per modificare un processo  
  
1.  In Esplora oggetti connettersi a un'istanza del motore di database ed espanderla.  
  
2.  Sulla barra degli strumenti fare clic su **Nuova query**.  
  
3.  Nella finestra Query utilizzare le stored procedure di sistema seguenti per modificare un processo.  
  
    -   Eseguire [sp_update_job &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) per modificare gli attributi di un processo.  
  
    -   Eseguire [sp_update_schedule &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql) per modificare i dettagli della pianificazione per una definizione del processo.  
  
    -   Eseguire [sp_add_jobstep &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql) per aggiungere nuovi passaggi al processo.  
  
    -   Eseguire [sp_update_jobstep &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) per modificare i passaggi di processo preesistenti.  
  
    -   Eseguire [sp_delete_jobstep &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql) per rimuovere un passaggio di processo da un processo.  
  
    -   Stored procedure aggiuntive per modificare qualsiasi processo master di SQL Server Agent:  
  
        -   Eseguire [sp_delete_jobserver &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql) per eliminare un server attualmente associato a un processo.  
  
        -   Eseguire [sp_add_jobserver &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql) per associare un server con il processo corrente.  
  
##  <a name="SMO"></a> Utilizzo di SQL Server Management Objects  
 **Per modificare un processo**  
  
 Usare la classe `Job` tramite un linguaggio di programmazione scelto come Visual Basic, Visual C# o PowerShell. Per altre informazioni, vedere [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
