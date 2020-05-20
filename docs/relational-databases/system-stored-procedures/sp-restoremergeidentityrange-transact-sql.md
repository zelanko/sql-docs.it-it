---
title: sp_restoremergeidentityrange (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_restoremergeidentityrange_TSQL
- sp_restoremergeidentityrange
helpviewer_keywords:
- sp_restoremergeidentityrange
ms.assetid: 7923e422-2748-40c0-b5a8-6410c48d5b70
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a41b725d46c96f1ab79444246ab538b0c3f539f0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82816941"
---
# <a name="sp_restoremergeidentityrange-transact-sql"></a>sp_restoremergeidentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa stored procedure viene utilizzata per aggiornare le assegnazioni degli intervalli di valori Identity. Garantisce inoltre che la gestione automatica degli intervalli di valori Identity funzioni correttamente dopo il ripristino di un server di pubblicazione da un backup. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_restoremergeidentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'`Nome della pubblicazione. *Publication* è di **tipo sysname**e il valore predefinito è **All**. Se viene specificato questo parametro, vengono ripristinati solo gli intervalli di valori Identity per la pubblicazione specificata.  
  
`[ @article = ] 'article'`Nome dell'articolo. *article* è di **tipo sysname**e il valore predefinito è **All**. Se specificato, vengono ripristinati solo gli intervalli di valori Identity per l'articolo specificato.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_restoremergeidentityrange** viene utilizzato con la replica di tipo merge.  
  
 **sp_restoremergeidentityrange** ottiene le informazioni di allocazione massime dell'intervallo di valori Identity dal server di distribuzione e aggiorna i valori nella colonna **max_used** di [MSmerge_identity_range_allocations &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msmerge-identity-range-allocations-transact-sql.md) per gli articoli che utilizzano la gestione automatica degli intervalli di valori Identity.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_restoremergeidentityrange**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addmergearticle &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [Replica colonne Identity](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
