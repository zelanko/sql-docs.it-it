---
title: Opzione di configurazione del server Agent XPs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Agent XPs option
- extended stored procedures [SQL Server], SQL Server Agent
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4598678cc4dea0a11c37545487ce09529dbb4584
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935927"
---
# <a name="agent-xps-server-configuration-option"></a>Opzione di configurazione del server Agent XPs
  L'opzione **Agent XPs** consente di abilitare le stored procedure estese del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel server. Se questa opzione non è attivata, il nodo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non sarà disponibile in Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 Quando si utilizza lo strumento [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, le stored procedure estese vengono abilitate automaticamente. Per ulteriori informazioni, vedere [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] In Esplora oggetti il nodo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent non viene visualizzato a meno che le stored procedure estese non vengano abilitate indipendentemente dallo stato del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 I valori possibili sono:  
  
-   **0**, che indica che le stored procedure estese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non sono disponibili e corrisponde al valore predefinito.  
  
-   **1**, che indica che le stored procedure estese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sono disponibili.  
  
 L'impostazione diventa effettiva immediatamente e non richiede l'arresto e il riavvio del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrata l'attivazione delle stored procedure estese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Agent XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Automatizzazione delle attività amministrative &#40;SQL Server Agent&#41;](../../ssms/agent/sql-server-agent.md)   
 [Start, Stop, or Pause the SQL Server Agent Service](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
