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
ms.openlocfilehash: 278af2ca1bd6abdb84cdf2371628c6b95662e46e
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962415"
---
# <a name="sp_addsubscriber-transact-sql"></a>sp_addsubscriber (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Aggiunge in un server di pubblicazione un nuovo Sottoscrittore per abilitarlo alla ricezione di pubblicazioni. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione per pubblicazioni snapshot e transazionali. Per pubblicazioni di tipo merge che utilizzano un server di distribuzione remoto, viene eseguita nel server di distribuzione.  
  
> [!IMPORTANT]  
>  Questa stored procedure è deprecata. Non è più necessario registrare in modo esplicito un Sottoscrittore nel server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @subscriber = ] 'subscriber'` è il nome del server da aggiungere come Sottoscrittore valido per le pubblicazioni in questo server. *Subscriber* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @type = ] type` è il tipo di Sottoscrittore. il *tipo* è **tinyint**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**0** (predefinito)|Sottoscrittore [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**1**|Server dell'origine dei dati ODBC.|  
|**2**|Database [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet|  
|**3**|Provider OLE DB|  
  
`[ @login = ] 'login'` è l'ID di accesso per l'autenticazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* è di tipo **sysname** e il valore predefinito è NULL.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @password = ] 'password'` è la password per l'autenticazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *password* è di **tipo nvarchar (524)** e il valore predefinito è null.  
  
> [!IMPORTANT]  
>  Non usare una password vuota. Usare una password complessa.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @commit_batch_size = ] commit_batch_size` questo parametro è stato deprecato e viene mantenuto per compatibilità con le versioni precedenti degli script.  
  
> [!NOTE]  
>  Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @status_batch_size = ] status_batch_size` questo parametro è stato deprecato e viene mantenuto per compatibilità con le versioni precedenti degli script.  
  
> [!NOTE]  
>  Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @flush_frequency = ] flush_frequency` questo parametro è stato deprecato e viene mantenuto per compatibilità con le versioni precedenti degli script.  
  
> [!NOTE]  
>  Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @frequency_type = ] frequency_type` è la frequenza con cui pianificare l'agente di replica. *frequency_type* è di **tipo int**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
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
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @frequency_interval = ] frequency_interval` è il valore applicato alla frequenza impostata da *frequency_type*. *frequency_interval* è di **tipo int**e il valore predefinito è 1.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` è la data dell'agente di replica. Questo parametro viene usato quando *frequency_type* è impostato su **32** (mensile relativo). *frequency_relative_interval* è di **tipo int**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**1** (impostazione predefinita)|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` è il fattore di ricorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* è di **tipo int**e il valore predefinito è **0**.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @frequency_subday = ] frequency_subday` la frequenza di ripianificazione durante il periodo definito. *frequency_subday* è di **tipo int**. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4** (impostazione predefinita)|Minuto|  
|**8**|Ora|  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` è l'intervallo per *frequency_subday*. *frequency_subday_interval* è di **tipo int**e il valore predefinito è **5**.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` è l'ora del giorno in cui l'agente di replica viene pianificato per la prima volta, formattato come HHMMSS. *active_start_time_of_day* è di **tipo int**e il valore predefinito è **0**.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` è l'ora del giorno in cui l'agente di replica smette di essere pianificato, formattato come HHMMSS. *active_end_time_of_day*è di **tipo int**e il valore predefinito è 235959, che indica le 11:59:59. nel formato 24 ore.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @active_start_date = ] active_start_date` è la data in cui l'agente di replica viene pianificato per la prima volta, formattato come AAAAMMGG. *active_start_date* è di **tipo int**e il valore predefinito è 0.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @active_end_date = ] active_end_date` è la data in cui viene arrestata la pianificazione dell'agente di replica, nel formato AAAAMMGG. *active_end_date* è di **tipo int**e il valore predefinito è 99991231, ovvero il 31 dicembre 9999.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @description = ] 'description'` è una descrizione testuale del Sottoscrittore. *Description* è di **tipo nvarchar (255)** e il valore predefinito è null.  
  
`[ @security_mode = ] security_mode` è la modalità di sicurezza implementata. *security_mode* è di **tipo int**e il valore predefinito è 1. **0** specifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione. **1** specifica l'autenticazione di Windows.  
  
> [!NOTE]  
>  Questo parametro è deprecato ed è ancora disponibile per compatibilità con gli script di versioni precedenti. La proprietà viene ora specificata per ogni sottoscrizione durante l'esecuzione di [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Se si specifica un valore, questo verrà utilizzato come valore predefinito per la creazione di sottoscrizioni nel Sottoscrittore e verrà restituito un messaggio di avviso.  
  
`[ @encrypted_password = ] encrypted_password` questo parametro è stato deprecato e viene fornito per la compatibilità con le versioni precedenti *encrypted_password* a qualsiasi valore, ma **0** genera un errore.  
  
`[ @publisher = ] 'publisher'` specifica un server di pubblicazione non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* è di **tipo sysname**e il valore predefinito è null.  
  
> [!NOTE]  
>  il *Server* di pubblicazione non deve essere utilizzato per la pubblicazione da un server di pubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_addsubscriber** viene utilizzata per la replica snapshot, la replica transazionale e la replica di tipo merge.  
  
 **sp_addsubscriber** non è obbligatorio se il Sottoscrittore avrà solo sottoscrizioni anonime per le pubblicazioni di tipo merge.  
  
 **sp_addsubscriber** scrive nella tabella [MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md) del database di **distribuzione** .  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_addsubscriber**.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Creare una sottoscrizione pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
