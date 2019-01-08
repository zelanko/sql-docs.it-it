---
title: sp_ivindexhasnullcols (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5e9ab98dc5beb4f2e07ac7fa62386f9fd44703ab
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823330"
---
# <a name="spivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verifica che l'indice cluster della vista indicizzata sia univoco e non includa colonne che ammettono valori Null se la vista indicizzata verrà utilizzata per la creazione di una pubblicazione transazionale. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@viewname**=] **'***view_name***'**  
 Nome della vista da verificare. *view_name* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@fhasnullcols**=] *field_has_null_columns* OUTPUT  
 Flag che indica se l'indice della vista include colonne che ammettono valori Null. *view_name* viene **sysname**, non prevede alcun valore predefinito. Restituisce un valore pari **1** se l'indice della vista include colonne che ammettono valori NULL. Restituisce un valore pari **0** se la vista non contiene colonne che ammettono valori null.  
  
> [!NOTE]  
>  Se la stored procedure restituisce un codice restituito del **1**, vale a dire l'esecuzione di stored procedure ha esito negativo, questo valore è **0** e deve essere ignorato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_ivindexhasnullcols** viene utilizzato dalla replica transazionale.  
  
 Per impostazione predefinita, gli articoli di vista indicizzata di una pubblicazione vengono creati sotto forma di tabella nei Sottoscrittori. Quando tuttavia la colonna indicizzata ammette valori Null, la vista indicizzata viene creata come vista indicizzata anziché come tabella nel Sottoscrittore. Tramite l'esecuzione di questa stored procedure è possibile verificare se nella vista indicizzata corrente esiste o meno questo problema.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_ivindexhasnullcols**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
