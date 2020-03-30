---
title: DROP MESSAGE TYPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_MESSAGE_TYPE_TSQL
- DROP MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- message types [Service Broker], removing
- deleting message types
- dropping message types
- DROP MESSAGE TYPE statement
- removing message types
ms.assetid: 805e8ad5-8a93-49f0-88e5-e6fca8814dd5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 48c1a96998adf9fddd8ffd8da0e6f6711b9277b0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "70745318"
---
# <a name="drop-message-type-transact-sql"></a>DROP MESSAGE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Elimina un tipo di messaggio esistente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP MESSAGE TYPE message_type_name  
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *message_type_name*  
 Nome del tipo di messaggio da eliminare. Non è possibile specificare i nomi del server, del database e dello schema.  
  
## <a name="permissions"></a>Autorizzazioni  
 L'autorizzazione per eliminare un tipo di messaggio viene assegnata per impostazione predefinita al proprietario del tipo di messaggio, ai membri del ruolo predefinito del database db_ddladmin o db_owner e ai membri del ruolo predefinito del server sysadmin.  
  
## <a name="remarks"></a>Osservazioni  
 Non è possibile eliminare un tipo di messaggio in caso di contratti che vi fanno riferimento.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato il tipo di messaggio `//Adventure-Works.com/Expenses/SubmitExpense` dal database.  
  
```  
DROP MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense] ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [CREATE MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
