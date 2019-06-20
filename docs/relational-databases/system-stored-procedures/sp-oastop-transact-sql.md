---
title: sp_OAStop (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAStop
- sp_OAStop_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAStop
ms.assetid: aa9eab66-c4f7-4ec7-9f0d-5d24d16da654
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db70245ce97811be77c102753b422c639531507b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65450042"
---
# <a name="spoastop-transact-sql"></a>sp_OAStop (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Arresta l'ambiente di esecuzione delle stored procedure di automazione OLE nell'intero server.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_OAStop      
```  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o un numero diverso da zero (esito negativo) corrispondente al valore intero del codice HRESULT restituito dall'oggetto di automazione OLE.  
  
 Per altre informazioni sui codici restituiti HRESULT, vedere [OLE Automation codici restituiti e informazioni sull'errore](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Note  
 Tutti i client che utilizzano le stored procedure di automazione OLE condividono uno stesso ambiente di esecuzione. Se un client richiama **sp_OAStop** verrà arrestato l'ambiente di esecuzione condiviso per tutti i client. Dopo che l'ambiente di esecuzione è stato arrestato, tutte le chiamate a **sp_OACreate** viene riavviato nell'ambiente di esecuzione.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **sysadmin** ruolo predefinito del server o execute direttamente su questa Stored Procedure. `Ole Automation Procedures` configurazione deve essere **abilitato** usare eventuali procedure di sistema correlate a automazione OLE.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene arrestato l'ambiente di esecuzione di automazione OLE condiviso.  
  
```  
EXEC sp_OAStop;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Automazione OLE Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script di automazione OLE di esempio](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
