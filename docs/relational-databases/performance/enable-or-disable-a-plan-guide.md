---
title: Abilitare o disabilitare una guida di piano | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], disabling
- enabling plan guides
- plan guides [SQL Server], enabling
- disabling plan guides
ms.assetid: b00ab550-5308-4cb8-8330-483cd1d25654
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 0aef47aa00c52bd5adb0069baf0a1d06a6848d43
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580766"
---
# <a name="enable-or-disable-a-plan-guide"></a>Abilitare o disabilitare una guida di piano
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile disabilitare e abilitare guide di piano in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. È possibile abilitare o disabilitare una sola guida di piano o tutte le guide di piano in un database.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Security](#Security)  
  
-   **Per disabilitare e abilitare le guide di piano utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Se si tenta di eliminare o modificare una funzione, una stored procedure o un trigger DML a cui viene fatto riferimento in una guida di piano abilitata o disabilitata, viene generato un errore. Verificare sempre le dipendenze prima di eliminare o modificare uno degli oggetti indicati sopra.  
  
-   La disabilitazione di una guida di piano disabilitata o l'abilitazione di una guida di piano abilitata non ha alcun effetto e viene eseguita senza la restituzione di un errore.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 La disabilitazione o l'abilitazione di una guida di piano OBJECT richiede l'autorizzazione ALTER per l'oggetto (ad esempio funzione, stored procedure) a cui fa riferimento la guida di piano. Per tutte le altre guide di piano è necessario disporre dell'autorizzazione ALTER DATABASE.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>Per disabilitare o abilitare una guida di piano  
  
1.  Fare clic sul segno più per espandere il database in cui si desidera disabilitare o abilitare una guida di piano, quindi fare clic sul segno più per espandere la cartella **Programmabilità** .  
  
2.  Fare clic sul segno più per espandere la cartella **Guide di piano** .  
  
3.  Fare clic con il pulsante destro del mouse sulla guida di piano da disabilitare o abilitare e scegliere **Abilita** o **Disabilita**.  
  
4.  Nella finestra di dialogo **Disabilita guida di piano** o **Abilita guida di piano** , verificare che l'azione scelta venga completata correttamente, quindi fare clic su **Chiudi**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>Per disabilitare o abilitare tutte le guide di piano in un database  
  
1.  Fare clic sul segno più per espandere il database in cui si desidera disabilitare o abilitare una guida di piano, quindi fare clic sul segno più per espandere la cartella **Programmabilità** .  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Guide di piano** , quindi scegliere **Abilita tutto** o **Disabilita tutto**.  
  
3.  Nella finestra di dialogo **Disabilita tutte le guide di piano** o **Abilita tutte le guide di piano** , verificare che l'azione scelta venga completata correttamente, quindi fare clic su **Chiudi**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-disable-or-enable-a-plan-guide"></a>Per disabilitare o abilitare una guida di piano  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    --Create a procedure on which to define the plan guide.  
    IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetSalesOrderByCountry;  
    GO  
    CREATE PROCEDURE Sales.GetSalesOrderByCountry   
        (@Country nvarchar(60))  
    AS  
    BEGIN  
        SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country;  
    END  
    GO  
    --Create the plan guide.  
    EXEC sp_create_plan_guide N'Guide3',  
        N'SELECT *  
        FROM Sales.SalesOrderHeader AS h   
        INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
        INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
        WHERE t.CountryRegionCode = @Country',  
        N'OBJECT',  
        N'Sales.GetSalesOrderByCountry',  
        NULL,  
        N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
    --Disable the plan guide.  
    EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
    GO  
    --Enable the plan guide.  
    EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
    GO  
  
    ```  
  
#### <a name="to-disable-or-enable-all-plan-guides-in-a-database"></a>Per disabilitare o abilitare tutte le guide di piano in un database  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    --Disable all plan guides in the database.  
    EXEC sp_control_plan_guide N'DISABLE ALL';  
    GO  
    --Enable all plan guides in the database.  
    EXEC sp_control_plan_guide N'ENABLE ALL';  
    GO  
  
    ```  
  
 Per altre informazioni, vedere [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md).  
  
  
