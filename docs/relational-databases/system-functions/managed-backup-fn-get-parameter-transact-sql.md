---
description: managed_backup. fn_get_parameter (Transact-SQL)
title: managed_backup. fn_get_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_get_parameter_TSQL
- smart_admin.fn_get_parameter
- fn_get_parameter_TSQL
- fn_get_parameter
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_parameter
- smart_admin.fn_get_parameter
ms.assetid: ed94e54d-4516-4806-a8ce-f013d3a04122
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: da8c646cca92a5ef25fd12322fd8a6bd222a1c9e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419515"
---
# <a name="managed_backupfn_get_parameter-transact-sql"></a>managed_backup. fn_get_parameter (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Restituisce una tabella con 0, 1 o più righe di coppie di parametri e valori.  
  
 Utilizzare questa stored procedure per esaminare tutte le impostazioni o quelle di una configurazione specifica per Smart Admin.  
  
 Se il parametro non è stato mai configurato, la funzione restituisce 0 righe.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
managed_backup.fn_get_parameter ('parameter_name' | '' | NULL )  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> Argomenti  
 parameter_name  
 Nome del parametro. parameter_name è di **tipo nvarchar (128)**. Se viene fornito come argomento della funzione NULL o una stringa vuota, vengono restituite coppie nome-valore per tutti i parametri Smart Admin configurati.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|parameter_name|NVARCHAR(128)|Nome del parametro. Di seguito è riportato un elenco corrente di parametri restituiti:<br/><br/>**FileRetentionDebugXevent**<br/><br/>**SSMBackup2WADebugXevent**<br/><br/>**SSMBackup2WANotificationEmailIds**<br/><br/>**SSMBackup2WAEnableUserDefinedPolicy**<br/><br/>**SSMBackup2WAEverConfigured**<br/><br/>**StorageOperationDebugXevent**|  
|parameter_value|NVARCHAR(128)|Valore impostato corrente del parametro.|  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Autorizzazioni  
 Sono richieste le autorizzazioni SELECT per la funzione.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti tutti i parametri configurati almeno una volta, con i relativi valori correnti.  
  
```  
USE MSDB  
GO  
SELECT *   
FROM managed_backup.fn_get_parameter (NULL)  
  
```  
  
 L'esempio seguente restituisce l'ID di posta elettronica specificato per ricevere notifiche di errore. Se non vengono restituite righe, l'opzione di notifica tramite posta elettronica non è stata abilitata.  
  
```  
USE MSDB  
GO  
SELECT *  
FROM managed_backup.fn_get_parameter ('SSMBackup2WANotficationEmailIds')  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Backup gestito di SQL Server in Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
