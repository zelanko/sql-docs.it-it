---
title: sp_helpsubscriberinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscriberinfo
- sp_helpsubscriberinfo_TSQL
helpviewer_keywords:
- sp_helpsubscriberinfo
ms.assetid: fbabe1ec-57cf-425c-bae7-af7f5d3198fd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 18a1de1e3b7dc1f312094a9023e0af9df014214b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526373"
---
# <a name="sphelpsubscriberinfo-transact-sql"></a>sp_helpsubscriberinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza informazioni su un Sottoscrittore. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpsubscriberinfo [ [ @subscriber =] 'subscriber']  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* viene **sysname**, il valore predefinito è **%**, che restituisce tutte le informazioni.  
  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *server di pubblicazione* viene **sysname**e il valore predefinito è il nome del server corrente.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere specificato, tranne nel caso un server di pubblicazione Oracle.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**subscriber**|**sysname**|Nome del Sottoscrittore.|  
|**type**|**tinyint**|Tipo di Sottoscrittore:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database **1** = origine dati ODBC|  
|**login**|**sysname**|ID dell'account di accesso per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**sysname**|Password per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**commit_batch_size**|**int**|Non supportato.|  
|**status_batch_size**|**int**|Non supportato.|  
|**flush_frequency**|**int**|Non supportato.|  
|**frequency_type**|**int**|Frequenza di esecuzione dell'agente di distribuzione:<br /><br /> **1** = una sola volta<br /><br /> **2** = su richiesta<br /><br /> **4** = giornaliera<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativa<br /><br /> **64** = avvio automatico<br /><br /> **128** = Recurring|  
|**frequency_interval**|**int**|Valore applicato alla frequenza impostata da *frequency_type*.|  
|**frequency_relative_interval**|**int**|Data dell'agente di distribuzione usata quando *frequency_type* è impostata su **32** (frequenza mensile relativa):<br /><br /> **1** = prima<br /><br /> **2** = Second<br /><br /> **4** = terza<br /><br /> **8** = quarta<br /><br /> **16** = ultima|  
|**frequency_recurrence_factor**|**int**|Fattore di occorrenza utilizzato da *frequency_type*.|  
|**frequency_subday**|**int**|Frequenza di ripianificazione durante il periodo definito:<br /><br /> **1** = Once<br /><br /> **2** = Second<br /><br /> **4** = minuti<br /><br /> **8** = ore|  
|**frequency_subday_interval**|**int**|Intervallo per la *frequency_subday*.|  
|**active_start_time_of_day**|**int**|Ora del giorno della prima esecuzione pianificata dell'agente di distribuzione nel formato HHMMSS.|  
|**active_end_time_of_day**|**int**|Ora del giorno in cui viene arrestata la pianificazione dell'agente di distribuzione nel formato HHMMSS.|  
|**active_start_date**|**int**|Data della prima esecuzione pianificata dell'agente di distribuzione nel formato AAAAMMGG.|  
|**active_end_date**|**int**|Data in cui viene arrestata la pianificazione dell'agente di distribuzione nel formato AAAAMMGG.|  
|**retryattempt**|**int**|Non supportato.|  
|**retrydelay**|**int**|Non supportato.|  
|**description**|**nvarchar(255)**|Descrizione in formato testo del Sottoscrittore.|  
|**security_mode**|**int**|Modalità di sicurezza implementata:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticazione<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] l'autenticazione di Windows|  
|**frequency_type2**|**int**|Frequenza di esecuzione dell'agente di merge:<br /><br /> **1** = una sola volta<br /><br /> **2** = su richiesta<br /><br /> **4** = giornaliera<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativa<br /><br /> **64** = avvio automatico<br /><br /> **128** = Recurring|  
|**frequency_interval2**|**int**|Valore applicato alla frequenza impostata da *frequency_type*.|  
|**frequency_relative_interval2**|**int**|Data dell'agente di Merge utilizzato quando *frequency_type* è impostato su 32 (mensile relativa):<br /><br /> **1** = prima<br /><br /> **2** = Second<br /><br /> **4** = terza<br /><br /> **8** = quarta<br /><br /> **16** = ultima|  
|**frequency_recurrence_factor2**|**int**|Fattore di occorrenza utilizzato da *frequency_type * *.*|  
|**frequency_subday2**|**int**|Frequenza di ripianificazione durante il periodo definito:<br /><br /> **1** = Once<br /><br /> **2** = Second<br /><br /> **4** = minuti<br /><br /> **8** = ore|  
|**frequency_subday_interval2**|**int**|Intervallo per la *frequency_subday*.|  
|**active_start_time_of_day2**|**int**|Ora del giorno della prima esecuzione pianificata dell'agente di merge nel formato HHMMSS.|  
|**active_end_time_of_day2**|**int**|Ora del giorno in cui viene arrestata la pianificazione dell'agente di merge nel formato HHMMSS|  
|**active_start_date2**|**int**|Data della prima pianificazione dell'agente di merge nel formato AAAAMMGG.|  
|**active_end_date2**|**int**|Data in cui viene arrestata la pianificazione dell'agente di merge nel formato AAAAMMGG.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpsubscriberinfo** viene utilizzata nella replica snapshot, la replica transazionale e di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database, o elenco di accesso alla pubblicazione per la pubblicazione può eseguire **sp_helpsubscriberinfo**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
