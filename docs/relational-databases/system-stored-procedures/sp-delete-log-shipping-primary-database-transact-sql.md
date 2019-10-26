---
title: sp_delete_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aff19eabc5738e986fca1bf13f85130daead3217
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909871"
---
# <a name="sp_delete_log_shipping_primary_database-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Questa stored procedure rimuove il log shipping del database primario, compreso il processo di backup, e la cronologia locale e remota. Usare questa stored procedure solo dopo aver rimosso i database secondari con **sp_delete_log_shipping_primary_secondary**.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @database = ] 'database'` è il nome del database log shipping primario. il *database* è di **tipo sysname**e non prevede alcun valore predefinito e non può essere null.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuna.  
  
## <a name="remarks"></a>Remarks  
 **sp_delete_log_shipping_primary_database** deve essere eseguito dal database **Master** nel server primario. Questa stored procedure esegue le operazioni seguenti:  
  
1.  Elimina il processo di backup per il database primario specificato.  
  
2.  Rimuove il record di monitoraggio locale in **log_shipping_monitor_primary** nel server primario.  
  
3.  Rimuove le voci corrispondenti in **log_shipping_monitor_history_detail** e **log_shipping_monitor_error_detail**.  
  
4.  Se il server di monitoraggio è diverso dal server primario, rimuove il record di monitoraggio in **log_shipping_monitor_primary** nel server di monitoraggio.  
  
5.  Rimuove le voci corrispondenti in **log_shipping_monitor_history_detail** e **log_shipping_monitor_error_detail** sul server di monitoraggio.  
  
6.  Rimuove la voce in **log_shipping_primary_databases** per il database primario.  
  
7.  Chiama **sp_delete_log_shipping_alert_job** sul server di monitoraggio.  

## <a name="permissions"></a>Permissions  
 Questa procedura può essere eseguita solo dai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Questo esempio illustra l'uso di **sp_delete_log_shipping_primary_database** per eliminare il database primario **AdventureWorks2012**.  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
