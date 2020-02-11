---
title: Assegnare un processo a una categoria di processi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], assigning
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- SQL Server Agent jobs, assigning
- assigning job to category
ms.assetid: a9ea65a2-1d73-4582-a335-63adeb450cb6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab7695b6a80772ddcd01996e783fffd806447c59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62473202"
---
# <a name="assign-a-job-to-a-job-category"></a>Assegnare un processo a una categoria di processi
  In questo argomento viene descritto come [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assegnare processi di Agent a categorie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di processi [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]in [!INCLUDE[tsql](../../includes/tsql-md.md)] tramite o SQL Server Management Objects.  
  
 Le categorie consentono di organizzare i processi per semplificare le operazioni di raggruppamento e filtro. È ad esempio possibile organizzare tutti i processi di backup dei database raggruppandoli nella categoria Manutenzione database. È possibile assegnare processi a categorie predefinite, oppure creare una categoria definita dall'utente e usarla per l'assegnazione dei processi.  
  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
  
  
##  <a name="SSMS"></a> Con SQL Server Management Studio  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>Per assegnare un processo a una categoria di processi  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si desidera assegnare un processo a una categoria di processi.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Processi** .  
  
4.  Fare clic con il pulsante destro del mouse sul processo da modificare e selezionare **Proprietà**.  
  
5.  Nell'elenco **categoria** della finestra di dialogo **proprietà processo-**_job_name_ Selezionare la categoria di processi che si desidera assegnare al processo.  
  
6.  Fare clic su **OK**.  
  
  
##  <a name="TSQL"></a> Con Transact-SQL  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>Per assegnare un processo a una categoria di processi  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_update_job &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql).  
  
  
  
##  <a name="SMO"></a>Utilizzo di SQL Server Management Objects  
 **Per assegnare un processo a una categoria di processi**  
  
 Usare la classe `JobCategory` tramite un linguaggio di programmazione scelto come Visual Basic, Visual C# o PowerShell.  
  
  
  
  
