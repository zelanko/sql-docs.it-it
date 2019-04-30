---
title: Creare un avviso usando i livelli di gravità | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8e94b24634eedf68afcb25c8c1ef957ce063cdc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63136737"
---
# <a name="create-an-alert-using-severity-level"></a>Creazione di un avviso utilizzando i livelli di gravità
  Nel presente argomento viene descritta la procedura di creazione di un avviso [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent generato quando si verifica un evento di un determinato livello di gravità in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Security](#Security)  
  
-   **Per creare un avviso utilizzando il livello di gravità utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] include un semplice strumento grafico per la gestione del sistema di avvisi ed è lo strumento consigliato per la configurazione di un'infrastruttura di avvisi.  
  
-   Gli eventi generati con la stored procedure **xp_logevent** si verificano nel database master. Pertanto, **xp_logevent** genera un avviso solo se **@database_name** per l'avviso è **'master'** o NULL.  
  
-   I livelli di gravità da 19 a 25 determinano l'invio di un messaggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al registro applicazioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e l'attivazione di un avviso. Gli eventi con livello di gravità inferiore a 19 determinano l'attivazione di avvisi solo se è stato usato **sp_altermessage**, RAISERROR WITH LOG oppure **xp_logevent** per forzarne la scrittura nel registro applicazioni di Windows.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per impostazione predefinita, solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_add_alert**.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-severity-level"></a>Per creare un avviso utilizzando il livello di gravità  
  
1.  In **Esplora oggetti** fare clic sul segno più per espandere il server in cui si desidera creare un avviso tramite un livello di gravità.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse su **Avvisi** e selezionare **Nuovo avviso**.  
  
4.  Nella casella **Nome** della finestra di dialogo **Nuovo avviso** immettere un nome per l'avviso.  
  
5.  Nell'elenco **Tipo** selezionare **Avviso per evento di SQL Server**.  
  
6.  Nell'elenco **Nome database**sotto **Definizione di avviso di evento** selezionare un database per limitare l'avviso a un database specifico.  
  
7.  In **Genera avvisi in base a**fare clic su **Gravità** , quindi selezionare una gravità specifica che genera l'avviso.  
  
8.  Per limitare l'avviso a una particolare sequenza di caratteri, selezionare la casella di controllo corrispondente a **Genera avviso quando il messaggio contiene** e immettere una parola chiave o una stringa di caratteri nella casella **Testo del messaggio**. Il numero massimo di caratteri consentito è 100.  
  
9. Fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-an-alert-using-severity-level"></a>Per creare un avviso utilizzando il livello di gravità  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_add_alert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql).  
  
  
