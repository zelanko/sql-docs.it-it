---
title: sp_OADestroy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OADestroy_TSQL
- sp_OADestroy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OADestroy
ms.assetid: 0bd1cff4-ceff-4095-9ae4-e1e65a80f5d6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b4a7b238d3f7ade1706a78c3e595ec63ae2cce7
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449725"
---
# <a name="spoadestroy-transact-sql"></a>sp_OADestroy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina un oggetto OLE creato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_OADestroy objecttoken      
```  
  
## <a name="arguments"></a>Argomenti  
 *objecttoken*  
 È il token di oggetto di un oggetto OLE creato in precedenza tramite **sp_OACreate**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o un numero diverso da zero (esito negativo) corrispondente al valore intero del codice HRESULT restituito dall'oggetto di automazione OLE.  
  
 Per altre informazioni sui codici restituiti HRESULT, vedere [OLE Automation codici restituiti e informazioni sull'errore](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Note  
 Se **sp_OADestroy** non viene chiamato, l'oggetto creato oggetto OLE viene eliminato automaticamente alla fine del batch.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **sysadmin** ruolo predefinito del server o execute direttamente su questa Stored Procedure. `Ole Automation Procedures` configurazione deve essere **abilitato** usare eventuali procedure di sistema correlate a automazione OLE.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente elimina creato in precedenza **SQLServer** oggetto.  
  
```  
EXEC @hr = sp_OADestroy @object;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Automazione OLE Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script di automazione OLE di esempio](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
