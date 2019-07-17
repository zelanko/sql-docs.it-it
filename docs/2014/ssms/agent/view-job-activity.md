---
title: Visualizzare l'attività dei processi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- viewing job activity
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- displaying job activity
ms.assetid: 5c284e5e-7775-435d-ac49-f3f12a27ddc7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fc6099fa9f523b351489ce4301596aeb90c1509
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211302"
---
# <a name="view-job-activity"></a>Visualizza attività processi
  In questo argomento viene illustrato come visualizzare lo stato di runtime dei processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 All'avvio di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene creata una nuova sessione e la tabella **sysjobactivity** del database **msdb** viene popolata con tutti i processi definiti esistenti. In questa tabella sono registrati l'attività e lo stato dei processi correnti. Per visualizzare lo stato corrente dei processi è possibile utilizzare Monitoraggio attività processo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene interrotto in modo imprevisto, per verificare quali processi erano in esecuzione al momento dell'interruzione è possibile fare riferimento alla tabella **sysjobactivity** .  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare l'attività del processo utilizzando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-job-activity"></a>Per visualizzare l'attività del processo  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
2.  Espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse su **Monitoraggio attività processi** e scegliere **Visualizza attività processi**.  
  
4.  In **Monitoraggio attività processo**è possibile visualizzare i dettagli relativi a ogni processo definito nel server.  
  
5.  Fare clic con il pulsante destro del mouse su un processo per avviarlo, arrestarlo, attivarlo o disabilitarlo, aggiornarne lo stato visualizzato in Monitoraggio attività processo, eliminarlo o visualizzarne la cronologia o le proprietà.  Per avviare, arrestare, attivare o disabilitare o aggiornare più processi, selezionare più righe in Monitoraggio attività processo e fare clic con il pulsante destro del mouse.  
  
6.  Per aggiornare Monitoraggio attività processo fare clic su **Aggiorna**. Per visualizzare un numero inferiore di righe, fare clic su **Filtro** e specificare i parametri del filtro.  
  
##  <a name="TSQL"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-view-job-activity"></a>Per visualizzare l'attività del processo  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- lists activity for all jobs that the current user has permission to view.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobactivity ;  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_help_jobactivity &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobactivity-transact-sql).  
  
  
