---
title: sp_addsubscriber (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ad13c4904270d3162dac8791b7724533e8da6656
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211750"
---
# <a name="spaddsubscriber-transact-sql"></a>sp_addsubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge in un server di pubblicazione un nuovo Sottoscrittore per abilitarlo alla ricezione di pubblicazioni. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione per pubblicazioni snapshot e transazionali. Per pubblicazioni di tipo merge che utilizzano un server di distribuzione remoto, viene eseguita nel server di distribuzione.  
  
> [!IMPORTANT]  
>  Questa stored procedure è deprecata. Non è più necessario registrare in modo esplicito un Sottoscrittore nel server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addsubscriber [ @subscriber = ] 'subscriber'  
    [ , [ @type = ] type ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @commit_batch_size = ] commit_batch_size ]  
    [ , [ @status_batch_size = ] status_batch_size ]  
    [ , [ @flush_frequency = ] flush_frequency ]  
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
    [ , [ @description = ] 'description' ]  
    [ , [ @security_mode = ] security_mode ]  
    [ , [ @encrypted_password = ] encrypted_password ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@subscriber=**] **'***sottoscrittore***'**  
 Nome del server da aggiungere come Sottoscrittore valido delle pubblicazioni in questo server. *Sottoscrittore* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@type=**] *tipo*  
 Tipo di Sottoscrittore. *tipo di* viene **tinyint**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0** (predefinito)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sottoscrittore|  
|**1**|Server dell'origine dei dati ODBC.|  
|**2**|Database [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet|  
|**3**|Provider OLE DB|  
  
 [  **@login=**] **'***account di accesso***'**  
 ID dell'account di accesso per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* è di tipo **sysname** e il valore predefinito è NULL.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@password=**] **'***password***'**  
 Password utilizzata per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *la password* viene **nvarchar(524**, con un valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  Non usare una password vuota. Usare una password complessa.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti.  
  
> [!NOTE]  
>  Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@status_batch_size=**] *status_batch_size*  
 Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti.  
  
> [!NOTE]  
>  Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@flush_frequency=**] *flush_frequency*  
 Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti.  
  
> [!NOTE]  
>  Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@frequency_type=**] *frequency_type*  
 Frequenza per l'esecuzione pianificata dell'agente di replica. *frequency_type* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Su richiesta|  
|**4**|Ogni giorno|  
|**8**|Settimanale|  
|**16**|Mensile|  
|**32**|Mensile relativa|  
|**64** (impostazione predefinita)|Avvio automatico|  
|**128**|Periodica|  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [**@frequency_interval=** ] *frequency_interval*  
 Valore applicato alla frequenza impostata *frequency_type*. *frequency_interval* viene **int**, con un valore predefinito è 1.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Data dell'agente di replica. Questo parametro viene utilizzato quando *frequency_type* è impostata su **32** (frequenza mensile relativa). *frequency_relative_interval* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1** (impostazione predefinita)|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, il valore predefinito è **0**.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Frequenza di ripianificazione durante il periodo definito. *frequency_subday* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4** (impostazione predefinita)|Minuto|  
|**8**|Ora|  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 È l'intervallo *frequency_subday*. *frequency_subday_interval* viene **int**, il valore predefinito è **5**.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Ora del giorno della prima esecuzione pianificata dell'agente di replica, nel formato HHMMSS. *active_start_time_of_day* viene **int**, il valore predefinito è **0**.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Ora del giorno dell'ultima esecuzione pianificata dell'agente di replica, nel formato HHMMSS. *active_end_time_of_day*viene **int**, con un valore predefinito è 235959, che significa 59: 11:59 P.M. nel formato 24 ore.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@active_start_date=**] *active_start_date*  
 Data della prima esecuzione pianificata dell'agente di replica, nel formato AAAAMMGG. *active_start_date* viene **int**, con un valore predefinito è 0.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@active_end_date=**] *active_end_date*  
 Data dell'ultima esecuzione pianificata dell'agente di replica, nel formato AAAAMMGG. *active_end_date* viene **int**, con un valore predefinito è 99991231, che corrisponde al 31 dicembre 9999.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@description=**] **'***descrizione***'**  
 Descrizione del Sottoscrittore. *Descrizione* viene **nvarchar(255**, con un valore predefinito è NULL.  
  
 [  **@security_mode=**] *security_mode*  
 Modalità di sicurezza implementata. *security_mode* viene **int**, con un valore predefinito è 1. **0** specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. **1** specifica l'autenticazione di Windows.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione quando si esegue [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
 [  **@encrypted_password=**] *encrypted_password*  
 Questo parametro è deprecato ed è disponibile per motivi di compatibilità solo l'impostazione *encrypted_password* su un valore qualsiasi, ma **0** comporterà un errore.  
  
 [ **@publisher**=] **'***publisher***'**  
 Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere usata durante la pubblicazione da un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addsubscriber** viene utilizzata nella replica snapshot, la replica transazionale e di tipo merge.  
  
 **sp_addsubscriber** non è obbligatorio quando il sottoscrittore avrà solo le sottoscrizioni anonime di pubblicazioni di tipo merge.  
  
 **sp_addsubscriber** scrive il [MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md) nella tabella di **distribuzione** database.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_addsubscriber**.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
