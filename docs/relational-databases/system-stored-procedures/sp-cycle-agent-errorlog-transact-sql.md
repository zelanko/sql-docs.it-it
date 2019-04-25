---
title: sp_cycle_agent_errorlog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dfb1f3ef9dc8bdac81ed7c3a3a490ca91f73ff23
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62507196"
---
# <a name="spcycleagenterrorlog-transact-sql"></a>sp_cycle_agent_errorlog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Chiude il log degli errori corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e rinumera le estensioni del log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, esattamente come quando si riavvia il server. Il nuovo log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent contiene una riga in cui è registrata l'operazione di creazione di un nuovo log.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_cycle_agent_errorlog  
```  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Ogni volta che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente è avviato, corrente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registro errori dell'agente è stato rinominato **SQLAgent.1**; **SQLAgent.1** diventa **SQLAgent.2**, **SQLAgent.2** diventa **SQLAgent.3**e così via. **sp_cycle_agent_errorlog** consente di rinumerare i file di log degli errori senza arrestare e riavviare il server.  
  
 Questa stored procedure deve essere eseguita dal **msdb** database.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni di esecuzione **sp_cycle_errorlog** sono limitati ai membri delle **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene rinumerato il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_cycle_errorlog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
