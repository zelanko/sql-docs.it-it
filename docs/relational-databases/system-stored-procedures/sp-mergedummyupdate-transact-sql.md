---
title: sp_mergedummyupdate (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergedummyupdate_TSQL
- sp_mergedummyupdate
helpviewer_keywords:
- sp_mergedummyupdate
ms.assetid: b834f7f6-9588-4d59-a3e2-83d8e8e722e1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bb4874233f85a2565c3d30546749fa9bffe79ebb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63017763"
---
# <a name="spmergedummyupdate-transact-sql"></a>sp_mergedummyupdate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esegue un aggiornamento fittizio della riga specificata in modo che venga inviata nuovamente durante la successiva operazione di merge. Questa stored procedure può essere eseguita nel database di pubblicazione del server di pubblicazione oppure nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_mergedummyupdate [ @source_object =] 'source_object', [ @rowguid =] 'rowguid'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @source_object = ] 'source_object'` È il nome dell'oggetto di origine. *source_object*viene **nvarchar(386)**, non prevede alcun valore predefinito.  
  
`[ @rowguid = ] 'rowguid'` È l'identificatore di riga. *ROWGUID* viene **uniqueidentifier**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_mergedummyupdate** viene utilizzata nella replica di tipo merge.  
  
 **sp_mergedummyupdate** è utile se si scrive il proprio alternativa per il Visualizzatore conflitti di replica (Wzcnflct.exe).  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **db_owner** ruolo predefinito del database possono eseguire **sp_mergedummyupdate**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
