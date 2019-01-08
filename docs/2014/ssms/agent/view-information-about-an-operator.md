---
title: Visualizzare le informazioni relative a un operatore | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- viewing operators
- operators (users) [Database Engine], viewing with Management Studio
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
- displaying operators
ms.assetid: 92c82cdf-f704-444e-9539-82aea7fe6fb7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 361511051bec6cc33f3062c0c4da13fe8a39329b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52751053"
---
# <a name="view-information-about-an-operator"></a>Visualizzazione delle informazioni relative a un operatore
  In questo argomento viene descritta la procedura per visualizzare le infomazioni relative a un operatoe di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare le informazioni relative a un operatore utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-operator"></a>Per visualizzare le informazioni relative a un operatore  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server che contiene l'operatore da visualizzare.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Operatori** .  
  
4.  Fare clic con il pulsante destro del mouse sull'operatore da visualizzare e selezionare **Proprietà**.  
  
     Per altre informazioni sulle opzioni disponibili contenute nella finestra di dialogo ****Proprietà nome_operatore** vedere:  
  
    -   [Proprietà operatore e operatore New &#40;pagina Generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
    -   [Proprietà operatore: Nuovo operatore &#40;pagina delle notifiche&#41;](operator-properties-new-operator-notifications-page.md)  
  
    -   [Proprietà operatore &#40;pagina Cronologia&#41;](operator-properties-history-page.md)  
  
5.  Al termine, fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-view-information-about-an-operator"></a>Per visualizzare le informazioni relative a un operatore  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    -- reports information about operator Fran??ois Ajenstat   
    -- This example assumes that the operator exists.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_operator  
        @operator_name = N'Fran??ois Ajenstat' ;  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_help_operator &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-operator-transact-sql).  
  
  
