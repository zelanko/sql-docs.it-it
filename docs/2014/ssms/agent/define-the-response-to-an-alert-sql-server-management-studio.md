---
title: Definire la risposta a un avviso (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], responding to
- responding to alerts
ms.assetid: c86ca6eb-c59f-46e9-bc32-d474e7c3b170
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6ac3e9ee443f0c10a39128fc1d6aab6813ec4f4d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62524071"
---
# <a name="define-the-response-to-an-alert-sql-server-management-studio"></a>Define the Response to an Alert (SQL Server Management Studio)
  In questo argomento viene descritto come definire [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il modo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cui risponde agli [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] avvisi di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Agent [!INCLUDE[tsql](../../includes/tsql-md.md)]in tramite o.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per definire la risposta a un avviso tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Le opzioni Cercapersone e **net send** verranno rimosse da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare pertanto di utilizzarle in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui sono state implementate.  
  
-   Si noti che per inviare notifiche tramite posta elettronica e cercapersone agli operatori, è necessario configurare SQL Server Agent per l'utilizzo di Posta elettronica database. Per ulteriori informazioni, vedere [Procedura: Assegnazione di avvisi a un operatore (SQL Server Management Studio)](assign-alerts-to-an-operator.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è incluso un semplice strumento grafico per la gestione dei processi, che è lo strumento consigliato per la creazione e la gestione dell'infrastruttura dei processi.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono definire la risposta a un avviso.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-define-the-response-to-an-alert"></a>Per definire la risposta a un avviso  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server contenente l'avviso per cui si desidera definire una risposta.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Avvisi** .  
  
4.  Fare clic con il pulsante destro del mouse sull'avviso per cui si desidera definire una risposta e selezionare **Proprietà**.  
  
5.  Nella finestra di dialogo**Proprietà avviso** _alert_name_selezionare **risposta**in **Selezione pagina**.  
  
6.  Selezionare la casella di controllo **Esegui processo** e, dall'elenco sottostante la casella di controllo **Esegui processo**, selezionare il processo da eseguire quando viene generato l'avviso. È possibile creare un nuovo processo facendo clic su **Nuovo processo**. Per visualizzare ulteriori informazioni sul processo, fare clic su **Visualizza processo**. Per ulteriori informazioni sulle opzioni disponibili nelle finestre di dialogo **nuovo processo** e **Proprietà processo**_Job_name_ , vedere [creare un processo](create-a-job.md) e [visualizzare un processo](view-a-job.md).  
  
7.  Selezionare la casella di controllo **Invia notifica a operatori** se si desidera notificare agli operatori quando viene attivato l'avviso. In **Elenco operatori**selezionare uno o più dei metodi seguenti per inviare la notifica all'operatore o agli operatori: **Posta elettronica**, **Cercapersone**o **Net Send**. È possibile creare un nuovo operatore facendo clic su **Nuovo operatore**. Per visualizzare ulteriori informazioni su un operatore, fare clic su **Visualizza operatore**. Per ulteriori informazioni sulle opzioni disponibili nelle finestre di dialogo delle proprietà **Nuovo operatore** e **Visualizza operatore** , vedere [Create an Operator](create-an-operator.md) e [View Information About an Operator](view-information-about-an-operator.md).  
  
8.  Al termine, fare clic su **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-define-the-response-to-an-alert"></a>Per definire la risposta a un avviso  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- adds an e-mail notification for Test Alert.  
    -- assumes that Test Alert already exists and that Fran??ois Ajenstat is a valid operator name   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'Fran??ois Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_add_notification &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql).  
  
  
