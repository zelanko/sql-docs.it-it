---
title: dbo.sysproxylogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxylogin_TSQL
- sysproxylogin_TSQL
- dbo.sysproxylogin
- sysproxylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxylogin system table
ms.assetid: 433d33cb-bdf2-47bb-af78-2a40b7c8dfce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b798627a09a9bb96e753221750711dbfe465657f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750297"
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Registra quali account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono associati ad ogni account proxy di SQL Server Agent. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|ID dell'account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questo valore corrisponde alla colonna **proxy_id** nella tabella **sysproxies** .|  
|**sid**|**varbinary (85)**|*Security_identifier* Microsoft Windows per l'account di accesso SQL Server.|  
|**principal_id**|**int**|ID dell'utente o del gruppo che dispone dell'autorizzazione per utilizzare l'account proxy per un processo del sottosistema specificato.|  
|**flags**|**int**|Tipo di account di accesso:<br /><br /> **0** = utente o gruppo di Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ruolo predefinito del sistema<br /><br /> **2**  =  ruolo del database **msdb**|  
  
## <a name="remarks"></a>Osservazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono accedere a questa tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Proxy didbo.sys&#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
