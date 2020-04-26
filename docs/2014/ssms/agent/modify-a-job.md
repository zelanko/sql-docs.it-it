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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62656384"
---
# <a name="modify-a-job"></a>Modificare un processo
  In questo argomento viene descritto come modificare le proprietà [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei processi di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]tramite [!INCLUDE[tsql](../../includes/tsql-md.md)], o SQL Server Management Objects.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:** ,  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per modificare un processo tramite:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 Un processo master di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non può essere destinato sia a server locali sia a server remoti.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 È possibile modificare solo i processi di cui si è proprietari, a meno che non si appartenga al ruolo predefinito del server **sysadmin** . Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-modify-a-job"></a>Per modificare un processo  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
2.  Espandere il nodo **SQL Server Agent**e il nodo **Processi**; fare clic con il pulsante destro del mouse sul processo che si vuole modificare e scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà processo** aggiornare le proprietà, i passaggi, la pianificazione e le notifiche del processo nelle schede corrispondenti.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Uso di Transact-SQL  
  
#### <a name="to-modify-a-job"></a>Per modificare un processo  
  
1.  In Esplora oggetti connettersi a un'istanza del motore di database ed espanderla.  
  
2.  Sulla barra degli strumenti fare clic su **Nuova query**.  
  
3.  Nella finestra Query utilizzare le stored procedure di sistema seguenti per modificare un processo.  
  
    -   Eseguire [sp_update_job &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) per modificare gli attributi di un processo.  
  
    -   Eseguire [sp_update_schedule &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql) per modificare i dettagli della pianificazione per la definizione di un processo.  
  
    -   Eseguire [sp_add_jobstep &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql) per aggiungere nuovi passaggi di processo.  
  
    -   Eseguire [sp_update_jobstep &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) per modificare i passaggi di processo pre-esistenti.  
  
    -   Eseguire [sp_delete_jobstep &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql) per rimuovere un passaggio di processo da un processo.  
  
    -   Stored procedure aggiuntive per modificare qualsiasi processo master di SQL Server Agent:  
  
        -   Eseguire [sp_delete_jobserver &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql) per eliminare un server attualmente associato a un processo.  
  
        -   Eseguire [sp_add_jobserver &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql) per associare un server al processo corrente.  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Utilizzo di SQL Server Management Objects  
 **Per modificare un processo**  
  
 Usare la classe `Job` tramite un linguaggio di programmazione scelto come Visual Basic, Visual C# o PowerShell. Per altre informazioni, vedere [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
