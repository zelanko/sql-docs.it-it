---
title: Eliminare una categoria di processi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bb392991afbb3707fafdb18a28cc3de53f97c78
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783195"
---
# <a name="delete-a-job-category"></a>Eliminare una categoria di processi
  In questo argomento viene descritto come eliminare [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una categoria di processi [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Agent in [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzando o SQL Server Management Objects.  
  
 Le categorie consentono di organizzare i processi per semplificare le operazioni di raggruppamento e filtro. È ad esempio possibile organizzare tutti i processi di backup dei database raggruppandoli nella categoria Manutenzione database.  

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 Quando si elimina una categoria di processi definita dall'utente, tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene richiesto di riassegnare i processi appartenenti alla categoria a un'altra categoria. È possibile eliminare solo categorie di processi definite dall'utente.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  

##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
### <a name="to-delete-a-job-category"></a>Per eliminare una categoria di processi  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si desidera eliminare una categoria di processi.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Processi** e selezionare **Gestione categorie processi**.  
  
4.  Nella finestra di dialogo **Gestisci categorie di processi**_nome_server_ selezionare la categoria di processi da eliminare.  
  
5.  Fare clic su **Elimina**.  
  
6.  Nella finestra di dialogo **Categorie di processi** fare clic su **Sì**.  
  
7.  Chiudere la finestra di dialogo **Gestione categorie processi**_nome_server_ .  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Uso di Transact-SQL  
  
### <a name="to-delete-a-job-category"></a>Per eliminare una categoria di processi  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    -- deletes the job category named AdminJobs.  
    USE msdb ;  
    GO   
    EXEC dbo.sp_delete_category  
        @name = N'AdminJobs',  
        @class = N'JOB' ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_delete_category &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-delete-category-transact-sql).  

  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Utilizzo di SQL Server Management Objects  

### <a name="to-delete-a-job-category"></a>Per eliminare una categoria di processi
  
 Chiamare la classe `JobCategory` tramite un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell.  
