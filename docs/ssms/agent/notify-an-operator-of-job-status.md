---
description: Notify an Operator of Job Status
title: Notify an Operator of Job Status
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 520495002a15790451321f486a069154e6469199
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418107"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate molte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Questo argomento descrive come impostare opzioni di notifica in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o SQL Server Management Objects, in modo che tramite [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia possibile inviare notifiche agli operatori relative ai processi.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="security"></a><a name="Security"></a>Sicurezza  
Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Per notificare lo stato di un processo a un operatore  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]ed espandere tale istanza.  
  
2.  Espandere **SQL Server Agent**e **Processi**, fare clic con il pulsante destro del mouse sul processo che si vuole modificare e scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà processo** selezionare la pagina **Notifiche** .  
  
4.  Se si vuole inviare una notifica a un operatore tramite posta elettronica, selezionare la casella **Posta elettronica**, selezionare un operatore nell'elenco e scegliere una delle opzioni seguenti:  
  
    -   **In caso di esito positivo processo** per inviare la notifica all'operatore se il processo è stato completato correttamente.  
  
    -   **In caso di esito negativo processo** per inviare all'operatore una notifica del completamento non riuscito del processo.  
  
    -   **Al termine del processo** per inviare la notifica all'operatore indipendentemente dallo stato di completamento.  
  
5.  Se si desidera inviare una notifica a un operatore tramite cercapersone, selezionare la casella **Cercapersone**, selezionare un operatore nell'elenco e quindi scegliere una delle opzioni seguenti:  
  
    -   **In caso di esito positivo processo** per inviare la notifica all'operatore se il processo è stato completato correttamente.  
  
    -   **In caso di esito negativo processo** per inviare all'operatore una notifica del completamento non riuscito del processo.  
  
    -   **Al termine del processo** per inviare la notifica all'operatore indipendentemente dallo stato di completamento.  
  
6.  Se si desidera inviare una notifica a un operatore tramite Net Send, selezionare la casella **Net Send**, selezionare un operatore nell'elenco e quindi scegliere una delle opzioni seguenti:  
  
    -   **In caso di esito positivo processo** per inviare la notifica all'operatore se il processo è stato completato correttamente.  
  
    -   **In caso di esito negativo processo** per inviare all'operatore una notifica del completamento non riuscito del processo.  
  
    -   **Al termine del processo** per inviare la notifica all'operatore indipendentemente dallo stato di completamento.  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Per notificare lo stato di un processo a un operatore  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists
    --  and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'François Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd).  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Utilizzo di SQL Server Management Objects  
**Per notificare lo stato di un processo a un operatore**  
  
Usare la classe **Job** tramite un linguaggio di programmazione a scelta, ad esempio Visual Basic, Visual C# o PowerShell. Per altre informazioni, vedere [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
