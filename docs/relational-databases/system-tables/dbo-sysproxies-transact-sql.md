---
description: dbo.sysproxies (Transact-SQL)
title: Proxy di dbo.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxies_TSQL
- sysproxies_TSQL
- dbo.sysproxies
- sysproxies
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxies system table
ms.assetid: a73da875-be22-45fc-b5e2-ea7ebd48e2d6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 40ffbc10351cf4ca0cccc54e810a358da9a3e9f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446618"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Definisce gli attributi di un account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|ID dell'account proxy.|  
|**nome**|**sysname**|ID dell'account proxy.|  
|**credential_id**|**int**|ID delle credenziali utilizzate dall'account proxy.|  
|**abilitato**|**tinyint**|Stato dell'account proxy.<br /><br /> **0** = disabilitato. **1** = abilitata.|  
|**description**|**nvarchar(512)**|Descrizione immessa dall'utente al momento della creazione dell'account proxy.|  
|**user_sid**|**varbinary (85)**|Microsoft Windows *security_identifier* dell'utente o del gruppo associato alla credenziale proxy.|  
|**credential_date_created**|**datetime**|Data e ora di creazione delle credenziali.|  
  
## <a name="remarks"></a>Osservazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono accedere alla tabella **sysproxies** .  
  
## <a name="see-also"></a>Vedere anche  
 [dbo.sysproxylogin &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [ Sottosistemidbo.sys&#40;&#41;Transact-SQL ](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
