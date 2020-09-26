---
description: DROP QUEUE (Transact-SQL)
title: DROP QUEUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4bf41bb420ddaaccd0f1899c641a30a17bbb8fcd
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2020
ms.locfileid: "91380346"
---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Elimina una coda esistente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *database_name*  
 Nome del database contenente la coda da eliminare. Se non si specifica *database_name*, per impostazione predefinita viene usato il database corrente.  
  
 *schema_name (object)*  
 Nome dello schema a cui appartiene la coda da eliminare. Se non si specifica *schema_name*, per impostazione predefinita viene usato lo schema predefinito dell'utente corrente.  
  
 *queue_name*  
 Nome della coda da eliminare.  
  
## <a name="remarks"></a>Commenti  
 Non è possibile eliminare una coda se esistono servizi che fanno riferimento a essa.  
  
## <a name="permissions"></a>Autorizzazioni  
 L'autorizzazione per eliminare una coda viene assegnata per impostazione predefinita al proprietario della coda, ai membri del ruolo predefinito del database **db_ddladmin** o **db_owner** e ai membri del ruolo predefinito del server **sysadmin**.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente elimina la coda **ExpenseQueue** dal database corrente.  
  
```sql  
DROP QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
