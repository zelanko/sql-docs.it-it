---
title: dbo.sysalerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7bad6fbd9229547318a060f08eeb102b21cda9bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470889"
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni avviso. Un avviso è un messaggio inviato in risposta a un evento con cui è possibile inoltrare messaggi all'esterno dell'ambiente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite posta elettronica o cercapersone. Un avviso può generare inoltre un'attività.  Questa tabella è archiviata nel **msdb** database.
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID dell'avviso.|  
|**name**|**sysname**|Nome dell'avviso.|  
|**event_source**|**nvarchar(100)**|Origine dell'evento: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**event_category_id**|**int**|Riservato per utilizzi futuri.|  
|**event_id**|**int**|Riservato per utilizzi futuri.|  
|**message_id**|**int**|Definito dall'utente ID messaggio o un riferimento a **sysmessages** messaggio che attiva l'avviso.|  
|**severity**|**int**|Livello di gravità che attiva l'avviso.|  
|**enabled**|**tinyint**|Stato dell'avviso:<br /><br /> **0** = disabilitata.<br /><br /> **1** = abilitato.|  
|**delay_between_responses**|**int**|Intervallo espresso in secondi tra due notifiche dell'avviso.|  
|**last_occurrence_date**|**int**|Data dell'ultima occorrenza dell'avviso.|  
|**last_occurrence_time**|**int**|Ora dell'ultima occorrenza dell'avviso.|  
|**last_response_date**|**int**|Data dell'ultima notifica dell'avviso.|  
|**last_response_time**|**int**|Ora dell'ultima notifica dell'avviso.|  
|**notification_message**|**nvarchar(512)**|Informazioni aggiuntive inviate con l'avviso.|  
|**include_event_description**|**tinyint**|Maschera di bit che indica se la descrizione dell'evento viene inviata tramite posta elettronica, cercapersone o Net send. Vedere grafico riportato di seguito per i valori.|  
|**database_name**|**nvarchar(512)**|Database in cui è necessario che si verifichi l'avviso affinché venga attivato.|  
|**event_description_keyword**|**nvarchar(100)**|Modello a cui deve corrispondere l'errore affinché venga attivato l'avviso.|  
|**occurrence_count**|**int**|Numero di occorrenze dell'avviso.|  
|**count_reset_date**|**int**|Numero di giorni (date) verrà reimpostato su **0**.|  
|**count_reset_time**|**int**|Ora del numero di giorni reimposteranno **0**.|  
|**job_id**|**uniqueidentifier**|ID dell'attività eseguita quando si verifica l'avviso.|  
|**has_notification**|**int**|Numero di operatori che ricevono una notifica tramite posta elettronica quando si verifica un avviso.|  
|**flags**|**int**|Riservato.|  
|**performance_condition**|**nvarchar(512)**|Riservato.|  
|**category_id**|**int**|Riservato.|  
  
 ## <a name="remarks"></a>Note

Nella tabella seguente mostra i valori per la maschera di bit include_event_description. Il valore decimale viene restituito da dbo.sysalerts. 

|Decimal | BINARY | Significato |
|------|------|------|
|0 |0000 |Nessun messaggio |
|1 |0001 |Posta elettronica |
|2 |0010 |cercapersone |
|3 |0011 |posta elettronica e cercapersone |
|4 |0100 |Net send |
|5 |0101 |Messaggio di posta elettronica e net send |
|6 |0110 |Tramite cercapersone e net send |
|7 |0111 |Messaggio di posta elettronica, cercapersone e net send |
  
