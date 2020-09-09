---
description: sp_cursorclose (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0363b69839d6cf58eebaa0394a591050c3443cd6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536636"
---
# <a name="sp_cursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
 [sp_cursoropen &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
