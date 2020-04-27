---
title: Sostituire l'utilizzo del xp_sqlagent_proxy_account stored procedure esteso con le nuove stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- xp_sqlagent_proxy_account
ms.assetid: 0e3cc931-6237-41dd-bf0d-0c03f4d8fff2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4faff8420e318f7250cfc67dda173197d8028f0b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092755"
---
# <a name="replace-usage-of-the-xp_sqlagent_proxy_account-extended-stored-procedure-with-new-stored-procedures"></a>Al posto della stored procedure estesa xp_sqlagent_proxy_account utilizzare le nuove stored procedure
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent vengono supportati più proxy. Per definire questi proxy, è necessario utilizzare un nuovo set di stored procedure. Per ulteriori informazioni sulle nuove stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere gli argomenti seguenti nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   "sp_add_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_delete_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_login_for_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_proxy_for_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_sqlagent_subsystems ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_grant_proxy_to_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_grant_login_to_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_help_proxy" ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_revoke_login_from_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_revoke_proxy_from_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_update_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
> [!NOTE]  
>  Dopo l'aggiornamento a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], le istruzioni che utilizzano il **xp_sqlagent_proxy_account** stored procedure esteso non funzioneranno. Utilizzare **sp_xp_cmdshell_proxy_account** anziché **xp_sqlagent_proxy_account** per impostare il proxy per **xp_cmdshell**.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="see-also"></a>Vedi anche  
 [Problemi di aggiornamento di SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
