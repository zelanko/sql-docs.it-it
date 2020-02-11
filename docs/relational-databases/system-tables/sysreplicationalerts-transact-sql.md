---
title: sysreplicationalerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6cbeab4c673390cb80300eb5ced2b4cb5c1bcf1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029740"
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene informazioni sulle condizioni che provocano l'attivazione di un avviso di replica. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|ID dell'avviso.|  
|**stato**|**int**|Valore definito dall'utente:<br /><br /> **0** = non servizio.<br /><br /> **1** = servito.|  
|**agent_type**|**int**|Tipo di agente:<br /><br /> **1** = agente di snapshot.<br /><br /> **2** = agente di lettura log.<br /><br /> **3** = agente di distribuzione.<br /><br /> **4** = agente di merge.|  
|**agent_id**|**int**|ID dell'agente dalle tabelle **MSsnapshot_agents**, **MSlogreader_agents**, **MSdistribution_agents**o **MSmerge_agents**.|  
|**error_id**|**int**|ID dell'errore archiviato in **MSrepl_errors**.|  
|**alert_error_code**|**int**|ID di messaggio dell'avviso generato durante la registrazione del record.|  
|**time**|**datetime**|Ora di inserimento del record.|  
|**publisher**|**sysname**|Nome del server di pubblicazione associato all'agente che ha attivato l'avviso.|  
|**publisher_db**|**sysname**|Database del server di pubblicazione associato all'agente che ha attivato l'avviso.|  
|**pubblicazione**|**sysname**|Pubblicazione associata all'agente che ha attivato l'avviso.|  
|**publication_type**|**int**|Tipo di pubblicazione:<br /><br /> **0** = snapshot.<br /><br /> **1** = transazionale.<br /><br /> **2** = Unione.|  
|**subscriber**|**sysname**|Nome del Sottoscrittore associato all'agente che ha attivato l'avviso.|  
|**subscriber_db**|**sysname**|Nome del database del Sottoscrittore associato all'agente che ha attivato l'avviso.|  
|**articolo**|**sysname**|Nome dell'articolo associato all'agente che ha attivato l'avviso.|  
|**destination_object**|**sysname**|Nome della tabella di sottoscrizione associata all'avviso.|  
|**source_object**|**sysname**|Nome della tabella pubblicata associata all'avviso.|  
|**alert_error_text**|**ntext**|Testo dell'avviso.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
