---
title: sp_changesubscriber_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber_schedule
- sp_changesubscriber_schedule_TSQL
helpviewer_keywords:
- sp_changesubscriber_schedule
ms.assetid: ff84e8e2-d496-482c-b23e-38a6626596e6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 83edeb0c94276e10528b05bc5a1cd8d9474d07aa
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127911"
---
# <a name="spchangesubscriberschedule-transact-sql"></a>sp_changesubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica la pianificazione dell'agente di distribuzione o di merge per un Sottoscrittore. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changesubscriber_schedule [ @subscriber = ] 'subscriber', [ @agent_type = ] type  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@subscriber=**] **'**_sottoscrittore_**'**  
 Nome del Sottoscrittore. *Sottoscrittore* viene **sysname**. Il nome del Sottoscrittore deve essere univoco all'interno del database, non deve essere già esistente e non può essere NULL.  
  
 [  **@agent_type=**] *tipo*  
 Tipo di agente. *tipo di* viene **smallint**, il valore predefinito è **0**. **0** indica un agente di distribuzione. **1** indica un agente di Merge.  
  
 [  **@frequency_type=**] *frequency_type*  
 Frequenza di pianificazione dell'attività di distribuzione. *frequency_type* viene **int**, il valore predefinito è **64**. Sono disponibili 10 colonne di pianificazione.  
  
 [  **@frequency_interval=**] *frequency_interval*  
 Valore applicato alla frequenza impostata *frequency_type*. *frequency_interval* viene **int**, il valore predefinito è **1**.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Data dell'attività di distribuzione. *frequency_relative_interval* viene **int**, il valore predefinito è **1**.  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, il valore predefinito è **0**.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Frequenza di ripianificazione in minuti durante il periodo definito. *frequency_subday* viene **int**, il valore predefinito è **4**.  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, il valore predefinito è **5**.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Ora del giorno della prima esecuzione pianificata dell'attività di distribuzione. *active_start_time_of_day* viene **int**, il valore predefinito è **0**.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Ora del giorno dell'ultima esecuzione pianificata dell'attività di distribuzione. *active_end_time_of_day* viene **int**, il valore predefinito è **235959**, ovvero 59: 11:59 P.M. nel formato 24 ore.  
  
 [  **@active_start_date=**] *active_start_date*  
 Data della prima esecuzione pianificata per l'attività di distribuzione, nel formato AAAAMMGG. *active_start_date* viene **int**, il valore predefinito è **0**.  
  
 [  **@active_end_date=**] *active_end_date*  
 Data dell'ultima esecuzione pianificata dell'attività di distribuzione, nel formato AAAAMMGG. *active_end_date* viene **int**, il valore predefinito è **99991231**, che corrisponde al 31 dicembre 9999.  
  
 [ **@publisher**=] **'**_editore_**'**  
 Specifica un non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzata quando si modificano le proprietà degli articoli in una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changesubscriber_schedule** viene utilizzata in tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_changesubscriber_schedule**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addsubscriber_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-schedule-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
