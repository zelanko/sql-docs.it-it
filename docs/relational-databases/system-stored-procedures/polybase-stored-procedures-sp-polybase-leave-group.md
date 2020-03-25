---
title: sp_polybase_leave_group (Transact-SQL) | Microsoft Docs
description: Il sp_polybase_leave_group comando Transact-SQL rimuove un'istanza SQL Server da un gruppo di base per il calcolo con scalabilità orizzontale.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords:
- sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
author: rothja
ms.author: jroth
ms.openlocfilehash: 3fd28f5a3cecb6da28603ae6f8a88d751081e80c
ms.sourcegitcommit: df21fd156cc833f107d22413c76991b67f3715c8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/24/2020
ms.locfileid: "80216501"
---
# <a name="sp_polybase_leave_group-transact-sql"></a>sp_polybase_leave_group (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Rimuove un'istanza di SQL Server da un gruppo di base per il calcolo con scalabilità orizzontale. 
 
 Per l'istanza di SQL Server deve essere installata la funzionalità della [Guida di base](../../relational-databases/polybase/polybase-guide.md) .  La polibase consente l'integrazione di origini dati non SQL Server, ad esempio Hadoop e l'archiviazione BLOB di Azure. Vedere anche [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione CONTROL SERVER.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile rimuovere un nodo di calcolo solo da un gruppo.  
  
 Dopo aver eseguito il stored procedure, riavviare il motore di base e il servizio PolyBase Data Movement nel computer. Per verificare, eseguire la DMV seguente sul nodo head: **sys. dm_exec_compute_nodes**.  
  
## <a name="example"></a>Esempio  
 Nell'esempio viene rimosso il computer corrente da un gruppo di base.  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione a polibase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
