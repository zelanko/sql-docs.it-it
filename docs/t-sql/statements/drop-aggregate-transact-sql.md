---
title: DROP AGGREGATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_AGGREGATE_TSQL
- DROP AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- aggregate functions [SQL Server], removing
- removing user-defined functions
- dropping user-defined functions
- user-defined functions [CLR integration]
- deleting user-defined functions
- DROP AGGREGATE statement
ms.assetid: 84ffc4e7-c451-4f1f-9a67-7fc3a120e53f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7c96206e70c39d1d69cc30e8f7f464352dbe3522
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882426"
---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Rimuove una funzione di aggregazione definita dall'utente dal database corrente. Le funzioni di aggregazione definite dall'utente vengono create tramite l'istruzione [CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
## <a name="arguments"></a>Argomenti  
 *IF EXISTS*  
 **Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Rimuove in modo condizionale la funzione di aggregazione solo se esiste già.  
  
 *schema_name*  
 Nome dello schema a cui appartiene la funzione di aggregazione definita dall'utente.  
  
 *aggregate_name*  
 Nome della funzione di aggregazione definita dall'utente che si desidera eliminare.  
  
## <a name="remarks"></a>Osservazioni  
 L'istruzione DROP AGGREGATE non viene eseguita se sono presenti viste, funzioni o stored procedure create in base all'associazione a schemi che fanno riferimento alla funzione di aggregazione definita dall'utente che si desidera eliminare.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire l'istruzione DROP AGGREGATE, è necessario disporre almeno dell'autorizzazione ALTER per lo schema al quale appartiene la funzione di aggregazione definita dall'utente oppure dell'autorizzazione CONTROL per la funzione di aggregazione.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente la funzione di aggregazione `Concatenate` viene eliminata.  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [Creare funzioni di aggregazione definite dall'utente](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  
