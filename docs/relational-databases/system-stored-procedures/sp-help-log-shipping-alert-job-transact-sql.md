---
title: sp_help_log_shipping_alert_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_alert_job_TSQL
- sp_help_log_shipping_alert_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_alert_job
ms.assetid: 4d4b4577-c393-4961-b2d3-b56e980b787b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9ca751ff6cf83b648e722a7577042adc0eb02681
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62744523"
---
# <a name="sphelplogshippingalertjob-transact-sql"></a>sp_help_log_shipping_alert_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa stored procedure restituisce l'ID del processo per la gestione degli avvisi dal server di monitoraggio log shipping.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_log_shipping_alert_job  
  
```  
  
## <a name="arguments"></a>Argomenti  
 None  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Questa stored procedure restituisce il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID processo dell'agente di processo degli avvisi del log shipping. Se non esiste alcun processo per la gestione degli avvisi di log shipping, restituisce un set di risultati vuoto.  
  
## <a name="remarks"></a>Note  
 **sp_help_log_shipping_alert_job** deve essere eseguita la **master** database nel server di monitoraggio.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server può eseguire questa procedura.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
