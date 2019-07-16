---
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b7be2bb99a92794ed8c1b5971edca47522c2552
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941930"
---
# <a name="sppolybasejoingroup-transact-sql"></a>sp_polybase_join_group (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Aggiunge un'istanza di SQL Server come nodo di calcolo a un gruppo di PolyBase per il calcolo della scalabilità orizzontale.  
  
 L'istanza di SQL Server deve disporre di [PolyBase](../../relational-databases/polybase/polybase-guide.md) funzionalità installata.  PolyBase consente l'integrazione di origini dati non SQL Server, ad esempio l'archivio blob di Hadoop e Azure. Vedere anche [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>Argomenti  
 *@head_node_address* = N'*head_node_address*'  
 Il nome del computer che ospita il nodo head di SQL Server del gruppo di scalabilità orizzontale di PolyBase. *@head_node_address* è nvarchar(255.  
  
 *@dms_control_channel_port* = dms_control_channel_port  
 La porta in cui viene eseguito il canale di controllo per il nodo head PolyBase Data Movement Service. *@dms_control_channel_port* è un __int16 senza segno. Il valore predefinito è **16450**.  
  
 *@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 Il nome dell'istanza di SQL Server del nodo head del gruppo di scalabilità orizzontale di PolyBase. *@head_node_sql_server_instance_name* è nvarchar (16).  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL SERVER.  
  
## <a name="remarks"></a>Note  
 Dopo aver eseguito la stored procedure, arrestare il motore PolyBase e riavviare PolyBase Data Movement Service nel computer. Per verificare eseguire sulla seguente DMV nel nodo head: **DM exec_compute_nodes**.  
  
## <a name="example"></a>Esempio  
 Nell'esempio viene aggiunto il computer corrente come nodo di calcolo a un gruppo PolyBase.  È il nome del nodo head **HST01** ed è il nome dell'istanza di SQL Server nel nodo head **MSSQLSERVER**.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
