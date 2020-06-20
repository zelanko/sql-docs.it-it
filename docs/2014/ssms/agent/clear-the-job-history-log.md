---
title: Cancellare il contenuto del log di cronologia processi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- clearing job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 34b9398a-c409-4040-8ea1-0deceb18f961
author: stevestein
ms.author: sstein
ms.openlocfilehash: dc1207f7b99089c70ca307177a6e984075c1654f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995802"
---
# <a name="clear-the-job-history-log"></a>Cancellare il contenuto del log di cronologia processi
  In questo argomento viene descritto come eliminare il contenuto del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log cronologia processi di Agent in utilizzando [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , [!INCLUDE[tsql](../../includes/tsql-md.md)] o SQL Server Management Objects.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per cancellare il contenuto del log di cronologia processo utilizzando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-clear-the-job-history-log"></a>Per cancellare il contenuto del log di cronologia processo  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
2.  Espandere **SQL Server Agent**e quindi espandere **Processi**.  
  
3.  Fare clic con il pulsante destro del mouse su un processo e scegliere **Visualizza cronologia**.  
  
4.  Nel **Visualizzatore file di log**selezionare il processo di cui si desidera cancellare la cronologia e quindi eseguire una delle operazioni seguenti:  
  
    -   Fare clic su **Elimina**e quindi su **Elimina tutta la cronologia** nella finestra di dialogo **Elimina cronologia** . È possibile eliminare tutta la cronologia processo oppure solo quella precedente a una data specificata. Per rimuovere tutta la cronologia processo, fare clic su **Elimina tutta la cronologia**. Per rimuovere solo i log cronologia processo più vecchi, fare clic su **Elimina la cronologia precedente a**e quindi specificare una data.  
  
    -   Fare clic su **Stato processo** se si desidera cancellare il contenuto del log della cronologia di un processo multiserver. Fare clic su **Processo**, selezionare il nome di un processo e quindi fare clic su **Visualizza cronologia processi remoti**.  
  
5.  Fare clic su **Elimina**.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Uso di Transact-SQL  
  
#### <a name="to-clear-the-job-history-log"></a>Per cancellare il contenuto del log di cronologia processo  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    -- example removes the history for a job named NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_purge_jobhistory  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Utilizzo di SQL Server Management Objects  
 **Per cancellare il contenuto del log di cronologia processo**  
  
 Utilizzare il metodo `PurgeJobHistory` della classe `JobServer` utilizzando un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell. Per altre informazioni, vedere [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
