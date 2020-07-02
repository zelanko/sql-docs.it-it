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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b2a0f6f23d38cb0841ba6e1b7891d9d32fc95b1f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85646259"
---
# <a name="sp_cursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Chiude e dealloca il cursore, oltre a rilasciare tutte le risorse associate; ovvero elimina la tabella temporanea utilizzata per il supporto di KEYSET o di un **cursore**statico. sp_cursorclose viene richiamato specificando ID = 9 in un pacchetto TDS (Tabular Data Stream).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>Argomenti  
 *cursor*  
 Valore dell' *handle* del cursore generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e restituito dalla routine sp_cursoropen. *Cursor* è un parametro obbligatorio che richiede un valore di input **int** .  
  
> [!NOTE]  
>  Il valore di input -1 verrà applicato a tutti i cursori della connessione corrente.  
  
## <a name="remarks"></a>Osservazioni  
 il *cursore* restituirà messaggi di errore se la procedura è stata eseguita dopo la chiusura del cursore o se è stato specificato un handle non valido.  
  
 Lo stato di RPC indica l'esito positivo o negativo complessivo.  
  
 Il conteggio delle righe per DONE è sempre 0.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_cursoropen &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
