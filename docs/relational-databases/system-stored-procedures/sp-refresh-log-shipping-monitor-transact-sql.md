---
title: sp_refresh_log_shipping_monitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
author: stevestein
ms.author: sstein
ms.openlocfilehash: c19f9b99173ca04e6ce15862e22a25f8a2bf06e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002502"
---
# <a name="sprefreshlogshippingmonitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa stored procedure aggiorna le tabelle di monitoraggio remote in base alle informazioni più recenti recuperate da un server primario o secondario specificato per l'agente di log shipping specificato. La procedura viene richiamata dal server primario o secondario.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @agent_id = ] 'agent_id'` ID primario per il backup o all'ID secondario per la copia o ripristino. *agent_id* viene **uniqueidentifier** e non può essere NULL.  
  
`[ @agent_type = ] 'agent_type'` Tipo di processo per il log shipping.  
  
 0 = backup.  
  
 1 = copia.  
  
 2 = ripristino.  
  
 *agent_type* viene **tinyint** e non può essere NULL.  
  
`[ @database = ] 'database'` Il database primario o secondario utilizzato dalla registrazione dagli agenti di backup o ripristino.  
  
`[ @mode ] n` Specifica se aggiornare i dati di monitoraggio oppure eliminarli. Il tipo di dati *m* è tinyint e i valori supportati sono:  
  
 1 = aggiornamento (valore predefinito)  
  
 2 = delete  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 No.  
  
## <a name="remarks"></a>Note  
 **sp_refresh_log_shipping_monitor** consente di aggiornare il **log_shipping_monitor_primary**, **log_shipping_monitor_secondary**, **log_shipping_monitor_history_detail** , e **log_shipping_monitor_error_detail** tabelle con le informazioni sulla sessione che non è già stata trasferita. Ciò consente di sincronizzare il server di monitoraggio con il server primario o secondario nel caso in cui il server di monitoraggio non sia più in sincronia. Consente inoltre di eliminare le informazioni di monitoraggio nel server di monitoraggio, se necessario.  
  
 **sp_refresh_log_shipping_monitor** deve essere eseguita la **master** database nel server primario o secondario.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server può eseguire questa procedura.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
