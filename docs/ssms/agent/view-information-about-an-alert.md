---
description: Visualizzare informazioni su un avviso
title: Visualizzare informazioni su un avviso
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- viewing alerts
- alerts [SQL Server], viewing
- displaying alerts
- status information [SQL Server], alerts
ms.assetid: a0e3a8c4-e3c2-42a5-b2f8-aa06061d3fa6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 96aaa12ce934da18818bd99fde009f6ec0747aee
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480732"
---
# <a name="view-information-about-an-alert"></a>Visualizzare informazioni su un avviso

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Questo argomento descrive come visualizzare le informazioni sugli avvisi di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="security"></a><a name="Security"></a>Sicurezza  
  
#### <a name="permissions"></a><a name="Permissions"></a>Autorizzazioni  
Per impostazione predefinita, i membri del ruolo predefinito del server **sysadmin** possono visualizzare le informazioni su un avviso. Gli altri utenti devono appartenere al ruolo predefinito del database **SQLAgentOperatorRole** nel database **msdb** .  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-alert"></a>Per visualizzare informazioni su un avviso  
  
1.  In **Esplora oggetti** fare clic sul segno più per espandere il server in cui si desidera visualizzare le informazioni su un avviso.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic sul segno più per espandere la cartella **Avvisi** .  
  
4.  Fare clic con il pulsante destro del mouse sull'avviso con le informazioni da visualizzare e selezionare **Proprietà**.  
  
    Per altre informazioni sulle opzioni disponibili contenute nella finestra di dialogo dell'interfaccia utente nella finestra di dialogo **Proprietà dell'avviso**_nome\_avviso_:  
  
    -   [Proprietà avviso - nuovo avviso &#40; pagina generale&#41;](../../ssms/agent/alert-properties-new-alert-general-page.md)  
  
    -   [Proprietà avviso - nuovo avviso &#40; pagina risposta&#41;](../../ssms/agent/alert-properties-new-alert-response-page.md)  
  
    -   [Proprietà avviso - nuovo avviso &#40; pagina Opzioni&#41;](../../ssms/agent/alert-properties-new-alert-options-page.md)  
  
    -   [Proprietà avviso &#40;pagina Cronologia&#41;](../../ssms/agent/alert-properties-history-page.md)  
  
5.  Al termine, fare clic su **OK**.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-view-information-about-an-alert"></a>Per visualizzare informazioni su un avviso  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- reports information about the Demo: Sev. 25 Errors alert  
    -- This example assumes that the 'Demo: Sev. 25 Errors' alert exists.  
    USE msdb ;  
    GO  
  
    EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors'  
    GO  
    ```  
  
Per altre informazioni, vedere [sp_help_alert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md).  
