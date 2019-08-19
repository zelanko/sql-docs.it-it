---
title: Modificare la disponibilità di un operatore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- canceling operators
- reactivating operators
- removing operators
- deleting operators
- available operators [SQL Server]
- dropping operators
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
- disabling operators
- operators (users) [Database Engine], changing availability with Management Studio
ms.assetid: 10d58b92-b67b-47e2-af9c-9f9fd6968bba
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8b9fa196aefb37de169439853704e9b52153c6a7
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553331"
---
# <a name="change-an-operator39s-availability"></a>Modificare la disponibilità di un operatore
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come modificare la pianificazione di un operatore relativa alla ricezione di notifiche degli avvisi in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
Solo i membri del ruolo predefinito del server **sysadmin** possono modificare gli operatori.  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-change-an-operators-availability"></a>Per modificare la disponibilità di un operatore  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server che contiene l'operatore da abilitare o disabilitare.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Operatori** .  
  
4.  Fare clic con il pulsante destro del mouse sull'operatore che si vuole abilitare o disabilitare, selezionare **Proprietà**e fare clic sulla scheda **Generale** .  
  
5.  Nella finestra di dialogo **Proprietà**_nome\_operatore_ selezionare o deselezionare la casella di controllo **Abilitato**.  
  
6.  Fare clic su **OK**.  
  
## <a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-change-an-operators-availability"></a>Per modificare la disponibilità di un operatore  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- disables the 'François Ajenstat' operator  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_operator   
        @name = N'François Ajenstat',  
        @enabled = 0;  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_update_operator (Transact-SQL)](https://msdn.microsoft.com/231750a6-4828-4d03-afe6-b91d38c42ed3).  
  
