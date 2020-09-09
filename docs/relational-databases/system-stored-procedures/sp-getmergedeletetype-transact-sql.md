---
description: sp_getmergedeletetype (Transact-SQL)
title: sp_getmergedeletetype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getmergedeletetype
- sp_getmergedeletetype_TSQL
helpviewer_keywords:
- sp_getmergedeletetype
ms.assetid: 64450e4d-844d-4176-874e-f3845536f7d2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d2a254a81bdd4b1a4d7718e8960ced22666b5705
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538924"
---
# <a name="sp_getmergedeletetype-transact-sql"></a>sp_getmergedeletetype (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce il tipo di eliminazione di tipo merge. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione o nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_getmergedeletetype [ @source_object = ] 'source_object', [ @rowguid =] 'rowguid', [ @delete_type=] delete_type OUTPUT  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @source_object = ] 'source_object'` Nome dell'oggetto di origine. *source_object* è di **tipo nvarchar (386)** e non prevede alcun valore predefinito.  
  
`[ @rowguid = ] 'rowguid'` Identificatore di riga per il tipo di eliminazione. *rowguid* è di tipo **uniqueidentifier**e non prevede alcun valore predefinito.  
  
`[ @delete_type = ] delete_type OUTPUT` Codice che indica il tipo di eliminazione. *delete_type* è di **tipo int**e non prevede alcun valore predefinito. *delete_type* è anche un parametro di output. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**1**|Eliminazione eseguita dall'utente|  
|**5**|Eliminazione parziale|  
|**6**|Eliminazione eseguita dal sistema|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_getmergedeletetype** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_getmergedeletetype**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
