---
title: MSsubscriber_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_schedule
- MSsubscriber_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_schedule system table
ms.assetid: ff428306-0ef4-49a3-b536-07ccdf6e2196
author: stevestein
ms.author: sstein
ms.openlocfilehash: 04ad122f6fc999aa285513d41e71bfc347dbfb82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139804"
---
# <a name="mssubscriberschedule-transact-sql"></a>MSsubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSsubscriber_schedule** tabella contiene l'unione predefinito e le pianificazioni della sincronizzazione transazionale per ogni coppia server di pubblicazione/sottoscrittore. Questa tabella è archiviata nel database di distribuzione.  
  
> [!NOTE]
>  Questa tabella di sistema è stata deprecata e viene mantenuta per supportare le versioni precedenti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**subscriber**|**sysname**|Nome del Sottoscrittore.|  
|**agent_type**|**smallint**|Tipo di agente:<br /><br /> 0 = agente di distribuzione<br /><br /> 1 = agente di merge|  
|**frequency_type**|**int**|Frequenza di pianificazione dell'agente di distribuzione:<br /><br /> **1** = una sola volta.<br /><br /> **2** = su richiesta.<br /><br /> **4** = giornaliera.<br /><br /> **8** = settimanale.<br /><br /> **16** = mensile.<br /><br /> **32** = mensile relativa.<br /><br /> **64** = avvio automatico.<br /><br /> **128** = periodica.|  
|**frequency_interval**|**int**|Il valore da applicare alla frequenza impostata da **frequency_type**.|  
|**frequency_relative_interval**|**int**|Data dell'agente di distribuzione:<br /><br /> **1** = first.<br /><br /> **2** = secondo.<br /><br /> **4** = terzo.<br /><br /> **8** = quarto.<br /><br /> **16** = ultima.|  
|**frequency_recurrence_factor**|**int**|Fattore di occorrenza utilizzato da **frequency_type**.|  
|**frequency_subday**|**int**|Frequenza di ripianificazione durante il periodo definito:<br /><br /> **1** = una sola volta.<br /><br /> **2** = secondo.<br /><br /> **4** = minuto.<br /><br /> **8** = ora.|  
|**frequency_subday_interval**|**int**|L'intervallo per la **frequency_subday**.|  
|**active_start_time_of_day**|**int**|Ora della prima pianificazione dell'agente di distribuzione, in formato HHMMSS.|  
|**active_end_time_of_day**|**int**|Ora della fine della pianificazione dell'agente di distribuzione, in formato HHMMSS|  
|**active_start_date**|**int**|Data della prima pianificazione dell'agente di distribuzione, in formato AAAAMMGG.|  
|**active_end_date**|**int**|Data della fine della pianificazione dell'agente di distribuzione, in formato AAAAMMGG.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
