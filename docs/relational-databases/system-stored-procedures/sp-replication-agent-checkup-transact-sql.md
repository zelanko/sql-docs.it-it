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
ms.openlocfilehash: b434d4bda50cf03442020ba2f0c029aaa1e09cd9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771235"
---
# <a name="sp_replication_agent_checkup-transact-sql"></a>sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Controlla tutti i database di distribuzione per identificare gli agenti di replica in esecuzione che non hanno eseguito alcuna registrazione della cronologia entro l'intervallo di attività specificato. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @heartbeat_interval = ] 'heartbeat_interval'`Numero massimo di minuti per cui un agente può passare senza registrare un messaggio di stato. *heartbeat_interval* è di **tipo int**e il valore predefinito è 10 minuti.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **sp_replication_agent_checkup** genera l'errore 14151 per ogni agente rilevato come sospetto. Registra inoltre nella cronologia un messaggio di errore relativo agli agenti.  
  
## <a name="remarks"></a>Osservazioni  
 **sp_replication_agent_checkup** viene utilizzata per la replica snapshot, la replica transazionale e la replica di tipo merge.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_replication_agent_checkup**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
