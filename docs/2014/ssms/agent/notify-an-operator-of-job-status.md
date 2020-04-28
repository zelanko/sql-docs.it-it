---
title: Notificare lo stato di un processo a un operatore | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ff9340d7c9fb768f9e057d00868a9e238421a5f4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798197"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
  In questo argomento viene descritto come impostare le opzioni [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di notifica [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]in [!INCLUDE[tsql](../../includes/tsql-md.md)]utilizzando, o SQL Server Management Objects, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modo che tramite Agent sia possibile inviare notifiche agli operatori relativi ai processi.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per notificare lo stato di un processo a un operatore mediante:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Per notificare lo stato di un processo a un operatore  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
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
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Uso di Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Per notificare lo stato di un processo a un operatore  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists and that Fran??ois Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'Fran??ois Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_add_notification &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql).  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Utilizzo di SQL Server Management Objects  
 **Per notificare lo stato di un processo a un operatore**  
  
 Usare la classe `Job` tramite un linguaggio di programmazione scelto come Visual Basic, Visual C# o PowerShell. Per altre informazioni, vedere [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
