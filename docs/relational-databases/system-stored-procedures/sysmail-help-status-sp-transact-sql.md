---
title: sysmail_help_status_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_status_sp
- sysmail_help_status_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_status_sp
ms.assetid: b44277c6-81e8-4b4d-85b3-a2f04d602e7a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 036fcaabc96f8f8c4688ff5643d2d9e1febff050
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890854"
---
# <a name="sysmail_help_status_sp-transact-sql"></a>sysmail_help_status_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Visualizza lo stato delle code di Posta elettronica database. Utilizzare **sysmail_start_sp** per avviare le code di Posta elettronica database e **sysmail_stop_sp** per arrestare le code di posta elettronica database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_help_status_sp  
```  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-set"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Status**|**nvarchar (7)**|Stato di Posta elettronica database. I valori possibili sono **Started** e **Stopped**.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Per impostazione predefinita, solo i membri del ruolo predefinito del server **sysadmin** possono accedere a questa procedura.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene visualizzato lo stato di Posta elettronica database.  
  
```  
EXECUTE msdb.dbo.sysmail_help_status_sp ;  
GO  
```  
  
 Set di risultati:  
  
```  
Status  
-------  
STARTED  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database programma esterno](../../relational-databases/database-mail/database-mail-external-program.md)   
 [sysmail_start_sp &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [sysmail_stop_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)  
  
  
