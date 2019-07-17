---
title: sp_recompile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_recompile_TSQL
- sp_recompile
dev_langs:
- TSQL
helpviewer_keywords:
- sp_recompile
ms.assetid: 6192ca87-febd-4075-8199-14b4fa609b8c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f9b72c1a97c17f975144ad0fd364260afab1fb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002561"
---
# <a name="sprecompile-transact-sql"></a>sp_recompile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Causa la ricompilazione di stored procedure, trigger e funzioni definite dall'utente alla successiva esecuzione degli stessi. Ciò avviene tramite l'eliminazione del piano esistente dalla cache delle procedure e la creazione forzata di un nuovo piano alla successiva esecuzione della stored procedure o del trigger. In una raccolta [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], viene registrato l'evento SP:CacheInsert anziché l'evento SP:Recompile.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
  
sp_recompile [ @objname = ] 'object'  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @objname=] '*oggetto*'  
 Nome qualificato o non qualificato di una stored procedure, un trigger, una tabella, una vista o una funzione definita dall'utente nel database corrente. *oggetto* viene **nvarchar(776)** , non prevede alcun valore predefinito. Se *oggetto* è il nome di una stored procedure, trigger o funzione definita dall'utente, la stored procedure, trigger o funzione verrà ricompilata alla successiva esecuzione. Se *oggetto* è il nome di una tabella o vista, tutte le stored procedure, trigger o funzioni definite dall'utente che fanno riferimento a tabella o della vista verranno ricompilate alla successiva esecuzione degli stessi.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o un numero diverso da zero (esito negativo)  
  
## <a name="remarks"></a>Note  
 La stored procedure sp_recompile esegue la ricerca di un oggetto solo nel database corrente.  
  
 Le query usate da stored procedure, trigger e funzioni definite dall'utente vengono ottimizzate solo in fase di compilazione. Poiché le indicizzazioni o le altre modifiche che hanno effetto sulle statistiche vengono effettuate nel database, il livello di efficienza di stored procedure, trigger e funzioni definite dall'utente dopo la compilazione potrebbe risultare minore. Tramite la ricompilazione delle stored procedure e dei trigger che modificano una tabella, è possibile riottimizzare le query.  
  
> [!NOTE]  
>  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le stored procedure, i trigger e le funzioni definite dall'utente vengono ricompilati automaticamente quando la ricompilazione risulta un'operazione vantaggiosa.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER per l'oggetto specificato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene definita la ricompilazione delle stored procedure, dei trigger e delle funzioni definite dall'utente che modificano la tabella `Customer` alla loro successiva esecuzione.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
