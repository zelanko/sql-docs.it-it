---
description: sp_update_targetservergroup (Transact-SQL)
title: sp_update_targetservergroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_targetservergroup_TSQL
- sp_update_targetservergroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_targetservergroup
ms.assetid: 4ac65ed6-e07e-40e4-a282-13bfd92dfa41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6aa33876376560cfc90cbf7ab03a69fcf94fa6a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473537"
---
# <a name="sp_update_targetservergroup-transact-sql"></a>sp_update_targetservergroup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Modifica il nome del gruppo di server di destinazione specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_update_targetservergroup  
     [@name =] 'current_name' ,  
     [@new_name =] 'new_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name = ] 'current_name'` Nome del gruppo di server di destinazione. *current_name* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @new_name = ] 'new_name'` Nuovo nome per il gruppo di server di destinazione. *new_name* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire questa stored procedure, è necessario che agli utenti venga concesso il ruolo predefinito del server **sysadmin** .  
  
## <a name="remarks"></a>Osservazioni  
 **sp_update_targetservergroup** deve essere eseguito dal database **msdb** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente il nome del gruppo di server di destinazione `Servers Processing Customer Orders` viene modificato in `Local Servers Processing Customer Orders`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_targetservergroup  
    @name = N'Servers Processing Customer Orders',  
    @new_name = N'Local Servers Processing Customer Orders' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_targetservergroup &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetservergroup &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_help_targetservergroup &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
