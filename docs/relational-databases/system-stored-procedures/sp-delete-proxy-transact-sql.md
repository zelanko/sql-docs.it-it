---
description: sp_delete_proxy (Transact-SQL)
title: sp_delete_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_proxy
- sp_delete_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_proxy
- DROP PROXY statement
ms.assetid: 44a1db13-b7f2-4dab-a1b5-b8dafb41737c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fe7fa16aa15e20be9419a3cb3705bc40d4bba9f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447294"
---
# <a name="sp_delete_proxy-transact-sql"></a>sp_delete_proxy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Rimuove il proxy specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_delete_proxy [ @proxy_id = ] id , [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @proxy_id = ] id` Numero di identificazione del proxy da rimuovere. Il *proxy_id* è di **tipo int**e il valore predefinito è null.  
  
`[ @proxy_name = ] 'proxy_name'` Nome del proxy da rimuovere. Il *proxy_name* è di **tipo sysname**e il valore predefinito è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="remarks"></a>Osservazioni  
 È necessario specificare ** \@ proxy_name** o ** \@ proxy_id** . Se si specificano entrambi gli argomenti, devono riferirsi tutti e due allo stesso proxy per consentire la corretta esecuzione della stored procedure.  
  
 Se un passaggio di processo fa riferimento al proxy specificato, non è possibile eliminare il proxy e la stored procedure non viene eseguita correttamente.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per impostazione predefinita, solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_delete_proxy**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato il proxy `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_proxy &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)  
  
  
