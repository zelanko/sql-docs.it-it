---
description: sys.sysremotelogins (Transact-SQL)
title: sys.sysremotelogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysremotelogins
- sysremotelogins_TSQL
- sys.sysremotelogins
- sys.sysremotelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysremotelogins system table
- sys.sysremotelogins compatibility view
ms.assetid: b7ffcfa6-aed8-41d4-8b70-845439ab813d
author: rothja
ms.author: jroth
ms.openlocfilehash: 39cf5ae09d0857acf7d0d89b2be789162a751b64
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482049"
---
# <a name="syssysremotelogins-transact-sql"></a>sys.sysremotelogins (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una riga per ogni utente remoto a cui è consentito chiamare stored procedure remote in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**remoteserverid**|**smallint**|Identificazione del server remoto.|  
|**remoteusername**|**sysname**|Nome dell'account di accesso dell'utente in un server remoto.|  
|**Stato**|**smallint**|Viene restituito 0.|  
|**sid**|**varbinary (85)**|ID di sicurezza dell'utente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.|  
|**changedate**|**datetime**|Data e ora di aggiunta dell'utente remoto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
