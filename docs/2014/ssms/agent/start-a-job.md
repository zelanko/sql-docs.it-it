---
title: Avviare un processo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], starting
- SQL Server Agent jobs, starting
- starting jobs
ms.assetid: cec9f7f7-d0a7-4239-9dc5-a69c011ebaa0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e94adcf8242c6acaca7c28ff9a854e0aa87cb3ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72798184"
---
# <a name="start-a-job"></a>Avviare un processo
  In questo argomento viene descritto come avviare l' [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esecuzione di un [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] processo di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Agent [!INCLUDE[tsql](../../includes/tsql-md.md)] in utilizzando o SQL Server Management Objects.  
  
 Un processo è una serie specificata di azioni eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent possono essere eseguiti in un server locale o in più server remoti.  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per avviare un processo utilizzando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Con SQL Server Management Studio  
  
### <a name="to-start-a-job"></a>Per avviare un processo  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espanderla.  
  
2.  Espandere **SQL Server Agent** e quindi **Processi**. In base alla modalità di avvio del processo desiderata, eseguire una delle seguenti operazioni:  
  
    -   Se si usa un unico server oppure un server di destinazione, oppure se si esegue un processo del server locale in un server master, fare clic con il pulsante destro del mouse sul processo da avviare e scegliere **Avvia processo**.  
  
    -   Se si vuole avviare più processi, fare clic con il pulsante destro del mouse su **Monitoraggio attività processi**e scegliere **Visualizza attività processi**. In Monitoraggio attività processi è possibile selezionare più processi; fare clic con il pulsante destro del mouse sui processi selezionati e scegliere **Avvia processi**.  
  
    -   Se si usa un server master e si vuole eseguire il processo contemporaneamente in tutti i server di destinazione, fare clic con il pulsante destro del mouse sul processo da avviare, scegliere **Avvia processo**e fare clic su **Avvia su tutti i server di destinazione**.  
  
    -   Se si usa un server master e si vogliono specificare i server di destinazione in cui eseguire il processo, fare clic con il pulsante destro del mouse sul processo da avviare, scegliere **Avvia processo**e fare clic su **Avvia sui server di destinazione specificati**. Nella finestra di dialogo **Invia istruzioni di download** selezionare la casella di controllo **Solo i server di destinazione seguenti** e quindi selezionare i server di destinazione in cui si desidera eseguire il processo.  
  
##  <a name="TSQL"></a> Con Transact-SQL  
  
### <a name="to-start-a-job"></a>Per avviare un processo  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    -- starts a job named Weekly Sales Data Backup.    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql).  
  
##  <a name="SMO"></a>Utilizzo di SQL Server Management Objects  

### <a name="to-start-a-job"></a>Per avviare un processo
  
 Chiamare il metodo `Start` della classe `Job` usando un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell. Per altre informazioni, vedere [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
