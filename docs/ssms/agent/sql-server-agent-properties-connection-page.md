---
title: Proprietà SQL Server Agent (pagina Connessione) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e6cdb4cc45876377a34e75fbdaffa8bd726d8e64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65089418"
---
# <a name="sql-server-agent-properties-connection-page"></a>Proprietà SQL Server Agent (pagina Connessione)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e modificare le impostazioni della connessione del servizio [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opzioni  
**Alias server host locale**  
Consente di specificare l'alias da utilizzare per la connessione all'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non è possibile utilizzare le opzioni di connessione predefinite per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, definire un alias per l'istanza e specificarlo qui.  
  
**Usa autenticazione di Windows**  
Consente di impostare l'autenticazione di [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows come metodo di autenticazione predefinito per la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent si connette come l'account con cui viene eseguito il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Usa autenticazione di SQL Server**  
Consente di impostare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come metodo di autenticazione predefinito per la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] L'autenticazione è disponibile per garantire la compatibilità con le versioni precedenti. Per un livello di sicurezza migliore, utilizzare l'autenticazione di Windows, se possibile.  
  
**Account di accesso**  
Consente di specificare il nome dell'account di accesso per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Password**  
Consente di specificare la password per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
