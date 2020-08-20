---
description: sp_add_category (Transact-SQL)
title: sp_add_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 40ce855f929a19f9dbcd757b0e1ea8774fbe2cb3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481691"
---
# <a name="sp_add_category-transact-sql"></a>sp_add_category (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Aggiunge al server la categoria specificata di processi, avvisi o operatori. Per un metodo alternativo, vedere [creare una categoria di processi usando SQL Server Management Studio](/sql/ssms/agent/create-a-job-category).
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 > [!IMPORTANT]  
 > Nel [istanza gestita SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la maggior parte delle funzionalità di SQL Server Agent sono attualmente supportate. Per informazioni dettagliate, vedere le [differenze di T-SQL in Azure sql istanza gestita da SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) .
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @class = ] 'class'` Classe della categoria da aggiungere. la classe è di *tipo* **varchar (8)** e il valore predefinito è job. i possibili valori sono i seguenti.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|JOB|Aggiunge una categoria di processi.|  
|ALERT|Aggiunge una categoria di avvisi.|  
|OPERATOR|Aggiunge una categoria di operatori.|  
  
`[ @type = ] 'type'` Tipo di categoria da aggiungere. il *tipo* è **varchar (12)** e il valore predefinito è **local**. i possibili valori sono i seguenti.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|LOCAL|Categoria di processi locali.|  
|FUNZIONALITÀ MULTISERVER|Categoria di processi multiserver.|  
|NONE|Categoria per una classe diversa da JOB **.**|  
  
`[ @name = ] 'name'` Nome della categoria da aggiungere. Il nome deve essere univoco all'interno della classe specificata. *Name* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="remarks"></a>Osservazioni  
 **sp_add_category** deve essere eseguito dal database **msdb** .  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_add_category**.  
  
## <a name="examples"></a>Esempi  
 In questo esempio viene creata la categoria di processi locale `AdminJobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_delete_category &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [ Processi didbo.sys&#40;&#41;Transact-SQL ](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo.sysjobservers &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
