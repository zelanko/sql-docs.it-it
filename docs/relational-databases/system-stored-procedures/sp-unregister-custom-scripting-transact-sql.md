---
description: sp_unregister_custom_scripting (Transact-SQL)
title: sp_unregister_custom_scripting (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0247061b99b53cb53e12fa4e5e3a1284430287e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480934"
---
# <a name="sp_unregister_custom_scripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Questo stored procedure rimuove un file di script o stored procedure personalizzato definito dall'utente [!INCLUDE[tsql](../../includes/tsql-md.md)] che è stato registrato eseguendo [sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @type = ] 'type'` Tipo di stored procedure o script personalizzato da rimuovere. il *tipo* è **varchar (16)** e non prevede alcun valore predefinito. i possibili valori sono i seguenti.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**insert**|La stored procedure o lo script personalizzato registrato viene eseguito quando viene replicata un'istruzione INSERT.|  
|**update**|La stored procedure o lo script personalizzato registrato viene eseguito quando viene replicata un'istruzione UPDATE.|  
|**delete**|La stored procedure o lo script personalizzato registrato viene eseguito quando viene replicata un'istruzione DELETE.|  
|**custom_script**|La stored procedure o lo script personalizzato registrato viene eseguito al termine del trigger DDL (Data Definition Language).|  
  
`[ @publication = ] 'publication'` Nome della pubblicazione per la quale è in corso la rimozione del stored procedure o dello script personalizzato. *Publication* è di **tipo sysname**e il valore predefinito è null.  
  
`[ @article = ] 'article'` Nome dell'articolo per cui è in corso la rimozione del stored procedure o dello script personalizzato. *article* è di **tipo sysname**e il valore predefinito è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_unregister_custom_scripting** viene utilizzata per la replica snapshot e transazionale.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** , del ruolo predefinito del database **db_owner** o del ruolo predefinito del database **db_ddladmin** possono eseguire **sp_unregister_custom_scripting**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_register_custom_scripting &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
