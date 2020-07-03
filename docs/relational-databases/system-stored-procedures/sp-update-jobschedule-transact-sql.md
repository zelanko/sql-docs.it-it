---
title: sp_update_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobschedule_TSQL
- sp_update_jobschedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobschedule
ms.assetid: 4df02594-4cd1-49a9-8d97-37c44e4d5423
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5a526a5a304d790cfa0bd373f6c9f7225ffe3d2f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891334"
---
# <a name="sp_update_jobschedule-transact-sql"></a>sp_update_jobschedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Modifica le impostazioni di pianificazione del processo specificato.  
  
 **sp_update_jobschedule** è disponibile solo per compatibilità con le versioni precedenti.  
  
> [!IMPORTANT]
>  Per ulteriori informazioni sulla sintassi utilizzata nelle versioni precedenti di Microsoft SQL Server, vedere Transact-SQL Referencefor Microsoft SQL Server 2000 *.*  
  
## <a name="remarks"></a>Osservazioni  
 È possibile gestire le pianificazioni dei processi in modo indipendente dai processi. Per aggiornare una pianificazione, utilizzare **sp_update_schedule**.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Solo i membri di **sysadmin** possono utilizzare questa stored procedure per aggiornare le pianificazioni dei processi di proprietà di altri utenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di SQL Server Agent &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_update_schedule &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)  
  
  
