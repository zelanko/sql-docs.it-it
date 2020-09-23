---
description: Avviare automaticamente SQL Server Agent
title: Avviare automaticamente SQL Server Agent
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, starting
- autostart SQL Server Agent
ms.assetid: 2ea332da-0ede-4d2b-b122-c4c10eaca191
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 796f2169a43d1d1e0741b88bc2d9a7c36e90356d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418357"
---
# <a name="autostart-sql-server-agent"></a>Avviare automaticamente SQL Server Agent

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Questo argomento descrive come configurare [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per il riavvio automatico in caso di arresto imprevisto in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitazioni e restrizioni  
In Esplora oggetti viene visualizzato il nodo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent solo se si dispone dell'autorizzazione per utilizzarlo.  
  
### <a name="security"></a><a name="Security"></a>Sicurezza  
  
#### <a name="permissions"></a><a name="Permissions"></a>Autorizzazioni  
Per la corretta esecuzione delle funzioni, è necessario che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia configurato per utilizzare le credenziali di un account membro del ruolo predefinito del server **sysadmin** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'account deve disporre delle autorizzazioni di Windows seguenti:  
  
-   Accesso come servizio (SeServiceLogonRight)  
  
-   Sostituzione di token a livello di processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorare controllo incrociato (SeChangeNotifyPrivilege)  
  
-   Regolazione quote di memoria per un processo (SeIncreaseQuotaPrivilege)  
  
Per altre informazioni sulle autorizzazioni di Windows necessarie per l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Selezionare un account per il servizio SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [Impostazione di account di servizio Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent-to-automatically-restart"></a>Per configurare SQL Server Agent per il riavvio automatico  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si desidera configurare SQL Server Agent per il riavvio automatico.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, quindi scegliere **Proprietà**.  
  
3.  Nella pagina **Generale** selezionare **Riavvia automaticamente SQL Server Agent in caso di arresto imprevisto**.  
  
