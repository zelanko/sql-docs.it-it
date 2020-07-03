---
title: sp_delete_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_operator
- sp_delete_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_operator
ms.assetid: ff6c2c4b-e9fe-4d0c-bbc2-a2ddcc1acb95
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c584dceb9306d6a74575b548bfd9d8548acb47a5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85862475"
---
# <a name="sp_delete_operator-transact-sql"></a>sp_delete_operator (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Rimuove un operatore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_delete_operator [ @name = ] 'name'   
     [ , [ @reassign_to_operator = ] 'reassign_operator' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name = ] 'name'`Nome dell'operatore da eliminare. *Name* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @reassign_to_operator = ] 'reassign_operator'`Nome di un operatore a cui è possibile riassegnare gli avvisi dell'operatore specificato. *reassign_operator* è di **tipo sysname**e il valore predefinito è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="remarks"></a>Osservazioni  
 Quando si rimuove un operatore, vengono rimosse tutte le notifiche associate.  
  
## <a name="permissions"></a>Autorizzazioni  
 I membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_delete_operator**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato l'operatore `François Ajenstat`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_operator @name = 'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_operator &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
