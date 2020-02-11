---
title: sp_delete_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_category_TSQL
- sp_delete_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_category
ms.assetid: 63ea7d0d-a567-456e-a778-bee99e21d16c
author: stevestein
ms.author: sstein
ms.openlocfilehash: a9a6812e12366900dfc1c5808eaede727c05f958
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68120054"
---
# <a name="sp_delete_category-transact-sql"></a>sp_delete_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove dal server corrente la categoria di processi, avvisi o operatori specificata.  
  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_delete_category [ @class = ] 'class' , [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @class = ] 'class'`Classe della categoria. la classe è di *tipo* **varchar (8)** e non prevede alcun valore predefinito e deve avere uno di questi valori.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**PROCESSO**|Elimina una categoria di processi.|  
|**AVVISO**|Elimina una categoria di avvisi.|  
|**OPERATORE**|Elimina una categoria di operatori.|  
  
`[ @name = ] 'name'`Nome della categoria da rimuovere. *Name* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="remarks"></a>Osservazioni  
 **sp_delete_category** deve essere eseguito dal database **msdb** .  
  
 Quando si elimina una categoria, tutti i processi, gli avvisi o gli operatori di tale categoria vengono riclassificati nella categoria predefinita per la classe.  
  
## <a name="permissions"></a>Autorizzazioni  
 Questa procedura può essere eseguita solo dai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminata la categoria di processi `AdminJobs`.  
  
```  
USE msdb ;  
GO   
  
EXEC dbo.sp_delete_category  
    @name = N'AdminJobs',  
    @class = N'JOB' ;  
GO   
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_help_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
