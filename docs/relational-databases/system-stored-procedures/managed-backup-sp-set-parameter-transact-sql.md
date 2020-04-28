---
title: managed_backup. sp_set_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_parameter_TSQL
- sp_set_parameter
- smart_admin.sp_set_parameter
- smart_admin.sp_set_parameter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_parameter
- smart_admin.sp_set_parameter
ms.assetid: bd8ae5fd-1337-4b7f-b0a4-153cbca9fa5f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 838a8b0d998476a37b0dd4d30cab5041ad4276a0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67942039"
---
# <a name="managed_backupsp_set_parameter-transact-sql"></a>managed_backup. sp_set_parameter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Imposta il valore del parametro di sistema dell'amministrazione intelligente specificato.  
  
 I parametri disponibili sono correlati al [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Questi parametri vengono utilizzati per impostare le notifiche tramite posta elettronica, abilitare eventi estesi specifici e abilitare i criteri di gestione basata su criteri impostati dall'utente. È necessario specificare il nome del parametro e le coppie di valori del parametro.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
EXEC managed_backup.sp_set_parameter   
    [@parameter_name = ] {'SSMBackup2WANotificationEmailIds' | 'SSMBackup2WAEnableUserDefinedPolicy' | 'SSMBackup2WADebugXevent' | 'FileRetentionDebugXevent' | 'StorageOperationDebugXevent'}  
    ,[@parameter_value = ] 'parameter_value'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>Argomenti  
 @parameter_name  
 Nome del parametro per cui si desidera impostare il valore. @parameter_nameè di tipo NVARCHAR (128). I nomi dei parametri disponibili sono **SSMBackup2WANotificationEmailIds**, **SSMBackup2WADebugXevent**, **SSMBackup2WAEnableUserDefinedPolicy**, **FileRetentionDebugXevent**e **StorageOperationDebugXevent**.  
  
 @parameter_value  
 Valore del parametro che si desidera impostare. @parametervalue è di tipo NVARCHAR (128).  Di seguito vengono indicati il nome del parametro e le coppie di valori consentiti:  
  
-   @parameter_name=' SSMBackup2WANotificationEmailIds ': @parameter_value =' email '  
  
-   @parameter_name=' SSMBackup2WAEnableUserDefinedPolicy ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name=' SSMBackup2WADebugXevent ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name=' FileRetentionDebugXevent ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name=' StorageOperationDebugXevent ' = {' true ' | ' false '}  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="best-practices"></a>Procedure consigliate  
 Sezione facoltativa in cui vengono descritte le procedure consigliate che l'utente deve conoscere quando viene eseguita l'istruzione o la routine.  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Autorizzazioni  
 Sono necessarie le autorizzazioni **Execute** per **managed_backup. sp_set_parameter** stored procedure.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti vengono abilitati eventi estesi operativi e di debug.  
  
```  
-- to enable operational events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionOperationalXevent', 'True'  
--  to enable debug events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
```  
  
 Nell'esempio seguente vengono abilitate le notifiche tramite posta elettronica di errori e avvisi e viene impostato l'ID di posta elettronica da utilizzare per inviare notifiche a:  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'  
  
```  
  
  
