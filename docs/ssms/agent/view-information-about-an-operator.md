---
title: Visualizzare le informazioni relative a un operatore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f59914cd2bb873080d7008dfc79018d2f3b5b33b
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2019
ms.locfileid: "69552426"
---
# <a name="view-information-about-an-operator"></a>Visualizzazione delle informazioni relative a un operatore
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritta la procedura per visualizzare le infomazioni relative a un operatoe di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-operator"></a>Per visualizzare le informazioni relative a un operatore  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server che contiene l'operatore da visualizzare.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Operatori** .  
  
4.  Fare clic con il pulsante destro del mouse sull'operatore da visualizzare e selezionare **Proprietà**.  
  
    Per altre informazioni sulle opzioni disponibili contenute nella finestra di dialogo _Proprietà_**nome_operatore** , vedere:  
  
    -   [Proprietà operatore - nuovo operatore &#40;pagina generale&#41;](../../ssms/agent/operator-properties-new-operator-general-page.md)  
  
    -   [Proprietà operatore -nuovo operatore &#40;pagina notifiche&#41;](../../ssms/agent/operator-properties-new-operator-notifications-page.md)  
  
    -   [Proprietà operatore &#40;pagina Cronologia&#41;](../../ssms/agent/operator-properties-history-page.md)  
  
5.  Al termine, fare clic su **OK**.  
  
## <a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-view-information-about-an-operator"></a>Per visualizzare le informazioni relative a un operatore  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- reports information about operator François Ajenstat   
    -- This example assumes that the operator exists.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_operator  
        @operator_name = N'François Ajenstat' ;  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_help_operator (Transact-SQL)](https://msdn.microsoft.com/caedc43d-44b8-415a-897e-92923f6de3b8).  
  
