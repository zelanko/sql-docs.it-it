---
title: sp_change_log_shipping_secondary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 136771c5bf691155b4547963fa2b6bd035f3f039
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62994230"
---
# <a name="spchangelogshippingsecondarydatabase-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica le impostazioni del database secondario.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @restore_delay = ] 'restore_delay'` La quantità di tempo, espresso in minuti, il server secondario deve attendere prima del ripristino di un file di backup specificato. *restore_delay* viene **int** e non può essere NULL. Il valore predefinito è 0.  
  
`[ @restore_all = ] 'restore_all'` Se impostato su 1, il server secondario Ripristina tutti i backup del log delle transazioni disponibili quando viene eseguito il processo di ripristino. In caso contrario, l'operazione viene arrestata dopo il ripristino di un file. *restore_all* viene **bit** e non può essere NULL.  
  
`[ @restore_mode = ] 'restore_mode'` La modalità di ripristino per il database secondario.  
  
 0 = ripristino log con NORECOVERY.  
  
 1 = Ripristina log con STANDBY.  
  
 *ripristinare* viene **bit** e non può essere NULL.  
  
`[ @disconnect_users = ] 'disconnect_users'` Se impostato su 1, gli utenti è disconnesso dal database secondario quando viene eseguita un'operazione di ripristino. Predefinito = 0. *disconnect_users* viene **bit** e non può essere NULL.  
  
`[ @block_size = ] 'block_size'` La dimensione, espressa in byte, che viene usata come dimensione del blocco per il dispositivo di backup. *block_size* viene **int** con valore predefinito è-1.  
  
`[ @buffer_count = ] 'buffer_count'` Numero totale di buffer utilizzati dall'operazione di backup o ripristino. *buffer_count* viene **int** con valore predefinito è-1.  
  
`[ @max_transfer_size = ] 'max_transfer_size'` Le dimensioni, in byte, della massima richiesta di input o output eseguita da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel dispositivo di backup. *max_transfersize* viene **int** e può essere NULL.  
  
`[ @restore_threshold = ] 'restore_threshold'` Il numero di minuti consentiti tra operazioni di ripristino prima che venga generato un avviso. *restore_threshold* viene **int** e non può essere NULL.  
  
`[ @threshold_alert = ] 'threshold_alert'` È l'avviso da generare quando viene superata la soglia di ripristino. *threshold_alert* viene **int**, predefinito 14420.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` Specifica se un avviso verrà generato quando *restore_threshold*viene superato. 1 = abilitato; 0 = disabilitato. *threshold_alert_enabled* viene **bit** e non può essere NULL.  
  
`[ @history_retention_period = ] 'history_retention_period'` È il periodo di tempo in minuti in cui verrà mantenuta la cronologia. *history_retention_period* viene **int**. Se non viene specificato, verrà utilizzato un valore 1440.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 **sp_change_log_shipping_secondary_database** deve essere eseguita la **master** database nel server secondario. Questa stored procedure esegue le operazioni seguenti:  
  
1.  Modifica le impostazioni nel **log_shipping_secondary_database** registra in base alle esigenze.  
  
2.  Il record di monitoraggio locale viene modificato **log_shipping_monitor_secondary** nel server secondario utilizzando gli argomenti specificati, se necessario.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server può eseguire questa procedura.  
  
## <a name="examples"></a>Esempi  
 In questo esempio viene illustrato l'utilizzo **sp_change_log_shipping_secondary_database** per aggiornare i parametri del database secondario per il database **LogShipAdventureWorks**.  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
