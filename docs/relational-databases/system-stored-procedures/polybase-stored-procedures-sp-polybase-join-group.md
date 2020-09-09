---
description: sp_polybase_join_group (Transact-SQL)
title: sp_polybase_join_group | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 53db2ff3554c095832a6fa21accb061f2575c3d6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548386"
---
# <a name="sp_polybase_join_group-transact-sql"></a>sp_polybase_join_group (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Aggiunge un'istanza di SQL Server come nodo di calcolo a un gruppo di base per il calcolo con scalabilità orizzontale.  
  
 Per l'istanza di SQL Server deve essere installata la funzionalità di  [base](../../relational-databases/polybase/polybase-guide.md) .  La polibase consente l'integrazione di origini dati non SQL Server, ad esempio Hadoop e l'archiviazione BLOB di Azure. Vedere anche [sp_polybase_leave_group &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>Argomenti  
 * \@ head_node_address* = n'*head_node_address*'  
 Nome del computer che ospita il SQL Server nodo head del gruppo con scalabilità orizzontale di base. * \@ head_node_address* è di tipo nvarchar (255).  
  
 * \@ dms_control_channel_port* = dms_control_channel_port  
 Porta in cui è in esecuzione il canale di controllo per il nodo head PolyBase Data Movement servizio. * \@ dms_control_channel_port* è un __int16 senza segno. Il valore predefinito è **16450**.  
  
 * \@ head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 Nome del nodo head SQL Server istanza nel gruppo con scalabilità orizzontale di base. * \@ head_node_sql_server_instance_name* è di tipo nvarchar (16).  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione CONTROL SERVER.  
  
## <a name="remarks"></a>Osservazioni  
 Dopo aver eseguito il stored procedure, arrestare il motore di base e riavviare il servizio PolyBase Data Movement nel computer. Per verificare, eseguire la DMV seguente sul nodo head: **sys. dm_exec_compute_nodes**.  
  
## <a name="example"></a>Esempio  
 Nell'esempio viene unito il computer corrente come nodo di calcolo a un gruppo di base.  Il nome del nodo Head è **HST01** e il nome dell'istanza SQL Server nel nodo Head è **MSSQLSERVER**.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
