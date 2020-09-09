---
description: sp_startpublication_snapshot (Transact-SQL)
title: sp_startpublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_startpublication_snapshot
- sp_startpublication_snapshot_TSQL
helpviewer_keywords:
- sp_startpublication_snapshot
ms.assetid: 2cf568ee-0679-4d19-a394-27210bff61e5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6c43d44067e92a9ec606d08d9a458392d04c4e66
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551221"
---
# <a name="sp_startpublication_snapshot-transact-sql"></a>sp_startpublication_snapshot (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Utilizzato per avviare il processo dell'agente snapshot che genera lo snapshot iniziale per una pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_startpublication_snapshot [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` Nome della pubblicazione. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @publisher = ] 'publisher'` Nome di un server di pubblicazione non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *Publisher* è di **tipo sysname**e il valore predefinito è null. Non specificare questo parametro per un server di pubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_startpublication_snapshot** viene utilizzato con tutti i tipi di replica.  
  
 Per un server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pubblicazione non, questo stored procedure viene eseguito nel database di distribuzione del server di distribuzione.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_startpublication_snapshot**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e applicare lo snapshot iniziale](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [sp_addpublication_snapshot &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)  
  
  
