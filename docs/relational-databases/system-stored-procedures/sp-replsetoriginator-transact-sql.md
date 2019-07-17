---
title: sp_replsetoriginator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords:
- sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
author: stevestein
ms.author: sstein
ms.openlocfilehash: dd3e27e935d7774c3882e8cc46430542351dd87c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113147"
---
# <a name="spreplsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Utilizzata per richiamare il rilevamento e la gestione di loopback nella replica transazionale bidirezionale. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @server_name = ] 'server_name'` È il nome del server in cui viene applicata la transazione. *originating_server* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @database_name = ] 'database_name'` È il nome del database in cui viene applicata la transazione. *originating_db* viene **sysname**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_replsetoriginator** viene eseguita dall'agente di distribuzione per registrare l'origine delle transazioni applicate dalla replica. Queste informazioni vengono utilizzate per richiamare il rilevamento di loopback per le sottoscrizioni transazionali bidirezionali per cui è stata impostata la proprietà di loopback.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** nel server di pubblicazione, i membri del ruolo predefinito del server di **db_owner** ruolo predefinito del database nel database di pubblicazione, o gli utenti nell'elenco di accesso (PAL) alla pubblicazione può eseguire **sp_replsetoriginator**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
