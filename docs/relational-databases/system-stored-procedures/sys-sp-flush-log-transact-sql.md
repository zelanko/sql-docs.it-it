---
title: sys.sp_flush_log (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 61c4cceab6c816d63226216a54d4f647e92e592d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066679"
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Scarica su disco il log delle transazioni del database corrente, finalizzando in questo modo tutte le transazioni durevoli posticipate sottoposte a commit in precedenza.  
  
 Se si sceglie di utilizzare la durabilità delle transazioni posticipate a causa dei vantaggi a livello di prestazioni, ma si desidera disporre anche di un limite garantito sulla quantità di dati che vengono persi per un arresto anomalo del server o per un failover, eseguire `sys.sp_flush_log` regolarmente. Ad esempio, se si desidera assicurarsi di non perdere più di x secondi dati relativi a, si eseguirà `sp_flush_log` ogni x secondi.  
  
 L'esecuzione di `sys.sp_flush_log` garantisce che tutte le transazioni durevoli posticipate sottoposte a commit in precedenza vengono rese durevoli. Vedere l'argomento concettuale [controllo della durabilità delle transazioni](../../relational-databases/logs/control-transaction-durability.md) per altre informazioni.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>Parametri  
 No.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Un codice restituito pari a 1 indica esito positivo.  Qualsiasi altro valore indica esito negativo.  
  
## <a name="result-sets"></a>Set di risultati  
 No.  
  
## <a name="sample-code"></a>Codice di esempio  
  
```sql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  
