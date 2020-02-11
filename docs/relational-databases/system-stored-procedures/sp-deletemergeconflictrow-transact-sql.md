---
title: sp_deletemergeconflictrow (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
author: stevestein
ms.author: sstein
ms.openlocfilehash: a315bc147cf86df40cf6fa216b8c45eeb1fcccca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111961"
---
# <a name="sp_deletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina le righe da una tabella dei conflitti o dalla [MSmerge_conflicts_info &#40;tabella&#41;Transact-SQL](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) . Questa stored procedure viene eseguita nella stessa posizione di archiviazione della tabella con conflitti in qualsiasi database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_deletemergeconflictrow [ [ @conflict_table = ] 'conflict_table' ]  
    [ , [ @source_object = ] 'source_object' ]  
    { , [ @rowguid = ] 'rowguid'  
        , [ @origin_datasource = ] 'origin_datasource' ] }  
    [ , [ @drop_table_if_empty = ] 'drop_table_if_empty' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @conflict_table = ] 'conflict_table'`Nome della tabella dei conflitti. *conflict_table* è di **%** **tipo sysname**e il valore predefinito è. Se il *conflict_table* viene specificato come null o **%**, si presuppone che si verifichi un conflitto di eliminazione e che la riga corrispondente a *rowguid* e *origin_datasource* e *source_object* venga eliminata dalla tabella [MSmerge_conflicts_info &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) .  
  
`[ @source_object = ] 'source_object'`Nome della tabella di origine. *source_object* è di **tipo nvarchar (386)** e il valore predefinito è null.  
  
`[ @rowguid = ] 'rowguid'`Identificatore di riga per il conflitto di eliminazione. *rowguid* è di tipo **uniqueidentifier**e non prevede alcun valore predefinito.  
  
`[ @origin_datasource = ] 'origin_datasource'`Origine del conflitto. *origin_datasource* è di tipo **varchar (255)** e non prevede alcun valore predefinito.  
  
`[ @drop_table_if_empty = ] 'drop_table_if_empty'`Flag che indica che la *conflict_table* deve essere eliminata se è vuota. *drop_table_if_empty* è di tipo **varchar (10)** e il valore predefinito è false.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_deletemergeconflictrow** viene utilizzata nella replica di tipo merge.  
  
 [MSmerge_conflicts_info &#40;tabella&#41;Transact-SQL](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) è una tabella di sistema e non viene eliminata dal database, anche se è vuota.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_deletemergeconflictrow**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
