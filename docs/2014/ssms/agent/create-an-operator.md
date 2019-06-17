---
title: Creare un operatore | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- jobs [SQL Server Agent], notification options
- operators (users) [Database Engine], creating with Management Studio
- SQL Server Agent jobs, notification options
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 1359d790-5905-4927-a208-e7155e7768a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d3a5414e845d8e625c852d628bf0d965432bc72a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136423"
---
# <a name="create-an-operator"></a>Creazione di un operatore
  In questo argomento viene illustrato come configurare un utente per la ricezione di notifiche relative ai processi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un operatore utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Le opzioni Cercapersone e **net send** verranno rimosse da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare pertanto di utilizzarle in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui sono state implementate.  
  
-   Si noti che per inviare notifiche tramite posta elettronica e cercapersone agli operatori, è necessario configurare SQL Server Agent per l'utilizzo di Posta elettronica database. Per ulteriori informazioni, vedere [Procedura: Assegnazione di avvisi a un operatore (SQL Server Management Studio)](assign-alerts-to-an-operator.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è incluso un semplice strumento grafico per la gestione dei processi, che è lo strumento consigliato per la creazione e la gestione dell'infrastruttura dei processi.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono creare gli operatori.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-an-operator"></a>Per creare un operatore  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si desidera creare un operatore di SQL Server Agent.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Operatori** e quindi scegliere **Nuovo operatore**.  
  
     Nella pagina **Generale** della finestra di dialogo **Nuovo operatore** sono disponibili le opzioni indicate di seguito.  
  
     **Name**  
     Consente di modificare il nome dell'operatore.  
  
     **Abilitata**  
     Consente di abilitare l'operatore. Se non è abilitato, all'operatore non verranno inviate notifiche.  
  
     **Indirizzo posta elettronica**  
     Specifica l'indirizzo di posta elettronica dell'operatore.  
  
     **Indirizzo Net Send**  
     Specifica l'indirizzo da usare per **Net Send**.  
  
     **Indirizzo cercapersone**  
     Specifica l'indirizzo di posta elettronica da utilizzare per il cercapersone dell'operatore.  
  
     **Pianificazione cercapersone per operatore in servizio**  
     Consente di impostare gli orari in cui il cercapersone è attivo.  
  
     **Lunedì - Domenica**  
     Consente di selezionare i giorni in cui il cercapersone è attivo.  
  
     **Inizio giornata lavorativa**  
     Consente di selezionare l'ora a partire da cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent invierà messaggi al cercapersone.  
  
     **Fine giornata lavorativa**  
     Consente di selezionare l'ora oltre cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non invierà più messaggi al cercapersone.  
  
     Nella pagina **Generale** della finestra di dialogo **Notifiche** sono disponibili le opzioni indicate di seguito.  
  
     **Avvisi**  
     Consente di visualizzare gli avvisi nell'istanza.  
  
     **Processi**  
     Consente di visualizzare i processi nell'istanza.  
  
     **Elenco avvisi**  
     Consente di visualizzare l'elenco degli avvisi nell'istanza.  
  
     **Elenco processi**  
     Consente di visualizzare l'elenco dei processi nell'istanza.  
  
     **Posta elettronica**  
     Consente di inviare una notifica all'operatore tramite posta elettronica.  
  
     **Cercapersone**  
     Inviare una notifica all'operatore tramite un messaggio di posta elettronica all'indirizzo del cercapersone.  
  
     **Net send**  
     Notificare questo operatore tramite **Net Send**.  
  
4.  Al termine della creazione del nuovo operatore, fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-an-operator"></a>Per creare un operatore  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- sets up the operator information for user 'danwi.' The operator is enabled.   
    -- SQL Server Agent sends notifications by pager from Monday through Friday from 8 A.M. to 5 P.M.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_operator  
        @name = N'Dan Wilson',  
        @enabled = 1,  
        @email_address = N'danwi',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 62 ;  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_add_operator &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-operator-transact-sql).  
  
  
