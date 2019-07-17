---
title: sp_changesubscriber (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
author: stevestein
ms.author: sstein
ms.openlocfilehash: d18282229ec2f481aaab91aff8273bd9b3e72a34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090057"
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di modificare le opzioni di un Sottoscrittore. Verranno aggiornate tutte le attività di distribuzione per i Sottoscrittori di questo server di pubblicazione. Questa stored procedure scrive per la **MSsubscriber_info** tabella nel database di distribuzione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore in cui si desidera modificare le opzioni. *Sottoscrittore* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @type = ] type` È il tipo di sottoscrittore. *tipo di* viene **tinyint**, con un valore predefinito è NULL. **0** indica una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittore. **1** specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un altro server di origine dati ODBC sottoscrittore.  
  
`[ @login = ] 'login'` È il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID di accesso di autenticazione. *login* è di tipo **sysname** e il valore predefinito è NULL.  
  
`[ @password = ] 'password'` È il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] password per l'autenticazione. *la password* viene **sysname**, il valore predefinito è **%** . **%** indica che nessuna modifica per la proprietà della password.  
  
`[ @commit_batch_size = ] commit_batch_size` Supportato solo per la compatibilità.  
  
`[ @status_batch_size = ] status_batch_size` Supportato solo per la compatibilità.  
  
`[ @flush_frequency = ] flush_frequency` Supportato solo per la compatibilità.  
  
`[ @frequency_type = ] frequency_type` È la frequenza con cui pianificare l'attività di distribuzione. *frequency_type* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Su richiesta|  
|**4**|Ogni giorno|  
|**8**|Settimanale|  
|**16**|Mensile|  
|**32**|Mensile relativa|  
|**64**|Avvio automatico|  
|**128**|Periodica|  
  
`[ @frequency_interval = ] frequency_interval` È l'intervallo *frequency_type*. *frequency_interval* viene **int**, con un valore predefinito è NULL.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` È la data dell'attività di distribuzione. Questo parametro viene utilizzato quando *frequency_type* è impostata su **32** (frequenza mensile relativa). *frequency_relative_interval* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` È la frequenza dell'attività di distribuzione deve durante il periodo definito *frequency_type*. *frequency_recurrence_factor* viene **int**, con un valore predefinito è NULL.  
  
`[ @frequency_subday = ] frequency_subday` È la frequenza di ripianificazione durante il periodo definito. *frequency_subday* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4**|Minuto|  
|**8**|Ora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` È l'intervallo *frequence_subday*. *frequency_subday_interval* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` È l'ora del giorno quando l'attività di distribuzione è primo pianificata, nel formato HHMMSS. *active_start_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` L'ora del giorno dell'ultima attività di distribuzione è pianificata, nel formato HHMMSS. *active_end_time_of_day*viene **int**, con un valore predefinito è NULL.  
  
`[ @active_start_date = ] active_start_date` È la data della prima attività di distribuzione pianificata, nel formato YYYYMMDD. *active_start_date* viene **int**, con un valore predefinito è NULL.  
  
`[ @active_end_date = ] active_end_date` Data dell'ultima attività di distribuzione è pianificata, nel formato aaaammgg. *active_end_date*viene **int**, con un valore predefinito è NULL.  
  
`[ @description = ] 'description'` È una descrizione facoltativa in formato testo. *Descrizione* viene **nvarchar(255**, con un valore predefinito è NULL.  
  
`[ @security_mode = ] security_mode` È la modalità di sicurezza implementata. *security_mode* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticazione|  
|**1**|Autenticazione di Windows|  
  
`[ @publisher = ] 'publisher'` Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzata quando si modificano le proprietà degli articoli in una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changesubscriber** viene utilizzata in tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_changesubscriber**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
