---
title: sys. sp_cdc_drop_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_drop_job_TSQL
- sp_cdc_drop_job_TSQL
- sp_cdc_drop_job
- sys.sp_cdc_drop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_drop_job
ms.assetid: e8265846-8051-4848-b28e-fac27c10bdeb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7429f2c375daa12035e0734cf7a205f03f9be765
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82808296"
---
# <a name="syssp_cdc_drop_job-transact-sql"></a>sys.sp_cdc_drop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove un processo di pulizia o di acquisizione di Change Data Capture per il database corrente da msdb.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.sp_cdc_drop_job [ [ @job_type = ] 'job_type' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @job_type **=** ]'*job_type*'  
 Tipo di processo da rimuovere. *job_type* è di **tipo nvarchar (20)** e non può essere null. Gli input validi sono 'capture' e 'cleanup'.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuno  
  
## <a name="remarks"></a>Commenti  
 sp_cdc_drop_job viene chiamato internamente da [sys. sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede l'appartenenza al ruolo predefinito del database db_owner.  
  
## <a name="examples"></a>Esempio  
 Nell'esempio seguente viene rimosso il processo di pulizia per il database `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_drop_job @job_type = N'cleanup';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [dbo. cdc_jobs &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys. sp_cdc_disable_db &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
