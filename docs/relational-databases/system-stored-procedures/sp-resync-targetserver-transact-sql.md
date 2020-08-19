---
description: sp_resync_targetserver (Transact-SQL)
title: sp_resync_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_resync_targetserver
- sp_resync_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_resync_targetserver
ms.assetid: 40e44df7-d3e3-44ee-b149-08aba629a21f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 858c2ffe0740c43892ff2245047823c9cecbd12a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469215"
---
# <a name="sp_resync_targetserver-transact-sql"></a>sp_resync_targetserver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Risincronizza tutti i processi multiserver nel server di destinazione specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_resync_targetserver  
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @server_name = ] 'server'` Nome del server da risincronizzare. *server* è di tipo **sysname**e non prevede alcun valore predefinito. Se si specifica **All** , tutti i server di destinazione vengono risincronizzati.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Segnala il risultato delle azioni **sp_post_msx_operation** .  
  
## <a name="remarks"></a>Osservazioni  
 **sp_resync_targetserver** Elimina il set di istruzioni corrente per il server di destinazione e invia un nuovo set per il server di destinazione da scaricare. Le nuove istruzioni prevedono l'eliminazione di tutti i processi multiserver e l'inserimento dei vari processi indirizzati al server.  
  
## <a name="permissions"></a>Autorizzazioni  
 Le autorizzazioni per l'esecuzione di questa procedura vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene risincronizzato il server di destinazione `SEATTLE1`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_resync_targetserver  
    N'SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_help_downloadlist &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)   
 [sp_post_msx_operation &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
