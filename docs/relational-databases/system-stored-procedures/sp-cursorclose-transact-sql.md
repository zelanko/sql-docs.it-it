---
title: sp_cursorclose (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56ff3e67c51be8618f0254298a7d8707e18884ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724228"
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Chiude e dealloca il cursore, nonché rilascia tutte le risorse associate; vale a dire, Elimina la tabella temporanea utilizzata per il supporto di KEYSET o STATIC **cursore**. richiamare sp_cursorclose specificando ID = 9 in un pacchetto del flusso TDS.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>Argomenti  
 *cursor*  
 È un cursore *gestiscono* valore generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e restituito dalla routine sp_cursoropen. *cursore* è un parametro obbligatorio che richiede un **int** valore di input.  
  
> [!NOTE]  
>  Il valore di input -1 verrà applicato a tutti i cursori della connessione corrente.  
  
## <a name="remarks"></a>Note  
 *cursore* restituirà messaggi di errore se la procedura è stata eseguita dopo che era stato chiuso il cursore o se viene specificato un handle non valido.  
  
 Lo stato di RPC indica l'esito positivo o negativo complessivo.  
  
 Il conteggio delle righe per DONE è sempre 0.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
