---
title: sp_replication_agent_checkup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replication_agent_checkup_TSQL
- sp_replication_agent_checkup
helpviewer_keywords:
- sp_replication_agent_checkup
ms.assetid: 50357c2e-71aa-4e13-9e2e-0977a3655cc9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c35b08bf98079af5f72c48c3912613cca6ec7db0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52789243"
---
# <a name="spreplicationagentcheckup-transact-sql"></a>sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Controlla tutti i database di distribuzione per identificare gli agenti di replica in esecuzione che non hanno eseguito alcuna registrazione della cronologia entro l'intervallo di attività specificato. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@heartbeat_interval** =] **'***heartbeat_interval***'**  
 Periodo massimo in minuti durante il quale un agente può non registrare alcun messaggio sullo stato. *heartbeat_interval* viene **int**, con un valore predefinito è 10 minuti.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **sp_replication_agent_checkup** genera l'errore 14151 per ogni agente rilevato come sospetto. Registra inoltre nella cronologia un messaggio di errore relativo agli agenti.  
  
## <a name="remarks"></a>Note  
 **sp_replication_agent_checkup** viene utilizzata nella replica snapshot, la replica transazionale e di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_replication_agent_checkup**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
