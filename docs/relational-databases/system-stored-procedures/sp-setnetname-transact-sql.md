---
title: sp_setnetname (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setnetname
- sp_setnetname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setnetname
ms.assetid: f416ba81-3835-4588-b0a3-2fe75589490e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67d07d2ea4bd1656ed8f24458410f5812ed22e70
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62656466"
---
# <a name="spsetnetname-transact-sql"></a>sp_setnetname (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Imposta i nomi di rete in **Sys. Servers** nei rispettivi nomi di computer di rete effettivi per le istanze remote di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa stored procedure può essere utilizzata per abilitare l'esecuzione di chiamate a stored procedure remote in computer il cui nome di rete contiene identificatori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non validi.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_setnetname  
@server = 'server',   
     @netname = 'network_name'  
```  
  
## <a name="arguments"></a>Argomenti  
 **@server = '** *server* **'**  
 Nome del server remoto specificato nella sintassi di chiamata a stored procedure remote codificata dall'utente. Esattamente una riga **Sys. Servers** deve esistere già per utilizzare questa *server*. *server* è di tipo **sysname**e non prevede alcun valore predefinito.  
  
 **@netname ='** *network_name* **'**  
 Nome di rete del computer a cui vengono effettuate chiamate a stored procedure remote. *nome_rete* viene **sysname**, non prevede alcun valore predefinito.  
  
 Questo nome deve corrispondere al nome del computer [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e può includere caratteri non consentiti negli identificatori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Se il nome del computer contiene identificatori non validi, potrebbero verificarsi problemi durante l'esecuzione di alcune chiamate a stored procedure remote a computer Windows.  
  
 I server collegati e i server remoti sono inclusi nello stesso spazio dei nomi. Devono quindi avere nomi diversi. Tuttavia, è possibile definire sia un server collegato e un server remoto in un server specificato tramite l'assegnazione di nomi diversi e usando **sp_setnetname** per impostare il nome di rete di uno di essi il nome di rete del server sottostante.  
  
```  
--Assume sqlserv2 is actual name of SQL Server   
--database server  
EXEC sp_addlinkedserver 'sqlserv2';  
GO  
EXEC sp_addserver 'rpcserv2';  
GO  
EXEC sp_setnetname 'rpcserv2', 'sqlserv2';  
```  
  
> [!NOTE]  
>  Usando **sp_setnetname** in modo che punti a un server collegato al server locale non è supportato. I server a cui viene fatto riferimento in questo modo non possono partecipare a transazioni distribuite.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **sysadmin** e **setupadmin** ruoli predefiniti del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrata una tipica sequenza di amministrazione utilizzata in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire la chiamata a una stored procedure remota.  
  
```  
USE master;  
GO  
EXEC sp_addserver 'Win_1';  
EXEC sp_setnetname 'Win_1','Win-1';  
EXEC Win_1.master.dbo.sp_who;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
