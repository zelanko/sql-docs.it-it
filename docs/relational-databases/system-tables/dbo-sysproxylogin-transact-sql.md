---
title: dbo. sysproxylogin (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: cfa29500a798cdcfe535a377abd8c649972415b0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82825956"
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra quali account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono associati ad ogni account proxy di SQL Server Agent. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|ID dell'account proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questo valore corrisponde alla colonna **proxy_id** nella tabella **sysproxies** .|  
|**sid**|**varbinary (85)**|*Security_identifier* Microsoft Windows per l'account di accesso SQL Server.|  
|**principal_id**|**int**|ID dell'utente o del gruppo che dispone dell'autorizzazione per utilizzare l'account proxy per un processo del sottosistema specificato.|  
|**flags**|**int**|Tipo di account di accesso:<br /><br /> **0** = utente o gruppo di Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ruolo predefinito del sistema<br /><br /> **2**  =  ruolo del database **msdb**|  
  
## <a name="remarks"></a>Commenti  
 Solo i membri del ruolo predefinito del server **sysadmin** possono accedere a questa tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [dbo. sysproxies &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
