---
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
ms.openlocfilehash: 076d5ade1f4951183578b1b46761d49dafbce8be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "70810550"
---
# <a name="sp_add_category-transact-sql"></a>sp_add_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Aggiunge al server la categoria specificata di processi, avvisi o operatori. Per un metodo alternativo, vedere [creare una categoria di processi usando SQL Server Management Studio](/sql/ssms/agent/create-a-job-category).
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 > [!IMPORTANT]  
 > In [istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la maggior parte delle funzionalità di SQL Server Agent sono attualmente supportate. Per informazioni dettagliate, vedere [istanza gestita di database SQL di Azure differenze di T-SQL da SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) .
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @class = ] 'class'`Classe della categoria da aggiungere. la classe è di *tipo* **varchar (8)** e il valore predefinito è job. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|JOB|Aggiunge una categoria di processi.|  
|ALERT|Aggiunge una categoria di avvisi.|  
|OPERATOR|Aggiunge una categoria di operatori.|  
  
`[ @type = ] 'type'`Tipo di categoria da aggiungere. il *tipo* è **varchar (12)** e il valore predefinito è **local**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|LOCAL|Categoria di processi locali.|  
|FUNZIONALITÀ MULTISERVER|Categoria di processi multiserver.|  
|Nessuno|Categoria per una classe diversa da JOB **.**|  
  
`[ @name = ] 'name'`Nome della categoria da aggiungere. Il nome deve essere univoco all'interno della classe specificata. *Name* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
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
 [sp_delete_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [dbo. sysjobs &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo. sysjobservers &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
