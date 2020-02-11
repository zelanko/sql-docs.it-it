---
title: MSreplication_subscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_subscriptions
- MSreplication_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_subscriptions system table
ms.assetid: fd0c5843-4e9b-4448-8bfb-0a4067d1d8d1
author: stevestein
ms.author: sstein
ms.openlocfilehash: a7164afe24d15abf195ebff96e4e96a82877deae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079990"
---
# <a name="msreplication_subscriptions-transact-sql"></a>MSreplication_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella **MSreplication_subscriptions** contiene una riga di informazioni di replica per ogni agente di distribuzione di manutenzione del database Sottoscrittore locale. Questa tabella è archiviata nel database di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**publisher_db**|**sysname**|Nome del database del server di pubblicazione.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione.|  
|**independent_agent**|**bit**|Indica se per questa pubblicazione è disponibile un agente di distribuzione autonomo.|  
|**subscription_type**|**int**|Tipo di sottoscrizione:<br /><br /> 0 = push<br /><br /> 1 = pull<br /><br /> 2 = anonima|  
|**distribution_agent**|**sysname**|Nome dell'agente di distribuzione.|  
|**Time**|**smalldatetime**|Ora dell'ultimo aggiornamento eseguito dall'agente di distribuzione.|  
|**Descrizione**|**nvarchar(255)**|Descrizione della sottoscrizione.|  
|**transaction_timestamp**|**varbinary (16)**|Solo per uso interno.|  
|**update_mode**|**tinyint**|Tipo di aggiornamento.|  
|**agent_id**|**binario (16)**|ID dell'agente.|  
|**subscription_guid**|**binario (16)**|Identificatore globale della versione della sottoscrizione associata alla pubblicazione.|  
|**subid**|**binario (16)**|Identificatore globale di una sottoscrizione anonima.|  
|**immediate_sync**|**bit**|Indica se i file di sincronizzazione vengono creati o aggiornati a ogni esecuzione dell'agente snapshot.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste di replica &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
