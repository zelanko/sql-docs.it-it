---
title: Creare una categoria di processi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d904f82c793acf6135f600e1ed5392bda96e1bb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856127"
---
# <a name="create-a-job-category"></a>Creare una categoria di processi
  In questo argomento si descrive come creare una categoria di processi in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent offre categorie di processi predefinite a cui possono essere assegnati processi. In alternativa, è possibile creare una nuova categoria e assegnarvi i processi. Le categorie consentono di organizzare i processi per semplificare le operazioni di raggruppamento e filtro. È ad esempio possibile organizzare tutti i processi di backup dei database raggruppandoli nella categoria Manutenzione database. È inoltre possibile creare categorie di processi personalizzate.  
  
 
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Le categorie multiserver sono disponibili solo in un server master. In un server master è disponibile una sola categoria di processi predefinita: [**Senza categoria (multiserver)**]. Quando viene scaricato un processo multiserver, la categoria viene modificata in **Processi dal server MSX** nel server di destinazione.  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  

  
##  <a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-job-category"></a>Per creare una categoria di processi  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si desidera creare una categoria di processi.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Processi** e selezionare **Gestione categorie processi**.  
  
4.  Nella finestra di dialogo **Gestione categorie processi**_nome_server_ fare clic su **Aggiungi**.  
  
5.  Nella casella **Nome** della nuova finestra di dialogo immettere un nome per la nuova categoria di processi.  
  
6.  Selezionare la casella di controllo **Mostra tutti i processi** . Selezionare uno o più processi per la nuova categoria selezionando le caselle corrispondenti ai processi.  
  
7.  Fare clic su **OK**.  
  
8.  Nella finestra di dialogo **Gestisci categorie processi**_nome_server_ fare clic su **Aggiorna** per assicurarsi che la nuova categoria di processi sia attiva. Se l'aspetto è quello previsto, chiudere questa finestra di dialogo.  
  
 Per altre informazioni su queste finestre di dialogo, vedere [categorie di processi: Gestisci categorie di processi](job-categories-manage-job-categories.md) e [processi nuova categoria di processi e le proprietà di categorie](job-categories-properties-new-job-category.md).  
  
 
  
##  <a name="TSQL"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-job-category"></a>Per creare una categoria di processi  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- creates a local job category named AdminJobs   
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_category  
        @class=N'JOB',  
        @type=N'LOCAL',  
        @name=N'AdminJobs' ;  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_add_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-category-transact-sql).  
  

  
##  <a name="SMO"></a> Utilizzo di SQL Server Management Objects  
 **Per creare una categoria di processi**  
  
 Chiamare la classe `JobCategory` tramite un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell. Per un codice di esempio, vedere [Pianificazione delle attività amministrative automatiche in SQL Server Agent](sql-server-agent.md).  
  
 
  
  
