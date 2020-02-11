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
ms.openlocfilehash: 38b653dcb51f428692401fb87609187a82449393
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771494"
---
# <a name="sp_helpsubscriberinfo-transact-sql"></a>sp_helpsubscriberinfo (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Visualizza informazioni su un Sottoscrittore. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpsubscriberinfo [ [ @subscriber =] 'subscriber']  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @subscriber = ] 'subscriber'`Nome del Sottoscrittore. *Subscriber* è di **%** **tipo sysname**e il valore predefinito è, che restituisce tutte le informazioni.  
  
`[ @publisher = ] 'publisher'`Nome del server di pubblicazione. *Publisher* è di **tipo sysname**e il valore predefinito è il nome del server corrente.  
  
> [!NOTE]  
>  il *server di pubblicazione* non deve essere specificato, tranne quando si tratta di un server di pubblicazione Oracle.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**subscriber**|**sysname**|Nome del Sottoscrittore.|  
|**tipo**|**tinyint**|Tipo di Sottoscrittore:<br /><br /> **** =  0[!INCLUDE[msCoName](../../includes/msconame-md.md)] database 1 = origine dati ODBC **** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**accesso**|**sysname**|ID dell'account di accesso per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**sysname**|Password per l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**commit_batch_size**|**int**|Non supportato.|  
|**status_batch_size**|**int**|Non supportato.|  
|**flush_frequency**|**int**|Non supportato.|  
|**frequency_type**|**int**|Frequenza di esecuzione dell'agente di distribuzione:<br /><br /> **1** = una volta<br /><br /> **2** = su richiesta<br /><br /> **4** = giornaliero<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativo<br /><br /> **64** = avvio automatico<br /><br /> **128** = ricorrente|  
|**frequency_interval**|**int**|Valore applicato alla frequenza impostata da *frequency_type*.|  
|**frequency_relative_interval**|**int**|Data di agente di distribuzione utilizzata quando *frequency_type* è impostato su **32** (mensile relativo):<br /><br /> **1** = prima<br /><br /> **2** = secondo<br /><br /> **4** = terzo<br /><br /> **8** = quarto<br /><br /> **16** = Ultima|  
|**frequency_recurrence_factor**|**int**|Fattore di occorrenza utilizzato da *frequency_type*.|  
|**frequency_subday**|**int**|Frequenza di ripianificazione durante il periodo definito:<br /><br /> **1** = una volta<br /><br /> **2** = secondo<br /><br /> **4** = minuto<br /><br /> **8** = ora|  
|**frequency_subday_interval**|**int**|Intervallo per *frequency_subday*.|  
|**active_start_time_of_day**|**int**|Ora del giorno della prima esecuzione pianificata dell'agente di distribuzione nel formato HHMMSS.|  
|**active_end_time_of_day**|**int**|Ora del giorno in cui viene arrestata la pianificazione dell'agente di distribuzione nel formato HHMMSS.|  
|**active_start_date**|**int**|Data della prima esecuzione pianificata dell'agente di distribuzione nel formato AAAAMMGG.|  
|**active_end_date**|**int**|Data in cui viene arrestata la pianificazione dell'agente di distribuzione nel formato AAAAMMGG.|  
|**retryattempt**|**int**|Non supportato.|  
|**retrydelay**|**int**|Non supportato.|  
|**Descrizione**|**nvarchar(255)**|Descrizione in formato testo del Sottoscrittore.|  
|**security_mode**|**int**|Modalità di sicurezza implementata:<br /><br /> **autenticazione 0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **** =  1[!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticazione di Windows|  
|**frequency_type2**|**int**|Frequenza di esecuzione dell'agente di merge:<br /><br /> **1** = una volta<br /><br /> **2** = su richiesta<br /><br /> **4** = giornaliero<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativo<br /><br /> **64** = avvio automatico<br /><br /> **128** = ricorrente|  
|**frequency_interval2**|**int**|Valore applicato alla frequenza impostata da *frequency_type*.|  
|**frequency_relative_interval2**|**int**|Data di agente di merge utilizzata quando *frequency_type* è impostato su 32 (mensile relativo):<br /><br /> **1** = prima<br /><br /> **2** = secondo<br /><br /> **4** = terzo<br /><br /> **8** = quarto<br /><br /> **16** = Ultima|  
|**frequency_recurrence_factor2**|**int**|Fattore di ricorrenza utilizzato da *frequency_type * *.*|  
|**frequency_subday2**|**int**|Frequenza di ripianificazione durante il periodo definito:<br /><br /> **1** = una volta<br /><br /> **2** = secondo<br /><br /> **4** = minuto<br /><br /> **8** = ora|  
|**frequency_subday_interval2**|**int**|Intervallo per *frequency_subday*.|  
|**active_start_time_of_day2**|**int**|Ora del giorno della prima esecuzione pianificata dell'agente di merge nel formato HHMMSS.|  
|**active_end_time_of_day2**|**int**|Ora del giorno in cui viene arrestata la pianificazione dell'agente di merge nel formato HHMMSS|  
|**active_start_date2**|**int**|Data della prima pianificazione dell'agente di merge nel formato AAAAMMGG.|  
|**active_end_date2**|**int**|Data in cui viene arrestata la pianificazione dell'agente di merge nel formato AAAAMMGG.|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_helpsubscriberinfo** viene utilizzata per la replica snapshot, la replica transazionale e la replica di tipo merge.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** , del ruolo predefinito del database **db_owner** o dell'elenco di accesso alla pubblicazione possono eseguire **sp_helpsubscriberinfo**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_adddistpublisher &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addpullsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_changesubscriber &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
